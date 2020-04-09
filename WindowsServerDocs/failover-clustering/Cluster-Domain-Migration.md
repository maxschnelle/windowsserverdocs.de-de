---
title: Domänen übergreifende Cluster Migration in Windows Server 2016/2019
description: In diesem Artikel wird das Verschieben eines Windows Server 2019-Clusters von einer Domäne in eine andere beschrieben.
ms.prod: windows-server
manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.author: johnmar
ms.date: 01/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: ba556b5a00f3932e2049135b177a7ad8bbceec9c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80828293"
---
# <a name="failover-cluster-domain-migration"></a>Migration der failoverclusterdomäne

> Gilt für: Windows Server 2019, Windows Server 2016

Dieses Thema enthält eine Übersicht über das Verschieben von Windows Server-Failoverclustern von einer Domäne in eine andere.

## <a name="why-migrate-between-domains"></a>Gründe für die Migration zwischen Domänen

Es gibt mehrere Szenarios, in denen das Migrieren eines Clusters von einem doamin zu einem anderen notwendig ist.

- CompanyA wird zusammen mit CompanyB zusammengeführt und muss alle Cluster in die Domäne "CompanyA" verschieben.
- Cluster werden im Hauptrechenzentrum erstellt und an Remote Standorten ausgeliefert.
- Der Cluster wurde als Arbeitsgruppen Cluster erstellt und muss nun Teil einer Domäne sein.
- Der Cluster wurde als Domänen Cluster erstellt und muss nun Teil einer Arbeitsgruppe sein.
- Der Cluster wird in einen anderen Bereich des Unternehmens verschoben und ist eine andere Unterdomäne.

Microsoft bietet keine Unterstützung für Administratoren, die versuchen, Ressourcen von einer Domäne in eine andere zu verschieben, wenn der zugrunde liegende Anwendungs Vorgang nicht unterstützt wird. Beispielsweise bietet Microsoft keine Unterstützung für Administratoren, die versuchen, einen Microsoft Exchange-Server von einer Domäne in eine andere zu verschieben.

   > [!WARNING]
   > Es wird empfohlen, dass Sie eine vollständige Sicherung des gesamten freigegebenen Speichers im Cluster durchführen, bevor Sie den Cluster verschieben.

## <a name="windows-server-2016-and-earlier"></a>Windows Server 2016 und früher

In Windows Server 2016 und früher hatte die Clusterdienst nicht die Möglichkeit, von einer Domäne in eine andere zu wechseln.  Dies war auf die zunehmende Abhängigkeit von Active Directory Domain Services und den erstellten virtuellen Namen zurückzuführen.   

## <a name="options"></a>Optionen

Um eine solche Verschiebung durchzuführen, gibt es zwei Optionen.

Die erste Option besteht darin, den Cluster zu zerstören und in der neuen Domäne neu zu erstellen.

![Zerstören und neu erstellen](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-1.gif)

Wie die Animation zeigt, ist diese Option mit den folgenden Schritten destruktiv:

1. Zerstören Sie den Cluster.
2. Ändern Sie die Domänen Mitgliedschaft der Knoten in die neue Domäne.
3. Erstellen Sie den Cluster neu in der aktualisierten Domäne.  Dies würde dazu führen, dass alle Ressourcen neu erstellt werden müssen.

Die zweite Option ist weniger destruktiv, erfordert jedoch zusätzliche Hardware, da ein neuer Cluster in der neuen Domäne erstellt werden muss.  Wenn sich der Cluster in der neuen Domäne befindet, führen Sie den Clustermigrations-Assistenten aus, um die Ressourcen zu migrieren. Beachten Sie, dass dadurch keine Daten migriert werden. Sie müssen ein anderes Tool zum Migrieren von Daten verwenden, z. b. den [Speicher Migrationsdienst](../storage/storage-migration-service/overview.md)(nachdem die Cluster Unterstützung hinzugefügt wurde).

![Erstellen und Migrieren](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-2.gif)

Wie die Animation zeigt, ist diese Option nicht destruktiv, erfordert jedoch entweder eine andere Hardware oder einen Knoten aus dem vorhandenen Cluster, als entfernt wurde.

1. Erstellen Sie eine neue Domäne, während der alte Cluster weiterhin verfügbar ist.
2. Verwenden Sie den [Clustermigrations-Assistenten](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754481(v=ws.10)) , um alle Ressourcen in den neuen Cluster zu migrieren. Erinnerung: Dadurch werden keine Daten kopiert, daher muss Sie separat durchgeführt werden.
3. Entfernen oder zerstören Sie den alten Cluster.

Bei beiden Optionen muss auf dem neuen Cluster alle [Cluster fähigen Anwendungen](https://technet.microsoft.com/aa369082(v=vs.90)) installiert sein, die Treiber sind auf dem neuesten Stand und möglicherweise Tests, um sicherzustellen, dass alles ordnungsgemäß ausgeführt wird.  Dies ist ein zeitaufwändiger Prozess, wenn Daten ebenfalls verschoben werden müssen.

## <a name="windows-server-2019"></a>Windows Server 2019

In Windows Server 2019 wurden Migrations Funktionen für Cluster übergreifende Domänen eingeführt.  Nun können die oben aufgeführten Szenarien problemlos durchgeführt werden, und die Notwendigkeit der Neuerstellung ist nicht mehr erforderlich.  

Das Verschieben eines Clusters aus einer Domäne ist ein geradliniger Prozess. Hierfür gibt es zwei neue PowerShell-Cmdlets.

**New-clusternameaccount** – erstellt ein Cluster Namen Konto in Active Directory **Remove-clusternameaccount** – entfernt die Cluster Namen Konten aus Active Directory

Um dies zu erreichen, müssen Sie den Cluster von einer Domäne in eine Arbeitsgruppe und zurück in die neue Domäne ändern.  Es ist nicht erforderlich, einen Cluster zu zerstören, einen Cluster neu zu erstellen, Anwendungen zu installieren usw. Dies sieht beispielsweise wie folgt aus:

![Migrieren](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-3.gif)

## <a name="migrating-a-cluster-to-a-new-domain"></a>Migrieren eines Clusters zu einer neuen Domäne

In den folgenden Schritten wird ein Cluster von der contoso.com-Domäne in die neue fabrikam.com-Domäne verschoben.  Der Cluster Name ist *clusclus* und verfügt über eine Dateiserver Rolle namens *FS-clusclus*.

1. Erstellen Sie ein lokales Administrator Konto mit dem gleichen Namen und Kennwort auf allen Servern im Cluster.  Dies ist möglicherweise erforderlich, um sich anzumelden, während die Server zwischen Domänen verschoben werden.
2. Melden Sie sich beim ersten Server mit einem Domänen Benutzer-oder Administrator Konto an, das über Active Directory Berechtigungen für das Cluster Namen Objekt (CNO), virtuelle Computer Objekte (VCO) verfügt, Zugriff auf den Cluster hat, und öffnen Sie PowerShell.
3. Stellen Sie sicher, dass alle Cluster Netzwerk-namens Ressourcen offline sind, und führen Sie den folgenden Befehl aus.  Mit diesem Befehl werden die Active Directory Objekte entfernt, die möglicherweise vom Cluster verwendet werden.

   ```PowerShell
   Remove-ClusterNameAccount -Cluster CLUSCLUS -DeleteComputerObjects
   ```
4. Verwenden Sie Active Directory-Benutzer und-Computer, um sicherzustellen, dass die diesem Cluster Namen zugeordneten CNO-und VCO-Computer Objekte entfernt wurden.

   > [!NOTE]
   > Es empfiehlt sich, die Clusterdienst auf allen Servern im Cluster zu beenden und den Starttyp des Dienst auf "manuell" festzulegen, damit das Clusterdienst nicht startet, wenn die Server beim Ändern von Domänen neu gestartet werden.

   ```PowerShell
   Stop-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Manual
   ```

5. Ändern Sie die Domänen Mitgliedschaft der Server in eine Arbeitsgruppe, starten Sie die Server neu, fügen Sie die Server der neuen Domäne hinzu, und starten Sie erneut.
6. Wenn sich die Server in der neuen Domäne befinden, melden Sie sich bei einem Server mit einem Domänen Benutzer-oder Administrator Konto an, das über Active Directory Berechtigungen zum Erstellen von Objekten, Zugriff auf den Cluster und Öffnen von PowerShell verfügt. Starten Sie den Cluster Dienst, und legen Sie ihn wieder auf automatisch fest.

   ```PowerShell
   Start-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Automatic
   ```
7. Schalten Sie den Cluster Namen und alle anderen Cluster Netzwerk-namens Ressourcen in den Online Zustand.

   ```PowerShell
   Start-ClusterResource -Name "Cluster Name"

   Start-ClusterResource -Name FS-CLUSCLUS
   ```

8. Ändern Sie den Cluster so, dass er Teil der neuen Domäne mit zugeordneten Active Directory-Objekten ist. Zu diesem Zweck ist der Befehl unten angegeben, und die Netzwerknamen Ressourcen müssen sich in einem Online Status befinden.  Mit diesem Befehl werden die namens Objekte in Active Directory neu erstellt.

   ```PowerShell
   New-ClusterNameAccount -Name CLUSTERNAME -Domain NEWDOMAINNAME.com -UpgradeVCOs
   ```

    Hinweis: Wenn Sie keine zusätzlichen Gruppen mit Netzwerknamen haben (d. h. ein Hyper-V-Cluster mit nur virtuellen Computern), wird der Schalter-upgradevcos Parameter nicht benötigt.

9. Verwenden Sie Active Directory Benutzer und Computer, um die neue Domäne zu überprüfen und sicherzustellen, dass die zugeordneten Computer Objekte erstellt wurden. Wenn dies der Fall ist, schalten Sie die verbleibenden Ressourcen in den Gruppen online.

   ```PowerShell
   Start-ClusterGroup -Name "Cluster Group"

   Start-ClusterGroup -Name FS-CLUSCLUS
   ```

## <a name="known-issues"></a>Bekannte Probleme

Wenn Sie die neue USB-Zeugen Funktion verwenden, können Sie den Cluster nicht der neuen Domäne hinzufügen.  Der Grund dafür ist, dass der Dateifreigabezeuge Kerberos für die Authentifizierung verwenden muss.  Ändern Sie den Zeugen in None, bevor Sie den Cluster der Domäne hinzufügen.  Nachdem der Vorgang abgeschlossen ist, erstellen Sie den USB-Zeugen neu.  Der folgende Fehler wird angezeigt:

```
New-ClusternameAccount : Cluster name account cannot be created.  This cluster contains a file share witness with invalid permissions for a cluster of type AdministrativeAccesssPoint ActiveDirectoryAndDns. To proceed, delete the file share witness.  After this you can create the cluster name account and recreate the file share witness.  The new file share witness will be automatically created with valid permissions.
```

