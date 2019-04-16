---
title: Aktualisieren von Failoverclustern mithilfe derselben Hardware
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 02/28/2019
description: Dieser Artikel beschreibt, Aktualisieren eines 2-Knoten-Failoverclusters mithilfe derselben hardware
ms.localizationpriority: medium
ms.openlocfilehash: 0bfeb05c8cbc205745dc16bc7ef04052481668ea
ms.sourcegitcommit: 2c2027b597e2483eea8967d0710d65c2247b6751
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "9121303"
---
# Aktualisieren der Failovercluster auf derselben hardware

> Gilt für: WindowsServer 2019, WindowsServer 2016

Ein Failovercluster ist eine Gruppe aus unabhängigen Computern, die miteinander interagieren zum Erhöhen der Verfügbarkeit von Anwendungen und Diensten. Die Clusterserver (sogenannte Knoten) sind durch physische Kabel und durch Software miteinander verbunden. Wenn einer der Clusterknoten ausfällt, beginnt einen anderen Knoten (ein Vorgang wird als Failover bezeichnet). Mindestens Anlass im Dienst bei Benutzern auftreten.

Dieses Handbuch beschreibt die Schritte zum Aktualisieren der Clusterknotens auf Windows Server 2019 oder Windows Server 2016 von einer früheren Version mithilfe derselben Hardware.

## Übersicht

Aktualisieren des Betriebssystems auf eine vorhandene Failover wird Cluster nur unterstützt, beim Wechseln von Windows Server 2016, Windows 2019.  Wenn der Failovercluster auf eine frühere Version ausgeführt wird, wie z. B. Windows Server 2012 R2 und früheren Versionen aktualisieren, während die Cluster-Dienste ausgeführt werden können nicht Zusammenführen von Knoten.  Wenn Sie die gleiche Hardware zu verwenden, können Schritte durchgeführt werden, um auf eine neuere Version zu erhalten.  

Vor einem Update des Failoverclusters finden Sie in der [Windows-Upgrade-Center](https://www.microsoft.com/upgradecenter).  Wenn Sie eine Windows Server direkt aktualisieren, migrieren Sie von einer bestehenden Betriebssystem-Version auf eine neuere Version und verwenden Sie dabei die gleiche Hardware. Windows Server kann es sich um aktualisierte direktes über mindestens eine und manchmal zwei Versionen vorwärts sein. Beispielsweise Windows Server 2012 R2 und Windows Server 2016 aktualisiert werden kann – direktes auf Windows Server 2019.  Auch Bedenken Sie, die den [Assistenten für die Cluster-Migration](https://blogs.msdn.microsoft.com/clustering/2012/06/25/how-to-move-highly-available-clustered-vms-to-windows-server-2012-with-the-cluster-migration-wizard/) kann verwendet werden, wird jedoch nur unterstützt bis zu zwei Versionen zurück. Die folgende Grafik zeigt die Upgradepfade für Windows Server. Nach unten zeigt Pfeile darstellen der unterstützten Upgradepfad von früheren Versionen bis zu Windows Server 2019 verschieben.

![Direktes Upgrade-Diagramm](media\In-Place-Upgrade\In-Place-Upgrade-1.png)

Die folgenden Schritte sind ein Beispiel für von einem Windows Server 2012 Failover Cluster-Server in Windows Server 2019 mithilfe derselben Hardware zu wechseln.  

Vor dem Start alle Upgrade, stellen Sie sicher, dass eine aktuelle Sicherung, einschließlich Systemstatus ausgeführt wurde.  Vergewissern Sie sich außerdem alle Treiber und Firmware aktualisiert wurden, um die zertifizierten Ebenen für das Betriebssystem, das Sie verwenden.  Diese beiden Hinweise werden hier nicht behandelt.

Im folgenden Beispiel wird der Name des Failovercluster CLUSTER und die Namen der Knoten sind Knoten 1 und Knoten 2.

## Schritt 1: Erste Knoten und upgrade auf Windows Server 2016

1. Ausgeglichen Sie im Failovercluster-Manager, alle Ressourcen von Knoten 1 auf Knoten 2 von rechten Maustaste auf den Knoten und auswählen **"Anhalten** " oder " **Rollen ausgleichen**.  Alternativ können Sie den PowerShell-Befehl [SUSPEND-CLUSTERNODE](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode)verwenden.

    ![Ausgleich Knoten](media\In-Place-Upgrade\In-Place-Upgrade-2.png)

2. Entfernen Sie Knoten 1 aus dem Cluster durch Rechte Maustaste klicken auf den Knoten und **Weitere Aktionen** und **Entfernen**auswählen.  Alternativ können Sie den PowerShell-Befehl [REMOVE-CLUSTERNODE](https://docs.microsoft.com/powershell/module/failoverclusters/remove-clusternode)verwenden.

    ![Ausgleich Knoten](media\In-Place-Upgrade\In-Place-Upgrade-3.png)

3. Trennen Sie als Vorsichtsmaßnahme Knoten 1 aus dem Speicher, die, den Sie verwenden werden.  In einigen Fällen ist der Computer die Speicherkabel trennen ausreichend.  Überprüfen Sie sich an den Speicherhersteller für die ordnungsgemäße Trennung Schritte bei Bedarf.  Je nach Ihren Speicher kann dies nicht erforderlich sein.

4. Erstellen Sie Knoten 1 mit WindowsServer 2016 neu.  Stellen Sie sicher, dass Sie alle erforderlichen Rollen, Features, Treiber und Sicherheitsupdates hinzugefügt haben.

5. Erstellen Sie einen neuen Cluster mit Knoten 1 CLUSTER1 aufgerufen.  Öffnen Sie Failovercluster-Manager, und wählen Sie im Bereich **Verwaltung** **Cluster erstellen** , und führen Sie die Schritte im Assistenten.

    ![Ausgleich Knoten](media\In-Place-Upgrade\In-Place-Upgrade-4.png)

6. Nach der Erstellung des Clusters, werden die Funktionen aus dem ursprünglichen Cluster mit diesem neuen Cluster migriert werden müssen.  Auf den neuen Cluster Rechte Maustaste klicken Sie auf die Clusternamen (CLUSTER1)- **Weitere Aktionen** und auswählen und **Kopieren Clusterrollen**.  Folgen Sie im Assistenten zum Migrieren von Rollen.

    ![Ausgleich Knoten](media\In-Place-Upgrade\In-Place-Upgrade-5.png)

7.  Nachdem alle Ressourcen migriert wurden, schalten Sie Knoten 2 (ursprünglichen Cluster), und trennen Sie den Speicher so, dass keine Störung verursachen.  Schließen Sie den Speicher an Knoten 1.  Nachdem alle verbunden ist, schalten Sie alle Ressourcen online, und stellen Sie sicher, dass sie funktionieren wie sollten.

## Schritt 2: Erstellen Sie neu zweiten Knoten auf Windows Server 2019

Nachdem Sie, dass alles überprüft haben wie gewünscht funktioniert, kann Knoten 2 neu erstellt, Windows Server 2019 und mit dem Cluster verknüpft werden.

1. Führen Sie eine Neuinstallation von Windows Server 2019 auf Knoten 2. Stellen Sie sicher, dass Sie alle erforderlichen Rollen, Features, Treiber und Sicherheitsupdates hinzugefügt haben.

2. Nachdem die ursprüngliche Cluster (CLUSTER) nicht mehr vorhanden ist, können Sie den neuen Clusternamen als CLUSTER1 lassen oder wechseln Sie zurück zu der ursprüngliche Name.  Wenn Sie der ursprüngliche Name zurückkehren möchten, gehen Sie folgendermaßen vor:
   
   a. Klicken Sie auf Knoten 1 im Failovercluster-Manager Rechte Maustaste klicken Sie auf den Namen des Clusters (CLUSTER1), und wählen Sie **Eigenschaften**aus.
   
   b. Benennen Sie auf der Registerkarte " **Allgemein** " Cluster zu-CLUSTER.

   c. Wenn Sie OK oder übernehmen auswählen, sehen Sie die unten Dialogfeld Popup.

    ![Ausgleich Knoten](media\In-Place-Upgrade\In-Place-Upgrade-6.png)

    d. Der Cluster-Dienst werden beendet und benötigt, um erneut gestartet werden, damit die Umbenennung abgeschlossen.

3. Öffnen Sie auf Knoten 1 Failovercluster-Manager.  Rechte Maustaste klicken Sie auf den **Knoten** , und wählen Sie **Knoten hinzufügen**.  Durchlaufen Sie den Assistenten Knoten 2 zum Cluster hinzufügen.

4. Fügen Sie den Speicher an Knoten 2. Dazu können gehören, erneut die Speicherkabel verbinden. 

5. Führen Sie alle Ressourcen von Knoten 1 auf Knoten 2 von rechten Maustaste klicken Sie auf den Knoten und **"Anhalten** " oder " **Rollen ausgleichen**auswählen kann.  Alternativ können Sie den PowerShell-Befehl [SUSPEND-CLUSTERNODE](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode)verwenden.  Stellen Sie sicher, alle Ressourcen online sind, und sie funktionieren wie sollten.

## Schritt 3: Erstellen Sie neu, erste Knoten auf Windows Server 2019

1. Entfernen Sie Knoten 1 aus dem Cluster und trennen Sie den Speicher von Knoten "" in die Art und Weise aus dem Sie zuvor.

2. Erstellen oder Aktualisieren von Knoten 1 auf Windows Server 2019.  Stellen Sie sicher, dass Sie alle erforderlichen Rollen, Features, Treiber und Sicherheitsupdates hinzugefügt haben.

3. Schließen Sie den Speicher wieder an, und fügen Sie Knoten 1 wieder zum Cluster hinzu.

4. Verschieben Sie alle Ressourcen auf Knoten 1, und sicherzustellen, dass sie online geschaltet und nach Bedarf funktionieren.

5. Die aktuellen Cluster-Funktionsebene bleibt Windows 2016.  Aktualisieren Sie die Funktionsebene Windows 2019 mit der PowerShell-Befehl [UPDATE-CLUSTERFUNCTIONALLEVEL](https://docs.microsoft.com/powershell/module/failoverclusters/update-clusterfunctionallevel).

Sie sind nun mit einem voll funktionsfähige Windows Server 2019 Failovercluster ausgeführt.

## Weitere Anmerkungen

- Wie zuvor erläutert, trennen den Speicher möglicherweise oder möglicherweise nicht erforderlich.  In der Dokumentation möchten wir seitlichen Vorsicht unklar.  Wenden Sie sich an den Speicher-Anbieter.
- Ist Ihr Ausgangspunkt Windows Server 2008 oder 2008 R2-Cluster, kann eine weitere Ausführung über Schritte erforderlich sein.
- Wenn der Cluster virtuellen Computer ausgeführt wird, stellen Sie sicher, dass die Ebene der virtuellen Maschine aktualisieren, sobald die Funktionsebene der Cluster mit dem PowerShell-Befehl [UPDATE-VMVERSION](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion)ausgeführt wurde.
- Bitte beachten Sie, dass, wenn Sie eine Anwendung wie z. B. SQL Server, Exchange-Server usw. ausführen, die Anwendung nicht mit dem Clusterrollen Kopie-Assistenten migriert werden.  Sie sollten den Hersteller der Anwendung ordnungsgemäße Migrationsschritte der Anwendung finden Sie in.