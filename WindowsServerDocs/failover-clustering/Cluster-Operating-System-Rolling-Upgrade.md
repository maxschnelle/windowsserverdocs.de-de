---
title: Cluster Operating System Rolling Upgrade
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: get-started-article
ms.assetid: 6e102c1f-df26-4eaa-bc7a-d0d55d3b82d5
author: jasongerend
ms.author: jgerend
ms.date: 10/17/2017
ms.openlocfilehash: 8463c163294a4d2223a74b7cfeaea6ac5ae4fcfe
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="cluster-operating-system-rolling-upgrade"></a>Cluster Operating System rolling Upgrade

> Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Cluster OS Rolling Upgrade kann ein Administrator zum Upgrade des Betriebssystems des Clusterknotens, ohne eine Unterbrechung von Hyper-V- oder Workloads des Dateiservers mit horizontaler Skalierung durchzuführen. Mit diesem Feature können die downtimesanktionen gegen Service LevelAgreements (SLA) vermieden werden.

Parallele Upgrades des Clusterbetriebssystems bietet folgende Vorteile:

- Failovercluster mit Hyper-V-Computer und mit horizontaler Skalierung Datei Server ERZEUGTE Arbeitslasten können ohne Ausfallzeiten von Windows Server2012 R2 (auf allen Knoten im Cluster ausgeführt) zu Windows Server2016 (für alle Knoten des Clusters ausgeführt) aktualisiert werden. Andere Arbeitsauslastungen, z.B. SQL Server, ist die Zeit (in der Regel weniger als fünf Minuten) nicht verfügbar, die für ein Failover zu Windows Server2016 benötigt.  
- Es ist keine zusätzlichen Hardware erforderlich. Obwohl Sie zusätzliche hinzufügen können verarbeiten Clusterknoten vorübergehend für kleine Cluster zur Verbesserung der Verfügbarkeit des Clusters während der Cluster OS Rolling Upgrade.  
- Der Cluster muss nicht beendet oder neu gestartet werden.  
- Ein neuer Cluster ist nicht erforderlich. Der vorhandene Cluster aktualisiert wird. Darüber hinaus werden die vorhandenen Clusterobjekte in Active Directory gespeicherten verwendet.  
- Der Aktualisierungsprozess ist rückgängig gemacht, bis der Kunde Treffergruppen "Point-des-ohne-zurückgegeben", wenn alle Clusterknoten Windows Server2016 ausgeführt werden, und wenn das Update-ClusterFunctionalLevel PowerShell-Cmdlet ausgeführt wird.  
- Der Cluster kann das Patchen und Wartungsvorgänge während der Ausführung im gemischten OS-Modus unterstützen.  
- Automatisierung über PowerShell und WMI unterstützt.  
- Die Cluster öffentliche Eigenschaft **ClusterFunctionalLevel** -Eigenschaft gibt den Status des Clusters auf Windows Server2016-Clusterknoten. Diese Eigenschaft kann mithilfe der PowerShell-Cmdlet von einem Windows Server2016-Clusterknoten, der zu einem Failovercluster gehört abgefragt werden:  
    ```PowerShell
    Get-Cluster | Select ClusterFunctionalLevel  
    ```  

    Der Wert **8** gibt an, dass der Cluster auf der Funktionsebene von Windows Server2012 R2 ausgeführt wird. Der Wert **9** gibt an, dass der Cluster auf der Funktionsebene von Windows Server2016 ausgeführt wird.  

Dieses Handbuch beschreibt die verschiedenen Stufen der Prozess Cluster OS Rolling Upgrade Installationsschritte, Feature Einschränkungen sowie häufig gestellte Fragen (FAQs) und gilt für die folgenden Szenarien in Windows Server2016, Cluster OS Rolling Upgrade:  
- Hyper-V-Cluster  
- Dateiserverclustern mit horizontaler Skalierung  

Im folgende Szenario wird in Windows Server2016 nicht unterstützt:  
-  Cluster OS Rolling Upgrade des Gast-Cluster mit virtuellen Festplatte (.vhdx file) als freigegebener Speicher  

Cluster OS Rolling Upgrade wird von System Center Virtual Machine Manager (SCVMM) 2016 vollständig unterstützt. Wenn Sie SCVMM 2016 verwenden, finden Sie unter [ein Upgrade von Windows Server2012 R2-Hostclustern zu Windows Server2016 in VMM](https://technet.microsoft.com/library/mt445417.aspx) Hinweise zur Aktualisierung der Cluster und automatisieren die Schritte, die in diesem Dokument beschrieben werden.  

## <a name="requirements"></a>Anforderungen  
Führen Sie die folgenden Anforderungen, bevor Sie den Cluster OS Rolling Upgrade zu starten:

- Beginnen Sie mit einem Failovercluster unter Windows Server (Semikolons jährlichen Channel), Windows Server2016 oder Windows Server2012 R2.
- Einen Cluster von direkte Speicherplätze auf Windows Server aktualisieren, wird Version 1709 nicht unterstützt.
- Wenn der clusterarbeitsauslastung Hyper-V-VMs oder Dateiserver mit horizontaler Skalierung ist, können Sie Ausfallzeiten Upgrade erwarten.
- Stellen Sie sicher, dass die Hyper-V-Knoten CPUs, die Second-Level-Adressierung Tabelle (SLAT verfügen) mit einer der folgenden Methoden zu unterstützen.  
        – Überprüfen Sie die [Sie SLAT kompatibel sind? WP8 SDK Tipp 01](http://blogs.msdn.com/b/devfish/archive/2012/11/06/are-you-slat-compatible-wp8-sdk-tip-01.aspx) Artikel, der beschreibt, zwei Methoden zum Überprüfen, ob eine CPU Vorfluegel unterstützt  
        -Herunterladen der [Coreinfo v3.31](https://technet.microsoft.com/sysinternals/cc835722) Tool, um festzustellen, ob eine CPU SLAT unterstützt.

## <a name="cluster-transition-states-during-cluster-os-rolling-upgrade"></a>Cluster Übergänge zwischen Zuständen während des Upgrades des Clusterbetriebssystems

Dieser Abschnittbeschreibt die verschiedenen Zustände der Übergang von Windows Server2012 R2-Cluster, der mit Windows Server2016 mithilfe der Cluster OS Rolling Upgrade aktualisiert wird.  

Damit bleibt der clusterarbeitsauslastung ausgeführt wird, während des Prozess Cluster OS Rolling Upgrade, verschieben eine Arbeitsauslastung aus einem Windows Server2012 R2-Knoten zu Windows Server2016 funktioniert Knoten beide Knoten des Betriebssystems Windows Server2012 R2 ausgeführt werden. Wenn Windows Server2016-Knoten zum Cluster hinzugefügt werden, arbeiten sie in einem Windows Server2012 R2-Kompatibilitätsmodus. Ein neuer konzeptionelle Clustermodus, namens "Gemischten OS-Modus" kann Knoten verschiedener Versionen identisch sein (siehe Abbildung1)-Cluster.  

![Abbildungder drei aktivierungsphasen des kein paralleles Upgrade für Cluster OS: alle Knoten Windows Server2012 R2, gemischten OS-Modus und allen Knoten Windows Server2016](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Overview.png)  
**Abbildung1: Cluster-Betriebssystem-Zustandsübergänge**  

Ein Windows Server2012 R2-Cluster in den gemischten OS wechselt, wenn ein Windows Server2016-Knoten zum Cluster hinzugefügt wird. Der Prozess vollständig umkehrbar ist – Windows Server2016-Knoten aus dem Cluster entfernt werden können, und der Cluster in diesem Modus können Windows Server2012 R2-Knoten hinzugefügt werden. Die "zeigen Sie kein zurück" tritt auf, wenn das Update-ClusterFunctionalLevel PowerShell-Cmdlet auf dem Cluster ausgeführt wird. Für dieses Cmdlet ist nur erfolgreich Windows Server2016 müssen sich alle Knoten befinden, und alle Knoten müssen online sein.  

## <a name="transition-states-of-a-four-node-cluster-while-performing-rolling-os-upgrade"></a>Status der Übergang von einem Cluster mit vier Knoten beim Ausführen des Upgrades des Clusterbetriebssystems

In diesem Abschnittwird veranschaulicht, und beschreibt die vier verschiedenen Stufen von einem Cluster mit freigegebenem Speicher, deren Knoten von Windows Server2012 R2 auf Windows Server2016 aktualisiert werden.  

"Schritt1" ist der ursprünglichen Zustand – wir beginnen mit einem Windows Server2012 R2-Cluster.  

![Abbildungden Anfangszustand: alle Knoten Windows Server2012 R2](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage1.png)  
**Abbildung2: Anfangszustand: Windows Server2012 R2-Failovercluster (Phase 1)**  

In "Schritt2", zwei Knoten wurde angehalten, leer, entfernt, neu formatiert und mit Windows Server2016 installiert.  

![Abbildungdes Clusters im gemischten OS-Modus: aus dem Beispiel 4-Knoten-Cluster werden zwei Knoten Windows Server2016 ausgeführt, und zwei Knoten Windows Server2012 R2 ausgeführt werden](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage2.png)  
**Abbildung3: Fortgeschrittene Status: gemischten OS-Modus: Windows Server2012 R2 und Windows Server2016 Failover Cluster (Phase 2)**  

Unter "Schritt3", alle Knoten im Cluster zu Windows Server2016 aktualisiert wurden, und des Clusters kann mit PowerShell-Cmdlet Update-ClusterFunctionalLevel aktualisiert werden.  

> [!NOTE]  
> An diesem Punkt wird der Prozess vollständig rückgängig gemacht werden kann, und Windows Server2012 R2-Knoten zu diesem Cluster hinzugefügt werden können.  

![Abbildungdes Clusters wurde vollständig auf Windows Server2016 aktualisiert und für das Cmdlet Update-ClusterFunctionalLevel bereit ist, schalten Sie die Cluster-Funktionsebene bis zu Windows Server2016](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage3.png)  
**Abbildung4: Fortgeschrittene Status: alle Knoten, die ein Upgrade auf Windows Server2016 für Update-ClusterFunctionalLevel (Schritt3)**  

Nach der Update-ClusterFunctionalLevelcmdlet ausgeführt wird, gibt der Cluster "Schritt4", in denen neue Features von Windows Server2016-Cluster verwendet werden kann.  

![Die Abbildungzeigt, dass der Cluster OS clusterupgrades erfolgreich abgeschlossen wurde; alle Knoten zu Windows Server2016 aktualisiert wurden, und der Cluster die Funktionsebene Windows Server2016-Cluster ausgeführt wird](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage4.png)  
**Abbildung5: Endzustand: Windows Server2016 Failovercluster (Phase 4)**  

## <a name="cluster-os-rolling-upgrade-process"></a>Cluster OS Rolling Upgrade-Prozess

In diesem Abschnittwird der Workflow für die Durchführung des Upgrades des Clusterbetriebssystems beschrieben.  

![Abbildungdes Workflows zum Aktualisieren eines Clusters](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Workflow.png)  
**Abbildung6: Des Upgradeprozesses Workflow Clusterbetriebssystems**  

Cluster OS Rolling Upgrade umfasst die folgenden Schritteaus:  

1. Bereiten Sie den Cluster für die Aktualisierung des Betriebssystems wie folgt vor:  
    1. Cluster OS Rolling Upgrade erforderlich ist, entfernen einen Knoten aus dem Cluster zu einem Zeitpunkt. Überprüfen Sie, ob Sie über genügend Kapazität verfügen, auf dem Cluster mit hoher Verfügbarkeit SLAs beibehalten, wenn einer der Clusterknoten vom Cluster für ein Upgrade des Betriebssystems entfernt wird. Anders ausgedrückt, benötigen Sie die Möglichkeit, Arbeitsauslastungen von Failover auf einen anderen Knoten, wenn ein Knoten aus dem Cluster, während der Prozess Cluster OS Rolling Upgrade entfernt wird? Verfügt der Cluster die Kapazität für die erforderlichen Arbeitsauslastungen ausführen, wenn ein Knoten für Cluster OS Rolling Upgrade aus dem Cluster entfernt werden?  
    2. Für Hyper-V-Arbeitslasten überprüfen, ob alle Windows Server2016 Hyper-V-Hosts CPU-Adresse Tabelle SLAT (Second Level) unterstützen. Nur SLAT-fähige Computer können Hyper-V-Rolle in Windows Server2016 verwenden.  
    3. Überprüfen Sie, dass alle Arbeitsauslastungssicherungen ausgeführt haben, und berücksichtigen Sie den Cluster sichern. Beenden Sie Sicherungsvorgänge beim Hinzufügen von Knoten im Cluster.  
    4. Überprüfen Sie, dass alle Clusterknoten online sind/ausführen bzw. oben mit der [`Get-ClusterNode`](https://technet.microsoft.com/library/ee460990.aspx)Cmdlet (siehe Abbildung7).  

        ![Zeigt die Ergebnisse der Ausführung des Cmdlets Get-ClusterNode ScreenCap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterNode.png)  
        **Abbildung7: Ermitteln der Knotenstatus mit Get-ClusterNode-Cmdlet**  

    5. Wenn Sie den Cluster Aware Updates (CAU) ausgeführt werden, überprüfen Sie, ob CAU mit derzeit ausgeführt wird die **Cluster bekannt aktualisieren** UI, oder die [`Get-CauRun`](https://technet.microsoft.com/library/hh847230.aspx)Cmdlet (siehe Abbildung8). Beenden der Verwendung von cau die [`Disable-CauClusterRole`](https://technet.microsoft.com/library/hh847219.aspx)Cmdlet (siehe Abbildung9), um zu verhindern, dass alle Knoten angehalten und von CAU während des Prozess Cluster OS Rolling Upgrade leer.  

        ![Mit der Ausgabe des Cmdlets Get-CauRun ScreenCap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetCAU.png)  
        **Abbildung8: Verwenden der [`Get-CauRun`](https://technet.microsoft.com/library/hh847230.aspx)Cmdlet, um zu bestimmen, ob der Cluster-Aware Updates auf dem Cluster ausgeführt wird**  

        ![Mit der Ausgabe des Cmdlets Disable-CauClusterRole ScreenCap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_DisableCAU.png)  
        **Abbildung9: Deaktivieren der Cluster-Aware Updates mithilfe der [`Disable-CauClusterRole`](https://technet.microsoft.com/library/hh847219.aspx)Cmdlet**  

2. Führen Sie für jeden Knoten im Cluster die folgenden Schritteaus:  
    1. Wählen Sie einen Knoten mit Cluster-Manager-UI, und verwenden Sie die **Pause | Ausgleichen** Menüoption zum Ausgleichen von Knoten (siehe Abbildung10), oder verwenden Sie die [`Suspend-ClusterNode`](https://technet.microsoft.com/library/ee461051.aspx)Cmdlet (siehe Abbildung11).  

        ![ScreenCap zum Ausgleichen von Rollen mit der Cluster-Manager-UI](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_FCM_DrainRoles.png)  
        **Abbildung10: Ausgleichsmodus Rollen von einem Knoten Failovercluster-Manager**  

        ![Mit der Ausgabe des Cmdlets Suspend-ClusterNode ScreenCap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SuspendNode.png)  
        **Abbildung11: Ausgleichen Rollen aus einem Knoten mithilfe der [`Suspend-ClusterNode`](https://technet.microsoft.com/library/ee461051.aspx)Cmdlet**  

    2.  Cluster-Manager-UI mit **entfernen** den angehaltenen Knoten aus dem Cluster, oder verwenden Sie die [`Remove-ClusterNode`](https://technet.microsoft.com/library/ee461001.aspx)Cmdlet.  

        ![Mit der Ausgabe des Cmdlets Remove-ClusterNode ScreenCap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_RemoveNode.png)  
        **Abbildung12: Entfernen ein Knotens aus dem Cluster mithilfe [`Remove-ClusterNode`](https://technet.microsoft.com/library/ee461001.aspx)Cmdlet**  

    3.  Formatieren Sie das Systemlaufwerk und führen Sie eine "Neuinstallation des Betriebssystems Installation" von Windows Server2016 auf dem Knoten mit der **Benutzerdefiniert: nur Windows installieren (erweitert)** Installationsoption (siehe Abbildung13) in setup.exe. Wählen Sie die **aktualisieren: Installieren von Windows und Keep-Dateien, Einstellungen und Anwendungen** Option, da der Cluster OS Rolling Upgrade keine direkten Upgrades empfehlen.  

        ![ScreenCap des Windows Server2016-Installations-Assistenten mit der benutzerdefinierten Installationsoption](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_InstallOption.png)  
        **Abbildung13: Verfügbaren Installationsoptionen für Windows Server2016**  

    4.  Fügen Sie den Knoten, um die entsprechenden Active Directory-Domäne.  
    5.  Fügen Sie die entsprechenden Benutzer der Gruppe "Administratoren" hinzu.  
    6.  Mithilfe des Server-Manager-UI oder Install-WindowsFeature-PowerShell-Cmdlets, installieren Sie alle Serverrollen, die Sie, z.B. Hyper-V benötigen.  

        ```PowerShell
        Install-WindowsFeature -Name Hyper-V  
        ```  

    7.  Mithilfe des Server-Manager-UI oder Install-WindowsFeature-PowerShell-Cmdlets, installieren Sie das Failoverclusterfeature.  

        ```PowerShell
        Install-WindowsFeature -Name Failover-Clustering  
        ```  

    8.  Installieren Sie zusätzliche Features, die von der clusterarbeitsauslastung benötigt.  
    9. Überprüfen Sie Netzwerk- und Konnektivität mit dem Failovercluster-Manager-UI.  
    10. Wenn Windows-Firewall verwendet wird, überprüfen Sie die Firewall-Einstellungen für den Cluster. So erfordert beispielsweise Cluster Aware Updating, CAU aktiviert Clustern Firewallkonfiguration.  
    11. Verwenden Sie die Hyper-V-Manager-UI für Hyper-V-Arbeitslasten, um das Dialogfeld "Manager für virtuelle Switches" zu starten (siehe Abbildung14).  

        Überprüfen Sie, dass der Name der die virtuellen Switches verwendet für alle Knoten des Hyper-V-Hosts im Cluster identisch sind.  

        ![ScreenCap, das die Position des Dialogfelds Hyper-V-Manager für virtuelle Switches](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_VMSwitch.png)  
        **Abbildung14: Manager für virtuelle Switches**  

    12. Auf einem Knoten Windows Server2016 (verwenden Sie einen Windows Server2012 R2-Knoten nicht), verwenden Sie den Failovercluster-Manager (siehe Abbildung15) eine Verbindung zum Cluster herstellen.  

        ![Anzeigen des Dialogfelds wählen Cluster ScreenCap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode.png)  
        **Abbildung15: Hinzufügen eines Knotens zum Cluster mithilfe des Failovercluster-Manager**  

    13. Verwenden Sie entweder den Failovercluster-Manager-UI oder der [`Add-ClusterNode`](https://technet.microsoft.com/library/ee461047.aspx)Cmdlet (siehe Abbildung16), um den Knoten zum Cluster hinzufügen.  

        ![Mit der Ausgabe des Cmdlets Add-ClusterNode ScreenCap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode3.png)  
        **Abbildung16: Hinzufügen eines Knotens mit dem Cluster [`Add-ClusterNode`](https://technet.microsoft.com/library/ee461047.aspx)Cmdlet**  

        > [!NOTE]  
        > Bei der erste Windows Server2016-Knoten dem Cluster beitritt, der Cluster in den "Mixed-BS" wechselt, und die Hauptressourcen des Clusters auf den Windows Server2016-Knoten verschoben werden. Ein "Mixed-BS"-Modus-Cluster ist eine voll funktionsfähige Cluster, auf dem die neuen Knoten in einem Kompatibilitätsmodus mit den alten Knoten ausführen. "Mixed-BS" Modus ist eine vorübergehende für den Cluster. Soll nicht dauerhaft sein und Kunden werden erwartet, dass alle Knoten ihre Cluster innerhalb von vier Wochen zu aktualisieren.  

    14. Nach der Windows Server2016 Knoten ist erfolgreich dem Cluster hinzugefügt, Sie (optional) Teil der clusterarbeitsauslastung auf den neu hinzugefügten Knoten verschieben können zum Ausgleich von der Arbeitsauslastung innerhalb des Clusters wie folgt:

        ![Mit der Ausgabe des Cmdlets Move-ClusterVirtualMachineRole ScreenCap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_MoveVMRole.png)  
        **Abbildung17: Verschieben von einem Cluster Arbeitslast (Cluster-VM-Rolle) mit einer [`Move-ClusterVirtualMachineRole`](https://technet.microsoft.com/library/ee461041.aspx)Cmdlet**  

        1. Verwendung **Livemigration** aus den Failovercluster-Manager für virtuelle Maschinen oder die [`Move-ClusterVirtualMachineRole`](https://technet.microsoft.com/library/ee461041.aspx)Cmdlet (siehe Abbildung17), um eine live Migration der virtuellen Computer ausführen.  

            ```PowerShell
            Move-ClusterVirtualMachineRole -Name VM1 -Node robhind-host3  
            ```  

        2. Verwendung **verschieben** aus den Failovercluster-Manager oder die [`Move-ClusterGroup`](https://technet.microsoft.com/library/ee461002.aspx)Cmdlet für andere Workloads Cluster.  

3. Wenn alle Knoten ein Upgrade auf Windows Server2016 und dem Cluster hinzugefügt wurde, oder alle verbleibenden Windows Server2012 R2-Knoten entfernt wurden, führen Sie folgende Schritteaus:  

    > [!IMPORTANT]  
    > -   Nachdem Sie die Funktionsebene der Cluster aktualisiert, Sie können nicht zurück auf Funktionsebene von Windows Server2012 R2 und Windows Server2012 R2-Knoten können nicht zum Cluster hinzugefügt werden.
    > -   Bis die [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)Cmdlet ausgeführt wird, der Prozess vollständig umkehrbar ist und Windows Server2012 R2-Knoten zu diesem Cluster hinzugefügt werden können und Windows Server2016-Knoten entfernt werden können.  
    > -   Nach der [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)Cmdlet ausgeführt wird, werden neue Features zur Verfügung stehen.  

    1.  Mit dem Failovercluster-Manager-UI oder der [`Get-ClusterGroup`](https://technet.microsoft.com/library/ee461017.aspx) -Cmdlet, Kontrollkästchen, die alle Clusterrollen auf dem Cluster ausgeführt werden, wie erwartet. Im folgenden Beispiel nicht verfügbarer Speicher verwendet wird, stattdessen CSV verwendet, daher verfügbarer Speicher zeigt eine **Offline** Status (siehe Abbildung18).  

        ![Mit der Ausgabe des Cmdlets Get-ClusterGroup ScreenCap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterGroup.png)  
        **Abbildung18: Überprüfen, dass alle Cluster-Gruppen (Clusterrollen) ausgeführt werden, mit der [`Get-ClusterGroup`](https://technet.microsoft.com/library/ee461017.aspx)Cmdlet**  

    2.  Überprüfen Sie, dass alle Clusterknoten online sind und ausgeführt wird, mit der [`Get-ClusterNode`](https://technet.microsoft.com/library/ee460990.aspx)Cmdlet.  
    3.  Führen Sie die [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)Cmdlet - keine Fehler zurückgegeben werden soll (siehe Abbildung19).  

        ![Mit der Ausgabe des Cmdlets Update-ClusterFunctionalLevel ScreenCap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SelectFunctionalLevel.png)  
        **Abbildung19: Aktualisieren der Funktionsebene von einem Cluster mit PowerShell**  

    4.  Nach der [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)Cmdlet ausgeführt wird, sind neue Features verfügbar.  

4. Windows Server 2016 – fortsetzen normalen clusteraktualisierungen und Sicherungen:  

    1. Wenn Sie zuvor für clusterfähiges aktualisieren ausgeführt haben, neu starten, verwenden die CAU-UI oder verwenden Sie die [`Enable-CauClusterRole`](https://technet.microsoft.com/library/hh847229.aspx)Cmdlet (siehe Abbildung20).  

        ![Mit der Ausgabe von den Enable-CauClusterRole ScreenCap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_EnableCAUClusterRole.png)  
        **Abbildung20: Enable Cluster Aware Updates mithilfe der [`Enable-CauClusterRole`](https://technet.microsoft.com/library/hh847229.aspx)Cmdlet**  

    2. Sicherung Betrieb wieder aufnehmen.  

5. Aktivieren Sie und verwenden Sie die Windows Server2016-Features auf Hyper-V-Computer.  

    1. Nach dem Upgrade des Clusters auf Windows Server2016-Funktionsebene haben viele Arbeitsauslastungen wie Hyper-V-VMs neue Funktionen. Eine Liste der neuen Hyper-V-Funktionen. Weitere Informationen finden Sie unter [migrieren und Aktualisieren von virtuellen Maschinen](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/migrating_vms)  

    2. Verwenden Sie auf den einzelnen Knoten Hyper-V-Host im Cluster die [`Get-VMHostSupportedVersion`](https://technet.microsoft.com/library/mt653838.aspx)Cmdlet, um die Version der Hyper-V-VM-Konfiguration anzuzeigen, die vom Host unterstützt werden.  

        ![Mit der Ausgabe des Cmdlets Get-VMHostSupportedVersion ScreenCap](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_GetVMHostSupportVersion.png)  
        **Abbildung21: Anzeigen der Hyper-V-VM-Konfiguration vom Host unterstützt**  

   3.  Auf den einzelnen Knoten Hyper-V-Host im Cluster Versionen von Hyper-V-VM-Konfiguration aktualisiert werden können, planen eine kurze Wartungsfenster mit Benutzern sichern, durch das Deaktivieren der virtuellen Maschinen und Ausführen der [`Update-VMVersion`](https://technet.microsoft.com/library/mt484146.aspx)Cmdlet (siehe Abbildung22). Dies wird die VM-Version aktualisieren und neue Hyper-V-Features, die überflüssig für zukünftige Updates für Hyper-V-Integration Komponente (IC) aktivieren. Dieses Cmdlet kann über den Hyper-V-Knoten, der den virtuellen Computer hostet ausgeführt werden oder die `-ComputerName` -Parameter kann verwendet werden, um Remote die VM-Version zu aktualisieren. In diesem Beispiel Konfigurationsversion hier wir von VM1 von 5.0 auf 7.0 profitieren von vielen neuen Hyper-V-Features, die mit dieser VM-Konfigurationsversion z.B. Produktionsprüfpunkte (einheitliche Anwendung Sicherungen) und binäre VM-Konfigurationsdatei verknüpft ist.  

        ![Mit dem Cmdlet Update-VMVersion in Aktion ScreenCap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_StopVM.png)  
        **Abbildung22: Aktualisieren Sie eine VM-Version mithilfe des PowerShell-Cmdlets Update-VMVersion**  

4.  Speicherpools können aktualisiert werden, mit der [Update-StoragePool](https://technet.microsoft.com/itpro/powershell/windows/storage/update-storagepool) PowerShell-Cmdlet - Dies ist eine Online-Operation.  

Obwohl wir Private Cloud-Szenarien, insbesondere Hyper-V abzielen und Dateiserver mit horizontaler Skalierung Clustern, die ohne Ausfallzeiten, den Prozess Cluster OS Rolling Upgrade aktualisiert werden können, die für eine Clusterrolle verwendet werden können.  

## <a name="restrictions--limitations"></a>Einschränkungen / Einschränkungen  
- Dieses Feature funktioniert nur für Windows Server2012 R2, nur für Windows Server2016-Versionen. Dieses Feature kann keine frühere Versionen von Windows Server, z.B. Windows Server2008, Windows Server2008 R2 oder Windows Server2012 zu Windows Server2016 aktualisieren.  
- Jeder Knoten Windows Server2016 sollte nur neu formatiert und neue Installation. "Direktes" oder "Upgrade" Installationstyp wird nicht empfohlen.  
- Windows Server2016-Knoten zum Cluster hinzufügen, muss ein Windows Server2016-Knoten verwendet werden.  
- Wenn Sie einen gemischte OS-Modus-Cluster zu verwalten, immer Verwaltungsaufgaben Sie die aus einem komplexe Knoten, auf der Windows Server2016 ausgeführt wird. Für kompatible Windows Server2012 R2-Knoten können nicht UI oder Management-Tools für Windows Server2016 verwenden.  
- Wir empfehlen Kunden durch den Cluster Aktualisierungsvorgang schnell verschieben, da einige Clusterfeatures für den gemischten OS-Modus nicht optimiert werden.  
- Vermeiden Sie erstellen oder Ändern der Größe Speicher auf Windows Server2016-Knoten, während der Cluster im gemischten OS-Modus aufgrund mögliche Inkompatibilitäten bei einem Failover von einem Knoten Windows Server2016 mit älteren Windows Server2012 R2-Knoten ausgeführt wird.  

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen  
**Wie lange Ausführen der Failovercluster kann im gemischten OS-Modus?**  
    Microsoft empfiehlt das Upgrade innerhalb von vier Wochen abschließen. Es gibt viele Optimierungen in Windows Server2016. Es wurden erfolgreich aktualisiert die Hyper-V und Dateiserver mit horizontaler Skalierung Clustern ohne Ausfallzeiten in weniger als vier Stunden insgesamt.  

**Werden Sie dieses Feature wieder zu Windows Server2012, Windows Server2008 R2 oder Windows Server2008 Portieren?**  
    Wir haben keine Pläne, diese Funktion auf vorherige Versionen zu portieren. Cluster OS Rolling Upgrade ist unsere Vision für Windows Server2012 R2-Cluster ein Upgrade von Windows Server2016 und darüber hinaus.  

**Muss die Windows Server2012 R2-Cluster alle Softwareupdates, die vor dem Starten des Prozesses Cluster OS Rolling Upgrade installiert haben?**  
    Ja, bevor Sie beginnen den Prozess Cluster OS Rolling Upgrade, stellen Sie sicher, dass alle Knoten des Clusters mit den neuesten Softwareupdates aktualisiert wurden.  

**Kann ich Ausführen der [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)Cmdlet während Knoten deaktiviert sind oder angehalten?**  
    Nein. Alle Knoten des Clusters muss auf und aktive Mitgliedschaft für die [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)Cmdlet funktioniert.  

**Paralleles Upgrade für alle clusterarbeitsauslastung funktioniert? Funktioniert es für SQL Server?**  
    Ja, funktioniert die paralleles Upgrade für alle Workloads Cluster. Es ist jedoch nur Ausfallzeiten für Hyper-V- und dateiserverclustern mit horizontaler Skalierung. Die meisten anderen Arbeitsauslastungen verursachen eine Ausfallzeit (in der Regel ein paar Minuten), wenn sie Failovercluster und Failovercluster mindestens einmal während der Prozess Cluster OS Rolling Upgrade erforderlich ist.  

**Kann ich diesen Prozess mithilfe von PowerShell automatisieren?**  
    Ja, haben wir Cluster OS Rolling Upgrade mithilfe von PowerShell automatisiert werden soll.  

**Bei einem großen Cluster, der zusätzliche Arbeitslast und Failover-Kapazität hat, kann ich mehrere Knoten gleichzeitig aktualisieren?**  
    Ja. Beim Entfernen eines Knotens aus dem Cluster, aktualisieren das Betriebssystem der Cluster haben, wird ein Knoten weniger für Failover, daher haben eine geringere Failover-Kapazität. Für großen Clustern mit genügend Arbeitslast und Failover-Kapazität können mehrere Knoten gleichzeitig aktualisiert werden. Sie können die Clusterknoten vorübergehend zum Cluster bieten verbesserte Arbeitsauslastung und Kapazität des Failover während der Prozess Cluster OS Rolling Upgrade hinzufügen.  

**Was geschieht, wenn ich ein Problem in den Cluster nach dem Ermitteln [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)erfolgreich ausgeführt wurde?**  
    Wenn Sie die Clusterdatenbank mit einer Sicherung des Systemstatus vor dem Ausführen gesichert haben [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx), Sie sollten in der Lage, führen Sie eine autorisierende Wiederherstellung auf einem Windows Server2012 R2-Clusterknoten und Wiederherstellen der ursprünglichen Clusterdatenbank und die Konfiguration.  

**Kann ich direktes Upgrade für jeden Knoten anstelle von bereinigen OS Install durch neu zu formatieren sowie das Systemlaufwerk verwenden?**  
    Sollten nicht die Verwendung von direkten Upgrades von Windows Server, aber wir bekannt, dass sie in einigen Fällen funktioniert, wenn die Standardtreiber verwendet werden. Bitte lesen Sie alle Warnmeldungen während der direkten Aktualisierung eines Clusterknotens angezeigt.  

**Wenn ich Hyper-V-Replikation für einen virtuellen Hyper-V-Computer auf den Hyper-V-Cluster verwende, bleibt Replikation intakt während und nach dem Prozess Cluster OS Rolling Upgrade?**  
    Ja, bleibt die Hyper-V-Replikat erhalten, während und nach dem Prozess Cluster OS Rolling Upgrade.  

**Kann ich System Center 2016 Virtual Machine Manager (SCVMM) verwenden, um den Cluster OS Rolling Upgrade zu automatisieren?**  
    Ja, können Sie den Cluster OS Rolling Upgrade-Prozess mithilfe von VMM in System Center 2016 automatisieren.  

## <a name="see-also"></a>Siehe auch  
-   [Anmerkungen zu dieser Version: Wichtige Probleme in Windows Server 2016](../get-started/Release-Notes--Important-Issues-in-Windows-Server-2016-Technical-Preview.md)  
-   [Was ist neu in Windows Server 2016](../get-started/What-s-New-in-windows-server-2016.md)  
-   [Neues beim Failoverclustering in Windows Server](whats-new-in-failover-clustering.md)  