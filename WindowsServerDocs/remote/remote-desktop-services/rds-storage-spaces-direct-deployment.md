---
title: Bereitstellen eines zwei Knoten Storage Spaces direkte SOFS für die Speicherung von Benutzerprofil-Datenträger in Azure
description: Erfahren Sie, wie von "direkte Speicherplätze" mit RDS.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1099f21d-5f07-475a-92dd-ad08bc155da1
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
manager: scottman
ms.openlocfilehash: 8af3a389ec726bbb5ebd62db57d9b3a9861ac63f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890961"
---
# <a name="deploy-a-two-node-storage-spaces-direct-scale-out-file-server-for-upd-storage-in-azure"></a>Bereitstellen eines "direkte Speicherplätze" Dateiserver mit horizontaler Skalierung-Servers von zwei Knoten für UPD-Speicherung in Azure

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Remote Desktop Services (RDS) erfordert einen Domäne eingebundenen Dateiserver für Benutzerprofil-Datenträgern (UPDs). Um einen Server mit hoher Verfügbarkeit mit domänenverknüpfung horizontal skalierten Dateiserver (SOFS) in Azure bereitstellen möchten, verwenden Sie "direkte Speicherplätze" mit Windows Server 2016 aus. Wenn Sie nicht mit dem Benutzerprofil-Datenträger oder Remote Desktop Services vertraut sind, sehen Sie sich [Willkommen bei Remotedesktopdienste](welcome-to-rds.md).

> [!NOTE] 
> Microsoft, die gerade veröffentlichten ein [Azure-Vorlage zum Bereitstellung eines "direkte Speicherplätze" Dateiserver mit horizontaler Skalierung Servers](https://azure.microsoft.com/documentation/templates/301-storage-spaces-direct/)! Sie können die Vorlage verwenden, um Ihre Bereitstellung zu erstellen oder verwenden die Schritte in diesem Artikel. 

Wir empfehlen die Bereitstellung Ihrer SOFS mit VMs der DS-Serie und Storage Premium-Datenträger, vorhanden sind, die gleiche Anzahl und Größe von Datenträgern für Daten auf jedem virtuellen Computer. Sie benötigen mindestens zwei Speicherkonten. 

Für kleine Bereitstellungen empfehlen wir einen Cluster mit 2 Knoten mit einem cloudzeugen, wobei das Volume mit 2 Kopien gespiegelt wird. Bauen Sie kleine Bereitstellungen, indem Sie Datenträger hinzugefügt. Wachsen Sie größere Bereitstellungen durch Hinzufügen von Knoten (VMs). 

Diese Anweisungen gelten für eine 2-Knoten-Bereitstellung. Die folgende Tabelle zeigt den Größen für virtuelle Computer und Datenträger, die Sie zum Speichern der Benutzerprofil-Datenträger für die Anzahl von Benutzern in Ihrem Unternehmen benötigen. 

| Benutzer | Gesamt (GB) | Virtuelle Maschine | Anzahl Datenträger | Datenträgertyp | Datenträgergröße (GB) | Konfiguration   |
|-------|------------|----|---------|-----------|----------------|-----------------|
| 10    | 50         | DS1 | 2       | P10       | 128            | 2x(DS1 + 2 P10)  |
| 25    | 125        | DS1 | 2       | P10       | 128            | 2x(DS1 + 2 P10)  |
| 50    | 250        | DS1 | 2       | P10       | 128            | 2x(DS1 + 2 P10)  |
| 100   | 500        | DS1 | 2       | P20       | 512            | 2x(DS1 + 2 P20)  |
| 250   | 1250       | DS1 | 2       | P30       | 1024           | 2x(DS1 + 2 P30)  |
| 500   | 2500       | DS2 | 3       | P30       | 1024           | 2 x (DS2 + 3 P30)  |
| 1000  | 5000       | DS3 | 5       | P30       | 1024           | 2 x (DS3 + 5 P30)  |
| 2500  | 12500      | DS4 | 13      | P30       | 1024           | 2x(DS4 + 13 P30) |
| 5000  | 25000      | DS5 | 25      | P30       | 1024           | 2x(DS5 + 25 P30) | 

Verwenden Sie die folgenden Schritte aus, erstellen Sie einen Domänencontroller (Wir haben Sie angerufen unsere "my-dc" unten) und zwei Knoten virtuelle Computer ("Mein fsn1" und "Meine fsn2"), und konfigurieren die virtuellen Computer, um eine direkte SOFS für 2 Knoten Storage Leerzeichen sein.

1. Erstellen Sie eine [Microsoft Azure-Abonnement](https://azure.microsoft.com).
2. Melden Sie sich bei der [Azure-Portal](https://ms.portal.azure.com).
3. Erstellen Sie eine [Azure Storage-Konto](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/#create-a-storage-account) im Azure-Ressourcen-Manager. Erstellen Sie ihn in eine neue Ressourcengruppe, und verwenden Sie die folgenden Konfigurationen:
   - Bereitstellungsmodell: Ressourcen-Manager
   - Der Typ des Speicherkontos: Allgemein
   - Leistungsstufe: Premium
   - Replication-Option: LRS
4. Richten Sie Active Directory-Gesamtstruktur durch Verwenden einer schnellstartvorlage oder manuelles Bereitstellen der Gesamtstruktur aus. 
   - Stellen Sie mithilfe einer Azure-Schnellstart-Vorlage bereit:
      - [Erstellen einer Azure-VM mit einer neuen AD-Gesamtstruktur](https://azure.microsoft.com/documentation/templates/active-directory-new-domain/)
      - [Erstellen Sie eine neue AD-Domäne mit 2 Domänencontroller](https://azure.microsoft.com/documentation/templates/active-directory-new-domain-ha-2-dc/) (für hohe Verfügbarkeit)
   - Manuell [bereitstellen die Gesamtstruktur](https://azure.microsoft.com/documentation/articles/active-directory-new-forest-virtual-machine/) mit folgenden Konfigurationen:
      - Erstellen des virtuellen Netzwerks in der gleichen Ressourcengruppe wie das Speicherkonto an.
      - Empfohlene Größe: DS2 (erhöhen Sie die Größe aus, wenn es sich bei der Domänencontroller mehr Domänenobjekte gehostet wird)
      - Verwenden Sie ein automatisch generiertes VNet.
      - Führen Sie die Schritte zum Installieren von AD DS.
5. Richten Sie den Dateiserver-Clusterknoten aus. Sie erreichen dies durch die Bereitstellung der [Windows Server 2016 Storage Spaces Direct SOFS-Cluster Azure-Vorlage](https://azure.microsoft.com/resources/templates/301-storage-spaces-direct/) oder indem Sie die folgenden Schritte 6 bis 11, manuell bereitstellen.
5. Der Dateiserver-Clusterknoten manuell einrichten möchten:
   1. Den ersten Knoten zu erstellen: 
      1. Erstellen Sie einen neuen virtuellen Computer mit dem Windows Server 2016-Image. (Klicken Sie auf **neu > virtuelle Computer > WindowsServer 2016.** SELECT **Resource Manager**, und klicken Sie dann auf **erstellen**.)
      2. Legen Sie die grundlegende Konfiguration wie folgt:
         - Name: my-fsn1
         - VM-Datenträgertyp SSD
         - Verwenden Sie eine vorhandene Ressourcengruppe aus, die Sie in Schritt 3 erstellt haben. 
      3. Größe: DS1, DS2, DS3, DS4 oder DS5 je nach der Benutzer muss (Tabelle am Anfang dieser Anweisungen anzuzeigen). Stellen Sie sicher, dass Unterstützung für Premium-Datenträger ausgewählt ist.
      4. Einstellungen: 
         - Speicherkonto: Wählen Sie das Speicherkonto, das Sie in Schritt 3 erstellt haben.
         - Hohe Verfügbarkeit – eine neue verfügbarkeitsgruppe erstellen. (Klicken Sie auf **Hochverfügbarkeit > erstellen, die neue**, und geben Sie dann einen Namen (z. B. s2d-Cluster). Verwenden Sie die Standardwerte für **Updatedomänen** und **Fehlerdomänen**.)
   2. Erstellen Sie den zweiten Knoten. Wiederholen Sie den obigen Schritt, um sich mit den folgenden Änderungen:
      - Name: my-fsn2
      - Hochverfügbarkeit – wählen Sie die verfügbarkeitsgruppe oben erstellten.  
6. [Fügen Sie Datenträger](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-attach-disk-portal/) auf den Clusterknoten-VMs nach der Benutzer muss (wie in der Tabelle oben dargestellt). Nachdem die Daten Datenträger erstellt und an den virtuellen Computer angefügten **hostzwischenspeicherung** zu **keine**.
7. Festlegen von IP-Adressen für alle virtuellen Computer zu **statische**. 
   1. In der Ressourcengruppe, wählen Sie eine VM, und klicken Sie dann auf **Netzwerkschnittstellen** (unter **Einstellungen**). Wählen Sie die aufgeführten Netzwerkschnittstelle aus, und klicken Sie dann auf **IP-Konfigurationen**. Wählen Sie die aufgelistete IP-Konfiguration, **statische**, und klicken Sie dann auf **speichern**.
   2. Beachten Sie die Domain Controller (Meine dc in unserem Beispiel) private IP-Adresse (10.x.x.x).
8. Legen Sie primäre DNS-Serveradresse auf NICs, die von den Clusterknoten-VMs, auf den my-dc-Server. Wählen Sie den virtuellen Computer aus, und klicken Sie dann auf **Netzwerkschnittstellen > DNS-Server > benutzerdefiniertes DNS**. Geben Sie die private IP-Adresse, die Sie oben notiert haben, und klicken Sie dann auf **speichern**.
9. Erstellen Sie eine [Azure Storage-Konto werden Ihre cloudzeugen](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness). (Wenn Sie die verknüpften Anweisungen verwenden, beendet, wenn man an "Konfigurieren von Cloud Witness mit Failover Cluster-Manager-GUI" – wir diesen Schritt unten machen.)
10. Richten Sie den "direkte Speicherplätze"-Dateiserver ein. Verbinden mit einem VM-Knoten, und führen Sie die folgenden Windows PowerShell-Cmdlets.
   1. Installieren Sie Failoverclustering-Features und Dateiserver, auf die zwei Server-Clusterknoten-VMs:

      ```powershell
      $nodes = ("my-fsn1", "my-fsn2")
      icm $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools} 
      icm $nodes {Install-WindowsFeature FS-FileServer} 
      ```
   2. Überprüfen Sie die Clusterknoten-VMs aus, und Erstellen von SOFS-Cluster mit 2 Knoten:

      ```powershell
      Test-Cluster -node $nodes
      New-Cluster -Name MY-CL1 -Node $nodes –NoStorage –StaticAddress [new address within your addr space]
      ``` 
   3. Konfigurieren des cloudzeugen. Verwenden Sie Ihren Cloud Zeuge und den speicherkontoschlüssel.

      ```powershell
      Set-ClusterQuorum –CloudWitness –AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey> 
      ```
   4. Aktivieren Sie direkte Speicherplätze.

      ```powershell
      Enable-ClusterS2D 
      ```
      
   5. Erstellen Sie ein Volume des virtuellen Datenträgers an.

      ```powershell
      New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 120GB 
      ```
      Um Informationen zu dem freigegebenen Clustervolume im SOFS-Cluster anzuzeigen, führen Sie das folgende Cmdlet aus:

      ```powershell
      Get-ClusterSharedVolume
      ```
   
   6. Erstellen Sie den Dateiserver mit horizontaler Skalierung (Server, SOFS):

      ```powershell
      Add-ClusterScaleOutFileServerRole -Name my-sofs1 -Cluster MY-CL1
      ```

   7. Erstellen Sie eine neue SMB-Dateifreigabe im SOFS-Cluster.

      ```powershell
      New-Item -Path C:\ClusterStorage\Volume1\Data -ItemType Directory
      New-SmbShare -Name UpdStorage -Path C:\ClusterStorage\Volume1\Data
      ```

Sie verfügen nun über eine Dateifreigabe unter &#92;\my-sofs1\UpdStorage, die Sie für die Speicherung von Benutzerprofil-Datenträger verwenden, können bei der Sie [Benutzerprofil-Datenträger aktivieren](https://social.technet.microsoft.com/wiki/contents/articles/15304.installing-and-configuring-user-profile-disks-upd-in-windows-server-2012.aspx) für Ihre Benutzer. 
