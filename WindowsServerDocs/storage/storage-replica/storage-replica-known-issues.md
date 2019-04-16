---
title: Bekannte Probleme mit Speicherreplikaten
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 10/13/2016
ms.assetid: ceddb0fa-e800-42b6-b4c6-c06eb1d4bc55
ms.openlocfilehash: 6f02ece1f327cf53667df09e6d13ace001259885
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="known-issues-with-storage-replica"></a>Bekannte Probleme mit Speicherreplikaten

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieser Abschnitt beschreibt bekannte Probleme mit Speicherreplikaten in Windows Server 2016.  

## <a name="after-removing-replication-disks-are-offline-and-you-cannot-configure-replication-again"></a>Nach dem Entfernen der Replikation sind Datenträger offline, und Sie können die Replikation nicht erneut konfigurieren  
In Windows Server 2016 können Sie auf einem Datenträger, der zuvor repliziert wurde, möglicherweise keine Replikation bereitstellen, oder es sind Volumes vorhanden, die nicht bereitgestellt werden können. Dies kann auftreten, wenn ein bestimmter Fehlerzustand das Entfernen der Replikation verhindert oder wenn Sie das Betriebssystem auf einem Computer neu installieren, der zuvor die Replikation von Daten ausgeführt hat.  

Um das Problem zu beheben, müssen Sie die versteckte Speicherreplikatpartition von den Datenträgern löschen und die Datenträger mithilfe des Cmdlets `Clear-SRMetadata` in einen beschreibbaren Status zurückversetzen.  

-   Um alle verwaisten Speicherreplikat-Partitionsdatenbankslots zu entfernen und alle Partitionen erneut bereitzustellen, verwenden Sie den Parameter `-AllPartitions` wie folgt:  

    ```  
    Clear-SRMetadata -AllPartitions  
    ```  

-   Um alle verwaisten Speicherreplikat-Protokolldaten zu entfernen, verwenden Sie den Parameter `-AllLogs` wie folgt:  

    ```  
    Clear-SRMetadata -AllLogs  
    ```  

-   Um alle verwaisten Failovercluster-Konfigurationsdaten zu entfernen, verwenden Sie den Parameter `-AllConfiguration` wie folgt:  

    ```  
    Clear-SRMetadata -AllConfiguration  
    ```  

-   Um einzelne Replikationsgruppen-Metadaten zu entfernen, verwenden Sie den Parameter `-Name` wie folgt:  

    ```  
    Clear-SRMetadata -Name RG01 -Logs -Partition  
    ```  

Der Server muss nach der Bereinigung der Partitionsdatenbank möglicherweise neu gestartet werden. Sie können den Neustart vorübergehend mit `-NoRestart` unterdrücken, aber Sie sollten den Neustart des Servers nicht komplett überspringen, wenn er vom Cmdlet angefordert wird. Dieses Cmdlet entfernt weder Datenvolumes noch die auf diesen Volumes enthaltenen Daten.  

## <a name="during-initial-sync-see-event-log-4004-warnings"></a>Während der ersten Synchronisierung werden Ereignisprotokoll 4004-Warnungen angezeigt  
In Windows Server 2016 können beim Konfigurieren der Replikation auf dem Quell- und/oder Zielserver während der ersten Synchronisierung mehrere **StorageReplica\Admin**-Ereignisprotokoll 4004-Warnungen mit dem Status „Nicht ausreichend Systemressourcen, um die API abzuschließen“ angezeigt werden. Sie werden wahrscheinlich auch 5014-Fehler angezeigt. Diese Fehler weisen darauf hin, dass die Server nicht über genügend Arbeitsspeicher (RAM) verfügen, um gleichzeitig die erste Synchronisierung und Workloads auszuführen. Fügen Sie RAM hinzu, oder reduzieren Sie den von Features und Anwendungen (mit Ausnahme des Speicherreplikats) verwendeten Arbeitsspeicher.  

## <a name="when-using-guest-clusters-with-shared-vhdx-and-a-host-without-a-csv-virtual-machines-stop-responding-after-configuring-replication"></a>Werden Gastcluster mit freigegebenem VHDX und ein Host ohne freigegebene Clustervolumes verwendet, reagieren virtuelle Computer nach dem Konfigurieren der Replikation nicht mehr  
Werden in Windows Server 2016 Hyper-V-Gastcluster für Speicherreplikat-Tests oder zu Demonstrationszwecken sowie freigegebene VHDX als Gastclusterspeicher verwendet, reagieren die virtuellen Computer nach dem Konfigurieren der Replikation nicht mehr. Wenn Sie den Hyper-V-Host neu starten, reagieren die virtuellen Computer wieder, aber die Replikationskonfiguration wird nicht abgeschlossen, und er erfolgt keine Replikation.  

Dieses Verhalten tritt auf, wenn Sie **fltmc.exe attach svhdxflt** verwenden, um die Voraussetzung zu umgehen, dass auf dem Hyper-V-Host ein freigegebenes Clustervolume ausgeführt werden muss. Dieser Befehl wird nicht unterstützt und ist ausschließlich für Test- und Demonstrationszwecke bestimmt.  

Die Ursache der Verlangsamung ist ein entwurfsbedingtes Interoperabilitätsproblem zwischen dem QoS für Speicher-Feature in Windows Server 2016 und dem manuell angeschlossenen freigegebenen VHDX-Filter. Um dieses Problem zu beheben, deaktivieren Sie den Speicher-QoS-Filtertreiber, und starten Sie den Hyper-V-Host neu:  

```  
SC config storqosflt start= disabled  
```  

## <a name="cannot-configure-replication-when-using-new-volume-and-differing-storage"></a>Replikation kann unter Verwendung von „New-Volume“ und unterschiedlichem Speicher nicht konfiguriert werden  
Wenn Sie das Cmdlet `New-Volume`zusammen mit unterschiedlichen Gruppen von Speicher auf Quell- und Zielserver verwenden, z. B. zwei verschiedene SANs oder zwei JBODs mit unterschiedlichen Datenträgern, können Sie die Replikation möglicherweise anschließend nicht mithilfe von `New-SRPartnership` konfigurieren. Der angezeigte Fehler kann folgenden Text enthalten:  

    Data partition sizes are different in those two groups  

Verwenden Sie das Cmdlet `New-Partition**` anstelle von `New-Volume`, um Volumes zu erstellen und zu formatieren, Weil das zweite Cmdlet die Volumegröße auf unterschiedliche Speicherarrays möglicherweise rundet. Wenn Sie bereits ein NTFS-Volume erstellt haben, können Sie mit `Resize-Partition` eines der Volumes vergrößern oder verkleinern, um es an die Größe des anderen anzupassen (dies ist bei ReFS-Volumes nicht möglich). Wenn Sie **Diskmgmt** oder den **Server-Manager** verwenden, erfolgt keine Rundung.  

## <a name="running-test-srtopology-fails-with-name-related-errors"></a>Das Ausführen von Test-SRTopology schlägt mit Fehlern im Zusammenhang mit Namen fehl

Bei der Verwendung von `Test-SRTopology` wird eine der folgenden Fehlermeldungen angezeigt:  

**FEHLERBEISPIEL 1:**

    WARNING: Invalid value entered for target computer name: sr-srv03. Test-SrTopology cmdlet does not accept IP address as  
    input for target computer name parameter. NetBIOS names and fully qualified domain names are acceptable inputs  
    WARNING: System.Exception  
    WARNING:    at Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand.BeginProcessing()  
    Test-SRTopology : Invalid value entered for target computer name: sr-srv03. Test-SrTopology cmdlet does not accept IP  
    address as input for target computer name parameter. NetBIOS names and fully qualified domain names are acceptable  
    inputs  
    At line:1 char:1  
    + Test-SRTopology -SourceComputerName sr-srv01 -SourceVolumeName d: -So ...  
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~  
        + CategoryInfo          : InvalidArgument: (:) [Test-SRTopology], Exception  
        + FullyQualifiedErrorId : TestSRTopologyFailure,Microsoft.FileServices.SR.Powershell.TestSRTopologyCommand  

**FEHLERBEISPIEL 2:**

    WARNING: Invalid value entered for source computer name

**FEHLERBEISPIEL 3:**

    The specified volume cannot be found G: cannot be found on computer SRCLUSTERNODE1

Dieses Cmdlet verfügt über eingeschränkte Fehlerberichterstattung in Windows Server 2016 und gibt für viele häufige Probleme die gleiche Ausgabe zurück. Der Fehler kann aus folgenden Gründen angezeigt werden:  

* Sie sind beim Quellcomputer als lokaler Benutzer und nicht als Domänenbenutzer angemeldet.  
* Der Zielcomputer wird nicht ausgeführt oder ist über das Netzwerk nicht verfügbar.  
* Sie haben einen falschen Namen für den Zielcomputer angegeben.  
* Sie haben eine IP-Adresse für den Zielserver angegeben.  
* Die Zielcomputerfirewall blockiert den Zugriff auf PowerShell und/oder CIM-Aufrufe.  
* Auf dem Zielcomputer wird der WMI-Dienst nicht ausgeführt.   
* Sie haben bei der Remoteausführung des Cmdlets `Test-SRTopology` von einem Verwaltungscomputer aus CREDSSP nicht verwendet.
* Die festgelegten Quell- oder Zielvolumes sind lokale Datenträger auf einem Clusterknoten, keine Clusterdatenträger.  

## <a name="configuring-new-storage-replica-partnership-returns-an-error---failed-to-provision-partition"></a>Beim Konfigurieren einer neuen Speicherreplikatpartnerschaft wird ein Fehler zurückgegeben: „Fehler beim Bereitstellen der Partition“
Beim Erstellen einer neuen Replikationspartnerschaft mit `New-SRPartnership` wird die folgende Fehlermeldung angezeigt:

    New-SRPartnership : Unable to create replication group test01, detailed reason: Failed to provision partition ed0dc93f-107c-4ab4-a785-afd687d3e734.
    At line: 1 char: 1
    + New-SRPartnership -SourceComputerName srv1 -SourceRGName test01
    + Categorylnfo : ObjectNotFound: (MSFT_WvrAdminTasks : root/ Microsoft/. . s) CNew-SRPartnership], CimException
    + FullyQua1ifiedErrorId : Windows System Error 1168 ,New-SRPartnership

Dies wird durch Auswahl eines Datenvolumes verursacht, das sich auf der gleichen Partition wie das Systemlaufwerk befindet (d. h. dem Laufwerk **C:** mit dem Windows-Ordner). Beispielsweise auf einem Laufwerk, das die aus der gleichen Partition erstellten Volumes **C:** und **D:** enthält. Dies wird im Speicherreplikatfeature nicht unterstützt. Sie müssen ein anderes Volume zum Replizieren auswählen.

## <a name="attempting-to-grow-a-replicated-volume-fails-due-to-missing-update"></a>Das Versuch, ein repliziertes Volume zu vergrößern, schlägt aufgrund eines fehlenden Updates fehl.
Wenn Sie versuchen, ein repliziertes Volume zu vergrößern oder zu erweitern, wird die folgende Fehlermeldung angezeigt:

    PS C:\> Resize-Partition -DriveLetter d -Size 44GB
    Resize-Partition : The operation failed with return code 8
    At line:1 char:1
    + Resize-Partition -DriveLetter d -Size 44GB
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (StorageWMI:ROOT/Microsoft/.../MSFT_Partition
    [Resize-Partition], CimException
    + FullyQualifiedErrorId : StorageWMI 8,Resize-Partition

Wenn Sie das MMC-Snap-In „Datenträgerverwaltung“ verwenden, wird diese Fehlermeldung angezeigt: 

    Element not found

Dies geschieht auch, wenn Sie das Ändern der Größe von Volumes auf dem Quellserver mithilfe von `Set-SRGroup -Name rg01 -AllowVolumeResize $TRUE` korrekt aktivieren. 

Dieses Problem wurde im kumulativen Update für Windows10 Version 1607 und Windows Server2016: 9.Dezember2016 (KB3201845) behoben. 

## <a name="attempting-to-grow-a-replicated-volume-fails-due-to-missing-step"></a>Das Versuch, ein repliziertes Volume zu vergrößern, schlägt aufgrund eines fehlenden Schritts fehl.
Wenn Sie versuchen, die Größe eines replizierten Volumes auf dem Quellserver zu änden, ohne zuvor `-AllowResizeVolume $TRUE` festzulegen, treten die folgenden Fehler auf:

    PS C:\> Resize-Partition -DriveLetter I -Size 8GB
    Resize-Partition : Failed
    Activity ID: {87aebbd6-4f47-4621-8aa4-5328dfa6c3be}
    At line:1 char:1
    + Resize-Partition -DriveLetter I -Size 8GB
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (StorageWMI:ROOT/Microsoft/.../MSFT_Partition) [Resize-Partition], CimException
        + FullyQualifiedErrorId : StorageWMI 4,Resize-Partition

Fehler 10307 im Speicherreplikat-Ereignisprotokoll:

    Attempted to resize a partition that is protected by Storage Replica .

    DeviceName: \Device\Harddisk1\DR1
    PartitionNumber: 7
    PartitionId: {b71a79ca-0efe-4f9a-a2b9-3ed4084a1822}

    Guidance: To grow a source data partition, set the policy on the replication group containing the data partition.

    Set-SRGroup -ComputerName [ComputerName] -Name [ReplicationGroupName] -AllowVolumeResize $true

    Before you grow the source data partition, ensure that the destination data partition has enough space to grow to an equal size. Shrinking of data partition protected by Storage Replica is blocked.

Fehler beim Snap-In „Datenträgerverwaltung“: 

    An unexpected error has occurred 

Denken Sie nach dem Ändern der Volumegröße daran, die Größenänderung mit `Set-SRGroup -Name rg01 -AllowVolumeResize $FALSE` zu deaktivieren. Dieser Parameter verhindert, dass Administratoren versuchen, die Volumegrößen zu ändern, bevor sie sichergestellt haben, dass auf dem Zielvolume ausreichend Speicherplatz verfügbar ist, in der Regel weil sie nicht wussten, dass Speicherreplikate vorhanden sind. 

## <a name="attempting-to-move-a-pdr-resource-between-sites-on-an-asynchronous-stretch-cluster-fails"></a>Fehler beim Versuch, eine PDR-Ressource zwischen Standorten in einem asynchronen Stretched Cluster zu verschieben
Beim Versuch, eine mit einer physischen Datenträgerressource verbundene Rolle (z.B. einen zur allgemeinen Verwendung bestimmten Dateiserver) zu verschieben, um den zugehörigen Speicher in einen asynchronen Stretched Cluster zu verschieben, wird eine Fehlermeldung angezeigt.

Bei Verwendung des Failovercluster-Manager-Snap-Ins:

    Error
    The operation has failed.
    The action 'Move' did not complete.
    Error Code: 0x80071398
    The operation failed because either the specified cluster node is not the owner of the group, or the node is not a possible owner of the group
    
Bei Verwendung des PowerShell-Cmdlets „Cluster“:

    PS C:\> Move-ClusterGroup -Name sr-fs-006 -Node sr-srv07
    Move-ClusterGroup : An error occurred while moving the clustered role 'sr-fs-006'.
    The operation failed because either the specified cluster node is not the owner of the group, or the node is not a
    possible owner of the group
    At line:1 char:1
    + Move-ClusterGroup -Name sr-fs-006 -Node sr-srv07
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Move-ClusterGroup], ClusterCmdletException
    + FullyQualifiedErrorId : Move-ClusterGroup,Microsoft.FailoverClusters.PowerShell.MoveClusterGroupCommand

Die Ursache für das Auftreten ist ein beabsichtigtes Verhalten in Windows Server2016. Verschieben Sie diese PDR-Datenträger mit `Set-SRPartnership` in einen asynchronen Stretched Cluster.  

## <a name="attempting-to-add-disks-to-a-two-node-asymmetric-cluster-returns-no-disks-suitable-for-cluster-disks-found"></a>Beim Versuch, Datenträger zu einem asymmetrischen Cluster mit zwei Knoten hinzuzufügen, wird „Keine geeigneten Datenträger für den Cluster gefunden“ angezeigt 
Wenn Sie vor dem Hinzufügen einer Speicherreplikat-Stretchreplikation versuchen, einen Cluster mit nur zwei Knoten bereitzustellen, wird versucht, die Datenträger am zweiten Standort zu „Verfügbare Datenträger“ hinzufügen. Es wird die folgende Fehlermeldung angezeigt:

    "No disks suitable for cluster disks found. For diagnostic information about disks available to the cluster, use the Validate a Configuration Wizard to run Storage tests." 

Dieser Fehler tritt nicht auf, wenn im Cluster mindestens drei Knoten vorhanden sind. Dieses Problem tritt aufgrund einer beabsichtigten Codeänderung in Windows Server 2016 für das Clusteringverhalten bei asymmetrischem Speicher auf. 

Um den Speicher hinzuzufügen, können Sie den folgenden Befehl auf dem Knoten am zweiten Standort ausführen:

`Get-ClusterAvailableDisk -All | Add-ClusterDisk`

Dies funktioniert nicht mit einem lokalen Speicher auf einem Knoten. Können Sie die Speicherreplikatfeature zum Replizieren eines Stretched Clusters zwischen zwei insgesamt Knoten verwenden, **bei dem jeder Knoten seinen eigenen freigegebenen Speicher verwendet.** 

## <a name="the-smb-bandwidth-limiter-fails-to-throttle-storage-replica-bandwidth"></a>SMB-Bandbreiteneinschränkung drosselt die Speicherreplikat-Bandbreite nicht
Wenn Sie dem Speicherreplikat eine Bandbreiteneinschränkung hinzufügen, wird das Limit ignoriert und die volle Bandbreite verwendet. Beispiele:

`Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond 32MB`

Dieses Problem tritt aufgrund eines Kompatibilitätsproblems zwischen Speicherreplikat und SMB auf. Dieses Problem wurde zuerst im Juli2017 im kumulativen Update von Windows Server 2016 und Windows Server, Version 1709, behoben.

## <a name="event-1241-warning-repeated-during-initial-sync"></a>Warnung 1241 im Zuge der ersten Synchronisierung wiederholt
Beim Angeben einer asynchronen Replikationspartnerschaft meldet der Quellcomputer Warnung 1241 wiederholt im Speicherreplikatverwaltungs-Kanal. Beispiele:

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

    Guidance: This is typically due to one of the following reasons: 

Das asynchrone Ziel ist derzeit nicht verbunden. Die RPO ist eventuell verfügbar, nachdem die Verbindung wiederhergestellt wurde.

    The asynchronous destination is unable to keep pace with the source such that the most recent destination log record is no longer present in the source log. The destination will start block copying. The RPO should become available after block copying completes.

Dies ist das erwartete Verhalten während der ersten Synchronisierung und kann ignoriert werden. In einer späteren Version wird dieses Verhalten möglicherweise geändert. Wenn dieses Verhalten während der asynchronen Replikation angezeigt wird, überprüfen Sie die Partnerschaft, um zu ermitteln, warum die Replikation von außerhalb der konfigurierten RPO (standardmäßig 30Sekunden) verzögert wird.

## <a name="event-4004-warning-repeated-after-rebooting-a-replicated-node"></a>Nach dem Neustart eines replizierten Knotens wiederholte Warnung 4004
Unter sehr seltenen Umständen, die in der Regel nicht reproduziert werden können, führt ein Neustart des Servers, der in einer Partnerschaft ist zu Replikationsfehlern und der neu gestartete Zielknoten zeigt Warnung 4004 mit einem „Zugriff verweigert”-Fehler an.

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

Beachten Sie `Status: "{Access Denied}"`und die Nachricht `A process has requested access to an object, but has not been granted those access rights.`. Dies ist ein bekanntes Problem im Speicher-Replikat und wurde in Qualitätsupdate am 12. September 2017 behoben – KB4038782 (OS Build 14393.1715) https://support.microsoft.com/en-us/help/4038782/windows-10-update-kb4038782 

## <a name="error-failed-to-bring-the-resource-cluster-disk-x-online-with-a-stretch-cluster"></a>Fehler "Die Ressource konnte nicht in den Onlinemodus 'Cluster Disk x' versetzt werden". mithilfe eines Stretched Clusters
Wenn Sie versuchen, einen Clusterdatenträger nach einem erfolgreichen Failover in den Onlinemodus zu versetzen, indem Sie die ursprüngliche Quellwebsite erneut als primären Site festlegen möchten, erhalten Sie eine Fehlermeldung im Failovercluster-Manager. Beispiele:

    Error
    The operation has failed.
    Failed to bring the resource 'Cluster Disk 2' online.
    
    Error Code: 0x80071397
    The operation failed because either the specified cluster node is not the owner of the resource, or the node is not a possible owner of the resource.
    
Wenn Sie versuchen, den Datenträger oder CSV manuell zu verschieben, erhalten Sie eine zusätzliche Fehlermeldung. Beispiele:

    Error
    The operation has failed.
    The action 'Move' did not complete.
    
    Error Code: 0x8007138d
    A cluster node is not available for this operation

Dieses Problem wird durch einen oder mehrere nicht initialisierte Datenträger an mindestens einem Clusterknoten verursacht. Um das Problem zu beheben, initialisieren Sie alle Speichermedien mithilfe von „DiskMgmt.msc, DISKPART.EXE” oder des Initialize-Disk PowerShell-Cmdlets.

Wir arbeiten an einem Update, das dieses Problem dauerhaft behebt. Wenn Sie an einer Unterstützung interessiert sind und über einen Microsoft Premier Support-Vertrag verfügen, senden Sie eine E-Mail an SRFEED@microsoft.com, damit wir mit Ihnen an einer Backport-Unterstützung arbeiten können.

## <a name="gpt-error-when-attempting-to-create-a-new-sr-partnership"></a>GPT-Fehler beim Versuch, eine neue SR-Partnerschaft zu erstellen

Wenn eine neue SR-Partnership ausgeführt wird, schlägt diese mit folgender Nachricht fehl: 

    Disk layout type for volume \\?\Volume{GUID}\ is not a valid GPT style layout.
    New-SRPartnership : Unable to create replication group SRG01, detailed reason: Disk layout type for volume
    \\?\Volume{GUID}\ is not a valid GPT style layout.
    At line:1 char:1
    + New-SRPartnership -SourceComputerName nodesrc01 -SourceRGName SRG01 ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (MSFT_WvrAdminTasks:root/Microsoft/...T_WvrAdminTasks) [New-SRPartnership]
    , CimException
    + FullyQualifiedErrorId : Windows System Error 5078,New-SRPartnership

In der grafischen Benutzeroberfläche des Failovercluster-Managers ist keine Option zum Einrichten von Replikationen für das Laufwerk vorhanden.

Wenn „Test-SRTopology” ausgeführt wird, schlägt diese mit folgender Nachricht fehl: 

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

Dies wird durch die noch auf Windows Server2012 R2 (d.h. FL 8) festgelegte Cluster-Funktionsebene verursacht. Speicherreplikat sollte einen bestimmten Fehler zurückgeben, gibt jedoch stattdessen einen falschen Verweis auf die standardmäßige Zuordnung zurück.

Führen Sie Get-Cluster | fl * für jeden Knoten aus.

Wenn ClusterFunctionalLevel = 9 ist, muss die Windows2016 ClusterFunctionalLevel Version das Speicherreplikat auf diesem Knoten installieren.
Wenn ClusterFunctionalLevel nicht 9 ist, müssen die ClusterFunctionalLevel aktualisiert werden, um das Speicherreplikat auf diesen Knoten zu implementieren.

Um das Problem zu beheben, stufen Sie die Funktionsebene der Cluster durch Ausführen des PowerShell-Cmdlets: https://technet.microsoft.com/itpro/powershell/windows/failoverclusters/update-clusterfunctionallevel herauf

## <a name="small-unknown-partition-listed-in-diskmgmt-for-each-replicated-volume"></a>Kleine unbekannte Partition in DISKMGMT für jedes replizierte Volume aufgeführt

Beim Ausführen des Snap-Ins „Datenträgerverwaltung“ (DISKMGMT.MSC) bemerken Sie, dass mindestens ein Volume ohne Bezeichnung oder Laufwerkbuchstabe und mit einer Größe von 1MB aufgeführt ist. Unter Umständen können Sie das unbekannte Volume löschen, oder Sie erhalten Folgendes:

    "An Unexpected Error has Occurred"  

Dieses Verhalten ist entwurfsbedingt. Dies ist kein Volume, sondern eine Partition. Das Speicherreplikat erstellt eine Partition mit 512KB als Datenbankslot für Replikationsvorgänge (das Legacytool „DiskMgmt.msc“ rundet auf den nächsten MB-Wert auf). Die Nutzung einer Partition für jedes replizierte Volume ist normal und wünschenswert. Wenn sie nicht mehr verwendet wird, können Sie diese Partition mit 512KB löschen. Sie können keine Partitionen löschen, die noch verwendet werden. Die Partition vergrößert oder verkleinert sich nicht. Beim Neuerstellen einer Replikation empfehlen wir Ihnen, die Partition beizubehalten, da nicht verwendete Partitionen vom Speicherreplikat beansprucht werden.

Verwenden Sie zum Anzeigen der Details das DISKPART-Tool oder das Get-Partition-Cmdlet. Diese Partitionen müssen den GPT-Typ `558d43c5-a1ac-43c0-aac8-d1472b2923d1` aufweisen. 

## <a name="see-also"></a>Weitere Informationen  
- [Speicherreplikat](storage-replica-overview.md)  
- [Replikation eines Stretched Clusters mithilfe von freigegebenem Speicher](stretch-cluster-replication-using-shared-storage.md)  
- [Server-zu-Server-Speicherreplikation](server-to-server-storage-replication.md)  
- [Cluster-zu-Cluster-Speicherreplikation](cluster-to-cluster-storage-replication.md)  
- [Speicherreplikate: Häufig gestellte Fragen](storage-replica-frequently-asked-questions.md)  
- [Speicherplätze DAS](../storage-spaces/storage-spaces-direct-overview.md)  
