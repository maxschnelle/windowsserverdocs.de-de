---
title: Paralleles Upgrade für Clusterbetriebssystem
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: get-started-article
ms.assetid: 6e102c1f-df26-4eaa-bc7a-d0d55d3b82d5
author: jasongerend
ms.author: jgerend
ms.date: 03/27/2018
ms.openlocfilehash: 60dacf63f1a355b961f84169060dbd7122a6fd32
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842731"
---
# <a name="cluster-operating-system-rolling-upgrade"></a>Cluster Upgrades des clusterbetriebssystems

> Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Cluster OS Rolling Upgrade kann ein Administrator das Betriebssystem der Clusterknoten zu aktualisieren, ohne Unterbrechung von Hyper-V oder Workloads des Dateiservers für horizontales Skalieren. Mit diesem Feature können die Downtimesanktionen laut Vereinbarungen zum Servicelevel (Service Level Agreements, SLA) vermieden werden.

Cluster OS Rolling Upgrade, bietet die folgenden Vorteile:

- Failovercluster mit Hyper-V-Computer und arbeitsauslastungen von Skalierung (Scale-Out-Datei Server, SOFS) können von Windows Server 2012 R2 (auf allen Knoten im Cluster ausgeführt) auf Windows Server 2016 (ausgeführt auf allen Clusterknoten des Clusters) ohne Ausfallzeiten aktualisiert werden. Andere arbeitsauslastungen, z. B. SQL Server, steht während des Zeitraums (in der Regel weniger als fünf Minuten) um ein Failover auf Windows Server 2016 dauert.  
- Es ist keine zusätzlichen Hardware erforderlich. Obwohl Sie zusätzliche hinzufügen können verarbeiten Clusterknoten vorübergehend mit kleinen Clustern zum Verbessern der Verfügbarkeit des Clusters während der Cluster OS Rolling Upgrade.  
- Der Cluster muss nicht beendet oder neu gestartet werden.  
- Ein neuer Cluster ist nicht erforderlich. Der vorhandene Cluster wird aktualisiert. Darüber hinaus werden in Active Directory gespeicherten vorhandenen Clusterobjekten verwendet.  
- Der Upgradevorgang kann rückgängig gemacht werden, bis der Kunde möchte die "Punkt-von-ohne Rückgabe", wenn alle Clusterknoten Windows Server 2016 ausgeführt werden, und wenn das Update-ClusterFunctionalLevel-PowerShell-Cmdlet ausgeführt wird.  
- Der Cluster kann das Patchen und Wartungsvorgänge unterstützt, während der Ausführung in den gemischten-OS-Modus.  
- Es unterstützt die Automatisierung mithilfe von PowerShell oder WMI.  
- Die öffentliche Eigenschaft des Clusters **ClusterFunctionalLevel** Eigenschaft gibt den Status des Clusters auf Windows Server 2016-Clusterknoten. Diese Eigenschaft kann mithilfe des PowerShell-Cmdlets von einem Windows Server 2016-Clusterknoten, der zu einem Failovercluster gehört abgefragt werden:  
    ```PowerShell
    Get-Cluster | Select ClusterFunctionalLevel  
    ```  

    Der Wert **8** gibt an, dass der Cluster auf der Funktionsebene von Windows Server 2012 R2 ausgeführt wird. Der Wert **9** gibt an, dass der Cluster auf der Funktionsebene von Windows Server 2016 ausgeführt wird.  

Dieses Handbuch beschreibt die verschiedenen Phasen des dem Prozess Cluster OS Rolling Upgrade, Installationsschritte, Einschränkungen für Funktionen und häufig gestellte Fragen (FAQs) und gilt für die folgenden Cluster OS Rolling Upgrade-Szenarien in Windows Server 2016:  
- Hyper-V-Cluster  
- Scale-Out-Dateiservercluster  

Das folgende Szenario ist in Windows Server 2016 nicht unterstützt:  
-  Upgrade für Clusterbetriebssysteme von gastclustern mithilfe von virtuellen Festplatte (vhdx-Datei) als freigegebener Speicher  

Cluster OS Rolling Upgrade wird vollständig von System Center Virtual Machine Manager (SCVMM) 2016 unterstützt. Wenn Sie SCVMM 2016 verwenden, finden Sie unter [ausführen ein paralleles Upgrades eines Hyper-V-Hostclusters auf Windows Server 2016 in VMM](https://docs.microsoft.com/system-center/vmm/hyper-v-rolling-upgrade?view=sc-vmm-1807) Anweisungen zum Aktualisieren der Cluster, und automatisieren die Schritte, die in diesem Dokument beschrieben werden.  

## <a name="requirements"></a>Anforderungen  
Schließen Sie die folgenden Anforderungen, bevor Sie den Prozess Cluster OS Rolling Upgrade:

- Beginnen Sie mit einem Failovercluster unter Windows Server (Halbjährlicher Kanal), Windows Server 2016 oder Windows Server 2012 R2.
- Aktualisieren eines "direkte Speicherplätze"-Clusters auf Windows Server wird Version 1709 nicht unterstützt.
- Ist der clusterworkload Hyper-V-VMs oder Scale-Out File Server, können Sie ohne Ausfallzeiten Upgrade erwarten.
- Stellen Sie sicher, dass die Hyper-V-Knoten CPUs, die-Adressierung Tabelle SLAT (Second Level verfügen) mit einer der folgenden Methoden unterstützen;  
        – Überprüfen Sie die [Sie SLAT kompatibel sind? WP8 SDK Tipp 01](http://blogs.msdn.com/b/devfish/archive/2012/11/06/are-you-slat-compatible-wp8-sdk-tip-01.aspx) Artikel, der beschreibt zwei Methoden zum Überprüfen, ob eine CPU Vorfluegel unterstützt  
        – Herunterladen der [Coreinfo v3.31](https://technet.microsoft.com/sysinternals/cc835722) Tool, um zu bestimmen, ob eine CPU SLAT unterstützt.

## <a name="cluster-transition-states-during-cluster-os-rolling-upgrade"></a>Cluster-Übergänge zwischen Zuständen während der Cluster OS Rolling Upgrade

Dieser Abschnitt beschreibt die verschiedenen Übergangsstatus von der Windows Server 2012 R2-Cluster, der auf Windows Server 2016 mit Cluster OS Rolling Upgrade aktualisiert wird.  

Damit bleibt der Cluster-Workloads, die während des Prozess Cluster OS Rolling Upgrade, verschieben eine clusterarbeitsauslastung von einem Windows Server 2012 R2-Knoten auf Windows Server 2016 ausgeführt funktioniert Knoten, als würden beide Knoten des Windows Server 2012 R2-Betriebssystems ausgeführt. Wenn Windows Server 2016-Knoten zum Cluster hinzugefügt werden, arbeiten sie in einem Kompatibilitätsmodus von Windows Server 2012 R2. Ein neuen konzeptionellen Clustermodus, dem Namen "Mixed-OS-Mode", kann Knoten mit unterschiedlichen Versionen in der gleichen vorhanden sein (siehe Abbildung 1)-cluster.  

![Abbildung zeigt die drei Phasen eines parallelen Upgrades von Cluster-Betriebssystemtypen: alle Knoten Windows Server 2012 R2, mixed-OS-Modus und allen Knoten Windows Server 2016](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Overview.png)  
**Abbildung 1: Cluster-Betriebssystem-Statusübergänge**  

Ein Windows Server 2012 R2-Cluster in den gemischten-OS wechselt, wenn ein Windows Server 2016-Knoten zum Cluster hinzugefügt wird. Der Prozess ist vollständig rückgängig gemacht werden: Windows Server 2016-Knoten können aus dem Cluster entfernt werden, und mit dem Cluster in diesem Modus können Windows Server 2012 R2-Knoten hinzugefügt werden. Die "Punkt kein zurück" tritt auf, wenn das Update-ClusterFunctionalLevel-PowerShell-Cmdlet auf dem Cluster ausgeführt wird. Damit für dieses Cmdlet erfolgreich ausgeführt werden kann müssen alle Knoten Windows Server 2016, und alle Knoten müssen online sein.  

## <a name="transition-states-of-a-four-node-cluster-while-performing-rolling-os-upgrade"></a>Übergänge zwischen Zuständen, der ein Cluster mit vier Knoten beim Ausführen von OS Rolling Upgrade werden.

In diesem Abschnitt wird veranschaulicht, und beschreibt die vier verschiedenen Stufen eines Clusters mit freigegebenem Speicher, dessen Knoten von Windows Server 2012 R2 auf Windows Server 2016 aktualisiert werden.  

"Phase 1" ist der anfängliche Status – wir beginnen mit einem Windows Server 2012 R2-Cluster.  

![Abbildung mit den ursprünglichen Zustand: alle Knoten Windows Server 2012 R2](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage1.png)  
**Abbildung 2: Anfangszustand: Windows Server 2012 R2-Failovercluster (Stufe 1)**  

In "Phase 2", zwei Knoten angehalten, ausgeglichen, entfernt, neu formatiert und wurden mit Windows Server 2016 installiert.  

![Abbildung mit dem Cluster im gemischten-OS-Modus: aus dem Beispiel für Cluster mit 4 Knoten, zwei Knoten Windows Server 2016 ausgeführt werden, und zwei Knoten Windows Server 2012 R2 ausgeführt werden](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage2.png)  
**Abbildung 3: Intermediate-Status: Mixed-OS-Modus: Windows Server 2012 R2 und Windows Server 2016 Failover Cluster (Stufe 2)**  

Unter "Schritt 3", alle Knoten im Cluster auf Windows Server 2016 aktualisiert wurden und der Cluster ist mit der Update-ClusterFunctionalLevel-PowerShell-Cmdlet aktualisiert werden.  

> [!NOTE]  
> In dieser Phase wird der Prozess vollständig umgekehrt werden kann, und Windows Server 2012 R2-Knoten können mit diesem Cluster hinzugefügt werden.  

![Abbildung zeigt, dass der Cluster vollständig zu Windows Server 2016 aktualisiert wurde, wird für das Cmdlet Update-ClusterFunctionalLevel bereit, die Funktionsebene des Clusters, bis Windows Server 2016 zu öffnen.](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage3.png)  
**Abbildung 4: Intermediate-Status: Alle Knoten, die ein Upgrade auf Windows Server 2016, bereit für die Update-ClusterFunctionalLevel (Stufe 3)**  

Nach dem Ausführen der Update-ClusterFunctionalLevelcmdlet gibt der Cluster "Schritt 4", wo die neuen Features von Windows Server 2016-Cluster verwendet werden kann.  

![Die Abbildung zeigt, dass der Cluster, das parallele Betriebssystemupgrade erfolgreich abgeschlossen wurde; alle Knoten auf Windows Server 2016 aktualisiert wurden, und der Cluster auf der Funktionsebene der Windows Server 2016-Cluster ausgeführt wird](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage4.png)  
**Abbildung 5: Endzustand: Windows Server 2016-Failovercluster (Stufe 4)**  

## <a name="cluster-os-rolling-upgrade-process"></a>Ein paralleles Upgrade eines Cluster-Betriebssystem

Dieser Abschnitt beschreibt den Workflow zum Ausführen von Cluster OS Rolling Upgrade.  

![Abbildung zeigt den Workflow für das Aktualisieren eines Clusters](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Workflow.png)  
**Abbildung 6: Cluster OS Rolling Upgrade-Prozess-Workflow**  

Cluster OS Rolling Upgrade umfasst die folgenden Schritte aus:  

1. Bereiten Sie den Cluster für die Aktualisierung des Betriebssystems wie folgt vor:  
    1. Cluster OS Rolling Upgrade, ist das Entfernen eines Knotens im Cluster zu einem Zeitpunkt erforderlich. Überprüfen Sie, ob Sie über genügend Kapazität verfügen, auf dem Cluster, HA-SLAs zu, wenn einer der Clusterknoten vom Cluster für ein Upgrade des Betriebssystems entfernt wird. Das heißt, benötigen Sie die Möglichkeit zum Failover von Workloads zu einem anderen Knoten, wenn ein Knoten aus dem Cluster, während der Prozess Cluster OS Rolling Upgrade entfernt wird? Verfügt der Cluster über die Kapazität für die erforderlichen arbeitsauslastungen ausgeführt werden, wenn ein Knoten für Cluster OS Rolling Upgrade aus dem Cluster entfernt wird?  
    2. Für Hyper-V-Workloads überprüfen, ob alle Windows Server 2016 Hyper-V-Hosts CPU Second-Level Address-Tabelle (SLAT) unterstützt. Nur SLAT-fähiger Computer können die Hyper-V-Rolle in Windows Server 2016 verwenden.  
    3. Überprüfen Sie, dass die arbeitsauslastungssicherungen abgeschlossen wurden, und Sichern des Clusters. Beenden Sie Sicherungsvorgänge, beim Hinzufügen von Knoten zum Cluster.  
    4. Überprüfen Sie, dass alle Clusterknoten online sind/Ausführung vertikale mithilfe der [ `Get-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterNode?view=win10-ps) Cmdlet (siehe Abbildung 7).  

        ![Abbildung zeigt die Ergebnisse der Ausführung des Cmdlets Get-ClusterNode](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterNode.png)  
        **Abbildung 7: Bestimmen mithilfe des Cmdlet "Get-ClusterNode" Knotenstatus**  

    5. Wenn Sie Cluster Aware Updates (CAU) ausgeführt werden, überprüfen Sie, ob für clusterfähiges aktualisieren derzeit ausgeführt wird, mit der **Aktualisieren von Cluster-zu-bekannt** -Benutzeroberfläche oder die [ `Get-CauRun` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Get-CauRun?view=win10-ps) Cmdlet (siehe Abbildung 8). Beenden der Verwendung von CAU die [ `Disable-CauClusterRole` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole?view=win10-ps) Cmdlet (siehe Abbildung 9), um zu verhindern, dass alle Knoten von CAU ausgeglichen werden, während des Prozess Cluster OS Rolling Upgrade und angehalten.  

        ![Abbildung mit der Ausgabe des Cmdlets Get-CauRun](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetCAU.png)  
        **Abbildung 8: Mithilfe der [ `Get-CauRun` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Get-CauRun?view=win10-ps) Cmdlet, um zu bestimmen, ob clusterfähigen Aktualisierungen auf dem Cluster ausgeführt wird**  

        ![Abbildung mit der Ausgabe des Cmdlets Disable-CauClusterRole](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_DisableCAU.png)  
        **Abbildung 9: Deaktivieren der clusterfähigen Aktualisierungen mithilfe der [ `Disable-CauClusterRole` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole?view=win10-ps) Cmdlet**  

2. Führen Sie für jeden Knoten im Cluster die folgenden Schritte aus:  
    1. Verwenden die Cluster-Manager-UI, wählen Sie einen Knoten, und Verwenden der **anhalten | Leeren** Menüoption zum Ausgleichen des Knotens (siehe Abbildung 10) oder verwenden Sie die [ `Suspend-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Suspend-ClusterNode?view=win10-ps) Cmdlet (siehe Abbildung 11).  

        ![Abbildung zeigt, wie Rollen mit der Cluster-Manager-UI zu beseitigen](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_FCM_DrainRoles.png)  
        **Abbildung 10: Leeren von Rollen von einem Knoten mit dem Failovercluster-Manager**  

        ![Abbildung mit der Ausgabe des Cmdlets Suspend-ClusterNode](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SuspendNode.png)  
        **Abbildung 11: Leeren von Rollen von einem Knoten unter Verwendung der [ `Suspend-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Suspend-ClusterNode?view=win10-ps) Cmdlet**  

    2.  Cluster-Manager-UI mit **entfernen** den angehaltenen Knoten aus Cluster, oder verwenden Sie die [ `Remove-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Remove-ClusterNode?view=win10-ps) Cmdlet.  

        ![Abbildung mit der Ausgabe des Cmdlets Get-ClusterNode entfernen](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_RemoveNode.png)  
        **Abbildung 12: Entfernen eines Knotens aus dem Cluster mit [ `Remove-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Remove-ClusterNode?view=win10-ps) Cmdlet**  

    3.  Formatieren von das Systemlaufwerk und eine "Neuinstallation des Betriebssystems Install" von Windows Server 2016 ausführen, auf dem Knoten mit der **benutzerdefinierte: Nur Windows zu installieren (Erweitert)** Installationsoption (Siehe abbildung13) in setup.exe. Vermeiden Sie die Auswahl der **aktualisieren: Installieren von Windows und Beibehalten von Dateien, Einstellungen und Anwendungen** option, da Cluster OS Rolling Upgrade keine direkten Upgrades empfehlen.  

        ![Abbildung des Windows Server 2016-Installations-Assistenten, die mit der ausgewählten Option für benutzerdefinierte Installation](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_InstallOption.png)  
        **Abbildung 13: Verfügbaren Installationsoptionen für Windows Server 2016**  

    4.  Fügen Sie den Knoten mit der entsprechenden Active Directory-Domäne hinzu.  
    5.  Fügen Sie die entsprechenden Benutzer der Gruppe "Administratoren" hinzu.  
    6.  Mithilfe des Server-Manager-UI oder Install-WindowsFeature-PowerShell-Cmdlets, installieren Sie alle Serverrollen, die Sie benötigen, können Sie z. B. Hyper-V.  

        ```PowerShell
        Install-WindowsFeature -Name Hyper-V  
        ```  

    7.  Mithilfe des Server-Manager-UI oder Install-WindowsFeature-PowerShell-Cmdlets, installieren Sie das Feature "Failoverclustering".  

        ```PowerShell
        Install-WindowsFeature -Name Failover-Clustering  
        ```  

    8.  Installieren Sie alle zusätzlichen Funktionen, die von Ihrer clusterarbeitsauslastung benötigt werden.  
    9. Überprüfen Sie die Netzwerk- und Einstellungen für die Netzwerkkonnektivität mit dem Failovercluster-Manager-UI.  
    10. Wenn es sich bei Windows-Firewall verwendet wird, überprüfen Sie, dass die Firewall-Einstellungen für den Cluster richtig sind. Unter Umständen Cluster Aware aktualisieren (CAU) aktiviert Cluster z. B. Konfiguration der Firewall.  
    11. Verwenden Sie für Hyper-V-Workloads, die Hyper-V-Manager-Benutzeroberfläche, um das Dialogfeld "Manager für virtuelle Switches" zu starten (siehe Abbildung 14).  

        Überprüfen Sie, dass der Name der den virtuellen Switches verwendet für alle Knoten der Hyper-V-Hosts im Cluster identisch sind.  

        ![Abbildung, das die Position im Dialogfeld für die Hyper-V-Manager für virtuelle Switches](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_VMSwitch.png)  
        **Abbildung 14: Manager für virtuelle Switches**  

    12. Auf einem Windows Server 2016-Knoten (einen Windows Server 2012 R2-Knoten nicht verwenden), verwenden Sie den Failovercluster-Manager (siehe Abbildung 15), um mit dem Cluster herstellen.  

        ![Abbildung zeigt das Dialogfeld "select-Cluster"](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode.png)  
        **Abbildung 15: Hinzufügen eines Knotens mit dem Cluster über Failovercluster-Manager**  

    13. Verwenden Sie entweder den Failovercluster-Manager-UI oder der [ `Add-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Add-ClusterNode?view=win10-ps) Cmdlet (siehe Abbildung 16), um den Knoten zum Cluster hinzuzufügen.  

        ![Abbildung mit der Ausgabe des Cmdlets Add-ClusterNode](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode3.png)  
        **Abbildung 16: Hinzufügen eines Knotens mit dem Cluster [ `Add-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Add-ClusterNode?view=win10-ps) Cmdlet**  

        > [!NOTE]  
        > Bei der erste Windows Server 2016-Knoten dem Cluster beitritt, der Cluster in den "Mixed-Betriebssystem" wechselt, und die Hauptressourcen des Clusters verschoben werden, auf den Knoten Windows Server 2016. Ein "Mixed-Betriebssystem"-Modus-Cluster ist eine voll funktionsfähige Cluster, auf dem neuen Knoten in einem Kompatibilitätsmodus mit den alten Knoten ausgeführt. "Gemischten OS"-Modus ist eine vorübergehende für den Cluster. Es nicht permanent sein soll, und Kunden sollen alle Knoten ihre Cluster innerhalb von vier Wochen zu aktualisieren.  

    14. Nach Windows Server 2016 Knoten wird erfolgreich dem Cluster hinzugefügt, (optional) einige der clusterworkload den neu hinzugefügten Knoten verschoben werden können zum Ausgleichen von der Workloads im Cluster wie folgt:

        ![Abbildung mit der Ausgabe des Cmdlets "Move-ClusterVirtualMachineRole der"](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_MoveVMRole.png)  
        **Abbildung 17: Verschieben einer Workload (Cluster-VM-Rolle)-Cluster verwenden [ `Move-ClusterVirtualMachineRole` ](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterVirtualMachineRole?view=win10-ps) Cmdlet**  

        1. Verwendung **Livemigration** aus dem Failovercluster-Manager für virtuelle Computer oder die [ `Move-ClusterVirtualMachineRole` ](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterVirtualMachineRole?view=win10-ps) Cmdlet (siehe Abbildung 17), um eine Livemigration der virtuellen Computer auszuführen.  

            ```PowerShell
            Move-ClusterVirtualMachineRole -Name VM1 -Node robhind-host3  
            ```  

        2. Verwendung **verschieben** aus dem Failovercluster-Manager oder das [ `Move-ClusterGroup` ](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterGroup?view=win10-ps) -Cmdlet für die anderen arbeitsauslastungen.  

3. Wenn jeder Knoten auf Windows Server 2016 aktualisiert und wieder dem Cluster hinzugefügt wurde, oder alle restlichen Windows Server 2012 R2-Knoten entfernt wurden, führen Sie folgende Schritte aus:  

    > [!IMPORTANT]  
    > -   Nach der Aktualisierung der Funktionsebene des Clusters Sie können nicht zurück auf die Funktionsebene der Windows Server 2012 R2 und Windows Server 2012 R2-Knoten können nicht mit dem Cluster hinzugefügt werden.
    > -   Bis die [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) Cmdlet ausgeführt wird, der Prozess ist vollständig rückgängig gemacht werden und können Windows Server 2012 R2-Knoten zu diesem Cluster hinzugefügt werden und Windows Server 2016-Knoten entfernt werden können.  
    > -   Nach der [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) Cmdlet ausgeführt wird, neue Features zur Verfügung.  

    1.  Verwenden den Failovercluster-Manager-UI oder der [ `Get-ClusterGroup` ](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterGroup?view=win10-ps) -Cmdlet, Überprüfung, die alle clusterrollen auf dem Cluster wie erwartet ausgeführt werden. Im folgenden Beispiel nicht verfügbaren Speicher verwendet wird, stattdessen CSV wird verwendet, daher zeigt der Speicherplatz einer **Offline** Status (siehe Abbildung 18).  

        ![Abbildung mit der Ausgabe des Cmdlets Get-ClusterGroup](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterGroup.png)  
        **Abbildung 18: Überprüfen, dass alle Gruppen (clusterrollen)-cluster ausgeführt werden, mithilfe der [ `Get-ClusterGroup` ](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterGroup?view=win10-ps) Cmdlet**  

    2.  Überprüfen Sie, dass alle Clusterknoten online sind und ausgeführt wird, mit der [ `Get-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterNode?view=win10-ps) Cmdlet.  
    3.  Führen Sie die [ `Update-ClusterFunctionalLevel` ](https://technet.microsoft.com/library/mt589702.aspx) Cmdlets – keine Fehler zurückgegeben werden sollen (siehe Abbildung 19).  

        ![Abbildung mit der Ausgabe des Cmdlets Update-ClusterFunctionalLevel](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SelectFunctionalLevel.png)  
        **Abbildung 19: Aktualisieren die Funktionsebene eines Clusters mithilfe von PowerShell**  

    4.  Nach der [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) Cmdlet wird ausgeführt, die neuen Features sind verfügbar.  

4. WindowsServer 2016 - werden normale clusteraktualisierungen und Sicherungen fortsetzen:  

    1. Wenn Sie zuvor für clusterfähiges aktualisieren ausgeführt haben, neu starten, verwenden die CAU-UI, oder verwenden Sie die [ `Enable-CauClusterRole` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole?view=win10-ps) Cmdlet (siehe Abbildung 20).  

        ![Abbildung zeigt die Ausgabe der Enable-CauClusterRole](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_EnableCAUClusterRole.png)  
        **Abbildung 20: Enable clusterfähigen Aktualisierungen mithilfe der [ `Enable-CauClusterRole` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole?view=win10-ps) Cmdlet**  

    2. Setzen Sie Sicherungsvorgänge fort.  

5. Aktivieren Sie und verwenden Sie die Windows Server 2016-Funktionen in Hyper-V-Computer.  

    1. Nachdem der Cluster auf Windows Server 2016-Funktionsebene aktualisiert wurde, müssen zahlreiche arbeitsauslastungen wie Hyper-V-VMs neue Funktionen. Eine Liste der neuen Hyper-V-Funktionen. finden Sie unter [migrieren und Aktualisieren von virtuellen Computern](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/migrating_vms)  

    2. Verwenden Sie auf jedem Hyper-V-Host-Knoten im Cluster, die [ `Get-VMHostSupportedVersion` ](https://docs.microsoft.com/powershell/module/hyper-v/Get-VMHostSupportedVersion?view=win10-ps) Cmdlet, um die Version der Hyper-V-VM-Konfiguration anzuzeigen, die vom Host unterstützt werden.  

        ![Abbildung mit der Ausgabe des Cmdlets Get-VMHostSupportedVersion](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_GetVMHostSupportVersion.png)  
        **Abbildung 21: Anzeigen der Hyper-V-VM-Konfiguration-Versionen, die vom Host unterstützt werden**  

   3.  Auf jedem Hyper-V-Host-Knoten im Cluster, Hyper-V-VM-Konfiguration-Version aktualisiert werden können, indem Planung eines Wartungsfensters für kurze mit Benutzern, sichern, deaktivieren virtuelle Computer und Ausführen der [ `Update-VMVersion` ](https://docs.microsoft.com/powershell/module/hyper-v/Update-VMVersion?view=win10-ps) Cmdlet (Siehe (Abbildung 22). Dadurch werden die VM-Version aktualisieren und neue Hyper-V-Funktionen, die beseitigt die Notwendigkeit von zukünftigen Updates von Hyper-V-Integration-Komponente (IC) aktivieren. Dieses Cmdlet kann über die Hyper-V-Knoten, der den virtuellen Computer hostet ausgeführt werden oder die `-ComputerName` Parameter kann verwendet werden, um die VM-Version zu aktualisieren, per Remotezugriff. In diesem Beispiel aktualisieren Sie hier wir die Version der Konfiguration von VM1 5.0 auf 7.0 profitieren von vielen neuen Hyper-V-Features, die mit dieser Version des VM-Konfiguration wie z. B. Produktionsprüfpunkte (anwendungskonsistente Sicherungen) und binäre VM verknüpft ist die Konfigurationsdatei.  

        ![Abbildung zeigt das Cmdlet Update-VMVersion in Aktion](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_StopVM.png)  
        **Abbildung 22: Aktualisieren Sie eine VM-Version, die mithilfe der Update-VMVersion-PowerShell-Cmdlets**  

4.  Speicherpools können aktualisiert werden, mithilfe der [Update-StoragePool](https://docs.microsoft.com/powershell/module/storage/Update-StoragePool?view=win10-ps) PowerShell-Cmdlets – Dies ist ein Onlinevorgang.  

Obwohl wir Private Cloud-Szenarien, insbesondere Hyper-V als Ziel dient, und Scale-Out File Server-Cluster, die ohne Ausfallzeiten, den Prozess Cluster OS Rolling Upgrade aktualisiert werden können, die für eine Clusterrolle verwendet werden können.  

## <a name="restrictions--limitations"></a>Beschränkungen / Einschränkungen  
- Dieses Feature funktioniert nur für Windows Server 2012 R2 auf Windows Server 2016-Versionen nur. Diese Funktion kann keine frühere Versionen von Windows Server, z. B. Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 auf Windows Server 2016 aktualisieren.  
- Jeder Knoten Windows Server 2016 sollte nur neu formatiert/neue Installation. "Direkt" oder "upgrade" Installationstyp wird abgeraten.  
- Ein Windows Server 2016-Knoten muss zum Hinzufügen von Windows Server 2016-Knoten im Cluster verwendet werden.  
- Wenn Sie einen gemischten-OS-Modus-Cluster zu verwalten, führen Sie die Verwaltungsaufgaben immer aus einem Uplevel-Knoten, auf der Windows Server 2016 ausgeführt wird. Kompatible Windows Server 2012 R2-Knoten können keine Benutzeroberfläche oder Management-Tools für Windows Server 2016.  
- Wir empfehlen Kunden, die durch den Upgradevorgang Cluster schnell verschoben werden, da einige Funktionen nicht für den gemischten-OS-Modus optimiert sind.  
- Vermeiden Sie erstellen oder Ändern der Größe Speicher auf Windows Server 2016-Knoten, während der Cluster im gemischten-OS-Modus aufgrund der möglichen Inkompatibilitäten bei einem Failover von einem Windows Server 2016-Knoten auf älteren Windows Server 2012 R2-Knoten ausgeführt wird.  

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen  
**Wie lange kann die Failovercluster in gemischten-OS-Modus ausführen?**  
    Wir empfehlen Kunden, die zum Abschließen des Upgrades innerhalb von vier Wochen. Es gibt zahlreiche Optimierungen in Windows Server 2016. Es wurden erfolgreich aktualisiert die Hyper-V und Scale-Out-Dateiservercluster mit und ohne Ausfallzeiten in weniger als vier Stunden insgesamt.  

**Werden Sie dieses Feature an Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 Portieren?**  
    Wir müssen keine Pläne So portieren Sie diese Funktion auf vorherige Versionen. Cluster OS Rolling Upgrade ist unsere Vision für das Upgrade von Windows Server 2012 R2-Clustern auf Windows Server 2016 und darüber hinaus.  

**Muss der Windows Server 2012 R2-Cluster alle Softwareupdates, die vor dem Starten des Prozesses Cluster OS Rolling Upgrade installiert haben?**  
    Ja, bevor der Prozess Cluster OS Rolling Upgrade starten, stellen Sie sicher, dass alle Knoten des Clusters mit den neuesten Softwareupdates aktualisiert werden.  

**Führe ich die [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) Cmdlet während Knoten deaktiviert sind oder angehalten wurde?**  
    Nein. Alle Knoten des Clusters muss auf und aktive Mitgliedschaft für die [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) Cmdlet funktioniert.  

**Funktioniert Cluster OS Rolling Upgrade für alle Workloads Cluster? Für SQL Server funktioniert das?**  
    Ja, funktioniert die Cluster OS Rolling Upgrade für alle Cluster-Workloads. Es ist jedoch nur ohne Ausfallzeiten für Hyper-V- und dateiserverclustern mit horizontaler. Die meisten anderen arbeitsauslastungen entstehen Ausfallzeiten (in der Regel ein paar Minuten) Wenn sie Failover und das Failover ist mindestens ein Mal während der Prozess Cluster OS Rolling Upgrade erforderlich.  

**Kann ich diesen Prozess mithilfe von PowerShell automatisieren?**  
    Ja, haben wir Cluster OS Rolling Upgrade, mithilfe von PowerShell automatisiert werden entworfen.  

**Für einen umfangreichen Cluster, der zusätzliche Workload und Failover-Kapazität verfügt, kann ich mehrere Knoten gleichzeitig upgraden?**  
    Ja. Beim Entfernen eines Knotens aus dem Cluster zum Aktualisieren des Betriebssystems Cluster haben, wird ein kleiner Knoten für das Failover, daher weisen eine geringere Failover-Kapazität. Bei großen Clustern mit genügend arbeitsauslastung und der Failover-Kapazität zu erhalten können mehrere Knoten gleichzeitig aktualisiert werden. Sie können den Cluster zu verbesserten Workload und Failover-Kapazität während des Prozesses Cluster OS Rolling Upgrade vorübergehend Clusterknoten hinzufügen.  

**Was geschieht, wenn ich ein Problem in meinem Cluster nach dem Ermitteln [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) erfolgreich ausgeführt wurde?**  
    Wenn Sie die Clusterdatenbank mit einer Sicherung des Systemstatus vor der Ausführung gesichert haben [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps), Sie sollten möglicherweise führen Sie eine autorisierend wiederherstellen auf einem Windows Server 2012 R2-Clusterknoten und Wiederherstellen des ursprünglichen Clusters Datenbank und Konfiguration.  

**Kann ich in-Place-Aktualisierung für jeden Knoten statt bereinigen-OS-Installation neu formatiert wird das Systemlaufwerk verwenden?**  
    Sollten nicht die Verwendung des direktes Upgrade von Windows Server, aber uns ist bekannt, dass es in einigen Fällen funktioniert, wenn die Standardtreiber verwendet werden. Bitte lesen Sie sorgfältig alle Warnmeldungen während des direktes Upgrade von einem Clusterknoten angezeigt.  

**Wenn ich Hyper-V-Replikation für einen virtuellen Hyper-V-Computer auf Hyper-V-Clusters verwende, werden Replikation während und nach dem Prozess Cluster OS Rolling Upgrade unverändert?**  
    Hyper-V-Replikat bleibt natürlich unverändert, während und nach dem Prozess Cluster OS Rolling Upgrade.  

**Kann ich System Center 2016 Virtual Machine Manager (SCVMM) verwenden, um den Cluster OS Rolling Upgrade zu automatisieren?**  
    Ja, können Sie die Verwendung von VMM in System Center 2016 Cluster OS Rolling Upgrade-Prozess automatisieren.  

## <a name="see-also"></a>Siehe auch  
-   [Anmerkungen zu dieser Version: Wichtige Probleme in WindowsServer 2016](../get-started/Release-Notes--Important-Issues-in-Windows-Server-2016-Technical-Preview.md)  
-   [Was ist neu in WindowsServer 2016](../get-started/What-s-New-in-windows-server-2016.md)  
-   [Neues beim Failoverclustering in WindowsServer](whats-new-in-failover-clustering.md)  
