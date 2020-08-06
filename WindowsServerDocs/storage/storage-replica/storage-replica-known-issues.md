---
title: Bekannte Probleme mit Speicherreplikaten
ms.prod: windows-server
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 06/25/2019
ms.assetid: ceddb0fa-e800-42b6-b4c6-c06eb1d4bc55
ms.openlocfilehash: 665d137673c3229f2b06283965c085ae25a2287c
ms.sourcegitcommit: acfdb7b2ad283d74f526972b47c371de903d2a3d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87769618"
---
# <a name="known-issues-with-storage-replica"></a>Bekannte Probleme mit Speicherreplikaten

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal)

In diesem Thema werden bekannte Probleme mit dem Speicher Replikat in Windows Server erörtert.

## <a name="after-removing-replication-disks-are-offline-and-you-cannot-configure-replication-again"></a>Nach dem Entfernen der Replikation sind Datenträger offline, und Sie können die Replikation nicht erneut konfigurieren

In Windows Server 2016 können Sie auf einem Datenträger, der zuvor repliziert wurde, möglicherweise keine Replikation bereitstellen, oder es sind Volumes vorhanden, die nicht bereitgestellt werden können. Dies kann auftreten, wenn ein bestimmter Fehlerzustand das Entfernen der Replikation verhindert oder wenn Sie das Betriebssystem auf einem Computer neu installieren, der zuvor die Replikation von Daten ausgeführt hat.

Um das Problem zu beheben, müssen Sie die versteckte Speicherreplikatpartition von den Datenträgern löschen und die Datenträger mithilfe des Cmdlets `Clear-SRMetadata` in einen beschreibbaren Status zurückversetzen.

- Um alle verwaisten Speicherreplikat-Partitionsdatenbankslots zu entfernen und alle Partitionen erneut bereitzustellen, verwenden Sie den Parameter `-AllPartitions` wie folgt:

    ```PowerShell
    Clear-SRMetadata -AllPartitions
    ```

- Um alle verwaisten Speicherreplikat-Protokolldaten zu entfernen, verwenden Sie den Parameter `-AllLogs` wie folgt:

    ```PowerShell
    Clear-SRMetadata -AllLogs
    ```

- Um alle verwaisten Failovercluster-Konfigurationsdaten zu entfernen, verwenden Sie den Parameter `-AllConfiguration` wie folgt:

    ```PowerShell
    Clear-SRMetadata -AllConfiguration
    ```

- Um einzelne Replikationsgruppen-Metadaten zu entfernen, verwenden Sie den Parameter `-Name` wie folgt:

    ```PowerShell
    Clear-SRMetadata -Name RG01 -Logs -Partition
    ```

Der Server muss nach der Bereinigung der Partitionsdatenbank möglicherweise neu gestartet werden. Sie können den Neustart vorübergehend mit `-NoRestart` unterdrücken, aber Sie sollten den Neustart des Servers nicht komplett überspringen, wenn er vom Cmdlet angefordert wird. Dieses Cmdlet entfernt weder Datenvolumes noch die auf diesen Volumes enthaltenen Daten.

## <a name="during-initial-sync-see-event-log-4004-warnings"></a>Während der ersten Synchronisierung werden Ereignisprotokoll 4004-Warnungen angezeigt

In Windows Server 2016 werden bei der Konfiguration der Replikation auf dem Quell-und dem Zielserver während der ersten Synchronisierung möglicherweise mehrere Warnungen vom Typ "**storagereplica\admin*-Event Log 4004" angezeigt, wobei der Status "nicht genügend Systemressourcen vorhanden ist, um die API abzuschließen" angezeigt wird. Sie werden wahrscheinlich auch 5014-Fehler angezeigt. Diese Fehler weisen darauf hin, dass die Server nicht über genügend Arbeitsspeicher (RAM) verfügen, um gleichzeitig die erste Synchronisierung und Workloads auszuführen. Fügen Sie RAM hinzu, oder reduzieren Sie den von Features und Anwendungen (mit Ausnahme des Speicherreplikats) verwendeten Arbeitsspeicher.

## <a name="when-using-guest-clusters-with-shared-vhdx-and-a-host-without-a-csv-virtual-machines-stop-responding-after-configuring-replication"></a>Werden Gastcluster mit freigegebenem VHDX und ein Host ohne freigegebene Clustervolumes verwendet, reagieren virtuelle Computer nach dem Konfigurieren der Replikation nicht mehr

Werden in Windows Server 2016 Hyper-V-Gastcluster für Speicherreplikat-Tests oder zu Demonstrationszwecken sowie freigegebene VHDX als Gastclusterspeicher verwendet, reagieren die virtuellen Computer nach dem Konfigurieren der Replikation nicht mehr. Wenn Sie den Hyper-V-Host neu starten, reagieren die virtuellen Computer wieder, aber die Replikationskonfiguration wird nicht abgeschlossen, und er erfolgt keine Replikation.

Dieses Verhalten tritt auf, wenn Sie **fltmc.exe Attach svhdxflt*-verwenden, um die Anforderung für den Hyper-V-Host, auf dem ein CSV ausgeführt wird, zu umgehen. Dieser Befehl wird nicht unterstützt und ist ausschließlich für Test- und Demonstrationszwecke bestimmt.

Die Ursache der Verlangsamung ist ein entwurfsbedingtes Interoperabilitätsproblem zwischen dem QoS für Speicher-Feature in Windows Server 2016 und dem manuell angeschlossenen freigegebenen VHDX-Filter. Um dieses Problem zu beheben, deaktivieren Sie den Speicher-QoS-Filtertreiber, und starten Sie den Hyper-V-Host neu:

```
SC config storqosflt start= disabled
```

## <a name="cannot-configure-replication-when-using-new-volume-and-differing-storage"></a>Replikation kann unter Verwendung von „New-Volume“ und unterschiedlichem Speicher nicht konfiguriert werden

Wenn Sie das Cmdlet `New-Volume`zusammen mit unterschiedlichen Gruppen von Speicher auf Quell- und Zielserver verwenden, z.B. zwei verschiedene SANs oder zwei JBODs mit unterschiedlichen Datenträgern, können Sie die Replikation möglicherweise anschließend nicht mithilfe von `New-SRPartnership` konfigurieren. Der angezeigte Fehler kann folgenden Text enthalten:

```
Data partition sizes are different in those two groups
```

Verwenden Sie das Cmdlet `New-Partition**` anstelle von `New-Volume`, um Volumes zu erstellen und zu formatieren, Weil das zweite Cmdlet die Volumegröße auf unterschiedliche Speicherarrays möglicherweise rundet. Wenn Sie bereits ein NTFS-Volume erstellt haben, können Sie mit `Resize-Partition` eines der Volumes vergrößern oder verkleinern, um es an die Größe des anderen anzupassen (dies ist bei ReFS-Volumes nicht möglich). Wenn Sie **Diskmgmt*-oder **Server-Manager**verwenden, erfolgt keine Rundung.

## <a name="running-test-srtopology-fails-with-name-related-errors"></a>Das Ausführen von Test-SRTopology schlägt mit Fehlern im Zusammenhang mit Namen fehl

Bei der Verwendung von `Test-SRTopology` wird eine der folgenden Fehlermeldungen angezeigt:

**FEHLERBEISPIEL 1:**

```
WARNING: Invalid value entered for target computer name: sr-srv03. Test-SrTopology cmdlet does not accept IP address as input for target computer name parameter. NetBIOS names and fully qualified domain names are acceptable inputs
WARNING: System.Exception
WARNING: at Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand.BeginProcessing()
Test-SRTopology : Invalid value entered for target computer name: sr-srv03. Test-SrTopology cmdlet does not accept IP address as input for target computer name parameter. NetBIOS names and fully qualified domain names are acceptable inputs
At line:1 char:1
+ Test-SRTopology -SourceComputerName sr-srv01 -SourceVolumeName d: -So ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo          : InvalidArgument: (:) [Test-SRTopology], Exception
+ FullyQualifiedErrorId : TestSRTopologyFailure,Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand
```

**FEHLERBEISPIEL 2:**

```
WARNING: Invalid value entered for source computer name
```

**FEHLERBEISPIEL 3:**

```
The specified volume cannot be found G: cannot be found on computer SRCLUSTERNODE1
```

Dieses Cmdlet verfügt über eingeschränkte Fehlerberichterstattung in Windows Server 2016 und gibt für viele häufige Probleme die gleiche Ausgabe zurück. Der Fehler kann aus folgenden Gründen angezeigt werden:

- Sie sind beim Quellcomputer als lokaler Benutzer und nicht als Domänenbenutzer angemeldet.

- Der Zielcomputer wird nicht ausgeführt oder ist über das Netzwerk nicht verfügbar.

- Sie haben einen falschen Namen für den Zielcomputer angegeben.

- Sie haben eine IP-Adresse für den Zielserver angegeben.

- Die Zielcomputerfirewall blockiert den Zugriff auf PowerShell und/oder CIM-Aufrufe.

- Auf dem Zielcomputer wird der WMI-Dienst nicht ausgeführt.

- Sie haben bei der Remoteausführung des Cmdlets `Test-SRTopology` von einem Verwaltungscomputer aus CREDSSP nicht verwendet.

- Die festgelegten Quell- oder Zielvolumes sind lokale Datenträger auf einem Clusterknoten, keine Clusterdatenträger.

## <a name="configuring-new-storage-replica-partnership-returns-an-error---failed-to-provision-partition"></a>Beim Konfigurieren einer neuen Speicherreplikatpartnerschaft wird ein Fehler zurückgegeben: „Fehler beim Bereitstellen der Partition“

Beim Erstellen einer neuen Replikationspartnerschaft mit `New-SRPartnership` wird die folgende Fehlermeldung angezeigt:

```
New-SRPartnership : Unable to create replication group test01, detailed reason: Failed to provision partition ed0dc93f-107c-4ab4-a785-afd687d3e734.
At line: 1 char: 1
+ New-SRPartnership -SourceComputerName srv1 -SourceRGName test01
+ Categorylnfo : ObjectNotFound: (MSFT_WvrAdminTasks : root/ Microsoft/. . s) CNew-SRPartnership], CimException
+ FullyQua1ifiedErrorId : Windows System Error 1168 ,New-SRPartnership
```

Dies wird dadurch verursacht, dass ein Daten Volume ausgewählt wird, das sich auf derselben Partition wie das System Laufwerk (d. h. das Laufwerk **C:*-Laufwerk mit dem zugehörigen Windows-Ordner) befindet. Beispielsweise auf einem Laufwerk, das sowohl die von der gleichen Partition erstellten Volumes **C:*-als auch **D:*-enthält. Dies wird im Speicherreplikatfeature nicht unterstützt. Sie müssen ein anderes Volume zum Replizieren auswählen.

## <a name="attempting-to-grow-a-replicated-volume-fails-due-to-missing-update"></a>Der Versuch, ein repliziertes Volume zu vergrößern, schlägt aufgrund fehlender Updates fehl

Wenn Sie versuchen, ein repliziertes Volume zu vergrößern oder zu erweitern, wird die folgende Fehlermeldung angezeigt:

```powershell
Resize-Partition -DriveLetter d -Size 44GB
Resize-Partition : The operation failed with return code 8
At line:1 char:1
+ Resize-Partition -DriveLetter d -Size 44GB
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo          : NotSpecified: (StorageWMI:ROOT/Microsoft/.../MSFT_Partition
[Resize-Partition], CimException
+ FullyQualifiedErrorId : StorageWMI 8,Resize-Partition
```

Wenn Sie das MMC-Snap-In „Datenträgerverwaltung“ verwenden, wird diese Fehlermeldung angezeigt:

```
Element not found
```

Dieser Fehler tritt auch dann auf, wenn Sie die Größenänderung des Volumes auf dem Quell Server mit ordnungsgemäß aktivieren `Set-SRGroup -Name rg01 -AllowVolumeResize $TRUE` .

Dieses Problem wurde im kumulativen Update für Windows 10, Version 1607 (Anniversary Update) und Windows Server 2016 behoben: 9. Dezember 2016 (KB3201845).

## <a name="attempting-to-grow-a-replicated-volume-fails-due-to-missing-step"></a>Der Versuch, ein repliziertes Volume zu vergrößern, schlägt aufgrund eines fehlenden Schritts fehl

Wenn Sie versuchen, die Größe eines replizierten Volumes auf dem Quell Server zu ändern, ohne zuerst festzulegen `-AllowResizeVolume $TRUE` , erhalten Sie folgende Fehlermeldung:

```powershell
Resize-Partition -DriveLetter I -Size 8GB
Resize-Partition : Failed

Activity ID: {87aebbd6-4f47-4621-8aa4-5328dfa6c3be}
At line:1 char:1
+ Resize-Partition -DriveLetter I -Size 8GB
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (StorageWMI:ROOT/Microsoft/.../MSFT_Partition) [Resize-Partition], CimException
     + FullyQualifiedErrorId : StorageWMI 4,Resize-Partition

Storage Replica Event log error 10307:

Attempted to resize a partition that is protected by Storage Replica.

DeviceName: \Device\Harddisk1\DR1
PartitionNumber: 7
PartitionId: {b71a79ca-0efe-4f9a-a2b9-3ed4084a1822}

Guidance: To grow a source data partition, set the policy on the replication group containing the data partition.
```

```powershell
Set-SRGroup -ComputerName [ComputerName] -Name [ReplicationGroupName] -AllowVolumeResize $true
```

Bevor Sie die Quelldaten Partition vergrößern, stellen Sie sicher, dass die Ziel Daten Partition über ausreichend Speicherplatz verfügt, um auf eine gleich große Größe zu erweitern. Das Verkleinern der durch das Speicher Replikat geschützten Daten Partition ist blockiert.

Datenträgerverwaltungs-Snap-in-Fehler:

```
An unexpected error has occurred
```

Denken Sie nach der Größenänderung des Volumes daran, die Größenänderung mit zu deaktivieren `Set-SRGroup -Name rg01 -AllowVolumeResize $FALSE` . Mit diesem Parameter wird verhindert, dass Administratoren versuchen, die Größe der Volumes zu ändern, bevor sichergestellt wird, dass genügend Speicherplatz auf dem Ziel Volume vorhanden ist

## <a name="attempting-to-move-a-pdr-resource-between-sites-on-an-asynchronous-stretch-cluster-fails"></a>Fehler beim Versuch, eine PDR-Ressource zwischen Standorten in einem asynchronen Stretched Cluster zu verschieben

Beim Versuch, eine mit einer physischen Datenträgerressource verbundene Rolle (z.B. einen zur allgemeinen Verwendung bestimmten Dateiserver) zu verschieben, um den zugehörigen Speicher in einen asynchronen Stretched Cluster zu verschieben, wird eine Fehlermeldung angezeigt.

Bei Verwendung des Failovercluster-Manager-Snap-Ins:

```
Error
The operation has failed.
The action 'Move' did not complete.
Error Code: 0x80071398
The operation failed because either the specified cluster node is not the owner of the group, or the node is not a possible owner of the group
```

Bei Verwendung des PowerShell-Cmdlets „Cluster“:

```powershell
Move-ClusterGroup -Name sr-fs-006 -Node sr-srv07
Move-ClusterGroup : An error occurred while moving the clustered role 'sr-fs-006'.
The operation failed because either the specified cluster node is not the owner of the group, or the node is not a possible owner of the group
At line:1 char:1
+ Move-ClusterGroup -Name sr-fs-006 -Node sr-srv07
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo          : NotSpecified: (:) [Move-ClusterGroup], ClusterCmdletException
+ FullyQualifiedErrorId : Move-ClusterGroup,Microsoft.FailoverClusters.PowerShell.MoveClusterGroupCommand
```

Die Ursache für das Auftreten ist ein beabsichtigtes Verhalten in Windows Server 2016. Verschieben Sie diese PDR-Datenträger mit `Set-SRPartnership` in einen asynchronen Stretched Cluster.

Dieses Verhalten wurde in Windows Server, Version 1709, geändert, um manuelle und automatisierte Failover mit asynchroner Replikation auf der Grundlage von Kundenfeedback zuzulassen.

## <a name="attempting-to-add-disks-to-a-two-node-asymmetric-cluster-returns-no-disks-suitable-for-cluster-disks-found"></a>Beim Versuch, Datenträger zu einem asymmetrischen Cluster mit zwei Knoten hinzuzufügen, wird „Keine geeigneten Datenträger für den Cluster gefunden“ angezeigt

Wenn Sie vor dem Hinzufügen einer Speicherreplikat-Stretchreplikation versuchen, einen Cluster mit nur zwei Knoten bereitzustellen, wird versucht, die Datenträger am zweiten Standort zu „Verfügbare Datenträger“ hinzuzufügen. Sie erhalten die folgende Fehlermeldung:

```
No disks suitable for cluster disks found. For diagnostic information about disks available to the cluster, use the Validate a Configuration Wizard to run Storage tests.
```

Dieser Fehler tritt nicht auf, wenn im Cluster mindestens drei Knoten vorhanden sind. Dieses Problem tritt aufgrund einer beabsichtigten Codeänderung in Windows Server 2016 für das Clusteringverhalten bei asymmetrischem Speicher auf.

Um den Speicher hinzuzufügen, können Sie den folgenden Befehl auf dem Knoten am zweiten Standort ausführen:

```
Get-ClusterAvailableDisk -All | Add-ClusterDisk
```

Dies funktioniert nicht mit lokalem Knoten Speicher. Sie können das Speicher Replikat verwenden, um einen Stretch-Cluster zwischen zwei Gesamt Knoten zu replizieren, **wobei jeder seinen eigenen Satz freigegebenen Speichers verwendet.**

## <a name="the-smb-bandwidth-limiter-fails-to-throttle-storage-replica-bandwidth"></a>Die SMB-Bandbreitenbeschränkung kann die Speicher Replikat Bandbreite nicht drosseln

Wenn Sie eine Bandbreitenbeschränkung für das Speicher Replikat angeben, wird der Grenzwert ignoriert und die volle Bandbreite verwendet. Beispiel:

```
Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond 32MB
```

Dieses Problem tritt auf, weil ein Interoperabilitäts Problem Zwischenspeicher Replikat und SMB vorliegt. Dieses Problem wurde zuerst im kumulativen Update vom Juli 2017 von Windows Server 2016 und in Windows Server, Version 1709, behoben.

## <a name="event-1241-warning-repeated-during-initial-sync"></a>Ereignis 1241 Warnung bei der anfänglichen Synchronisierung wiederholt

Wenn eine Replikations Partnerschaft als asynchron angegeben wird, protokolliert der Quellcomputer wiederholt das Warnungs Ereignis 1241 im Verwaltungs Kanal des Speicher Replikats. Beispiel:

```
Log Name:      Microsoft-Windows-StorageReplica/Admin
Source:        Microsoft-Windows-StorageReplica
Date:          3/21/2017 3:10:41 PM
Event ID:      1241
Task Category: (1)
Level:         Warning
Keywords:      (1)
User:          SYSTEM
Computer:      sr-srv05.corp.contoso.com
Description:
The Recovery Point Objective (RPO) of the asynchronous destination is unavailable.

LocalReplicationGroupName: rg01
LocalReplicationGroupId: {e20b6c68-1758-4ce4-bd3b-84a5b5ef2a87}
LocalReplicaName: f:\
LocalPartitionId: {27484a49-0f62-4515-8588-3755a292657f}
ReplicaSetId: {1f6446b5-d5fd-4776-b29b-f235d97d8c63}
RemoteReplicationGroupName: rg02
RemoteReplicationGroupId: {7f18e5ea-53ca-4b50-989c-9ac6afb3cc81}
TargetRPO: 30
```

Leitfaden: Dies ist in der Regel auf einen der folgenden Gründe zurückzuführen:

- Das asynchrone Ziel ist derzeit nicht getrennt. Die RPO kann nach der Wiederherstellung der Verbindung verfügbar werden.

- Das asynchrone Ziel kann keine Geschwindigkeit mit der Quelle behalten, sodass der aktuelle Datensatz des Ziel Protokolls nicht mehr im Quell Protokoll vorhanden ist. Das Ziel startet das Kopieren von Blöcken. Die RPO sollte verfügbar werden, nachdem das Kopieren des Blocks abgeschlossen ist.

Dies ist das erwartete Verhalten während der ersten Synchronisierung und kann sicher ignoriert werden. In einer späteren Version wird dieses Verhalten möglicherweise geändert. Wenn dieses Verhalten während der laufenden asynchronen Replikation angezeigt wird, untersuchen Sie die Partnerschaft, um zu bestimmen, warum die Replikation über die konfigurierte RPO hinaus verzögert wird (standardmäßig 30 Sekunden).

## <a name="event-4004-warning-repeated-after-rebooting-a-replicated-node"></a>Ereignis 4004 Warnung wird nach dem Neustart eines replizierten Knotens wiederholt

In seltenen und in der Regel nicht reproduzierbaren Fällen führt das Neustarten eines Servers in einer Partnerschaft zu einem Replikations Fehler, und das Warn Ereignis 4004 für die neu gestartet-Knoten Protokollierung mit dem Fehler "Zugriff verweigert".

```
Log Name:      Microsoft-Windows-StorageReplica/Admin
Source:        Microsoft-Windows-StorageReplica
Date:          3/21/2017 11:43:25 AM
Event ID:      4004
Task Category: (7)
Level:         Warning
Keywords:      (256)
User:          SYSTEM
Computer:      server.contoso.com
Description:
Failed to establish a connection to a remote computer.

RemoteComputerName: server
LocalReplicationGroupName: rg01
LocalReplicationGroupId: {a386f747-bcae-40ac-9f4b-1942eb4498a0}
RemoteReplicationGroupName: rg02
RemoteReplicationGroupId: {a386f747-bcae-40ac-9f4b-1942eb4498a0}
ReplicaSetId: {00000000-0000-0000-0000-000000000000}
RemoteShareName:{a386f747-bcae-40ac-9f4b-1942eb4498a0}.{00000000-0000-0000-0000-000000000000}
Status: {Access Denied}
A process has requested access to an object, but has not been granted those access rights.

Guidance: Possible causes include network failures, share creation failures for the remote replication group, or firewall settings. Make sure SMB traffic is allowed and there are no connectivity issues between the local computer and the remote computer. You should expect this event when suspending replication or removing a replication partnership.
```

Beachten Sie, dass `Status: "{Access Denied}"` `A process has requested access to an object, but has not been granted those access rights.` es sich bei diesem Problem um ein bekanntes Problem im Speicher Replikat handelt, das in Qualitäts Update vom 12. September 2017 – KB4038782 (OS-Build 14393,1715) korrigiert wurde.https://support.microsoft.com/help/4038782/windows-10-update-kb4038782

## <a name="error-failed-to-bring-the-resource-cluster-disk-x-online-with-a-stretch-cluster"></a>Fehler "Fehler beim Verschieben der Ressource" Cluster Datenträger x ' Online ". mit einem Stretch-Cluster

Wenn Sie versuchen, einen Cluster Datenträger nach einem erfolgreichen Failover online zu schalten, wenn Sie versuchen, den ursprünglichen primären Quell Standort erneut zu erstellen, erhalten Sie einen Fehler in Failovercluster-Manager. Beispiel:

```
Error
The operation has failed.
Failed to bring the resource 'Cluster Disk 2' online.

Error Code: 0x80071397
The operation failed because either the specified cluster node is not the owner of the resource, or the node is not a possible owner of the resource.
```

Wenn Sie versuchen, den Datenträger oder das CSV manuell zu verschieben, erhalten Sie einen zusätzlichen Fehler. Beispiel:

```
Error
The operation has failed.
The action 'Move' did not complete.

Error Code: 0x8007138d
A cluster node is not available for this operation
```

Dieses Problem wird dadurch verursacht, dass ein oder mehrere nicht initialisierte Datenträger an mindestens einen Cluster Knoten angefügt werden. Um das Problem zu beheben, initialisieren Sie den gesamten zugeordneten Speicher mithilfe von diskmgmt. msc, DISKPART.EXE oder dem PowerShell-Cmdlet "Initialisieren-Disk".

Wir arbeiten an der Bereitstellung eines Updates, das dieses Problem dauerhaft löst. Wenn Sie uns bei der Unterstützung von Microsoft Premier Support-Vereinbarung interessiert sind, senden Sie eine e-Mail SRFEED@microsoft.com an, damit wir mit Ihnen beim Einreichen einer backportanforderung zusammenarbeiten können.

## <a name="gpt-error-when-attempting-to-create-a-new-sr-partnership"></a>GPT-Fehler beim Erstellen einer neuen SR-Partnerschaft.

Beim Ausführen von "New-srpartnership" tritt der folgende Fehler auf:

```
Disk layout type for volume \\?\Volume{GUID}\ is not a valid GPT style layout.
New-SRPartnership : Unable to create replication group SRG01, detailed reason: Disk layout type for volume
\\?\Volume{GUID}\ is not a valid GPT style layout.
At line:1 char:1
+ New-SRPartnership -SourceComputerName nodesrc01 -SourceRGName SRG01 ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo : NotSpecified: (MSFT_WvrAdminTasks:root/Microsoft/...T_WvrAdminTasks) [New-SRPartnership], CimException
+ FullyQualifiedErrorId : Windows System Error 5078,New-SRPartnership
```

In der Failovercluster-Manager GUI gibt es keine Option zum Einrichten der Replikation für den Datenträger.

Beim Ausführen von Test-srtopology schlägt der Vorgang mit folgenden Fehlern fehl:

```
WARNING: Object reference not set to an instance of an object.
WARNING: System.NullReferenceException
WARNING:    at Microsoft.FileServices.SR.Powershell.MSFTPartition.GetPartitionInStorageNodeByAccessPath(String AccessPath, String ComputerName, MIObject StorageNode)
    at Microsoft.FileServices.SR.Powershell.Volume.GetVolume(String Path, String ComputerName)
    at Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand.BeginProcessing()
Test-SRTopology : Object reference not set to an instance of an object.
At line:1 char:1
+ Test-SRTopology -SourceComputerName nodesrc01 -SourceVolumeName U: - ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo : InvalidArgument: (:) [Test-SRTopology], NullReferenceException
+ FullyQualifiedErrorId : TestSRTopologyFailure,Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand
```

Dies ist darauf zurückzuführen, dass die Cluster Funktionsebene auf Windows Server 2012 R2 (d.h. FL 8) festgelegt ist. Das Speicher Replikat sollte hier einen bestimmten Fehler zurückgeben. stattdessen wird eine falsche Fehler Zuordnung zurückgegeben.

```
Run Get-Cluster | fl - on each node.
```

Wenn `ClusterFunctionalLevel = 9` der Wert ist, ist dies die Windows 2016 clusterfunctionallevel-Version, die zum Implementieren des Speicher Replikats auf diesem Knoten erforderlich
Wenn "clusterfunctionallevel" nicht 9 ist, muss "clusterfunctionallevel" aktualisiert werden, um das Speicher Replikat auf diesem Knoten zu implementieren.

Um das Problem zu beheben, müssen Sie die Cluster Funktionsebene durch Ausführen des PowerShell-Cmdlets " [Update-clusterfunctionallevel](/powershell/module/failoverclusters/update-clusterfunctionallevel)" erhöhen.

## <a name="small-unknown-partition-listed-in-diskmgmt-for-each-replicated-volume"></a>In diskmgmt für jedes repliziertes Volume ist eine kleine Unbekannte Partition aufgeführt.

Beim Ausführen des Datenträgerverwaltungs-Snap-Ins (diskmgmt). MSC) bemerken Sie ein oder mehrere Volumes, die ohne Bezeichnung oder Laufwerk Buchstabe und 1 MB groß sind. Möglicherweise sind Sie in der Lage, das unbekannte Volume zu löschen, oder Sie erhalten Folgendes:

```
An Unexpected Error has Occurred
```

Dieses Verhalten ist beabsichtigt. Dabei handelt es sich nicht um ein Volume, sondern um eine Partition. Das Speicher Replikat erstellt eine Partition mit 512 KB als Daten Bank Slot für Replikations Vorgänge (das Legacy Tool "diskmgmt. msc" rundet auf das nächste MB). Eine Partition wie diese für jedes replizierte Volume ist normal und erwünscht. Wenn Sie nicht mehr verwendet werden, können Sie diese 512 KB-Partition löschen. verwendete Verwendungszwecke können nicht gelöscht werden. Die Partition wird nie vergrößert oder verkleinert. Wenn Sie die Replikation neu erstellen, empfiehlt es sich, die Partition zu belassen, da Speicher Replikate nicht verwendete Partitionen beanspruchen.

Verwenden Sie zum Anzeigen von Details das Tool DiskPart oder das Cmdlet Get-Partition. Diese Partitionen weisen den GPT-Typ auf `558d43c5-a1ac-43c0-aac8-d1472b2923d1` .

## <a name="a-storage-replica-node-hangs-when-creating-snapshots"></a>Beim Erstellen von Momentaufnahmen hängt ein Speicher Replikat Knoten

Beim Erstellen einer VSS-Momentaufnahme (durch Sicherung, vssadmin usw.) ist ein Speicher Replikat Knoten nicht mehr vorhanden, und Sie müssen einen Neustart des Knotens erzwingen, um ihn wiederherzustellen. Es gibt keinen Fehler, sondern nur einen festen Absturz des Servers.

Dieses Problem tritt auf, wenn Sie eine VSS-Momentaufnahme des Protokoll Volumes erstellen. Die zugrunde liegende Ursache ist ein Legacy Design Aspekt von VSS, nicht Speicher Replikat. Das resultierende Verhalten beim Erstellen einer Momentaufnahme des Speicher Replikat Protokoll Volumes ist ein VSS-e/a-Abfrage Mechanismus, der den Server Deadlocks blockiert.

Um dieses Verhalten zu verhindern, erstellen Sie keine Momentaufnahme Speicher Replikat Protokollvolumes. Es ist nicht erforderlich, Speicher Replikat-Protokoll Volumes zu erstellen, da diese Protokolle nicht wieder hergestellt werden können. Außerdem sollte das Protokoll Volume nie andere Workloads enthalten, daher ist im Allgemeinen keine Momentaufnahme erforderlich.

## <a name="high-io-latency-increase-when-using-storage-spaces-direct-with-storage-replica"></a>Erhöhung der e/a-Latenz bei Verwendung direkte Speicherplätze mit Speicher Replikat

Wenn Sie direkte Speicherplätze mit einem nvme-oder SSD-Cache verwenden, wird bei der Konfiguration der Speicher Replikat Replikation zwischen direkte Speicherplätze Clustern eine höhere Latenz als erwartet angezeigt. Die Änderung der Latenz ist proportional sehr viel höher als bei der Verwendung von nvme und SSD in einer Leistungs-und Kapazitäts Konfiguration und ohne HDD-Ebene und Kapazitäts Ebene.

Dieses Problem tritt aufgrund von architektonischen Einschränkungen im Protokoll Mechanismus des Speicher Replikats in Kombination mit der extrem niedrigen Latenz von nvme im Vergleich zu langsameren Medien auf. Bei Verwendung des direkte Speicherplätze Caches werden alle e/a-Vorgänge von Speicher Replikat Protokollen zusammen mit allen aktuellen Lese-/Schreib-e/a-Vorgängen im Cache und nie auf den Leistungs-oder Kapazitäts Ebenen ausgeführt. Dies bedeutet, dass alle Speicher Replikat Aktivitäten auf der gleichen Geschwindigkeit erfolgen. diese Konfiguration wird zwar unterstützt, wird jedoch nicht empfohlen (Weitere Informationen finden Sie unter https://aka.ms/srfaq für Protokoll Empfehlungen).

Wenn Sie direkte Speicherplätze mit HDDs verwenden, ist es nicht möglich, den Cache zu deaktivieren oder zu vermeiden. Um dieses Problem zu umgehen, können Sie, wenn Sie nur SSD und nvme verwenden, nur die Leistungs-und Kapazitäts Ebenen konfigurieren. Wenn Sie diese Konfiguration verwenden und die SR-Protokolle nur mit den Datenvolumes, auf denen Sie sich auf der Kapazitäts Ebene befinden, auf der Leistungs Ebene platzieren, vermeiden Sie das oben beschriebene Problem mit hoher Latenz. Dies kann mit einer Mischung aus schnelleren und langsameren SSDs und ohne nvme erfolgen.

Diese Problem Umgehung ist natürlich nicht ideal, und einige Kunden sind möglicherweise nicht in der Lage, Sie zu nutzen. Das Speicher Replikat Team arbeitet an Optimierungen und einem aktualisierten Protokoll Mechanismus für die Zukunft, um diese künstlichen Engpässe zu verringern. Dieses v 1.1-Protokoll wurde zunächst in Windows Server 2019 verfügbar, und die verbesserte Leistung wird im [Server Storage-Blog](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)beschrieben.

## <a name="error-could-not-find-file-when-running-test-srtopology-between-two-clusters"></a>Fehler "Datei konnte nicht gefunden werden" beim Ausführen von "Test-srtopology" zwischen zwei Clustern

Wenn Sie Test-srtopology zwischen zwei Clustern und ihren CSV-Pfaden ausführen, tritt ein Fehler mit dem folgenden Fehler auf:

```powershell
PS C:\Windows\system32> Test-SRTopology -SourceComputerName NedClusterA -SourceVolumeName C:\ClusterStorage\Volume1 -SourceLogVolumeName L: -DestinationComputerName NedClusterB -DestinationVolumeName C:\ClusterStorage\Volume1 -DestinationLogVolumeName L: -DurationInMinutes 1 -ResultPath C:\Temp

Validating data and log volumes...
Measuring Storage Replica recovery and initial synchronization performance...
WARNING: Could not find file '\\NedNode1\C$\CLUSTERSTORAGE\VOLUME1TestSRTopologyRecoveryTest\SRRecoveryTestFile01.txt'.
WARNING: System.IO.FileNotFoundException
WARNING:    at System.IO.__Error.WinIOError(Int32 errorCode, String maybeFullPath)
at System.IO.FileStream.Init(String path, FileMode mode, FileAccess access, Int32 rights, Boolean useRights, FileShare share, Int32 bufferSize, FileOptions options, SECURITY_ATTRIBUTES secAttrs, String msgPath, Boolean bFromProxy, Boolean useLongPath, Boolean checkHost) at System.IO.FileStream..ctor(String path, FileMode mode, FileAccess access, FileShare share, Int32 bufferSize, FileOptions options) at Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand.GenerateWriteIOWorkload(String Path, UInt32 IoSizeInBytes, UInt32 Parallel IoCount, UInt32 Duration)at Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand.<>c__DisplayClass75_0.<PerformRecoveryTest>b__0()at System.Threading.Tasks.Task.Execute()
Test-SRTopology : Could not find file '\\NedNode1\C$\CLUSTERSTORAGE\VOLUME1TestSRTopologyRecoveryTest\SRRecoveryTestFile01.txt'.
At line:1 char:1
+ Test-SRTopology -SourceComputerName NedClusterA -SourceVolumeName  ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo          : ObjectNotFound: (:) [Test-SRTopology], FileNotFoundException
+ FullyQualifiedErrorId : TestSRTopologyFailure,Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand
```

Dies wird durch einen bekannten Code Fehler in Windows Server 2016 verursacht. Dieses Problem wurde zunächst in Windows Server, Version 1709 und den zugehörigen RSAT-Tools behoben. Wenden Sie sich für eine downlevelauflösung an Microsoft-Support, und fordern Sie eine backportaktualisierung an. Es gibt keine Problemumgehung.

## <a name="error-specified-volume-could-not-be-found-when-running-test-srtopology-between-two-clusters"></a>Fehler "das angegebene Volume wurde nicht gefunden" beim Ausführen von "Test-srtopology" zwischen zwei Clustern

Wenn Sie Test-srtopology zwischen zwei Clustern und ihren CSV-Pfaden ausführen, tritt ein Fehler mit dem folgenden Fehler auf:

```
PS C:\> Test-SRTopology -SourceComputerName RRN44-14-09 -SourceVolumeName C:\ClusterStorage\Volume1 -SourceLogVolumeName L: -DestinationComputerName RRN44-14-13 -DestinationVolumeName C:\ClusterStorage\Volume1 -DestinationLogVolumeName L: -DurationInMinutes 30 -ResultPath c:\report

Test-SRTopology : The specified volume C:\ClusterStorage\Volume1 cannot be found on computer RRN44-14-09. If this is a cluster node, the volume must be part of a role or CSV; volumes in Available Storage are not accessible
At line:1 char:1
+ Test-SRTopology -SourceComputerName RRN44-14-09 -SourceVolumeName C:\ ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (:) [Test-SRTopology], Exception
    + FullyQualifiedErrorId : TestSRTopologyFailure,Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand
```

Wenn Sie das Quellknoten-CSV als Quell Volume angeben, müssen Sie den Knoten auswählen, der das CSV besitzt. Sie können das CSV entweder auf den angegebenen Knoten verschieben oder den Namen des Knotens ändern, den Sie in angegeben haben `-SourceComputerName` . Dieser Fehler hat eine verbesserte Nachricht in Windows Server 2019 erhalten.

## <a name="unable-to-access-the-data-drive-in-storage-replica-after-unexpected-reboot-when-bitlocker-is-enabled"></a>Auf das Daten Laufwerk im Speicher Replikat kann nach unerwartetem Neustart nicht zugegriffen werden, wenn BitLocker aktiviert ist.

Wenn BitLocker auf beiden Laufwerken (Protokoll Laufwerk und Daten Laufwerk) und auf beiden Speicher Replikat Laufwerken aktiviert ist, können Sie, wenn der primäre Server neu gestartet wird, nicht auf das primäre Laufwerk zugreifen, auch nachdem das Protokoll Laufwerk aus BitLocker entsperrt wurde.

Dies entspricht dem erwarteten Verhalten. Zum Wiederherstellen der Daten oder zum Zugreifen auf das Laufwerk müssen Sie zuerst das Protokoll Laufwerk entsperren und dann "diskmgmt. msc" öffnen, um das Daten Laufwerk zu suchen. Schalten Sie das Daten Laufwerk offline und online. Suchen Sie auf dem Laufwerk das BitLocker-Symbol, und Entsperren Sie das Laufwerk.

## <a name="issue-unlocking-the-data-drive-on-secondary-server-after-breaking-the-storage-replica-partnership"></a>Problem beim Entsperren des Daten Laufwerks auf dem sekundären Server, nachdem die Speicher Replikat Partnerschaft

Nachdem Sie die SR-Partnerschaft deaktiviert und das Speicher Replikat entfernt haben, wird Sie erwartet, wenn Sie das Daten Laufwerk des sekundären Servers nicht mit dem entsprechenden Kennwort oder Schlüssel entsperren können.

Zum Entsperren des Daten Laufwerks des sekundären Servers müssen Sie den Schlüssel oder das Kennwort des Daten Laufwerks des primären Servers verwenden.

## <a name="test-failover-doesnt-mount-when-using-asynchronous-replication"></a>Das Test Failover wird bei Verwendung der asynchronen Replikation nicht ausgeführt.

Wenn Sie "Mount-srdestination" ausführen, um ein Ziel Volume als Teil des Test Failover online zu schalten, tritt ein Fehler mit dem folgenden Fehler auf:

```
Mount-SRDestination: Unable to mount SR group <TEST>, detailed reason: The group or resource is not in the correct state to perform the supported operation.
    At line:1 char:1
    + Mount-SRDestination -ComputerName SRV1 -Name TEST -TemporaryP . . .
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (MSFT WvrAdminTasks : root/Microsoft/...(MSFT WvrAdminTasks : root/Microsoft/. T_WvrAdminTasks) (Mount-SRDestination], CimException
        + FullyQua1ifiedErrorId : Windows System Error 5823, Mount-SRDestination.
```

Wenn Sie einen synchronen partnerschaftentyp verwenden, funktioniert das Test Failover normal.

Dies wird durch einen bekannten Code Fehler in Windows Server, Version 1709, verursacht. Um dieses Problem zu beheben, installieren Sie das [Update vom 18. Oktober 2018](https://support.microsoft.com/help/4462932/windows-10-update-kb4462932). Dieses Problem ist in Windows Server 2019 und Windows Server, Version 1809 und höher, nicht enthalten.

## <a name="additional-references"></a>Weitere Verweise

- [Speicherreplikat](storage-replica-overview.md)
- [Stretch-Cluster Replikation mit frei gegebenem Speicher](stretch-cluster-replication-using-shared-storage.md)
- [Replikation von Server zu Server Speicher](server-to-server-storage-replication.md)
- [Cluster-zu-Cluster Speicher Replikation](cluster-to-cluster-storage-replication.md)
- [Speicherreplikat: Häufig gestellte Fragen](storage-replica-frequently-asked-questions.md)
- [Direkte Speicherplätze](../storage-spaces/storage-spaces-direct-overview.md)
