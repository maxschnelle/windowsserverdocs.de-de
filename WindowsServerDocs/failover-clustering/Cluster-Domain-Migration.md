---
title: Cross-Domain-Clustermigration in Windows Server 2016/2019
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 01/18/2019
description: Dieser Artikel beschreibt das Verschieben eines 2019 für Windows Server-Clusters von einer Domäne in eine andere
ms.localizationpriority: medium
ms.openlocfilehash: 5d5aaa333d2e20fa25e4738e343f326d63f75c6b
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280213"
---
# <a name="failover-cluster-domain-migration"></a>Migration von Failover-Cluster

> Gilt für: Windows Server 2019, Windows Server 2016

Dieses Thema enthält eine Übersicht für Windows Server-Failoverclusterknoten Verschieben von einer Domäne zu einem anderen Cluster.

## <a name="why-migrate-between-domains"></a>Warum migrieren zwischen Domänen

Es gibt mehrere Szenarien, in denen Migration eines Clusters aus einem Domain in ein anderes erforderlich ist.

- FirmaA führt mit UnternehmenB zusammen, und muss allen Clustern in FirmaA Domäne verschieben
- Cluster in der main-Rechenzentrum erstellt und an Remotestandorte versandt
- Cluster als ein workgroupcluster erstellt wurde und nun Teil einer Domäne sein muss.
- Cluster, die als Netzwerklastenausgleich-Cluster Domäne erstellt wurde und nun Teil einer Arbeitsgruppe sein muss
- Cluster auf einen Bereich des Unternehmens auf einen anderen verschoben wird, und ist eine andere Unterdomäne

Microsoft bereit keine Unterstützung für Administratoren, die versuchen, Ressourcen von einer Domäne in eine andere verschoben wird, wenn die zugrunde liegenden Vorgang für die Anwendung nicht unterstützt wird. Z. B. bereit nicht Microsoft Support für Administratoren, die versuchen, einen Microsoft Exchange-Server von einer Domäne in eine andere zu verschieben.

   > [!WARNING]
   > Es wird empfohlen, dass Sie eine vollständige Sicherung der gesamten freigegebenen Speichers im Cluster ausführen, bevor Sie den Cluster verschieben.

## <a name="windows-server-2016-and-earlier"></a>WindowsServer 2016 und früher

In Windows Server 2016 und früher muss nicht der Clusterdienst die Möglichkeit, von einer Domäne in eine andere verschieben.  Dies war aufgrund der erhöhten Abhängigkeit von Active Directory Domain Services und die virtuellen Namen erstellt.   

## <a name="options"></a>Optionen

Um eine solche Verschiebung zu tun, gibt es zwei Optionen zur Verfügung.

Die erste Option umfasst den Cluster löschen und ihn in der neuen Domäne neu zu erstellen.

![Löschen und neu erstellen](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-1.gif)

Diese Option ist destruktive mit den Schritten, wie die Animation wird gezeigt, wird:

1. Löschen Sie den Cluster ein.
2. Ändern Sie die Domänenmitgliedschaft der Knoten in der neuen Domäne ein.
3. Erstellen Sie den Cluster wie in der aktualisierten Domäne neu.  Dies würde hingegen, dass alle Ressourcen neu erstellen.

Die zweite Option ist weniger destruktiv jedoch zusätzliche Hardware erforderlich ist, wie Sie ein neuer Cluster in der neuen Domäne erstellt werden müssten.  Sobald der Cluster in der neuen Domäne ist, führen Sie der Cluster-Assistent zum Migrieren von Ressourcen. Beachten Sie, dass dies nicht von Daten migrieren – Sie ein anderes Tool verwenden, z. B. Datenmigration müssen [Speicherung Datenbankmigrationsdienst](../storage/storage-migration-service/overview.md)(sobald der Cluster-Unterstützung hinzugefügt wurde).

![Erstellen und migrieren](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-2.gif)

Wie die Animation wird gezeigt, wird diese Option ist nicht zerstörerische jedoch erfordert entweder auf anderer Hardware oder auf einen Knoten aus dem vorhandenen Cluster als entfernt wurde.

1. Erstellen Sie eine neue Clusterin der neuen Domäne, während Sie weiterhin den alten Cluster zur Verfügung.
2. Verwenden der [Cluster Migration Wizard](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754481(v=ws.10)) alle Ressourcen für den neuen Cluster migrieren. Zur Erinnerung: Dies kopiert keine Daten, daher müssen separat ausgeführt werden.
3. Außer Betrieb nehmen Sie, oder entfernen Sie den alten Cluster.

Bei beiden Optionen müssen im neue Cluster, dass alle [clusterfähige Anwendungen](https://technet.microsoft.com/aa369082(v=vs.90)) installiert ist, Treiber, die alle auf dem neuesten Stand, und möglicherweise testen, um sicherzustellen, dass alle ordnungsgemäß ausgeführt wird.  Dies ist ein zeitaufwändiger Prozess, wenn die Daten auch verschoben werden müssen.

## <a name="windows-server-2019"></a>Windows Server 2019

Windows Server-2019 wir Cross Cluster Domäne migrationsfunktionalitäten eingeführt.  Jetzt die oben genannten Szenarien problemlos ausgeführt werden können und die Notwendigkeit der erneuten Erstellung nicht mehr benötigt.  

Verschieben eines Clusters von einer Domäne ist ein Prozess einfach. Um dies zu erreichen, gibt es zwei neue PowerShell-Cmdlets.

**Neue ClusterNameAccount** – erstellt ein Clusternamenkonto in Active Directory **Remove-ClusterNameAccount** – entfernt die Cluster-Name-Konten aus Active Directory

Der Prozess hierfür ist so ändern Sie den Cluster aus einer Domäne mit einer Arbeitsgruppe und zurück in die neue Domäne.  Die Notwendigkeit, einen Cluster entfernen, erstellen Sie einen Cluster neu installieren, Anwendungen usw. ist nicht erforderlich. Beispielsweise würde es folgendermaßen aussehen:

![Migrieren](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-3.gif)

## <a name="migrating-a-cluster-to-a-new-domain"></a>Die Migration eines Clusters in eine neue Domäne

In den folgenden Schritten wird ein Cluster aus der Domäne "contoso.com" in die neue Domäne "Fabrikam.com" verschoben.  Der Clustername ist *CLUSCLUS* und mit einer Dateiserverfunktion namens *FS-CLUSCLUS*.

1. Erstellen Sie ein lokales Administratorkonto, mit dem gleichen Namen und Kennwort auf allen Servern im Cluster.  Dies kann erforderlich sein, für die Anmeldung beim Server zwischen Domänen verschoben werden.
2. Melden Sie sich an den ersten Server mit einem Domänenkonto Benutzer oder Administrator, die Active Directory-Berechtigungen auf den Cluster Name Objekt (CNO), virtuelle Computer Objekte (VCO), hat Zugriff auf den Cluster, und öffnen Sie PowerShell.
3. Sicherstellen, dass alle Cluster-Netzwerknamenressourcen sind eine Offline-Status, und führen den folgenden Befehl aus.  Dieser Befehl entfernt die Active Directory-Objekte, die der Cluster möglicherweise.

   ```PowerShell
   Remove-ClusterNameAccount -Cluster CLUSCLUS -DeleteComputerObjects
   ```
4. Verwenden Sie Active Directory-Benutzer und Computer, um sicherzustellen, dass den CNO und VCO-Computer, die alle gruppierten Namen zugeordneten Objekte entfernt wurden.

   > [!NOTE]
   > Es ist eine gute Idee, beenden den Clusterdienst auf allen Servern im Cluster und der Starttyp des Diensts auf manuell festgelegt werden, so dass der Clusterdienst gestartet wird, wenn der Server neu, beim Ändern von Domänen gestartet werden.

   ```PowerShell
   Stop-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Manual
   ```

5. Ändern Sie der Domänenmitgliedschaft für den Server zu einer Arbeitsgruppe, starten Sie Server erneut, verknüpfen Sie die Server mit der neuen Domäne und starten Sie neu.
6. Nachdem Sie die Server in der neuen Domäne sind, melden Sie sich mit einem Server mit einem Domänenkonto Benutzer oder Administrator, die Active Directory-Berechtigungen zum Erstellen von Objekten ist, hat Zugriff auf den Cluster, und öffnen Sie PowerShell. Starten Sie des Clusterdiensts an, und legen Sie sie zurück auf automatisch.

   ```PowerShell
   Start-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Automatic
   ```
7. Schalten Sie den Namen des Clusters und aller anderen Cluster-Netzwerknamenressourcen in einen Onlinestatus.

   ```PowerShell
   Start-ClusterResource -Name "Cluster Name"

   Start-ClusterResource -Name FS-CLUSCLUS
   ```

8. Ändern Sie den Cluster, um die neue Domäne mit zugeordneten active Directory-Objekten gehören. Zu diesem Zweck wird der Befehl unten ist ein, und die Netzwerknamenressourcen muss sich im Onlinestatus.  Was durchgeführt wird, mit diesem Befehl ist die Name-Objekte in Active Directory neu erstellen.

   ```PowerShell
   New-ClusterNameAccount -Name CLUSTERNAME -Domain NEWDOMAINNAME.com -UpgradeVCOs
   ```

    HINWEIS: Wenn Sie nicht über alle weiteren Gruppen Netzwerknamen (d. h. ein Hyper-V-Cluster mit nur virtuelle Computer) verfügen, wird der Schalter - UpgradeVCOs ist nicht erforderlich.

9. Verwenden Sie Active Directory-Benutzer und-Computer zum Überprüfen der neuen Domäne ein, und stellen Sie sicher, dass die zugeordneten Computerobjekte erstellt wurden. Wenn sie aufweisen, fahren Sie die verbleibenden Ressourcen in der Gruppe online.

   ```PowerShell
   Start-ClusterGroup -Name "Cluster Group"

   Start-ClusterGroup -Name FS-CLUSCLUS
   ```

## <a name="known-issues"></a>Bekannte Probleme

Wenn Sie die neue USB-Zeuge-Funktion verwenden, werden Sie nicht möglich, um den Cluster in die neue Domäne hinzuzufügen.  Der Grund dafür ist, dass der Zeuge-Dateifreigabetyp Kerberos für die Authentifizierung verwenden muss.  Ändern Sie den Zeugen auf "None", bevor Sie den Cluster mit der Domäne hinzuzufügen.  Sobald er abgeschlossen ist, erstellen Sie den Zeugen USB-neu.  Der Fehler, die angezeigt werden, ist:

```
New-ClusternameAccount : Cluster name account cannot be created.  This cluster contains a file share witness with invalid permissions for a cluster of type AdministrativeAccesssPoint ActiveDirectoryAndDns. To proceed, delete the file share witness.  After this you can create the cluster name account and recreate the file share witness.  The new file share witness will be automatically created with valid permissions.
```

