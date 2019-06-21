---
title: Aktualisieren von Failoverclustern, die mit derselben Hardware
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 02/28/2019
description: In diesem Artikel wird beschrieben, einen Failovercluster mit 2 Knoten mit derselben Hardware, aktualisieren
ms.localizationpriority: medium
ms.openlocfilehash: 6787d852cc5075e306373a163814135190f27fd6
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280243"
---
# <a name="upgrading-failover-clusters-on-the-same-hardware"></a>Aktualisieren von Failoverclustern auf derselben hardware

> Gilt für: Windows Server 2019, Windows Server 2016

Ein Failovercluster besteht aus einer Gruppe von unabhängigen Computern, die miteinander interagieren und somit die Verfügbarkeit von Anwendungen und Diensten erhöhen. Die Clusterserver (sogenannte Knoten) sind durch physische Kabel und durch Software miteinander verbunden. Wenn auf einem der Clusterknoten ein Fehler auftritt, werden seine Aufgaben sofort auf einen anderen Knoten übertragen. Dies wird als Failover bezeichnet. So ergeben sich für die Benutzer nur minimale Unterbrechungen des Betriebs.

Dieses Handbuch beschreibt die Schritte zum Aktualisieren der Clusterknoten 2019 für Windows Server oder Windows Server 2016 von einer früheren Version, die mit derselben Hardware.

## <a name="overview"></a>Übersicht

Upgrade des Betriebssystems auf einem vorhandenen Failovercluster wird Cluster nur unterstützt, wenn Sie von Windows Server 2016 zur Windows-2019.  Wenn Sie der Failovercluster auf eine frühere Version, z. B. Windows Server 2012 R2 und früher ausgeführt wird lässt aktualisieren, während die Cluster-Dienste ausgeführt werden nicht Knoten verknüpfen.  Wenn Sie dieselbe Hardware verwenden zu können, können Maßnahmen ergriffen werden, um es auf die neuere Version zu erhalten.  

Vor jedem Upgrade des Failoverclusters finden Sie in der [Windows Upgrade Center](https://www.microsoft.com/upgradecenter).  Wenn Sie eine Windows-Server direkt aktualisieren, verschieben Sie in einer neueren Version und verwenden dabei die gleiche Hardware von einer vorhandenen Betriebssystem-Version ein. Windows Server möglich aktualisierten direktes mindestens und manchmal zwei Versionen weiterleiten. Z. B. Windows Server 2012 R2 und Windows Server 2016 aktualisiert werden können direkt auf Windows Server-2019.  Außerdem Beachten Sie, dass die [Cluster Migration Wizard](https://blogs.msdn.microsoft.com/clustering/2012/06/25/how-to-move-highly-available-clustered-vms-to-windows-server-2012-with-the-cluster-migration-wizard/) kann verwendet werden, jedoch wird nur unterstützt, bis zu zwei Versionen zurück. Die folgende Grafik zeigt die Upgradepfade für Windows Server. Nach unten zeigenden Pfeil darstellen der unterstützte Upgradepfad von früheren Versionen bis 2019 für Windows-Server zu verschieben.

![Ein direktes Upgrade-Diagramm](media/In-Place-Upgrade/In-Place-Upgrade-1.png)

Die folgenden Schritte sind ein Beispiel der Übergang von einem Windows Server 2012 Failover Cluster-Server, Windows Server-2019 mit derselben Hardware.  

Vor jedem Upgrade zu verwenden, stellen Sie sicher, dass eine aktuelle Sicherung des Systemstatus, einschließlich erfolgt ist.  Stellen Sie außerdem sicher, alle Treiber und Firmware aktualisiert wurden, um die zertifizierten Ebenen für das Betriebssystem, das Sie verwenden.  Diese beiden Anmerkungen zu dieser Version werden hier nicht behandelt.

Im folgenden Beispiel wird der Name des Failoverclusters CLUSTER und die Knotennamen sind NODE1 und NODE2.

## <a name="step-1-evict-first-node-and-upgrade-to-windows-server-2016"></a>Schritt 1: Entfernen des ersten Knotens und ein upgrade auf Windows Server 2016

1. Im Failovercluster-Manager alle Ressourcen von Knoten1 auf Knoten2 mit der rechten Maus auf den Knoten klicken und auswählen zu leeren **anhalten** und **Rollen ausgleichen**.  Alternativ können Sie den PowerShell-Befehl [SUSPEND-CLUSTERNODE](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode).

    ![Ausgleichen von Knoten](media/In-Place-Upgrade/In-Place-Upgrade-2.png)

2. Entfernen Sie Knoten 1 aus dem Cluster, von der rechten Maustaste auf den Knoten klicken und Auswählen von **Weitere Aktionen** und **entfernen**.  Alternativ können Sie den PowerShell-Befehl [REMOVE-CLUSTERNODE](https://docs.microsoft.com/powershell/module/failoverclusters/remove-clusternode).

    ![Ausgleichen von Knoten](media/In-Place-Upgrade/In-Place-Upgrade-3.png)

3. Trennen Sie als Vorsichtsmaßnahme NODE1 aus dem Speicher, die, den Sie verwenden.  In einigen Fällen genügt der Computer die Speicherkabel trennen.  Wenden Sie sich an den Hersteller Ihrer speicherlösung für die ordnungsgemäße Trennung Schritte bei Bedarf.  Je nach Ihren Speicher kann dies nicht erforderlich sein.

4. Erstellen Sie Knoten1 mit WindowsServer 2016 neu.  Stellen Sie sicher, dass Sie alle erforderlichen Rollen, Features, Treiber und Sicherheitsupdates hinzugefügt haben.

5. Erstellen eines neuen Clusters, der Namen CLUSTER1 mit Knoten1 an.  Öffnen des Failovercluster-Manager und klicken Sie in der **Management** Bereich wählen **Clustererstellungs** und befolgen Sie die Anweisungen im Assistenten.

    ![Ausgleichen von Knoten](media/In-Place-Upgrade/In-Place-Upgrade-4.png)

6. Nachdem der Cluster erstellt wurde, müssen die Rollen aus dem ursprünglichen Cluster in dieser neuen Cluster migriert werden.  Rechten Maustaste auf den neuen Cluster, die Maus klicken Sie auf den Namen des Clusters (CLUSTER1) und Auswahl **Weitere Aktionen** und **Clusterrollen kopieren**.  Folgen Sie den Assistenten zum Migrieren von Rollen.

    ![Ausgleichen von Knoten](media/In-Place-Upgrade/In-Place-Upgrade-5.png)

7.  Nachdem Sie alle Ressourcen, die migriert wurden, die Stromversorgung NODE2 (ursprünglichen Cluster), und trennen Sie den Speicher, dass keine Störungen zu verursachen.  Verbinden Sie den Speicher auf Node1 her.  Sobald alle verbunden ist, alle Ressourcen online zu schalten, und stellen Sie sicher, dass sie funktionieren, wie sollte.

## <a name="step-2-rebuild-second-node-to-windows-server-2019"></a>Schritt 2: Zweiten Knoten zum Windows Server-2019 neu erstellen

Nachdem Sie, dass alles überprüft haben wie gewünscht, können NODE2 zu Windows Server-2019 neu erstellt und mit dem Cluster verknüpft werden.

1. Führen Sie eine Neuinstallation von Windows Server-2019 auf Node2 her. Stellen Sie sicher, dass Sie alle erforderlichen Rollen, Features, Treiber und Sicherheitsupdates hinzugefügt haben.

2. Die nun im ursprüngliche Cluster (CLUSTER) nicht mehr vorhanden ist, kann der neue Clustername als CLUSTER1 lassen oder wechseln Sie zurück zu den ursprünglichen Namen.  Wenn Sie auf den ursprünglichen Namen zurückkehren möchten, gehen Sie wie folgt vor:
   
   a. Auf Node1 her, klicken Sie im Failovercluster-Manager-Rechte Maustaste klicken Sie auf den Namen des Clusters (CLUSTER1), und wählen Sie **Eigenschaften**.
   
   b. Auf der **allgemeine** Registerkarte, benennen Sie den Cluster, Cluster.

   c. Wenn OK oder übernehmen Sie auswählen, sehen Sie die unten dargestellte Popupfenster Dialogfeld angezeigt.

    ![Ausgleichen von Knoten](media/In-Place-Upgrade/In-Place-Upgrade-6.png)

    d. Der Clusterdienst werden beendet und musste erneut gestartet werden, damit die Umbenennung abgeschlossen werden.

3. Öffnen Sie auf Node1 her die Failovercluster-Manager.  Auf der rechten Maustaste **Knoten** , und wählen Sie **AddNode**.  Wechseln Sie mithilfe des Assistenten NODE2 dem Cluster hinzufügen.

4. Fügen Sie den Speicher auf NODE2. Dazu gehören die Erneutes Anschließen der Speicherkabel. 

5. Alle Ressourcen von Knoten1 auf Knoten2 mit der rechten Maus auf den Knoten klicken und auswählen zu leeren **anhalten** und **Rollen ausgleichen**.  Alternativ können Sie den PowerShell-Befehl [SUSPEND-CLUSTERNODE](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode).  Stellen Sie sicher, alle Ressourcen online sind und sie funktionieren, wie sollte.

## <a name="step-3-rebuild-first-node-to-windows-server-2019"></a>Schritt 3: Ersten Knoten auf Windows Server-2019 neu erstellen

1. Entfernen Sie Knoten 1 aus dem Cluster, und trennen Sie den Speicher über den Knoten in die Art und Weise, in die Sie zuvor.

2. Neu erstellen oder Aktualisieren von Knoten1 auf Windows Server-2019.  Stellen Sie sicher, dass Sie alle erforderlichen Rollen, Features, Treiber und Sicherheitsupdates hinzugefügt haben.

3. Fügen Sie den Speicher erneut ein, und fügen Sie Knoten1 wieder dem Cluster hinzu.

4. Verschieben Sie alle Ressourcen auf Node1 her, und stellen Sie sicher, sie online geschaltet und Funktion wie erforderlich.

5. Die Funktionsebene des aktuellen Clusters bleibt auf der Windows 2016.  Aktualisieren Sie die Funktionsebene auf Windows 2019, mit dem PowerShell-Befehl [UPDATE-CLUSTERFUNCTIONALLEVEL](https://docs.microsoft.com/powershell/module/failoverclusters/update-clusterfunctionallevel).

Sie sind jetzt mit einer voll funktionsfähigen Windows-Failovercluster für den Server 2019 ausgeführt.

## <a name="additional-notes"></a>Weitere Anmerkungen

- Wie zuvor erläutert wurde, trennen den Speicher kann oder möglicherweise nicht erforderlich.  In unserer Dokumentation möchten wir Verbindungsschutzes err.  Wenden Sie sich mit Ihrem Speicherhersteller.
- Ist der Ausgangspunkt, Windows Server 2008 oder 2008 R2-Cluster, kann eine zusätzliche Ausführen der Schritte erforderlich sein.
- Wenn der Cluster auf virtuellen Computern ausgeführt wird, vergewissern Sie sich upgrade Ebene der virtuellen Maschine, sobald die Funktionsebene des Clusters mit dem PowerShell-Befehl ausgeführt wurde [UPDATE-VMVERSION](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion).
- Bitte beachten Sie, dass wenn Sie eine Anwendung z. B. SQL Server, Exchange Server usw. ausgeführt werden, die Anwendung nicht mit dem Assistenten für die Clusterrollen migriert werden.  Sie sollten den Anwendungshersteller, entsprechenden Migrationsschritte der Anwendung finden Sie in.