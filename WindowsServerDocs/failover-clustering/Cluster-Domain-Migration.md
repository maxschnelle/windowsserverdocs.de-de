---
title: Überschreiten Sie Migration von Cluster in Windows Server 2016/2019
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 01/18/2019
description: Dieser Artikel beschreibt, verschieben einen Windows Server 2019 Cluster von einer Domäne zu einer anderen
ms.localizationpriority: medium
ms.openlocfilehash: bcfd458c94d33820f434cde3313dc069fc42ffd9
ms.sourcegitcommit: 21677706eb85cb1396c1f40bf443146c09ef1b0d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2019
ms.locfileid: "9042034"
---
# Migration von Failovercluster

> Gilt für: WindowsServer 2019, WindowsServer 2016

Dieses Thema enthält eine Übersicht über für ein Failover Gleitender Windows Server von einer Domäne zu einer anderen Cluster.

## Warum migrieren zwischen Domänen

Es gibt mehrere Szenarien, in denen Migrieren von eines Clusters von einem Domain zu einem anderen erforderlich ist.

- FirmaA mit UnternehmenB zusammengeführt, und verschieben alle Cluster muss in FirmaA Domäne
- Cluster im Hauptmenü Datencenter erstellt und sich an Remotestandorten ausgeliefert
- Cluster als Arbeitsgruppe Cluster erstellt wurde, und jetzt muss Teil einer Domäne
- Cluster als Domäne Cluster erstellt wurde, und jetzt muss Teil einer Arbeitsgruppe
- Cluster mit einem Bereich des Unternehmens zu einer anderen verschoben wird, und ist eine andere untergeordnete Domäne

Microsoft stellt keine Unterstützung für Administratoren bereit, die versuchen, Ressourcen aus einer Domäne zu einer anderen zu verschieben, wenn der zugrunde liegenden Anwendung Vorgang nicht unterstützt wird. Beispielsweise unterstützen nicht Microsoft an Administratoren, die versuchen, einen Microsoft Exchange-Server von einer Domäne zu einer anderen zu verschieben.

   > [!WARNING]
   > Es wird empfohlen, dass Sie eine vollständige Sicherung der freigegebene Speicher im Cluster ausführen, bevor Sie den Cluster verschieben.

## WindowsServer 2016 und frühere Versionen

In Windows Server 2016 und früher, war der Cluster-Dienst die Funktion Verschieben von einer Domäne in eine andere nicht vorhanden.  Dies ist aufgrund der zunehmende Abhängigkeit von Active Directory Domain Services und die virtuellen Namen erstellt.   

## Optionen

Es gibt zwei Optionen, um eine solche Verschiebung Zweck.

Die erste Option umfasst das Löschen des Clusters und Neuerstellen in die neue Domäne.

![Löschen und neu erstellen](media\Cross-Domain-Cluster-Migration\Cross-Cluster-Domain-Migration-1.gif)

Die Animation zeigt, ist diese Option mit den Schritten destruktiv wird:

1. Löschen Sie den Cluster.
2. Ändern Sie die Domänenmitgliedschaft der Knoten in die neue Domäne.
3. Erstellen des Clusters als neue in der aktualisierten Domäne neu.  Dies würde vorliegen, müssen alle Ressourcen neu erstellen.

Die zweite Option ist weniger destruktive jedoch zusätzlichen Hardware erforderlich, wie Sie ein neuer Cluster in der neuen Domäne erstellt werden muss.  Nachdem der Cluster in der neuen Domäne wird, führen Sie den Cluster-Migration-Assistenten, um die Ressourcen zu migrieren. Beachten Sie, dass dies nicht von Daten migrieren – Sie müssen mit einem anderen Tool migriert Daten, z. B. [Storage Migration Service](../storage/storage-migration-service/overview.md)(nach Unterstützung für Cluster hinzugefügt wird).

![Erstellen und migrieren](media\Cross-Domain-Cluster-Migration\Cross-Cluster-Domain-Migration-2.gif)

Die Animation zeigt, diese Option ist nicht destruktive erfordert jedoch unterschiedliche Hardware oder eines Knotens aus einem vorhandenen Cluster als entfernt wurde.

1. Erstellen Sie eine neue Clusterin die neue Domäne, während Sie gleichzeitig den alten Cluster verfügbar.
2. Verwenden Sie den [Assistenten für die Cluster-Migration](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754481(v=ws.10)) , um alle Ressourcen für den neuen Cluster zu migrieren. Zur Erinnerung dies nicht kopiert Daten, daher müssen einzeln ausgeführt werden.
3. Außer Betrieb genommen Sie oder löschen Sie den alten Cluster.

In beiden Optionen des neuen Clusters müssten alle [Clusteranwendungen](https://technet.microsoft.com/aa369082(v=vs.90)) installiert haben, Treiber, die alle auf dem neuesten Stand, und möglicherweise testen, um sicherzustellen, dass alle ordnungsgemäß ausgeführt wird.  Dies ist die Zeit in Anspruch, wenn Daten auch verschoben werden.

## Windows Server 2019

In Windows Server 2019 vorgestellt Cross Cluster Domäne Migration-Funktionen.  Nun, die oben genannten Szenarien einfach möglich ist und die Notwendigkeit der erneuten Erstellung wird nicht mehr benötigt.  

Verschieben von einem Cluster von einer Domäne ist ein Vorgang. Zu diesem Zweck stehen zwei neue PowerShell-Cmdlets.

**New-ClusterNameAccount** – erstellt ein Cluster Name-Konto in Active Directory- **Remove-ClusterNameAccount** – entfernt den Namen Clusterkonten aus Active Directory

Der Prozess zu diesem Zweck besteht darin, Cluster von einer Domäne in einer Arbeitsgruppe und wieder in die neue Domäne zu ändern.  Die Notwendigkeit, Zerstören eines Clusters, erstellen Sie einen Cluster neu installieren von Anwendungen usw. ist nicht erforderlich. Beispielsweise würde es wie folgt aussehen:

![Migrieren](media\Cross-Domain-Cluster-Migration\Cross-Cluster-Domain-Migration-3.gif)

## Migrieren eines Clusters mit einer neuen Domäne

In den folgenden Schritten wird ein Cluster aus der Domäne "contoso.com" in die neue Domäne Fabrikam.com verschoben.  Der Clustername ist *CLUSCLUS* und mit einer Datei-Serverrolle *FS-CLUSCLUS*aufgerufen.

1. Erstellen Sie ein lokales Administratorkonto mit den gleichen Namen und das Kennwort auf allen Servern im Cluster.  Dies kann erforderlich sein, um anmelden, während die Server zwischen Domänen verschieben.
2. Melden Sie sich mit einem Domänenkonto Benutzer oder Administrator, die Active Directory-Berechtigungen für das Cluster Name Objekt (Clusternamenobjekt), virtuelle Computer Objekte (VCO), ist der erste Server hat Zugriff auf den Cluster und PowerShell öffnen.
3. Sicherstellen, dass alle Cluster Netzwerk Benennen von Ressourcen in einer Offline Zustands- und Ausführen der folgenden Befehl.  Dieser Befehl entfernt Active Directory-Objekte, die möglicherweise Cluster.

   ```PowerShell
   Remove-ClusterNameAccount -Cluster CLUSCLUS -DeleteComputerObjects
   ```
4. Verwenden Sie Active Directory-Benutzer und-Computer, um sicherzustellen, dass den Computer CNO und VCO, die alle gruppierten Namen zugeordneten Objekte entfernt wurden.

   > [!NOTE]
   > Es ist sinnvoll, beenden Sie den Cluster-Dienst auf allen Servern im Cluster und Starttyp des Dienstes manuell so festzulegen, dass der Cluster-Dienst nicht startet, wenn die Server neu starten, während der Änderung von Domänen.

   ```PowerShell
   Stop-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Manual
   ```

5. Ändern Sie der Server-Domänenmitgliedschaft in einer Arbeitsgruppe und starten Sie die Servern, die Server in die neue Domäne beitreten erneut starten.
6. Sobald die Server in der neuen Domäne sind, melden Sie sich mit einem Server mit einem Domänenkonto Benutzer oder Administrator, die Active Directory-Berechtigungen zum Erstellen von Objekten, hat Zugriff auf den Cluster, und öffnen Sie PowerShell. Starten Sie den Cluster-Dienst, und legen Sie sie wieder auf automatisch.

   ```PowerShell
   Start-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Automatic
   ```
7. Schalten Sie den Namen des Clusters und alle anderen Cluster Netzwerknamen Ressourcen Onlinestatus.

   ```PowerShell
   Start-ClusterResource -Name "Cluster Name"

   Start-ClusterResource -Name FS-CLUSCLUS
   ```

8. Ändern Sie den Cluster zum Teil die neue Domäne mit zugeordneten active Directory-Objekte werden soll. Zu diesem Zweck wird der Befehl unten ist, und die Netzwerk Benennen von Ressourcen in einem online Zustand sein.  Dieser Befehl Vorgehen ist Name-Objekte in Active Directory neu erstellen.

   ```PowerShell
   New-ClusterNameAccount -Name CLUSTERNAME -Domain NEWDOMAINNAME.com -UpgradeVCOs
   ```

    Hinweis: Wenn Sie keinen zusätzlichen Gruppen mit Netzwerknamen (d. h. einem Hyper-V-Cluster mit nur virtuelle Computer) ist der Switch - UpgradeVCOs Parameter nicht erforderlich.

9. Verwenden Sie Active Directory-Benutzer und-Computer, um die neue Domäne zu überprüfen und sicherzustellen, dass die zugeordnete Computerobjekte erstellt wurden. Wenn sie aufweisen, schalten Sie die verbleibenden Ressourcen in den Gruppen online.

   ```PowerShell
   Start-ClusterGroup -Name "Cluster Group"

   Start-ClusterGroup -Name FS-CLUSCLUS
   ```

## Bekannte Probleme

Wenn Sie das neue Feature der USB-Zeugen verwenden, werden kann nicht in die neue Domäne den Cluster hinzugefügt.  Die Logik ist, dass der Freigabe Zeugen Dateityp Kerberos für die Authentifizierung verwenden muss.  Ändern Sie den Zeugen None vor dem Hinzufügen des Clusters mit der Domäne.  Abgeschlossen ist, erstellen Sie den USB-Zeugen neu.  Der Fehler, die angezeigt wird, ist:

```
New-ClusternameAccount : Cluster name account cannot be created.  This cluster contains a file share witness with invalid permissions for a cluster of type AdministrativeAccesssPoint ActiveDirectoryAndDns. To proceed, delete the file share witness.  After this you can create the cluster name account and recreate the file share witness.  The new file share witness will be automatically created with valid permissions.
```

