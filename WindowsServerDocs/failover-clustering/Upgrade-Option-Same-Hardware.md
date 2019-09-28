---
title: Aktualisieren von Failoverclustern mit der gleichen Hardware
ms.prod: windows-server
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 02/28/2019
description: In diesem Artikel wird beschrieben, wie Sie einen Failovercluster mit zwei Knoten mithilfe derselben Hardware aktualisieren.
ms.localizationpriority: medium
ms.openlocfilehash: 5fe93f1d43e0c3a1bc4269b585cb9d021d3461aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361397"
---
# <a name="upgrading-failover-clusters-on-the-same-hardware"></a>Aktualisieren von Failoverclustern auf derselben Hardware

> Gilt für: Windows Server 2019, Windows Server 2016

Ein Failovercluster besteht aus einer Gruppe von unabhängigen Computern, die miteinander interagieren und somit die Verfügbarkeit von Anwendungen und Diensten erhöhen. Die Clusterserver (sogenannte Knoten) sind durch physische Kabel und durch Software miteinander verbunden. Wenn auf einem der Clusterknoten ein Fehler auftritt, werden seine Aufgaben sofort auf einen anderen Knoten übertragen. Dies wird als Failover bezeichnet. So ergeben sich für die Benutzer nur minimale Unterbrechungen des Betriebs.

In dieser Anleitung werden die Schritte zum Aktualisieren der Cluster Knoten auf Windows Server 2019 oder Windows Server 2016 von einer früheren Version mit derselben Hardware beschrieben.

## <a name="overview"></a>Übersicht

Das Upgrade des Betriebssystems auf einem vorhandenen Failovercluster wird nur unterstützt, wenn Sie von Windows Server 2016 zu Windows 2019 wechseln.  Wenn auf dem Failovercluster eine frühere Version ausgeführt wird, wie z. b. Windows Server 2012 R2 und früher, können bei der Ausführung des Cluster Diensts keine Verbindungsknoten miteinander verknüpft werden.  Wenn Sie dieselbe Hardware verwenden, können Sie Schritte ausführen, um Sie auf die neuere Version zu übernehmen.  

Lesen Sie vor dem Upgrade des Failoverclusters den [Windows Server-upgradeinhalt](../upgrade/upgrade-overview.md).  Wenn Sie einen Windows-Server direkt aktualisieren, wechseln Sie von einer vorhandenen Betriebssystemversion zu einer neueren Version, während Sie auf derselben Hardware bleiben. Für Windows Server kann ein direktes Upgrade von mindestens einem ausgeführt werden, manchmal aber auch für zwei Versionen. Beispielsweise können Windows Server 2012 R2 und Windows Server 2016 direkt auf Windows Server 2019 aktualisiert werden.  Beachten Sie auch, dass der [Clustermigrations-Assistent](https://blogs.msdn.microsoft.com/clustering/2012/06/25/how-to-move-highly-available-clustered-vms-to-windows-server-2012-with-the-cluster-migration-wizard/) verwendet werden kann, jedoch nur bis zu zwei Versionen wieder unterstützt werden. Die folgende Grafik zeigt die Upgradepfade für Windows Server. Nach unten zeigende Pfeile stellen den unterstützten Upgradepfad dar, der von früheren Versionen bis zu Windows Server 2019 wechselt.

![Diagramm für ein direktes Upgrade](media/In-Place-Upgrade/In-Place-Upgrade-1.png)

Die folgenden Schritte sind ein Beispiel für den Wechsel von einem Windows Server 2012-Failoverclusterserver zu Windows Server 2019 unter Verwendung derselben Hardware.  

Stellen Sie vor dem Start eines Upgrades sicher, dass eine aktuelle Sicherung, einschließlich des Systemstatus, abgeschlossen ist.  Stellen Sie außerdem sicher, dass alle Treiber und Firmware auf die zertifizierten Stufen des Betriebssystems aktualisiert wurden, das Sie verwenden werden.  Diese beiden Notizen werden hier nicht behandelt.

Im folgenden Beispiel ist der Name des Failoverclusters Cluster, und die Knoten Namen lauten Node1 und Node2.

## <a name="step-1-evict-first-node-and-upgrade-to-windows-server-2016"></a>Schritt 1: Entfernen des ersten Knotens und Upgrade auf Windows Server 2016

1. Entfernen Sie in Failovercluster-Manager alle Ressourcen von Node1 zu Node2, indem Sie mit der rechten Maustaste auf den Knoten klicken und **Rollen**anhalten und **Entfernen auswählen.**  Alternativ können Sie den PowerShell [-Befehl Suspend-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode)verwenden.

    ![Knoten entladen](media/In-Place-Upgrade/In-Place-Upgrade-2.png)

2. Entfernen Sie Node1 aus dem Cluster, indem Sie mit der rechten Maustaste auf den Knoten klicken **und** **Weitere Aktionen** auswählen und entfernen.  Alternativ können Sie den PowerShell [-Befehl Remove-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/remove-clusternode)verwenden.

    ![Knoten entladen](media/In-Place-Upgrade/In-Place-Upgrade-3.png)

3. Trennen Sie als Vorsichtsmaßnahme Node1 vom verwendeten Speicher.  In einigen Fällen genügt das Trennen der Speicher Kabel vom Computer.  Wenden Sie sich bei Bedarf an Ihren Speicher Anbieter.  Abhängig von Ihrem Speicher ist dies möglicherweise nicht erforderlich.

4. Erstellen Sie Node1 mit Windows Server 2016 neu.  Stellen Sie sicher, dass Sie alle erforderlichen Rollen, Features, Treiber und Sicherheitsupdates hinzugefügt haben.

5. Erstellen Sie einen neuen Cluster mit dem Namen CLUSTER1 mit Node1.  Öffnen Sie Failovercluster-Manager, und wählen Sie im Bereich **Verwaltung** die Option **Cluster erstellen** aus, und befolgen Sie die Anweisungen im Assistenten.

    ![Knoten entladen](media/In-Place-Upgrade/In-Place-Upgrade-4.png)

6. Nachdem der Cluster erstellt wurde, müssen die Rollen vom ursprünglichen Cluster zu diesem neuen Cluster migriert werden.  Klicken Sie im neuen Cluster mit der rechten Maustaste auf den Cluster Namen (CLUSTER1), und wählen Sie **Weitere Aktionen** und **Cluster Rollen kopieren**aus.  Befolgen Sie die Anweisungen im Assistenten, um die Rollen zu migrieren.

    ![Knoten entladen](media/In-Place-Upgrade/In-Place-Upgrade-5.png)

7.  Nachdem alle Ressourcen migriert wurden, schalten Sie Node2 (ursprünglicher Cluster) ein, und trennen Sie den Speicher so, dass keine Störungen auftreten.  Verbinden Sie den Speicher mit Node1.  Sobald die Verbindung hergestellt ist, schalten Sie alle Ressourcen Online, und stellen Sie sicher, dass Sie wie folgt funktionieren.

## <a name="step-2-rebuild-second-node-to-windows-server-2019"></a>Schritt 2: Neuerstellen des zweiten Knotens in Windows Server 2019

Nachdem Sie überprüft haben, dass alles wie erforderlich funktioniert, kann Node2 auf Windows Server 2019 neu erstellt und dem Cluster hinzugefügt werden.

1. Führen Sie eine Neuinstallation von Windows Server 2019 auf Node2 aus. Stellen Sie sicher, dass Sie alle erforderlichen Rollen, Features, Treiber und Sicherheitsupdates hinzugefügt haben.

2. Nachdem der ursprüngliche Cluster (Cluster) nicht mehr vorhanden ist, können Sie den neuen Cluster Namen als CLUSTER1 belassen oder zum ursprünglichen Namen zurückkehren.  Wenn Sie zum ursprünglichen Namen zurückkehren möchten, führen Sie die folgenden Schritte aus:
   
   a. Klicken Sie auf Node1 in Failovercluster-Manager klicken Sie mit der rechten Maustaste auf den Namen des Clusters (CLUSTER1), und wählen Sie **Eigenschaften**aus.
   
   b. Benennen Sie den Cluster auf der Registerkarte **Allgemein** in Cluster um.

   c. Wenn Sie "OK" oder "anwenden" auswählen, wird das folgende Dialogfeld angezeigt.

    ![Knoten entladen](media/In-Place-Upgrade/In-Place-Upgrade-6.png)

    d. Der Cluster Dienst wird beendet und muss erneut gestartet werden, damit die Umbenennung beendet wird.

3. Öffnen Sie auf Node1 Failovercluster-Manager.  Klicken Sie mit der rechten Maustaste auf **Knoten** , und wählen Sie **Knoten hinzufügen**  Durchlaufen Sie den Assistenten, indem Sie Node2 zum Cluster hinzufügen.

4. Fügen Sie den Speicher an Node2 an. Dies kann das erneute Verbinden der Speicher Kabel einschließen. 

5. Entfernen Sie alle Ressourcen von Node1 zu Node2, indem Sie mit der rechten Maustaste auf den Knoten klicken und **Rollen**anhalten und **Entfernen auswählen.**  Alternativ können Sie den PowerShell [-Befehl Suspend-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode)verwenden.  Stellen Sie sicher, dass alle Ressourcen online sind und wie Sie funktionieren.

## <a name="step-3-rebuild-first-node-to-windows-server-2019"></a>Schritt 3: Neuerstellen des ersten Knotens auf Windows Server 2019

1. Entfernen Sie Node1 aus dem Cluster, und trennen Sie die Verbindung zwischen dem Speicher und dem Knoten.

2. Erneutes Erstellen oder Aktualisieren von Node1 auf Windows Server 2019.  Stellen Sie sicher, dass Sie alle erforderlichen Rollen, Features, Treiber und Sicherheitsupdates hinzugefügt haben.

3. Fügen Sie den Speicher erneut an, und fügen Sie Node1 wieder zum Cluster hinzu.

4. Verschieben Sie alle Ressourcen in Node1, und stellen Sie sicher, dass Sie online geschaltet werden und bei Bedarf funktionieren.

5. Die aktuelle Cluster Funktionsebene bleibt bei Windows 2016.  Aktualisieren Sie die Funktionsebene mit dem PowerShell [-Befehl Update-clusterfunctionallevel](https://docs.microsoft.com/powershell/module/failoverclusters/update-clusterfunctionallevel)auf Windows 2019.

Sie führen jetzt mit einem voll funktionsfähigen Windows Server 2019-Failovercluster aus.

## <a name="additional-notes"></a>Weitere Anmerkungen

- Wie bereits erläutert, ist die Trennung des Speichers möglicherweise nicht erforderlich.  Wir möchten uns in unserer Dokumentation auf der Seite mit Vorsicht befinden.  Wenden Sie sich an den Speicher Anbieter.
- Wenn als Ausgangspunkt Windows Server 2008-oder 2008 R2-Cluster verwendet wird, sind möglicherweise weitere Schritte erforderlich.
- Wenn auf dem Cluster virtuelle Computer ausgeführt werden, stellen Sie sicher, dass Sie die Ebene der virtuellen Maschine aktualisieren, sobald die Cluster Funktionsebene mit dem PowerShell [-Befehl Update-VMVersion](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion)erreicht wurde.
- Beachten Sie Folgendes: Wenn Sie eine Anwendung wie SQL Server, Exchange Server usw. ausführen, wird die Anwendung nicht mit dem Assistenten zum Kopieren von Cluster Rollen migriert.  Wenden Sie sich an den Hersteller der Anwendung, um die entsprechenden Migrations Schritte für die Anwendung auszuführen.