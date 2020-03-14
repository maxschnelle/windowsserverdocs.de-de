---
title: Bereitstellen eines Scale-Out-Dateiservers mit direkten Speicherplätzen und zwei Knoten für die Speicherung von Benutzerprofil-Datenträgern
description: Hier erfährst du, wie du direkte Speicherplätze mit den Remotedesktopdiensten verwendest.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: e320f0eb04e81d80f7288d4d7b20b5369e209932
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79319984"
---
# <a name="deploy-a-two-node-storage-spaces-direct-scale-out-file-server-for-upd-storage-in-azure"></a>Bereitstellen eines Scale-Out-Dateiservers mit direkten Speicherplätzen und zwei Knoten für die Speicherung von Benutzerprofil-Datenträgern

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Die Remotedesktopdienste (Remote Desktop Services, RDS) benötigen einen in die Domäne eingebundenen Dateiserver für Benutzerprofil-Datenträger (User Profile Disks, UPDs). Um einen hochverfügbaren, in die Domäne eingebundenen Scale-Out-Dateiserver (Scale-Out File Server, SOFS) in Azure bereitzustellen, verwende direkte Speicherplätze mit Windows Server 2016. Wenn du mit UPDs oder den Remotedesktopdiensten noch nicht vertraut bist, lies den Artikel [Willkommen bei den Remotedesktopdiensten](welcome-to-rds.md).

> [!NOTE] 
> Microsoft hat eine [Azure-Vorlage für die Bereitstellung eines Scale-Out-Dateiservers mit direkten Speicherplätzen](https://azure.microsoft.com/documentation/templates/301-storage-spaces-direct/) veröffentlicht. Du kannst deine Bereitstellung mithilfe dieser Vorlage oder anhand der Schritte im vorliegenden Artikel erstellen. 

Wir empfehlen die Bereitstellung des Scale-Out-Dateiservers mit VMs der DS-Serie und Storage Premium-Datenträgern, wobei auf jeder VM die gleiche Anzahl von Datenträgern gleicher Größe vorhanden sein sollte. Du benötigst mindestens zwei Speicherkonten. 

Für kleine Bereitstellungen empfehlen wir einen Cluster mit zwei Knoten und einem Cloudzeugen, wobei das Volume mit zwei Kopien gespiegelt wird. Kleine Bereitstellungen werden am besten durch Hinzufügen von Datenträgern erweitert. Bei größeren Bereitstellungen sollten zur Erweiterung Knoten (VMs) hinzugefügt werden. 

Die vorliegenden Anweisungen gelten für eine Bereitstellung mit zwei Knoten. Die folgende Tabelle zeigt die VM- und Datenträgergrößen, die du zum Speichern von UPDs für die Anzahl von Benutzern in deinem Unternehmen benötigst. 

| Benutzer | Gesamt (GB) | Virtuelle Maschine | Anzahl Datenträger | Datenträgertyp | Datenträgergröße (GB) | Konfiguration   |
|-------|------------|----|---------|-----------|----------------|-----------------|
| 10    | 50         | DS1 | 2       | P10       | 128            | 2 × (DS1 + 2 P10)  |
| 25    | 125        | DS1 | 2       | P10       | 128            | 2 × (DS1 + 2 P10)  |
| 50    | 250        | DS1 | 2       | P10       | 128            | 2 × (DS1 + 2 P10)  |
| 100   | 500        | DS1 | 2       | P20       | 512            | 2 × (DS1 + 2 P20)  |
| 250   | 1250       | DS1 | 2       | P30       | 1024           | 2 × (DS1 + 2 P30)  |
| 500   | 2500       | DS2 | 3       | P30       | 1024           | 2 × (DS2 + 3 P30)  |
| 1000  | 5000       | DS3 | 5       | P30       | 1024           | 2 × (DS3 + 5 P30)  |
| 2500  | 12500      | DS4 | 13      | P30       | 1024           | 2 × (DS4 + 13 P30) |
| 5000  | 25000      | DS5 | 25      | P30       | 1024           | 2 × (DS5 + 25 P30) | 

Mithilfe der folgenden Schritte kannst du einen Domänencontroller (im Beispiel „my-dc“) und zwei Knoten-VMs („my-fsn1“ und „my-fsn2“) erstellen und die VMs als Scale-Out-Dateiserver mit direkten Speicherplätzen und zwei Knoten konfigurieren.

1. Erstelle ein [Microsoft Azure-Abonnement](https://azure.microsoft.com).
2. Melde dich beim [Azure-Portal](https://ms.portal.azure.com) an.
3. Erstelle ein [Azure-Speicherkonto](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/#create-a-storage-account) in Azure Resource Manager. Erstelle das Konto in einer neuen Ressourcengruppe und verwende die folgenden Konfigurationen:
   - Bereitstellungsmodell: Resource Manager
   - Art des Speicherkontos: Allgemeine Zwecke
   - Leistungstarif: Premium
   - Replikationsoption: LRS
4. Richte eine Active Directory-Gesamtstruktur ein, entweder mithilfe einer Schnellstartvorlage oder manuell. 
   - Stelle die Gesamtstruktur mithilfe einer Azure-Schnellstartvorlage bereit:
      - [Create an Azure VM with a new AD Forest](https://azure.microsoft.com/documentation/templates/active-directory-new-domain/) (Erstellen einer Azure-VM mit einer neuen AD-Gesamtstruktur)
      - [Create an new AD Domain with 2 Domain Controllers](https://azure.microsoft.com/documentation/templates/active-directory-new-domain-ha-2-dc/) (Erstellen einer neuen AD-Domäne mit zwei Domänencontrollern) – für Hochverfügbarkeit
   - [Stelle die Gesamtstruktur](https://azure.microsoft.com/documentation/articles/active-directory-new-forest-virtual-machine/) mit folgenden Konfigurationen manuell bereit:
      - Erstelle das virtuelle Netzwerk in der gleichen Ressourcengruppe wie das Speicherkonto.
      - Empfohlene Größe: DS2 (erhöhe die Größe, wenn der Domänencontroller mehr Domänenobjekte hostet)
      - Verwende ein automatisch generiertes VNET.
      - Installiere AD DS gemäß den entsprechenden Anleitungen.
5. Richte die Dateiserver-Clusterknoten ein. Hierfür kannst du die Azure-Vorlage [Windows Server 2016 Storage Spaces Direct (S2D) SOFS cluster](https://azure.microsoft.com/resources/templates/301-storage-spaces-direct/) verwenden oder die Schritte 6–11 ausführen, um die Knoten manuell bereitzustellen.
6. So richtest du die Dateiserver-Clusterknoten manuell ein:
   1. Erstelle den ersten Knoten: 
      1. Erstelle einen neuen virtuellen Computer mit dem Windows Server 2016-Image. (Klicke auf **Neu > Virtuelle Computer > Windows Server 2016**. Wähle **Resource Manager** aus, und klicke auf **Erstellen**.)
      2. Lege die grundlegende Konfiguration wie folgt fest:
         - Name: my-fsn1
         - VM-Datenträgertyp: SSD
         - Verwende die in Schritt 3 erstellte Ressourcengruppe. 
      3. Größe: DS1, DS2, DS3, DS4 oder DS5, je nach Benutzeranforderungen (siehe die Tabelle am Anfang dieser Anleitung). Stelle sicher, dass die Unterstützung für Premium-Datenträger ausgewählt ist.
      4. Einstellungen: 
         - Speicherkonto: Wähle das Speicherkonto aus, das du in Schritt 3 erstellt hast.
         - Hochverfügbarkeit: Erstelle eine neue Verfügbarkeitsgruppe. (Klicke auf **Hochverfügbarkeit > Neu erstellen**, und gib einen Namen ein [z.B. „s2d-cluster“]. Verwende die Standardwerte für **Updatedomänen** und **Fehlerdomänen**.)
   2. Erstelle den zweiten Knoten. Wiederhole die obigen Schritte, aber mit folgenden Änderungen:
      - Name: my-fsn2
      - Hochverfügbarkeit: Wähle die oben erstellte Verfügbarkeitsgruppe aus.  
7. [Füge Datenträger](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-attach-disk-portal/) gemäß Benutzeranforderungen an die Clusterknoten-VMs an (wie in der obigen Tabelle zu sehen). Nachdem die Datenträger erstellt und an die VMs angefügt wurden, lege die **Hostzwischenspeicherung** auf **Keine** fest.
8. Lege die IP-Adressen für alle VMs auf **statisch** fest. 
   1. Wähle eine VM in der Ressourcengruppe aus, und klicke auf **Netzwerkschnittstellen** (unter **Einstellungen**). Wähle die aufgeführte Netzwerkschnittstelle aus, und klicke auf **IP-Konfigurationen**. Wähle die aufgeführte IP-Konfiguration aus, klicke auf **statisch**, und klicke dann auf **Speichern**.
   2. Notiere die private IP-Adresse (10.x.x.x) des Domänencontrollers (in unserem Beispiel „my-dc“).
9. Lege die primäre DNS-Serveradresse für die Netzwerkadapter der Clusterknoten-VMs auf den Server „my-dc“ fest. Wähle die VM aus, und klicke dann auf **Netzwerkschnittstellen > DNS-Server > Benutzerdefiniertes DNS**. Gib die oben notierte IP-Adresse ein, und klicke dann auf **Speichern**.
10. Erstelle ein [Azure-Speicherkonto als Cloudzeugen](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness). (Wenn du die verknüpften Anweisungen verwendest, hör bei „Configuring Cloud Witness with Failover Cluster Manager GUI“ [Konfigurieren des Cloudzeugen mit der GUI des Failovercluster-Managers] auf – wir führen diesen Schritt später aus.)
11. Richte den Dateiserver mit direkten Speicherplätzen ein. Stelle eine Verbindung mit einer Knoten-VM her, und führe die folgenden Windows PowerShell-Cmdlets aus.
    1. Installiere die Features „Failoverclustering“ und „Dateiserver“ auf den beiden Dateiserver-Clusterknoten-VMs:

       ```powershell
       $nodes = ("my-fsn1", "my-fsn2")
       icm $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools} 
       icm $nodes {Install-WindowsFeature FS-FileServer} 
       ```
    2. Überprüfe die Clusterknoten-VMs, und erstelle einen SOFS-Cluster mit zwei Knoten:

       ```powershell
       Test-Cluster -node $nodes
       New-Cluster -Name MY-CL1 -Node $nodes –NoStorage –StaticAddress [new address within your addr space]
       ``` 
    3. Konfiguriere den Cloudzeugen. Verwende den Speicherkontonamen und Zugriffsschlüssel des Cloudzeugen.

       ```powershell
       Set-ClusterQuorum –CloudWitness –AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey> 
       ```
    4. Aktiviere direkte Speicherplätze.

       ```powershell
       Enable-ClusterS2D 
       ```
      
    5. Erstelle ein virtuelles Datenträgervolume.

       ```powershell
       New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 120GB 
       ```
       Um Informationen zum freigegebenen Clustervolume im SOFS-Cluster anzuzeigen, führe das folgende Cmdlet aus:

       ```powershell
       Get-ClusterSharedVolume
       ```
   
    6. Erstelle den Scale-Out-Dateiserver:

       ```powershell
       Add-ClusterScaleOutFileServerRole -Name my-sofs1 -Cluster MY-CL1
       ```

    7. Erstelle eine neue SMB-Dateifreigabe im SOFS-Cluster.

       ```powershell
       New-Item -Path C:\ClusterStorage\VDisk01\Data -ItemType Directory
       New-SmbShare -Name UpdStorage -Path C:\ClusterStorage\VDisk01\Data
       ```

Du verfügst jetzt über eine Freigabe unter `\\my-sofs1\UpdStorage`, die du zur UPD-Speicherung verwenden kannst, wenn du [UPD](https://social.technet.microsoft.com/wiki/contents/articles/15304.installing-and-configuring-user-profile-disks-upd-in-windows-server-2012.aspx) für deine Benutzer aktivierst. 
