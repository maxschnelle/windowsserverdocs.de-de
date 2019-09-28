---
title: Quality of Service für Speicher
ms.prod: windows-server
manager: dongill
ms.author: JGerend
ms.technology: storage-qos
ms.topic: get-started-article
ms.assetid: 8dcb8cf9-0e08-4fdd-9d7e-ec577ce8d8a0
author: kumudd
ms.date: 10/10/2016
ms.openlocfilehash: 0e848260dd4ba3b37d1351fba7c24dd3cd283e69
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393943"
---
# <a name="storage-quality-of-service"></a>Quality of Service für Speicher

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Quality of Service (QoS) für Speicher in Windows Server 2016 ermöglicht eine zentrale Überwachung und Verwaltung der Speicherleistung für virtuelle Computer unter Verwendung der Hyper-V-Rolle und der Rolle des Dateiservers mit horizontaler Skalierung. Mit diesem Feature werden Speicherressourcen automatisch fairer auf mehrere virtuelle Computer verteilt, die denselben Dateiservercluster verwenden. Außerdem können richtlinienbasierte Mindest- und Maximalwerte als Leistungsziele konfiguriert werden. Die dabei verwendete Einheit sind normalisierte IOPS.  

Sie können QoS für Speicher in Windows Server 2016 nutzen, um folgende Ziele zu erreichen:  

-   **Vermeiden Sie Probleme mit dem Noisy-Nachbar** Mit Speicher-QoS wird standardmäßig sichergestellt, dass ein einzelner virtueller Computer nicht die gesamten Speicherressourcen belegen kann, sodass keine Speicherbandbreite für die übrigen virtuellen Computer verfügbar ist.  

-   **Überwachen der End-to-End-Speicherleistung.** Sobald die virtuellen Computer auf einem Dateiserver mit horizontaler Skalierung gestartet werden, wird ihre Leistung überwacht. Die Leistungsdetails aller ausgeführten virtuellen Computer sowie die Konfiguration des Dateiserverclusters mit horizontaler Skalierung können zentralisiert angezeigt werden.  

-   **Verwalten der Speicher-E/A in Übereinstimmung mit den Workloadanforderungen des Unternehmens** Speicher-QoS-Richtlinien definieren Mindest- und Höchstwerte für virtuelle Computer und stellen die Einhaltung dieser Vorgaben sicher. Dadurch wird selbst in Umgebungen mit hoher Dichte oder zu umfangreicher Bereitstellung eine einheitliche Leistung für virtuelle Computer erreicht. Wenn die Richtlinien nicht eingehalten werden können, kann anhand von Warnungen nachverfolgt werden, wann eine Richtlinie nicht von einer VM eingehalten wurde oder ob einer VM eine ungültige Richtlinie zugewiesen ist.  

In diesem Dokument wird beschrieben, wie Ihr Unternehmen von der neuen Speicher-QoS-Funktionalität profitieren kann. Es wird davon ausgegangen, dass Sie bereits mit Windows Server, mit Windows Server-Failoverclustering, mit Dateiservern mit horizontaler Skalierung, mit Hyper-V sowie mit Windows PowerShell vertraut sind.

## <a name="BKMK_Overview"></a>Übersicht über  
In diesem Abschnitt werden die Anforderungen für die Verwendung von Speicher-QoS beschrieben. Außerdem finden Sie eine Übersicht über eine softwaredefinierte Lösung unter Verwendung von Speicher-QoS sowie eine Terminologieliste zu Speicher-QoS.  

### <a name="BKMK_Requirements"></a>QoS-Speicheranforderungen  
Speicher-QoS unterstützt zwei Bereitstellungsszenarien:  

-   **Hyper-V unter Verwendung eines Dateiservers mit horizontaler Skalierung** Für dieses Szenario werden die beiden folgenden Komponenten benötigt:  

    -   Ein Speichercluster, bei dem es sich um einen Dateiservercluster mit horizontaler Skalierung handelt  

    -   Ein Computecluster mit mindestens einem Server, auf dem die Hyper-V-Rolle aktiviert ist  

    Für Speicher-QoS wird der Failovercluster auf Speicherservern benötigt, die Computeserver müssen sich jedoch nicht in einem Failovercluster befinden. Auf allen Servern (sowohl für Speicher als auch für Compute) muss Windows Server 2016 ausgeführt werden.  

    Wenn Sie keinen Dateiserver mit horizontaler Skalierung Cluster zu Evaluierungs Zwecken bereitgestellt haben, finden Sie unter [windows Server 2012 R2-Speicher eine Schritt-für-Schritt-Anleitung zum Erstellen eines Clusters mit vorhandenen Servern oder virtuellen Computern: Schritt für Schritt mit Speicherplätzen, SMB-Skalierung und frei gegebenem vhdx (Physical) ](http://blogs.technet.com/b/josebda/archive/2013/07/31/windows-server-2012-r2-storage-step-by-step-with-storage-spaces-smb-scale-out-and-shared-vhdx-physical.aspx).  

-   **Hyper-V mit freigegebenen Clustervolumes.** Für dieses Szenario sind die beiden folgenden Komponenten erforderlich:  

    -   Computecluster mit aktivierter Hyper-V-Rolle  

    -   Hyper-V unter Verwendung freigegebener Clustervolumes für Speicher  

Ein Failovercluster ist erforderlich. Auf allen Servern muss die gleiche Version von Windows Server 2016 ausgeführt werden.  

### <a name="BKMK_SolutionOverview"></a>Verwenden von Speicher-QoS in einer Software definierten Speicherlösung  
Speicher-QoS ist in die softwaredefinierte Speicherlösung von Microsoft integriert, die mit dem Dateiserver mit horizontaler Skalierung und Hyper-V bereitgestellt wird. Der Dateiserver mit horizontaler Skalierung legt Dateifreigaben für die Hyper-V-Server über das SMB3-Protokoll offen. Der Dateiservercluster wurde um einen neuen Richtlinien-Manager erweitert, der eine zentrale Überwachung der Speicherleistung ermöglicht.  

![Dateiserver mit horizontaler Skalierung und QoS für Speicher](media/overview-Clustering_SOFSStorageQoS.png)  

**Abbildung 1: Verwenden von Speicher-QoS in einer Software definierten Speicherlösung in Dateiserver mit horizontaler Skalierung @ no__t-0  

Sobald Hyper-V-Server virtuelle Computer starten, werden diese vom Richtlinien-Manager überwacht. Der Richtlinien-Manager übermittelt die Speicher-QoS-Richtlinie sowie die zugehörigen Grenzwerte und Reservierungen an den Hyper-V-Server, der die Leistung der virtuellen Computer entsprechend steuert.  

Bei Änderungen der Speicher-QoS-Richtlinien oder der Leistungsanforderungen virtueller Computer benachrichtigt der Richtlinien-Manager die Hyper-V-Server, damit diese ihr Verhalten anpassen. Durch diese Kommunikation zwischen den beiden Komponenten wird sichergestellt, dass alle VM-VHDs eine einheitliche Leistung bieten, die den Speicher-QoS-Richtlinien entspricht.  

### <a name="BKMK_Glossary"></a>Aren  

|Begriff|Beschreibung|  
|--------|---------------|  
|Normalisierte IOPS|Die gesamte Speichernutzung wird in normalisierten IOPS gemessen.  Dies ist die Anzahl von Speicher-E/A-Vorgängen pro Sekunde.  Jeder E/A-Vorgang bis 8 KB wird als ein normalisierter E/A-Vorgang betrachtet.  E/A-Vorgänge von mehr als 8 KB werden als mehrere normalisierte E/A-Vorgänge betrachtet. Eine Anforderung mit 256 KB wird z. B. als 32 normalisierte IOPS betrachtet.<br /><br />In Windows Server 2016 kann die verwendete Größe für das Normalisieren von E/A-Vorgängen angegeben werden.  Auf dem Speichercluster kann die normalisierte Größe angegeben werden, die anschließend clusterweit für Normalisierungsberechnungen verwendet wird.  Der Standardwert ist weiterhin 8 KB.|  
|Fluss|Jedes Dateihandle, das von einem Hyper-V-Server für eine VHD- oder VHDX-Datei geöffnet wird, wird als „Fluss“ betrachtet. Wenn ein virtueller Computer mit zwei virtuellen Festplatten verknüpft ist, verfügt er für jede Datei über einen Fluss zum Dateiservercluster. Wenn ein VHDX-Datenträger für mehrere virtuelle Computer freigegeben ist, verfügt er über einen Fluss pro VM.|  
|InitiatorName|Der Name des virtuellen Computers, der dem Dateiserver mit horizontaler Skalierung für jeden Fluss gemeldet wird.|  
|InitiatorID|Ein Bezeichner, der der VM-ID entspricht.  Dieser Bezeichner kann immer zur eindeutigen Identifizierung einzelner VM-Flüsse verwendet werden (selbst dann, wenn die VMs denselben InitiatorName-Wert aufweisen).|  
|Richtlinie|Speicher-QoS-Richtlinien werden in der Cluster Datenbank gespeichert und weisen die folgenden Eigenschaften auf: PolicyId, minimumiops, maximumiops, para Policy und policyType.|  
|PolicyId|Eindeutiger Bezeichner für eine Richtlinie.  Dieser Wert wird standardmäßig generiert, kann bei Bedarf jedoch auch festgelegt werden.|  
|MinimumIOPs|Mindestwert für normalisierte IOPS, die von einer Richtlinie bereitgestellt werden.  Auch als „Reservierung“ bezeichnet.|  
|MaximumIOPs|Höchstwert für normalisierte IOPS, die von einer Richtlinie eingeschränkt werden.  Auch als „Grenzwert“ bezeichnet.|  
|Aggregated |Ein Richtlinientyp, bei dem die angegebenen MinimumIOPs und MaximumIOPs sowie die Bandbreite auf alle Flüsse verteilt werden, die der Richtlinie zugewiesen sind. Alle VHDs, die der Richtlinie innerhalb des Speichersystems zugewiesen sind, weisen eine einzige Zuordnung von E/A-Bandbreite auf, die auf die VHDs verteilt wird.|  
|Dedicated|Ein Richtlinientyp, bei dem die angegebenen MinimumIOPs und MaximumIOPs sowie die Bandbreite für einzelne VHD/VHDx-Datenträger verwaltet werden.|  

## <a name="BKMK_SetUpQoS"></a>Einrichten von Speicher-QoS und Überwachen der grundlegenden Leistung  
In diesem Abschnitt wird beschrieben, wie Sie das neue Speicher-QoS-Feature aktivieren und die Speicherleistung überwachen, ohne benutzerdefinierte Richtlinien anzuwenden.  

### <a name="BKMK_SetupStorageQoSonStorageCluster"></a>Einrichten von Speicher-QoS auf einem Speicher Cluster  
In diesem Abschnitt wird erläutert, wie Sie QoS für Speicher auf einem neuen oder vorhandenen Failovercluster und Dateiserver mit horizontaler Skalierung aktivieren, auf dem Windows Server 2016 ausgeführt wird.  

#### <a name="set-up-storage-qos-on-a-new-installation"></a>Einrichten von Speicher-QoS auf einer Neuinstallation  
Wenn Sie einen neuen Failovercluster und ein freigegebenes Clustervolume (Cluster Shared Volume, CSV) auf Windows Server 2016 konfiguriert haben, wird das Feature „QoS für Speicher“ automatisch eingerichtet.  

#### <a name="verify-storage-qos-installation"></a>Überprüfen der Speicher-QoS-Installation  
Nachdem Sie einen Failovercluster erstellt und einen CSV-Datenträger konfiguriert haben, wird als Clustercoreressource **Speicher-QoS-Ressource** angezeigt. Dies ist sowohl im Failovercluster-Manager als auch in Windows PowerShell sichtbar. Der Grund dafür ist, dass das Failoverclustersystem diese Ressource verwaltet und es nicht notwendig sein sollte, dass Sie Aktionen für diese Ressource ausführen.  Sie wird sowohl im Failovercluster-Manager als auch in PowerShell angezeigt, um Konsistenz mit anderen Ressourcen im Failoverclustersystem (z. B. der neue Integritätsdienst) zu bieten.  

![QoS für Speicher-Ressource wird in Hauptressourcen des Clusters angezeigt](media/overview-Clustering_StorageQoSFCM.png)  

**Abbildung 2: Speicher-QoS-Ressource wird als Cluster Kernressource in Failovercluster-Manager @ no__t-0  

Verwenden Sie das folgende PowerShell-Cmdlet, um den Status der Speicher-QoS-Ressource anzuzeigen.  

```PowerShell  
PS C:\> Get-ClusterResource -Name "Storage Qos Resource"  

Name                   State      OwnerGroup        ResourceType                 
----                   -----      ----------        ------------                 
Storage Qos Resource   Online     Cluster Group     Storage QoS Policy Manager  
```  

### <a name="BKMK_SetupStorageQoSonComputeCluster"></a>Einrichten von Speicher-QoS auf einem Computecluster  
Die Hyper-V-Rolle in Windows Server 2016 bietet integrierte Unterstützung für QoS für Speicher. Das Feature ist standardmäßig aktiviert.  

#### <a name="install-remote-administration-tools-to-manage-storage-qos-policies-from-remote-computers"></a>Installieren von Remoteverwaltungstools, um Speicher-QoS-Richtlinien von Remotecomputern zu verwalten  
Sie können die Remoteserver-Verwaltungstools verwenden, um Speicher-QoS-Richtlinien zu verwalten und Flüsse von Computehosts zu überwachen.  Diese sind als optionale Features bei allen Installationen von Windows Server 2016 verfügbar und können für Windows 10 separat auf der [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=45520)-Website heruntergeladen werden.

Das optionale Feature **RSAT-Clustering** umfasst das Windows PowerShell-Modul für die Remoteverwaltung des Failoverclusterings (einschließlich Speicher-QoS).  

-   Windows PowerShell: Add-Windows Feature RSAT-Clustering  

Das optionale Feature **RSAT-Hyper-V-Tools** umfasst das Windows PowerShell-Modul für die Remoteverwaltung von Hyper-V.  

-   Windows PowerShell: Add-Windows Feature RSAT-Hyper-V-Tools  

#### <a name="deploy-virtual-machines-to-run-workloads-for-testing"></a>Bereitstellen von virtuellen Computern, um Workloads zu Testzwecken auszuführen  
Sie benötigen virtuelle Computer auf dem Dateiserver mit horizontaler Skalierung, auf denen relevante Workloads ausgeführt werden.  Einige Tipps zum Simulieren der Auslastung und zum Durchführen von Belastungstests finden Sie auf der folgenden Seite für ein empfohlenes Tool (diskspd) und einige Beispiele für die Verwendung: [Diskspd, PowerShell und Speicherleistung: Messen von IOPS, Durchsatz und Latenz für lokale Datenträger und SMB-Dateifreigaben.](http://blogs.technet.com/b/josebda/archive/2014/10/13/diskspd-powershell-and-storage-performance-measuring-iops-throughput-and-latency-for-both-local-disks-and-smb-file-shares.aspx)  

Die Beispielszenarien in diesem Leitfaden umfassen fünf virtuelle Computer. BuildVM1, BuildVM2, BuildVM3 und BuildVM4 führen eine Desktopworkload mit geringen bis mittleren Speicheranforderungen aus. TestVm1 führt einen Onlinetransaktionsverarbeitungs-Benchmark mit hohen Speicheranforderungen aus.  

### <a name="view-current-storage-performance-metrics"></a>Anzeigen von Metriken zur aktuellen Speicherleistung  
Dieser Abschnitt umfasst Folgendes:  

-   Abfragen von Flüssen mithilfe des Cmdlets `Get-StorageQosFlow`.  

-   Anzeigen der Leistung für ein Volume mithilfe des Cmdlets `Get-StorageQosVolume`.  

#### <a name="query-flows-using-the-get-storageqosflow-cmdlet"></a>Abfragen von Flüssen mithilfe des Cmdlets Get-StorageQosFlow  

Das Cmdlet Get-StorageQosFlow zeigt alle aktuellen Flüsse an, die von Hyper-V-Server initiiert wurden. Da alle Daten vom Dateiservercluster mit horizontaler Skalierung erfasst werden, kann das Cmdlet auf allen Knoten innerhalb des Dateiserverclusters mit horizontaler Skalierung verwendet werden. Alternativ kann es unter Verwendung des Parameters -CimSession auf einem Remoteserver verwendet werden.  

**Der folgende Beispielbefehl zeigt, wie alle von Hyper-V auf dem Server geöffneten Dateien mithilfe von Get-StorageQoSFlow angezeigt werden können**.  

```PowerShell
PS C:\> Get-StorageQosFlow  

InitiatorName    InitiatorNodeNam StorageNodeName  FilePath        Status  
                 e  
-------------    ---------------- ---------------  --------        ------  
                                  plang-fs3.pla... C:\ClusterSt... Ok  
                                  plang-fs2.pla... C:\ClusterSt... Ok  
                                  plang-fs1.pla... C:\ClusterSt... Ok  
                                  plang-fs3.pla... C:\ClusterSt... Ok  
                                  plang-fs2.pla... C:\ClusterSt... Ok  
                                  plang-fs1.pla... C:\ClusterSt... Ok  
TR20-VMM         plang-z400.pl... plang-fs1.pla... C:\ClusterSt... Ok  
BuildVM4         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok  
WinOltp1         plang-c1.plan... plang-fs1.pla... C:\ClusterSt... Ok  
BuildVM3         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok  
BuildVM1         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok  
TR20-VMM         plang-z400.pl... plang-fs1.pla... C:\ClusterSt... Ok  
BuildVM2         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok  
TR20-VMM         plang-z400.pl... plang-fs1.pla... C:\ClusterSt... Ok  
                                  plang-fs3.pla... C:\ClusterSt... Ok  
                                  plang-fs2.pla... C:\ClusterSt... Ok  
BuildVM4         plang-c2.plan... plang-fs2.pla... C:\ClusterSt... Ok  
WinOltp1         plang-c1.plan... plang-fs2.pla... C:\ClusterSt... Ok  
BuildVM3         plang-c2.plan... plang-fs2.pla... C:\ClusterSt... Ok  
WinOltp1         plang-c1.plan... plang-fs2.pla... C:\ClusterSt... Ok  
                                  plang-fs1.pla... C:\ClusterSt... Ok  
```  

Der folgende Beispielbefehl ist so formatiert, dass der VM-Name, der Hyper-V-Hostname, IOPS und der VHD-Dateiname angezeigt werden. Dabei wird die Ausgabe nach IOPS sortiert.  

```PowerShell  
PS C:\> Get-StorageQosFlow | Sort-Object StorageNodeIOPs -Descending | ft InitiatorName, @{Expression={$_.InitiatorNodeName.Substring(0,$_.InitiatorNodeName.IndexOf('.'))};Label="InitiatorNodeName"}, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize  

InitiatorName InitiatorNodeName StorageNodeIOPs Status File  
------------- ----------------- --------------- ------ ----  
WinOltp1      plang-c1                     3482     Ok IOMETER.VHDX  
BuildVM2      plang-c2                      544     Ok BUILDVM2.VHDX  
BuildVM1      plang-c2                      497     Ok BUILDVM1.VHDX  
BuildVM4      plang-c2                      316     Ok BUILDVM4.VHDX  
BuildVM3      plang-c2                      296     Ok BUILDVM3.VHDX  
BuildVM4      plang-c2                      195     Ok WIN8RTM_ENTERPRISE_VL_BU...  
TR20-VMM      plang-z400                    156     Ok DATA1.VHDX  
BuildVM3      plang-c2                       81     Ok WIN8RTM_ENTERPRISE_VL_BU...  
WinOltp1      plang-c1                       65     Ok BOOT.VHDX  
                                             18     Ok DefaultFlow  
                                             12     Ok DefaultFlow  
WinOltp1      plang-c1                        4     Ok 9914.0.AMD64FRE.WINMAIN....  
TR20-VMM      plang-z400                      4     Ok DATA2.VHDX  
TR20-VMM      plang-z400                      3     Ok BOOT.VHDX  
                                              0     Ok DefaultFlow  
                                              0     Ok DefaultFlow  
                                              0     Ok DefaultFlow  
                                              0     Ok DefaultFlow  
                                              0     Ok DefaultFlow  
                                              0     Ok DefaultFlow  
                                              0     Ok DefaultFlow  
```  

Der folgende Beispielbefehl zeigt, wie Flüsse basierend auf InitiatorName gefiltert werden können, um problemlos die Speicherleistung und Einstellungen für eine bestimmte VM anzuzeigen.  

```PowerShell
PS C:\> Get-StorageQosFlow -InitiatorName BuildVm1 | Format-List

FilePath           : C:\ClusterStorage\Volume2\SHARES\TWO\BUILDWORKLOAD\BUILDVM1.V  
                     HDX  
FlowId             : ebfecb54-e47a-5a2d-8ec0-0940994ff21c  
InitiatorId        : ae4e3dd0-3bde-42ef-b035-9064309e6fec  
InitiatorIOPS      : 464  
InitiatorLatency   : 26.2684  
InitiatorName      : BuildVM1  
InitiatorNodeName  : plang-c2.plang.nttest.microsoft.com  
Interval           : 300000  
Limit              : 500  
PolicyId           : b145e63a-3c9e-48a8-87f8-1dfc2abfe5f4  
Reservation        : 500  
Status             : Ok  
StorageNodeIOPS    : 475  
StorageNodeLatency : 7.9725  
StorageNodeName    : plang-fs1.plang.nttest.microsoft.com  
TimeStamp          : 2/12/2015 2:58:49 PM  
VolumeId           : 4d91fc3a-1a1e-4917-86f6-54853b2a6787  
PSComputerName     :  
MaximumIops        : 500  
MinimumIops        : 500  
```  

Das Cmdlet `Get-StorageQosFlow` gibt u. a. folgende Daten zurück:  

-   Den Hyper-V-Hostnamen (InitiatorNodeName)  

-   Den Namen und die ID des virtuellen Computers (InitiatorName und InitiatorId)  

-   Die aktuelle durchschnittliche Leistung, die vom Hyper-V-Host für den virtuellen Datenträger gemessen wurde (InitiatorIOPS, InitiatorLatency)  

-   Die aktuelle durchschnittliche Leistung, die vom Speichercluster für den virtuellen Datenträger gemessen wurde (StorageNodeIOPS, StorageNodeLatency)  

-   Die aktuelle Richtlinie, die gegebenenfalls auf die Datei angewendet wird, sowie die resultierende Konfiguration (PolicyId, Reservation, Limit)  

-   Richtlinienstatus  

    -   **Ok**: Es liegen keine Probleme vor.  

    -   InsufficientThroughput: Eine Richtlinie wird angewendet, die Mindestzahl von IOPS wird jedoch nicht erreicht.  Diese Situation kann eintreten, wenn der Mindestwert für eine VM (oder für alle VMs) über der Leistung liegt, die das Speichervolume maximal bietet.  

    -   **UnknownPolicyId**: Dem virtuellen Computer wurde auf dem Hyper-V-Host eine Richtlinie zugewiesen, sie fehlt jedoch auf dem Dateiserver.  Diese Richtlinie sollte aus der VM-Konfiguration entfernt werden, oder Sie sollten eine übereinstimmende Richtlinie auf dem Dateiservercluster erstellen.  

#### <a name="view-performance-for-a-volume-using-get-storageqosvolume"></a>Anzeigen der Leistung für ein Volume mithilfe von Get-StorageQosVolume  
Zusätzlich zu den flussbasierten Leistungsmetriken werden auch volumebasiert Metriken zur Speicherleistung erfasst.  Dadurch können problemlos die durchschnittliche Gesamtauslastung in normalisierten IOPS, die Latenz und die aggregierten Grenzwerte und Reservierungen für ein Volume angezeigt werden.  

```PowerShell
PS C:\> Get-StorageQosVolume | Format-List  

Interval       : 300000  
IOPS           : 0  
Latency        : 0  
Limit          : 0  
Reservation    : 0  
Status         : Ok  
TimeStamp      : 2/12/2015 2:59:38 PM  
VolumeId       : 434f561f-88ae-46c0-a152-8c6641561504  
PSComputerName :  
MaximumIops    : 0  
MinimumIops    : 0  

Interval       : 300000  
IOPS           : 1097  
Latency        : 3.1524  
Limit          : 0  
Reservation    : 1568  
Status         : Ok  
TimeStamp      : 2/12/2015 2:59:38 PM  
VolumeId       : 4d91fc3a-1a1e-4917-86f6-54853b2a6787  
PSComputerName :  
MaximumIops    : 0  
MinimumIops    : 1568  

Interval       : 300000  
IOPS           : 5354  
Latency        : 6.5084  
Limit          : 0  
Reservation    : 781  
Status         : Ok  
TimeStamp      : 2/12/2015 2:59:38 PM  
VolumeId       : 0d2fd367-8d74-4146-9934-306726913dda  
PSComputerName :  
MaximumIops    : 0  
MinimumIops    : 781  
```  

## <a name="BKMK_CreateQoSPolicies"></a>Erstellen und Überwachen von Speicher-QoS-Richtlinien  
In diesem Abschnitt wird beschrieben, wie Sie Speicher-QoS-Richtlinien erstellen, diese Richtlinien auf virtuelle Computer anwenden und einen Speichercluster überwachen, nachdem Richtlinien angewendet wurden.  

### <a name="create-storage-qos-policies"></a>Erstellen von Speicher-QoS-Richtlinien  
Speicher-QoS-Richtlinien werden im Dateiservercluster mit horizontaler Skalierung definiert und verwaltet.  Für flexible Bereitstellungen kann eine beliebige Anzahl von Richtlinien erstellt werden (bis zu 10.000 pro Speichercluster).  

Für jede VHD/VHDX-Datei, die einem virtuellen Computer zugewiesen ist, kann eine Richtlinie konfiguriert werden. Unterschiedliche Dateien und VMs können dieselbe Richtlinie verwenden, oder für jede Datei und VM kann eine separate Richtlinie konfiguriert werden.  Wenn mehrere VHD/VHDX-Dateien oder mehrere virtuelle Computer mit derselben Richtlinie konfiguriert sind, werden sie aggregiert, und die MinimumIOPs and MaximumIOPs werden gleichmäßig auf diese Dateien oder VMs verteilt. Wenn Sie separate Richtlinien für mehrere VHD/VHDX-Dateien oder virtuelle Computer verwenden, werden die Mindest- und Höchstwerte separat für jede Datei oder VM nachverfolgt.  

Wenn Sie mehrere ähnliche Richtlinien für unterschiedliche virtuelle Computer erstellen und für die virtuellen Computer identische Speicheranforderungen gelten, erhalten sie einen ähnlichen Anteil von IOPS.  Wenn die Speicheranforderungen einer VM höher oder geringer sind, werden die entsprechenden IOPS bereitgestellt.  

### <a name="types-of-storage-qos-policies"></a>Typen von Speicher-QoS-Richtlinien  
Es gibt zwei Arten von Richtlinien: Aggregiert (früher als "SingleInstance" bezeichnet) und "Dedicated" (früher als "MultiInstance" bezeichnet). Aggregierte Richtlinien wenden die Höchst- und Mindestwerte für den kombinierten Satz an VHD/VHDX-Dateien und virtuellen Computern an. Eine festgelegte Bandbreite und Menge von IOPS wird also gemeinsam verwendet. Dedizierte Richtlinien wenden die Mindest- und Höchstwerte für jede VHD/VHDX separat an. Dadurch lässt sich problemlos eine einzelne Richtlinie erstellen, die ähnliche Grenzwerte auf mehrere VHD/VHDX-Dateien anwendet.  

Beispiel: Sie erstellen eine aggregierte Richtlinie mit einem Mindestwert von 300 IOPS und einem Höchstwert von 500 IOPS. Wenn Sie diese Richtlinie auf 5 unterschiedliche VHD/VHDX-Dateien anwenden, stellen Sie sicher, dass für diese 5 VHD/VHDX-Dateien insgesamt mindestens 300 IOPS und maximal 500 IOPS bereitgestellt werden (sofern diese Leistung erforderlich ist und das Speichersystem diese Leistung bieten kann). Wenn die VHD/VHDX-Dateien ähnliche IOPS-Anforderungen haben und das Speichersystem diese Leistung bieten kann, erhält jede VHD/VHDX-Datei ca. 100 IOPS.  

Wenn Sie jedoch stattdessen eine dedizierte Richtlinie mit ähnlichen Grenzwerten erstellen und auf VHD/VHDX-Dateien auf 5 unterschiedlichen virtuellen Computern anwenden, erhält jeder virtuelle Computer mindestens 300 IOPS und maximal 500 IOPS. Wenn die virtuellen Computer ähnliche IOPS-Anforderungen haben und das Speichersystem diese Leistung bieten kann, erhält jeder virtuelle Computer ca. 500 IOPS. .  Wenn einer der virtuellen Computer über mehrere VHD/VHDX-Dateien verfügt, für die dieselbe MultiInstance-Richtlinie konfiguriert ist, gilt der Grenzwert für alle Dateien gemeinsam. Die Gesamt-E/A von VM-Dateien mit dieser Richtlinie darf die Grenzwerte also nicht überschreiten.  

Wenn Sie über eine Gruppe von VHD/VHDX-Dateien verfügen, denen dieselben Leistungsmerkmale zugewiesen werden sollen, und Sie nicht mehrere ähnliche Richtlinien erstellen möchten, können Sie eine einzige dedizierte Richtlinie erstellen und diese auf die Dateien der einzelnen virtuellen Computer anwenden.

Halten Sie die Anzahl von VHD-/vhdx-Dateien, die einer einzelnen aggregierten Richtlinie zugewiesen sind, auf maximal 20.  Dieser Richtlinientyp soll Aggregationen mit einigen virtuellen Computern in einem Cluster durchführen.

### <a name="create-and-apply-a-dedicated-policy"></a>Erstellen und Anwenden einer dedizierten Richtlinie  
Verwenden Sie zunächst das Cmdlet `New-StorageQosPolicy`, um eine Richtlinie auf dem Dateiserver mit horizontaler Skalierung zu erstellen, wie im folgenden Beispiel gezeigt:  

```PowerShell
$desktopVmPolicy = New-StorageQosPolicy -Name Desktop -PolicyType Dedicated -MinimumIops 100 -MaximumIops 200  
```  

Wenden Sie die Richtlinie dann auf die Festplattenlaufwerke der virtuellen Computer auf dem Hyper-V-Server an.  Notieren Sie die PolicyId aus dem vorherigen Schritt, oder speichern Sie sie als Variable in Ihren Skripts.  

Erstellen Sie auf dem Dateiserver mit horizontaler Skalierung mithilfe von PowerShell eine Speicher-QoS-Richtlinie, und rufen Sie die Richtlinien-ID wie im folgenden Beispiel gezeigt ab:  

```PowerShell
PS C:\> $desktopVmPolicy = New-StorageQosPolicy -Name Desktop -PolicyType Dedicated -MinimumIops 100 -MaximumIops 200  

C:\> $desktopVmPolicy.PolicyId  

Guid  
----  
cd6e6b87-fb13-492b-9103-41c6f631f8e0  
```  

Legen Sie die Speicher-QoS-Richtlinie auf dem Hyper-V-Server mithilfe von PowerShell und unter Verwendung der Richtlinien-ID fest, wie im folgenden Beispiel gezeigt:  

```PowerShell
Get-VM -Name Build* | Get-VMHardDiskDrive | Set-VMHardDiskDrive -QoSPolicyID cd6e6b87-fb13-492b-9103-41c6f631f8e0  
```  

### <a name="confirm-that-the-policies-are-applied"></a>Überprüfen, ob die Richtlinien angewendet werden  
Überprüfen Sie mithilfe des PowerShell-Cmdlets `Get-StorageQosFlow`, ob die MinimumIOPs und MaximumIOPs auf die richtigen Flüsse angewendet wurden (wie im folgenden Beispiel gezeigt).  

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName |  
 ft InitiatorName, Status, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize  

InitiatorName Status MinimumIops MaximumIops StorageNodeIOPs Status File  
------------- ------ ----------- ----------- --------------- ------ ----  
BuildVM1          Ok         100         200             250     Ok BUILDVM1.VHDX  
BuildVM2          Ok         100         200             251     Ok BUILDVM2.VHDX  
BuildVM3          Ok         100         200             252     Ok BUILDVM3.VHDX  
BuildVM4          Ok         100         200             233     Ok BUILDVM4.VHDX  
TR20-VMM          Ok          33         666               1     Ok DATA2.VHDX  
TR20-VMM          Ok          33         666               5     Ok DATA1.VHDX  
TR20-VMM          Ok          33         666               4     Ok BOOT.VHDX  
WinOltp1          Ok           0           0               0     Ok 9914.0.AMD6...  
WinOltp1          Ok           0           0            5166     Ok IOMETER.VHDX  
WinOltp1          Ok           0           0               0     Ok BOOT.VHDX  
```  

Auf dem Hyper-V-Server können Sie auch das bereitgestellte Skript **Get-VMHardDiskDrivePolicy.ps1** verwenden, um die Richtlinie anzuzeigen, die auf ein virtuelles Festplattenlaufwerk angewendet wird.  

```PowerShell
PS C:\> Get-VM -Name BuildVM1 | Get-VMHardDiskDrive | Format-List  

Path                          : \\plang-fs.plang.nttest.microsoft.com\two\BuildWorkload  
                                \BuildVM1.vhdx  
DiskNumber                    :  
MaximumIOPS                   : 0  
MinimumIOPS                   : 0  
QoSPolicyID                   : cd6e6b87-fb13-492b-9103-41c6f631f8e0  
SupportPersistentReservations : False  
ControllerLocation            : 0  
ControllerNumber              : 0  
ControllerType                : IDE  
PoolName                      : Primordial  
Name                          : Hard Drive  
Id                            : Microsoft:AE4E3DD0-3BDE-42EF-B035-9064309E6FEC\83F8638B  
                                -8DCA-4152-9EDA-2CA8B33039B4\0\0\D  
VMId                          : ae4e3dd0-3bde-42ef-b035-9064309e6fec  
VMName                        : BuildVM1  
VMSnapshotId                  : 00000000-0000-0000-0000-000000000000  
VMSnapshotName                :  
ComputerName                  : PLANG-C2  
IsDeleted                     : False  
```  

### <a name="query-for-storage-qos-policies"></a>Abfragen von Speicher-QoS-Richtlinien  
`Get-StorageQosPolicy` listet alle konfigurierten Richtlinien und deren Status auf einem Dateiserver mit horizontaler Skalierung auf.  

```PowerShell
PS C:\> Get-StorageQosPolicy  

Name                 MinimumIops          MaximumIops          Status  
----                 -----------          -----------          ------  
Default              0                    0                    Ok  
Limit500             0                    500                  Ok  
SilverVm             500                  500                  Ok  
Desktop              100                  200                  Ok  
Limit500             0                    0                    Ok  
VMM                  100                  2000                 Ok  
Vdi                  1                    100                  Ok  
```  

Status können sich basierend auf der Systemleistung im Lauf der Zeit ändern.  

-   **Ok**: Alle Flüsse, die diese Richtlinie verwenden, erhalten die angeforderten MinimumIOPs.  

-   **InsufficientThroughput**: Mindestens einer der Flüsse, die diese Richtlinien verwenden, erhalten nicht die erforderlichen MinimumIOPs.  

Sie können eine Richtlinie auch wie unten gezeigt mittels Pipe an `Get-StorageQosPolicy` übergeben, um den Status aller Flüsse abzurufen, die für die Verwendung der Richtlinie konfiguriert sind:  

```PowerShell
PS C:\> Get-StorageQosPolicy -Name Desktop | Get-StorageQosFlow | ft InitiatorName, *IOPS, Status, FilePath -AutoSize  

InitiatorName MaximumIops MinimumIops InitiatorIOPS StorageNodeIOPS Status FilePat  
                                                                           h  
------------- ----------- ----------- ------------- --------------- ------ -------  
BuildVM4              100          50           187              17     Ok C:\C...  
BuildVM3              100          50           194              25     Ok C:\C...  
BuildVM1              200         100           195             196     Ok C:\C...  
BuildVM2              200         100           193             192     Ok C:\C...  
BuildVM4              200         100           187             169     Ok C:\C...  
BuildVM3              200         100           194             169     Ok C:\C...  
```  

### <a name="create-an-aggregated-policy"></a>Erstellen einer aggregierten Richtlinie  
Aggregierte Richtlinien können verwendet werden, wenn mehrere virtuelle Festplatten einen einzigen Pool an IOPS und Bandbreite gemeinsam nutzen sollen.  Wenn Sie z. B. dieselbe aggregierte Richtlinie auf die Festplatten von zwei virtuellen Computern anwenden, wird der Mindestdurchsatz abhängig vom Bedarf auf die beiden Festplatten verteilt.  Für beide Festplatten gilt ein kombinierter Mindestwert, und die beiden Festplatten dürfen insgesamt die festgelegten Höchstwerte für IOPS und Bandbreite nicht überschreiten.  

Derselbe Ansatz könnte verwendet werden, um eine einzige Zuordnung zu allen VHD/VHDX-Dateien für die virtuellen Computer zu konfigurieren, die einen Dienst umfassen oder zu einem Mandanten in einer Multihosted-Umgebung gehören.  

Die Schritte zum Erstellen von dedizierten und aggregierten Richtlinien unterscheiden sich lediglich durch die Angabe von PolicyType.  

Das folgende Beispiel zeigt, wie eine aggregierte Speicher-QoS-Richtlinie erstellt und die PolicyId auf einem Dateiserver mit horizontaler Skalierung abgerufen wird:  

```PowerShell
PS C:\> $highPerf = New-StorageQosPolicy -Name SqlWorkload -MinimumIops 1000 -MaximumIops 5000 -PolicyType Aggregated  
[plang-fs]: PS C:\Users\plang\Documents> $highPerf.PolicyId  

Guid  
----  
7e2f3e73-1ae4-4710-8219-0769a4aba072  
```  

Das folgende Beispiel zeigt, wie die Speicher-QoS-Richtlinie unter Verwendung der im vorherigen Beispiel abgerufenen PolicyId auf dem Hyper-V-Server angewendet wird:  

```PowerShell
PS C:\> Get-VM -Name WinOltp1 | Get-VMHardDiskDrive | Set-VMHardDiskDrive -QoSPolicyID 7e2f3e73-1ae4-4710-8219-0769a4aba072  
```  

Das folgende Beispiel zeigt, wie die Auswirkungen der Speicher-QoS-Richtlinie auf dem Dateiserver angezeigt werden:  

```PowerShell
PS C:\> Get-StorageQosFlow -InitiatorName WinOltp1 | format-list InitiatorName, PolicyId, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, FilePath  

InitiatorName   : WinOltp1  
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072  
MinimumIops     : 250  
MaximumIops     : 1250  
StorageNodeIOPs : 0  
FilePath        : C:\ClusterStorage\Volume2\SHARES\TWO\BASEVHD\9914.0.AMD64FRE.WIN  
                  MAIN.141218-1718_SERVER_SERVERDATACENTER_EN-US.VHDX  

InitiatorName   : WinOltp1  
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072  
MinimumIops     : 250  
MaximumIops     : 1250  
StorageNodeIOPs : 0  
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\BOOT.VHDX  

InitiatorName   : WinOltp1  
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072  
MinimumIops     : 1000  
MaximumIops     : 5000  
StorageNodeIOPs : 4550  
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX  
PS C:\> Get-StorageQosFlow -InitiatorName WinOltp1 | for  
mat-list InitiatorName, PolicyId, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, FilePath  

InitiatorName   : WinOltp1  
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072  
MinimumIops     : 250  
MaximumIops     : 1250  
StorageNodeIOPs : 0  
FilePath        : C:\ClusterStorage\Volume2\SHARES\TWO\BASEVHD\9914.0.AMD64FRE.WIN  
                  MAIN.141218-1718_SERVER_SERVERDATACENTER_EN-US.VHDX  

InitiatorName   : WinOltp1  
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072  
MinimumIops     : 250  
MaximumIops     : 1250  
StorageNodeIOPs : 0  
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\BOOT.VHDX  

InitiatorName   : WinOltp1  
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072  
MinimumIops     : 1000  
MaximumIops     : 5000  
StorageNodeIOPs : 4550  
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX  
```  

Jede virtuelle Festplatte verfügt über die MinimumIOPs und MaximumIOPs sowie über einen MaximumIobandwidth-Wert, der basierend auf der jeweiligen Last angepasst wird.  Dadurch wird sichergestellt, dass die Gesamtbandbreite für die Datenträger innerhalb des durch die Richtlinie definierten Bereichs bleibt.  Im obigen Beispiel befinden sich die zwei ersten Datenträger im Leerlauf, und der dritte Datenträger darf die maximale Anzahl von IOPS nutzen.  Wenn die zwei ersten Datenträger erneut E/A generieren, wird die maximale Anzahl von IOPS des dritten Datenträgers automatisch gesenkt.  

### <a name="modify-an-existing-policy"></a>Ändern einer vorhandenen Richtlinie  
Die Eigenschaften Name, MinimumIOPs,  MaximumIOPs und MaximumIoBandwidth können nach dem Erstellen einer Richtlinie geändert werden.  Der Richtlinientyp (Aggregated/Dedicated) kann jedoch nicht geändert werden, nachdem die Richtlinie erstellt wurde.  

Das folgende Windows PowerShell-Cmdlet zeigt, wie die Eigenschaft MaximumIOPs für eine vorhandene Richtlinie geändert wird:  

```PowerShell
[DBG]: PS C:\demoscripts>> Get-StorageQosPolicy -Name SqlWorkload | Set-StorageQosPolicy -MaximumIops 6000  
```  

Mithilfe des folgenden Cmdlets wird die Änderung überprüft:  

```PowerShell
PS C:\> Get-StorageQosPolicy -Name SqlWorkload  

Name                    MinimumIops            MaximumIops            Status  
----                    -----------            -----------            ------  
SqlWorkload             1000                   6000                   Ok    

[plang-fs1]: PS C:\Users\plang\Documents> Get-StorageQosPolicy -Name SqlWorkload | Get-Storag  
eQosFlow | Format-Table InitiatorName, PolicyId, MaximumIops, MinimumIops, StorageNodeIops -A  
utoSize  

InitiatorName PolicyId                             MaximumIops MinimumIops StorageNodeIops  
------------- --------                             ----------- ----------- ---------------  
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072        1500         250               0  
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072        1500         250               0  
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072        6000        1000            4507  
```  

## <a name="BKMK_KnownIssues"></a>Identifizieren und behandeln gängiger Probleme  
In diesem Abschnitt wird beschrieben, wie Sie virtuelle Computer mit ungültigen Speicher-QoS-Richtlinien ermitteln, wie eine übereinstimmende Richtlinie neu erstellt wird, wie eine Richtlinie von einem virtuellen Computer entfernt und wie virtuelle Computer ermittelt werden, die die Anforderungen der Speicher-QoS-Richtlinie nicht erfüllen.  

### <a name="BKMK_FindingVMsWithInvalidPolicies"></a>Erkennen von virtuellen Computern mit ungültigen Richtlinien  

Wenn eine Richtlinie vom Dateiserver gelöscht wird, bevor sie von einem virtuellen Computer entfernt wird, wird der virtuelle Computer so weiter ausgeführt, als wäre keine Richtlinie angewendet worden.  

```PowerShell
PS C:\> Get-StorageQosPolicy -Name SqlWorkload | Remove-StorageQosPolicy  

Confirm  
Are you sure you want to perform this action?  
Performing the operation "DeletePolicy" on target "MSFT_StorageQoSPolicy (PolicyId =  
"7e2f3e73-1ae4-4710-8219-0769a4aba072")".  
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [?] Help (default is "Y"):  
```  

Der Status für die Flüsse lautet anschließend UnknownPolicyId.  

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, Status, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize  

InitiatorName          Status MinimumIops MaximumIops StorageNodeIOPs          Status File  
-------------          ------ ----------- ----------- ---------------          ------ ----  
                           Ok           0           0               0              Ok Def...  
                           Ok           0           0              10              Ok Def...  
                           Ok           0           0              13              Ok Def...  
                           Ok           0           0               0              Ok Def...  
                           Ok           0           0               0              Ok Def...  
                           Ok           0           0               0              Ok Def...  
                           Ok           0           0               0              Ok Def...  
                           Ok           0           0               0              Ok Def...  
                           Ok           0           0               0              Ok Def...  
BuildVM1                   Ok         100         200             193              Ok BUI...  
BuildVM2                   Ok         100         200             196              Ok BUI...  
BuildVM3                   Ok          50          64              17              Ok WIN...  
BuildVM3                   Ok          50         136             179              Ok BUI...  
BuildVM4                   Ok          50         100              23              Ok WIN...  
BuildVM4                   Ok         100         200             173              Ok BUI...  
TR20-VMM                   Ok          33         666               2              Ok DAT...  
TR20-VMM                   Ok          25         975               3              Ok DAT...  
TR20-VMM                   Ok          75        1025              12              Ok BOO...  
WinOltp1      UnknownPolicyId           0           0               0 UnknownPolicyId 991...  
WinOltp1      UnknownPolicyId           0           0            4926 UnknownPolicyId IOM...  
WinOltp1      UnknownPolicyId           0           0               0 UnknownPolicyId BOO...  
```  

#### <a name="BKMK_RecreateMatchingPolicy"></a>Erneutes Erstellen einer entsprechenden Speicher-QoS-Richtlinie  
Wenn eine Richtlinie unbeabsichtigterweise entfernt wurde, können Sie eine neue Richtlinie unter Verwendung der alten PolicyId erstellen.  Rufen Sie zunächst die benötigte PolicyId ab.  

```PowerShell
PS C:\> Get-StorageQosFlow -Status UnknownPolicyId | ft InitiatorName, PolicyId -AutoSize  

InitiatorName PolicyId  
------------- --------  
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072  
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072  
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072  
```  

Erstellen Sie dann unter Verwendung dieser PolicyId eine neue Richtlinie.  

```PowerShell
PS C:\> New-StorageQosPolicy -PolicyId 7e2f3e73-1ae4-4710-8219-0769a4aba072 -PolicyType Aggregated -Name RestoredPolicy -MinimumIops 100 -MaximumIops 2000  

Name                    MinimumIops            MaximumIops            Status  
----                    -----------            -----------            ------  
RestoredPolicy          100                    2000                   Ok  
```  

Überprüfen Sie im letzten Schritt, ob die Richtlinie angewendet wurde.  

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, Status, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize  

InitiatorName Status MinimumIops MaximumIops StorageNodeIOPs Status File  
------------- ------ ----------- ----------- --------------- ------ ----  
                  Ok           0           0               0     Ok DefaultFlow  
                  Ok           0           0               8     Ok DefaultFlow  
                  Ok           0           0               9     Ok DefaultFlow  
                  Ok           0           0               0     Ok DefaultFlow  
                  Ok           0           0               0     Ok DefaultFlow  
                  Ok           0           0               0     Ok DefaultFlow  
                  Ok           0           0               0     Ok DefaultFlow  
                  Ok           0           0               0     Ok DefaultFlow  
                  Ok           0           0               0     Ok DefaultFlow  
BuildVM1          Ok         100         200             192     Ok BUILDVM1.VHDX  
BuildVM2          Ok         100         200             193     Ok BUILDVM2.VHDX  
BuildVM3          Ok          50         100              24     Ok WIN8RTM_ENTERPRISE_VL...  
BuildVM3          Ok         100         200             166     Ok BUILDVM3.VHDX  
BuildVM4          Ok          50         100              12     Ok WIN8RTM_ENTERPRISE_VL...  
BuildVM4          Ok         100         200             178     Ok BUILDVM4.VHDX  
TR20-VMM          Ok          33         666               2     Ok DATA2.VHDX  
TR20-VMM          Ok          33         666               2     Ok DATA1.VHDX  
TR20-VMM          Ok          33         666              10     Ok BOOT.VHDX  
WinOltp1          Ok          25         500               0     Ok 9914.0.AMD64FRE.WINMA...  
```  

#### <a name="BKMK_RemovePolicyFromVM"></a>Speicher-QoS-Richtlinien entfernen  

Wenn die Richtlinie absichtlich entfernt oder eine VM mit einer Richtlinie importiert wurde, die Sie nicht benötigen, kann sie entfernt werden.  

```PowerShell
PS C:\> Get-VM -Name WinOltp1 | Get-VMHardDiskDrive | Set-VMHardDiskDrive -QoSPolicyID $null  
```  

Nachdem die PolicyId aus den Einstellungen der virtuellen Festplatte entfernt wurde, lautet der Status „Ok“, und es werden keine Mindest- oder Höchstwerte angewendet.  

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize  

InitiatorName MinimumIops MaximumIops StorageNodeIOPs Status File  
------------- ----------- ----------- --------------- ------ ----  
                        0           0               0     Ok DefaultFlow  
                        0           0              16     Ok DefaultFlow  
                        0           0              12     Ok DefaultFlow  
                        0           0               0     Ok DefaultFlow  
                        0           0               0     Ok DefaultFlow  
                        0           0               0     Ok DefaultFlow  
                        0           0               0     Ok DefaultFlow  
                        0           0               0     Ok DefaultFlow  
                        0           0               0     Ok DefaultFlow  
BuildVM1              100         200             197     Ok BUILDVM1.VHDX  
BuildVM2              100         200             192     Ok BUILDVM2.VHDX  
BuildVM3                9           9              23     Ok WIN8RTM_ENTERPRISE_VL_BUILDW...  
BuildVM3               91         191             171     Ok BUILDVM3.VHDX  
BuildVM4                8           8              18     Ok WIN8RTM_ENTERPRISE_VL_BUILDW...  
BuildVM4               92         192             163     Ok BUILDVM4.VHDX  
TR20-VMM               33         666               2     Ok DATA2.VHDX  
TR20-VMM               33         666               1     Ok DATA1.VHDX  
TR20-VMM               33         666               5     Ok BOOT.VHDX  
WinOltp1                0           0               0     Ok 9914.0.AMD64FRE.WINMAIN.1412...  
WinOltp1                0           0            1811     Ok IOMETER.VHDX  
WinOltp1                0           0               0     Ok BOOT.VHDX  
```  

### <a name="BKMK_VMsThatDoNotMeetStorageQoSPoilicies"></a>Suchen von virtuellen Computern, die keine Speicher-QoS-Richtlinien erfüllen  
Der Status **InsufficientThroughput** wird Flüssen zugewiesen, die folgende Merkmale aufweisen:  

-   Für den Fluss ist in einer Richtlinie ein Mindestwert für IOPS definiert  

-   Die Flüsse initiieren E/A mit einer Geschwindigkeit, die den Mindestwert erreicht oder überschreitet  

-   Der Mindestwert für IOPS wird nicht erreicht  

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize  

InitiatorName MinimumIops MaximumIops StorageNodeIOPs                 Status File  
------------- ----------- ----------- ---------------                 ------ ----  
                        0           0               0                     Ok DefaultFlow  
                        0           0               0                     Ok DefaultFlow  
                        0           0              15                     Ok DefaultFlow  
                        0           0               0                     Ok DefaultFlow  
                        0           0               0                     Ok DefaultFlow  
                        0           0               0                     Ok DefaultFlow  
                        0           0               0                     Ok DefaultFlow  
                        0           0               0                     Ok DefaultFlow  
                        0           0               0                     Ok DefaultFlow  
BuildVM3               50         100              20                     Ok WIN8RTM_ENTE...  
BuildVM3              100         200             174                     Ok BUILDVM3.VHDX  
BuildVM4               50         100              11                     Ok WIN8RTM_ENTE...  
BuildVM4              100         200             188                     Ok BUILDVM4.VHDX  
TR20-VMM               33         666               3                     Ok DATA1.VHDX  
TR20-VMM               78        1032             180                     Ok BOOT.VHDX  
TR20-VMM               22         968               4                     Ok DATA2.VHDX  
WinOltp1             3750        5000               0                     Ok 9914.0.AMD64...  
WinOltp1            15000       20000           11679 InsufficientThroughput IOMETER.VHDX  
WinOltp1             3750        5000               0                     Ok BOOT.VHDX  
```  

Sie können Flüsse mit einem beliebigen Status (einschließlich **InsufficientThroughput**) wie nachfolgend gezeigt ermitteln:  

```PowerShell
PS C:\> Get-StorageQosFlow -Status InsufficientThroughput | fl  

FilePath           : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX  
FlowId             : 1ca356ff-fd33-5b5d-b60a-2c8659dc803e  
InitiatorId        : 2ceabcef-2eba-4f1b-9e66-10f960b50bbf  
InitiatorIOPS      : 12168  
InitiatorLatency   : 22.983  
InitiatorName      : WinOltp1  
InitiatorNodeName  : plang-c1.plang.nttest.microsoft.com  
Interval           : 300000  
Limit              : 20000  
PolicyId           : 5d1bf221-c8f0-4368-abcf-aa139e8a7c72  
Reservation        : 15000  
Status             : InsufficientThroughput  
StorageNodeIOPS    : 12181  
StorageNodeLatency : 22.0514  
StorageNodeName    : plang-fs2.plang.nttest.microsoft.com  
TimeStamp          : 2/13/2015 12:07:30 PM  
VolumeId           : 0d2fd367-8d74-4146-9934-306726913dda  
PSComputerName     :  
MaximumIops        : 20000  
MinimumIops        : 15000  
```  

## <a name="BKMK_Health"></a>Überwachen der Integrität mit Speicher-QoS  
Der neue Integritätsdienst vereinfacht die Überwachung des Speicherclusters und bietet eine zentrale Oberfläche, um das System auf Ereignisse auf einem Knoten zu überprüfen, für die Maßnahmen ergriffen werden müssen. In diesem Abschnitt wird beschrieben, wie Sie die Integrität Ihres Speicherclusters mithilfe des Cmdlets `debug-storagesubsystem` überwachen.  

### <a name="view-storage-status-with-debug-storagesubsystem"></a>Anzeigen des Speicherstatus mit Debug-StorageSubSystem  
Gruppierte Speicherplätze bieten ebenfalls eine zentrale Anzeige von Informationen zur Integrität des Speicherclusters. Dadurch können Administratoren im Handumdrehen aktuelle Probleme in Speicherbereitstellungen ermitteln und gemeldete Probleme überwachen.  

#### <a name="vm-with-invalid-policy"></a>VM mit ungültiger Richtlinie  
VMs mit ungültigen Richtlinien werden ebenfalls bei der Integritätsüberwachung des Speichersubsystems gemeldet.  Nachfolgend finden Sie ein Beispiel mit demselben Status, der auch im Abschnitt zum [Ermitteln von VMs mit ungültigen Richtlinien](#BKMK_FindingVMsWithInvalidPolicies) dieses Dokuments beschrieben ist.  

```PowerShell
C:\> Get-StorageSubSystem -FriendlyName Clustered* | Debug-StorageSubSystem  

EventTime                 :  
FaultId                   : 0d16d034-9f15-4920-a305-f9852abf47c3  
FaultingObject            :  
FaultingObjectDescription : Storage QoS Policy 5d1bf221-c8f0-4368-abcf-aa139e8a7c72  
FaultingObjectLocation    :  
FaultType                 : Storage QoS policy used by consumer does not exist.  
PerceivedSeverity         : Minor  
Reason                    : One or more storage consumers (usually Virtual Machines) are  
                            using a non-existent policy with id  
                            5d1bf221-c8f0-4368-abcf-aa139e8a7c72. Consumer details:  

                            Flow ID: 1ca356ff-fd33-5b5d-b60a-2c8659dc803e  
                            Initiator ID: 2ceabcef-2eba-4f1b-9e66-10f960b50bbf  
                            Initiator Name: WinOltp1  
                            Initiator Node: plang-c1.plang.nttest.microsoft.com  
                            File Path:  
                            C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX  
RecommendedActions        : {Reconfigure the storage consumers (usually Virtual Machines)  
                            to use a valid policy., Recreate any missing Storage QoS  
                            policies.}  
PSComputerName            :  
```  

#### <a name="lost-redundancy-for-a-storage-spaces-virtual-disk"></a>Verlorene Redundanz für einen virtuellen Datenträger mit Speicherplätzen  

In diesem Beispiel verfügt ein gruppierter Speicherplatz über einen virtuellen Datenträger, der mit Drei-Wege-Spiegelung erstellt wurde.  Ein ausgefallener Datenträger wurde aus dem System entfernt, es wurde jedoch kein Ersatzdatenträger hinzugefügt.  Das Speichersubsystem meldet den Verlust der Redundanz mit dem HealthStatus **Warning**, der OperationalStatus lautet jedoch **OK**, da das Volume weiterhin online ist.  

```PowerShell
PS C:\> Get-StorageSubSystem -FriendlyName Clustered*  

FriendlyName                   HealthStatus                   OperationalStatus  
------------                   ------------                   -----------------  
Clustered Windows Storage o... Warning                        OK  

[plang-fs1]: PS C:\Users\plang\Documents> Get-StorageSubSystem -FriendlyName Clustered* | Deb  
ug-StorageSubSystem  

EventTime                 :  
FaultId                   : dfb4b672-22a6-4229-b2ed-c29d7485bede  
FaultingObject            :  
FaultingObjectDescription : Virtual disk 'Two'  
FaultingObjectLocation    :  
FaultType                 : VirtualDiskDegradedFaultType  
PerceivedSeverity         : Minor  
Reason                    : Virtual disk 'Two' does not have enough redundancy remaining to  
                            successfully repair or regenerate its data.  
RecommendedActions        : {Rebalance the pool, replace failed physical disks, or add new  
                            physical disks to the storage pool, then repair the virtual  
                            disk.}  
PSComputerName            :  
```  

### <a name="sample-script-for-continuous-monitoring-of-storage-qos"></a>Beispielskript für eine kontinuierliche Überwachung von Speicher-QoS  

Dieser Abschnitt umfasst ein Beispielskript, das zeigt, wie gängige Ausfälle mithilfe eines WMI-Skripts überwacht werden können.  Dieses Skript dient als Ausgangspunkt für Entwickler, um Integritätsereignisse in Echtzeit abzurufen.  

**Beispielskript:**  

```PowerShell
param($cimSession)  
# Register and display events  
Register-CimIndicationEvent -Namespace root\microsoft\windows\storage -ClassName msft_storagefaultevent -CimSession $cimSession  

while ($true)  
{  
     $e = (Wait-Event)  
     $e.SourceEventArgs.NewEvent  
     Remove-Event $e.SourceIdentifier  
}  
```  

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen  

### <a name="how-do-i-retain-a-storage-qos-policy-being-enforced-for-my-virtual-machine-if-i-move-its-vhdvhdx-files-to-another-storage-cluster"></a>Wie behalte ich eine QoS für Speicher-Richtlinie bei, die für meine virtuellen Computer erzwungen wird, wenn ich die zugehörigen VHD-/VHDX-Dateien in einen anderen Speichercluster verschiebe  

Die Einstellung der VHD/VHDX-Datei, die die Richtlinie angibt, ist die GUID einer Richtlinien-ID.  Beim Erstellen einer Richtlinie kann die GUID mithilfe des Parameters **PolicyID** angegeben werden.  Wenn dieser Parameter nicht angegeben wird, wird eine zufällige GUID erstellt.  Sie können also die PolicyID auf dem Speichercluster abrufen, auf dem die VMs ihre VHD/VHDX-Dateien aktuell speichern, und auf dem Zielspeichercluster eine identische Richtlinie mit derselben GUID erstellen.  Wenn die VM-Dateien auf die neuen Speichercluster verschoben werden, wird die Richtlinie mit derselben GUID angewendet.  

Zum Anwenden von Richtlinien über mehrere Speichercluster hinweg kann System Center Virtual Machine Manager verwendet werden. Dadurch lässt sich dieses Szenario deutlich vereinfachen.  
### <a name="if-i-change-the-storage-qos-policy-why-dont-i-see-it-take-effect-immediately-when-i-run-get-storageqosflow"></a>Weshalb sind Änderungen an der QoS für Speicher-Richtlinie beim Ausführen von Get-StorageQoSFlow nicht umgehend sichtbar  

Wenn ein Fluss den Höchstwert einer Richtlinie erreicht, Sie die Richtlinie ändern, und Sie dann umgehend ein PowerShell-Cmdlet ausführen, um die Latenz/IOPS/Bandbreite der Flüsse zu ermitteln, dauert es bis zu 5 Minuten, bis die Richtlinienänderungen sichtbar sind.  Die neuen Grenzwerte sind nach einigen wenigen Sekunden wirksam, das PowerShell-Cmdlet **Get-StorgeQoSFlow** arbeitet jedoch mit einem Durchschnittswert der einzelnen Zähler sowie mit einem 5-minütigen gleitenden Fenster.  Wenn ein aktueller Wert angezeigt würde und Sie das PowerShell-Cmdlet mehrmals hintereinander ausführen würden, würde andernfalls eine große Anzahl unterschiedlicher Werte angezeigt, da die Werte für IOPS und Latenzen erheblich schwanken können.

### <a name="BKMK_Updates"></a>Welche neuen Funktionen wurden in Windows Server 2016 hinzugefügt?

In Windows 2016 wurden einige Namen der Richtlinientypen für Speicher-QoS geändert.  Der Name des Richtlinientyps **MultiInstance** wurde in **Dedicated** und der Name **SingleInstance** in **Aggregated** geändert. Das Verwaltungsverhalten dedizierter Richtlinien hat sich ebenfalls geändert. Bei VHD/VHDX-Dateien innerhalb desselben virtuellen Computers, auf die dieselbe Richtlinie vom Typ **Dedicated** angewendet wird, wird die zugewiesene E/A-Leistung nicht gemeinsam verwendet.  

Es gibt zwei neue QoS für Speicher-Features in Windows Server 2016:  

-   **Maximale Bandbreite**  

    Mit QoS für Speicher in Windows Server 2016 gibt es nun die Möglichkeit, eine maximale Bandbreite für die Flüsse anzugeben, die der Richtlinie zugewiesen sind.  Zur Angabe der maximalen Bandbreite in den **StorageQosPolicy**-Cmdlets wird der Parameter **MaximumIOBandwidth** verwendet, und die Ausgabe erfolgt in Bytes pro Sekunde.  
    Wenn sowohl **MaximimIops** als auch **MaximumIOBandwidth** in einer Richtlinie angegeben werden, finden beide Werte Anwendung. Die E/A der Flüsse ist durch den ersten Wert beschränkt, der von den Flüssen erreicht wird.  

-   **IOPS-Normalisierung ist konfigurierbar**  

    Speicher-QoS verwendet die Normalisierung von IOPS.  Standardmäßig wird eine Normalisierungsgröße von 8 KB verwendet.  Mit QoS für Speicher in Windows Server 2016 gibt es nun die Möglichkeit, eine andere Normalisierungsgröße für den Speichercluster anzugeben.  Diese Normalisierungsgröße wirkt sich auf alle Flüsse des Speicherclusters aus und ist nach der Änderung umgehend (innerhalb weniger Sekunden) wirksam.  Der Mindestwert beträgt 1 KB, der Höchstwert 4 GB (ein höherer Wert als 4 MB sollte jedoch nicht festgelegt werden, da E/A-Vorgänge diese Größe üblicherweise nicht überschreiten).  

    Beachten Sie Folgendes: Wenn Sie die IOPS-Normalisierung ändern, wird dasselbe E/A-Muster bzw. derselbe E/A-Durchsatz aufgrund der geänderten Normalisierungsberechnung mit unterschiedlichen IOPS-Werten in der Speicher-QoS-Ausgabe angezeigt.  Beim Vergleich von IOPS auf verschiedenen Speicherclustern sollten Sie auch den jeweils verwendeten Normalisierungswert überprüfen, da dieser sich auf die angezeigten normalisierten IOPS auswirkt.    

#### <a name="example-1-creating-a-new-policy-and-viewing-the-maximum-bandwidth-on-the-storage-cluster"></a>Beispiel 1: Erstellen einer neuen Richtlinie und Anzeigen der maximalen Bandbreite im Speicher Cluster  
Sie können in PowerShell die Einheiten angeben, in denen eine Zahl ausgedrückt wird.  Im folgenden Beispiel wird eine Größe von 10 MB als maximale Bandbreite verwendet.  Speicher-QoS wandelt diesen Wert um und speichert ihn in Bytes pro Sekunde. Die Größe von 10 MB wird also in 10485760 Bytes pro Sekunde umgewandelt.  

```PowerShell
PS C:\Windows\system32> New-StorageQosPolicy -Name HR_VMs -MaximumIops 1000 -MinimumIops 20 -MaximumIOBandwidth 10MB  

Name   MinimumIops MaximumIops MaximumIOBandwidth Status  
----   ----------- ----------- ------------------ ------  
HR_VMs 20          1000        10485760           Ok  

PS C:\Windows\system32> Get-StorageQosPolicy  

Name    MinimumIops MaximumIops MaximumIOBandwidth Status  
----    ----------- ----------- ------------------ ------  
Default 0           0           0                  Ok  
HR_VMs  20          1000        10485760           Ok  

PS C:\Windows\system32> Get-StorageQoSFlow | fL InitiatorName,FilePath,InitiatorIOPS,InitiatorLatency,InitiatorBandwidth  

InitiatorName      : testsQoS  
FilePath           : C:\ClusterStorage\Volume2\TESTSQOS\VIRTUAL HARD DISKS\TESTSQOS.VHDX  
InitiatorIOPS      : 5  
InitiatorLatency   : 1.5455  
InitiatorBandwidth : 37888  
```  

#### <a name="example-2-get-iops-normalization-settings-and-specify--a-new-value"></a>Beispiel 2: IOPS-normalisierungs Einstellungen erhalten und einen neuen Wert angeben  

Das folgende Beispiel zeigt, wie Sie die IOPS-Normalisierungseinstellungen für einen Speichercluster abrufen (standardmäßig 8 KB), diesen Wert in 32 KB ändern und ihn anschließend erneut anzeigen.  Beachten Sie, dass Sie den Wert in diesem Beispiel als „32KB“ angeben, da in PowerShell keine Umwandlung in Bytes erforderlich ist.   Bei der Ausgabe wird der Wert jedoch in Bytes pro Sekunde angezeigt.  

```PowerShell
PS C:\Windows\system32> Get-StorageQosPolicyStore  

IOPSNormalizationSize  
---------------------  
8192  

PS C:\Windows\system32> Set-StorageQosPolicyStore -IOPSNormalizationSize 32KB  
PS C:\Windows\system32> Get-StorageQosPolicyStore  

IOPSNormalizationSize  
---------------------  
32768  
```    

## <a name="see-also"></a>Siehe auch  
- [Windows Server 2016](../../get-started/windows-server-2016.md)  
- [Speicher Replikat in Windows Server 2016](../storage-replica/storage-replica-overview.md)  
- [Direkte Speicherplätze in Windows Server 2016](../storage-spaces/storage-spaces-direct-overview.md)  
