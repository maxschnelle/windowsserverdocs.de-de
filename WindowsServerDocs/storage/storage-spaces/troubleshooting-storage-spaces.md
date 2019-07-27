---
title: Direkte Speicherplätze Problembehandlung
description: Erfahren Sie, wie Sie Probleme bei der direkte Speicherplätze Bereitstellung behandeln.
keywords: Speicherplätze
ms.prod: windows-server-threshold
ms.author: ''
ms.technology: storage-spaces
ms.topic: article
author: kaushika-msft
ms.date: 10/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7cc5709723b300f46ce108b36501e7ace272cd45
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544567"
---
# <a name="troubleshoot-storage-spaces-direct"></a>Problembehandlung direkte Speicherplätze

> Gilt für: Windows Server 2019, Windows Server 2016

Verwenden Sie die folgenden Informationen, um Probleme bei der direkte Speicherplätze Bereitstellung zu beheben.

Beginnen Sie im Allgemeinen mit den folgenden Schritten:

1. Vergewissern Sie sich, dass das Make/Model von SSD für Windows Server 2016 und Windows Server 2019 mithilfe des Windows Server-Katalogs zertifiziert ist. Bestätigen Sie mit dem Hersteller, dass die Laufwerke für direkte Speicherplätze unterstützt werden.
2. Überprüfen Sie den Speicher auf fehlerhafte Laufwerke. Verwenden Sie die Speicherverwaltungssoftware, um den Status der Laufwerke zu überprüfen. Wenn eines der Laufwerke fehlerhaft ist, arbeiten Sie mit dem Hersteller zusammen. 
3. Aktualisieren Sie den Speicher, und aktualisieren Sie die Firmware bei Bedarf
   Stellen Sie sicher, dass die neuesten Windows-Updates auf allen Knoten installiert sind. Sie erhalten die neuesten Updates für Windows Server 2016 aus dem [Windows 10-und Windows Server 2016 Update Verlauf](https://aka.ms/update2016) und für Windows Server 2019 aus dem [Windows 10-und Windows Server 2019 Update Verlauf](https://support.microsoft.com/help/4464619).
4. Aktualisieren Sie Treiber und Firmware von Netzwerkadaptern.
5. Führen Sie die Cluster Überprüfung aus, und überprüfen Sie den Abschnitt "Storage Space Direct", und stellen Sie sicher, dass die für den Cache verwendeten Laufwerke ordnungsgemäß und ohne Fehler

Wenn weiterhin Probleme auftreten, überprüfen Sie die unten aufgeführten Szenarien.

## <a name="virtual-disk-resources-are-in-no-redundancy-state"></a>Virtuelle Datenträger Ressourcen weisen keinen Redundanz Status auf
Die Knoten eines direkte Speicherplätze Systems werden aufgrund eines Absturzes oder eines Stromausfalls unerwartet neu gestartet. Eine oder mehrere der virtuellen Datenträger werden möglicherweise nicht online geschaltet, und Sie sehen die Beschreibung "nicht genügend Redundanz Informationen".

|FriendlyName|ResiliencySettingName| OperationalStatus| HealthStatus| IsManualAttach|Größe| PSComputerName|
|------------|---------------------| -----------------| ------------| --------------|-----| --------------|
|Disk4| Spiegelung| OK|  Fehlerfrei| True|  10 TB|  Knoten-01....|
|Disk3         |Spiegelung                 |OK                          |Fehlerfrei       |True            |10 TB | Knoten-01....|
|Disk2         |Spiegelung                 |Keine Redundanz               |Unhealthy     |True            |10 TB | Knoten-01....|
|Disk1         |Spiegelung                 |{Keine Redundanz, INService}  |Unhealthy     |True            |10 TB | Knoten-01....| 

Außerdem werden nach dem Versuch, den virtuellen Datenträger online zu schalten, die folgenden Informationen im Cluster Protokoll (diskherstellungsaction) protokolliert.  

```
[Verbose] 00002904.00001040::YYYY/MM/DD-12:03:44.891 INFO [RES] Physical Disk <DiskName>: OnlineThread: SuGetSpace returned 0.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 WARN [RES] Physical Disk < DiskName>: Underlying virtual disk is in 'no redundancy' state; its volume(s) may fail to mount.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 ERR [RES] Physical Disk <DiskName>: Failing online due to virtual disk in 'no redundancy' state. If you would like to attempt to online the disk anyway, first set this resource's private property 'DiskRecoveryAction' to 1. We will try to bring the disk online for recovery, but even if successful, its volume(s) or CSV may be unavailable. 
``` 

Der **Betriebs Status "keine Redundanz** " kann auftreten, wenn ein Datenträger fehlgeschlagen ist oder wenn das System nicht auf die Daten auf dem virtuellen Datenträger zugreifen kann. Dieses Problem kann auftreten, wenn ein Neustart auf einem Knoten während der Wartung auf den Knoten erfolgt.

Um dieses Problem zu beheben, führen Sie die folgenden Schritte aus:

1. Entfernen Sie die betroffenen virtuellen Datenträger aus dem CSV. Dadurch werden Sie in der Gruppe "verfügbarer Speicher" im Cluster abgelegt und als ResourceType "physischer Datenträger" angezeigt.

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. Führen Sie auf dem Knoten, der Besitzer der verfügbaren Speicher Gruppe ist, den folgenden Befehl auf jedem Datenträger aus, der sich in einem nicht Redundanz Zustand befindet. Zum Identifizieren des Knotens, auf dem sich die Gruppe "verfügbarer Speicher" befindet, können Sie den folgenden Befehl ausführen.

   ```powershell
   Get-ClusterGroup
   ```
3. Legen Sie die Aktion "Datenträger Wiederherstellung" fest, und starten Sie dann die Datenträger.
   ```powershell
   Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 1
   Start-ClusterResource -Name "VdiskName"
   ```
4. Eine Reparatur sollte automatisch gestartet werden. Warten Sie, bis die Reparatur abgeschlossen ist. Möglicherweise wechselt Sie in einen angehaltenen Zustand und startet erneut. So überwachen Sie den Fortschritt: 
    - Führen Sie **Get-storagejob** aus, um den Status der Reparatur zu überwachen und zu sehen, wann Sie abgeschlossen ist.
    - Führen **Sie "Get-virtualdisk** " aus, und vergewissern Sie sich, dass der Speicherplatz den Integritäts Status "
5. Nachdem die Reparatur abgeschlossen und die virtuellen Datenträger fehlerfrei sind, ändern Sie die Parameter der virtuellen Festplatte zurück.

   ```powershell
    Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 0
   ```
6. Schalten Sie die Datenträger offline und dann erneut Online, damit die diskherstellenaction wirksam wird:

   ```powershell
   Stop-ClusterResource "VdiskName"
   Start-ClusterResource "VdiskName"
   ``` 
7. Fügen Sie die betroffenen virtuellen Datenträger wieder zum CSV hinzu.

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```

**Diskherstellungsaction** ist ein Überschreibungs Schalter, der das Anfügen des Speicherplatzes im Lese-/Schreibmodus ohne Überprüfungen ermöglicht. Die-Eigenschaft ermöglicht es Ihnen, Diagnosemöglichkeiten zu bieten, warum ein Volume nicht online geschaltet wird. Das ähnelt dem Wartungsmodus, aber Sie können ihn für eine Ressource in einem fehlerhaften Zustand aufrufen. Außerdem können Sie auf die Daten zugreifen. Dies kann in Situationen wie "keine Redundanz" hilfreich sein, in denen Sie Zugriff auf alle Daten erhalten, die Sie kopieren können. Die diskherstellyaction-Eigenschaft wurde am 22. Februar 2018, Update, KB 4077525 hinzugefügt.


## <a name="detached-status-in-a-cluster"></a>Getrennter Status in einem Cluster 

Wenn Sie das **Get-virtualdisk-** Cmdlet ausführen, wird der OperationalStatus für mindestens einen direkte Speicherplätze virtuellen Datenträger getrennt. Der Integritäts Status, der vom Cmdlet " **Get-PhysicalDisk** " gemeldet wird, weist jedoch darauf hin, dass sich alle physischen Datenträger in einem fehlerfreien Zustand befinden.

Im folgenden finden Sie ein Beispiel für die Ausgabe des Cmdlets **Get-virtualdisk** .

|FriendlyName|  ResiliencySettingName|  OperationalStatus|   HealthStatus|  IsManualAttach|  Größe|   PSComputerName|
|-|-|-|-|-|-|-|
|Disk4|         Spiegelung|                 OK|                  Fehlerfrei|       True|            10 TB|  Knoten-01....|
|Disk3|         Spiegelung|                 OK|                  Fehlerfrei|       True|            10 TB|  Knoten-01....|
|Disk2|         Spiegelung|                 „Getrennt“|            Unbekannt|       True|            10 TB|  Knoten-01....|
|Disk1|         Spiegelung|                 „Getrennt“|            Unbekannt|       True|            10 TB|  Knoten-01....| 


Außerdem können die folgenden Ereignisse auf den Knoten protokolliert werden:

```
Log Name: Microsoft-Windows-StorageSpaces-Driver/Operational
Source: Microsoft-Windows-StorageSpaces-Driver 
Event ID: 311 
Level: Error
User: SYSTEM 
Computer: Node#.contoso.local 
Description: Virtual disk {GUID} requires a data integrity scan.  

Data on the disk is out-of-sync and a data integrity scan is required. 

To start the scan, run the following command:   
Get-ScheduledTask -TaskName "Data Integrity Scan for Crash Recovery" | Start-ScheduledTask                

Once you have resolved the condition listed above, you can online the disk by using the following commands in PowerShell:   

Get-VirtualDisk | ?{ $_.ObjectId -Match "{GUID}" } | Get-Disk | Set-Disk -IsReadOnly $false 
Get-VirtualDisk | ?{ $_.ObjectId -Match "{GUID}" } | Get-Disk | Set-Disk -IsOffline  $false
------------------------------------------------------------

Log Name: System
Source: Microsoft-Windows-ReFS 
Event ID: 134
Level: Error 
User: SYSTEM
Computer: Node#.contoso.local 
Description: The file system was unable to write metadata to the media backing volume <VolumeId>. A write failed with status "A device which does not exist was specified." ReFS will take the volume offline. It may be mounted again automatically.
------------------------------------------------------------
Log Name: Microsoft-Windows-ReFS/Operational
Source: Microsoft-Windows-ReFS 
Event ID: 5 
Level: Error 
User: SYSTEM 
Computer: Node#.contoso.local 
Description: ReFS failed to mount the volume. 
Context: 0xffffbb89f53f4180 
Error: A device which does not exist was specified.
Volume GUID:{00000000-0000-0000-0000-000000000000} 
DeviceName: 
Volume Name:
``` 

Der **getrennte Betriebs Status** kann auftreten, wenn das DRT-Protokoll (Dirty Region Tracking) voll ist. Speicherplätze verwenden die Änderungs Bereichs Überwachung (Dirty Region Tracking, DRT) für gespiegelte Speicherplätze, um sicherzustellen, dass bei einem Stromausfall alle in-Flight-Aktualisierungen der Metadaten protokolliert werden, um sicherzustellen, dass der Speicherplatz Vorgänge wiederholen oder rückgängig machen kann, um den Speicherplatz wieder in einen flexiblen und der konsistente Zustand, wenn die Stromversorgung wieder hergestellt wird und das System wieder hergestellt wird. Wenn das DRT-Protokoll voll ist, kann der virtuelle Datenträger erst online geschaltet werden, wenn die DRT-Metadaten synchronisiert und geleert wurden. Dieser Vorgang erfordert das Ausführen einer vollständigen Überprüfung, die mehrere Stunden in Anspruch nehmen kann.

Um dieses Problem zu beheben, führen Sie die folgenden Schritte aus:
1. Entfernen Sie die betroffenen virtuellen Datenträger aus dem CSV.

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. Führen Sie die folgenden Befehle auf allen Datenträgern aus, die nicht online geschaltet werden. 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 7
   Start-ClusterResource -Name "VdiskName"
   ``` 
3. Führen Sie den folgenden Befehl auf jedem Knoten aus, in dem das getrennte Volume online ist. 

   ```powershell
   Get-ScheduledTask -TaskName "Data Integrity Scan for Crash Recovery" | Start-ScheduledTask 
   ```
   Diese Aufgabe sollte auf allen Knoten initiiert werden, auf denen das getrennte Volume online ist. Eine Reparatur sollte automatisch gestartet werden. Warten Sie, bis die Reparatur abgeschlossen ist. Möglicherweise wechselt Sie in einen angehaltenen Zustand und startet erneut. So überwachen Sie den Fortschritt: 
   - Führen Sie **Get-storagejob** aus, um den Status der Reparatur zu überwachen und zu sehen, wann Sie abgeschlossen ist.
   - Führen **Sie Get-virtualdisk** aus, und vergewissern Sie sich, dass der Speicherplatz den Integritäts Status fehlerfrei
     - "Daten Integritäts Überprüfung für die Wiederherstellung von Abstürzen" ist ein Task, der nicht als Speicher Auftrag angezeigt wird und keine Statusanzeige vorliegt. Wenn die Aufgabe als wird ausgeführt angezeigt wird, wird Sie ausgeführt. Wenn er abgeschlossen ist, wird er als abgeschlossen angezeigt.

       Mit dem folgenden Cmdlet können Sie außerdem den Status eines Tasks zum Ausführen eines Zeitplans anzeigen: 
       ```powershell
       Get-ScheduledTask | ? State -eq running
       ``` 
4. Sobald die Daten Integritäts Überprüfung für die Wiederherstellung von Abstürzen abgeschlossen ist, die Reparatur abgeschlossen ist und die virtuellen Datenträger fehlerfrei sind, ändern Sie die Parameter der virtuellen Festplatten. 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 0 
   ```

5. Schalten Sie die Datenträger offline und dann erneut Online, damit die diskherstellenaction wirksam wird:

   ```powershell
   Stop-ClusterResource "VdiskName"
   Start-ClusterResource "VdiskName"
   ``` 

6. Fügen Sie die betroffenen virtuellen Datenträger wieder zum CSV hinzu.    

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```  
   Der **diskrunchkdsk-Wert 7** wird verwendet, um das Speicherplatz Volume anzufügen und die Partition im schreibgeschützten Modus zu haben. Dies ermöglicht es Ihnen, sich selbst zu erkennen und selbst zu korrigieren, indem Sie eine Reparatur auslösen. Die Reparatur wird automatisch nach der Bereitstellung ausgeführt. Außerdem können Sie auf die Daten zugreifen. Dies kann hilfreich sein, um Zugriff auf alle Daten zu erhalten, die Sie kopieren können. Bei einigen Fehlerzuständen (z. b. einem vollständigen DRT-Protokoll) müssen Sie die Daten Integritäts Überprüfung für den geplanten Task "Absturz Wiederherstellung" ausführen.

Die **Daten Integritäts Überprüfung für den Task "Absturz Wiederherstellung** " wird zum Synchronisieren und Löschen eines DRT (Full Dirty Region Tracking)-Protokolls verwendet. Diese Aufgabe kann mehrere Stunden in Anspruch nehmen. "Daten Integritäts Überprüfung für die Wiederherstellung von Abstürzen" ist ein Task, der nicht als Speicher Auftrag angezeigt wird und keine Statusanzeige vorliegt. Wenn die Aufgabe als wird ausgeführt angezeigt wird, wird Sie ausgeführt. Wenn er abgeschlossen ist, wird er als abgeschlossen angezeigt. Wenn Sie die Aufgabe abbrechen oder einen Knoten neu starten, während diese Aufgabe ausgeführt wird, muss der Task von Anfang an gestartet werden.

Weitere Informationen finden Sie unter [Problembehandlung direkte Speicherplätze Integritäts-und Betriebs](storage-spaces-states.md)Status.

## <a name="event-5120-with-statusiotimeout-c00000b5"></a>Ereignis 5120 mit STATUS_IO_TIMEOUT c00000b5 

> [!Important]
> **Für Windows Server 2016:** Um die Wahrscheinlichkeit zu verringern, dass diese Symptome beim Anwenden des Updates behoben werden, empfiehlt es sich, die unten stehende Prozedur für den Speicher Wartungsmodus zu verwenden, um den [18. Oktober 2018, das kumulative Update für Windows Server 2016](https://support.microsoft.com/help/4462928) oder eine höhere Version zu installieren. Wenn auf den Knoten derzeit ein kumulatives Update für Windows Server 2016 installiert wurde, das vom [8. Mai 2018](https://support.microsoft.com/help/4103723) bis zum [9. Oktober 2018](https://support.microsoft.com/help/KB4462917)veröffentlicht wurde.

Sie können das Ereignis 5120 mit STATUS_IO_TIMEOUT c00000b5 erhalten, nachdem Sie einen Knoten unter Windows Server 2016 mit dem kumulativen Update neu gestartet haben, das vom [8. Mai 2018 KB 4103723](https://support.microsoft.com/help/4103723) bis [2018 9](https://support.microsoft.com/help/4462917) .

Wenn Sie den Knoten neu starten, wird das Ereignis 5120 im System Ereignisprotokoll protokolliert. es enthält einen der folgenden Fehlercodes:

```
Event Source: Microsoft-Windows-FailoverClustering
Event ID: 5120
Description:    Cluster Shared Volume 'CSVName' ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_IO_TIMEOUT(c00000b5)'. All I/O will temporarily be queued until a path to the volume is reestablished. 

Cluster Shared Volume ‘CSVName’ ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_CONNECTION_DISCONNECTED(c000020c)'. All I/O will temporarily be queued until a path to the volume is reestablished.    
```

Wenn ein Ereignis 5120 protokolliert wird, wird ein livedump generiert, um Debuginformationen zu sammeln, die möglicherweise zusätzliche Symptome verursachen oder einen Leistungs Effekt haben. Durch das Erstellen des liveabbilds wird eine kurze Pause erstellt, um das Erstellen einer Momentaufnahme des Speichers zum Schreiben der Dumpdatei zu ermöglichen Systeme mit sehr viel Arbeitsspeicher und hoher Belastung können dazu führen, dass Knoten die Cluster Mitgliedschaft verwerfen und auch das folgende Ereignis 1135 protokolliert werden.

```
Event source: Microsoft-Windows-FailoverClustering
Event ID: 1135  
Description: Cluster node 'NODENAME'was removed from the active failover cluster membership. The Cluster service on this node may have stopped. This could also be due to the node having lost communication with other active nodes in the failover cluster. Run the Validate a Configuration wizard to check your network configuration. If the condition persists, check for hardware or software errors related to the network adapters on this node. Also check for failures in any other network components to which the node is connected such as hubs, switches, or bridges.
```

Eine Änderung, die am 8. Mai 2018 in Windows Server 2016 eingeführt wurde. Hierbei handelt es sich um ein kumulatives Update zum Hinzufügen von SMB-robusten Handles für die direkte Speicherplätze Cluster übergreifende SMB-Netzwerksitzungen. Dies wurde erreicht, um die Resilienz bei vorübergehenden Netzwerkfehlern zu verbessern und zu verbessern, wie ROCE die Netzwerk Überlastung behandelt. Diese Verbesserungen haben auch versehentlich größere Timeout Zeiten erreicht, wenn SMB-Verbindungen versuchen, erneut eine Verbindung herzustellen, und auf einen Timeout wartet, wenn ein Knoten neu gestartet wird. Diese Probleme können sich auf ein System auswirken, das ausgelastet ist. Bei ungeplanten Ausfallzeiten wurden e/a-Pausen von bis zu 60 Sekunden ebenfalls beobachtet, während das System auf Verbindungen mit Timeout wartet. Um dieses Problem zu beheben, installieren Sie den [18. Oktober 2018, das kumulative Update für Windows Server 2016](https://support.microsoft.com/help/4462928) oder eine höhere Version.

*Hinweis* Dieses Update richtet die CSV-Timeouts mit Timeout Werten für die SMB-Verbindung aus, um das Problem zu beheben. Die Änderungen zum Deaktivieren der im Abschnitt "Problem Umgehung" erwähnten Live Dump-Generierung werden nicht implementiert.

### <a name="shutdown-process-flow"></a>Prozessablauf für das Herunterfahren:

1. Führen Sie das Get-virtualdisk-Cmdlet aus, und vergewissern Sie sich, dass der Wert healthstatus fehlerfrei ist.
2. Führen Sie das folgende Cmdlet aus, um den Knoten zu entfernen:

   ```powershell
   Suspend-ClusterNode -Drain
   ```
3. Fügen Sie die Datenträger auf diesem Knoten im Speicher Wartungsmodus ein, indem Sie das folgende Cmdlet ausführen: 

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Enable-StorageMaintenanceMode
   ```
4. Führen Sie das **Get-PhysicalDisk-** Cmdlet aus, und vergewissern Sie sich, dass sich der Wert OperationalStatus im Wartungsmodus befindet.
5. Führen Sie das Cmdlet **Restart-Computer** aus, um den Knoten neu zu starten.
6. Nachdem der Knoten neu gestartet wurde, entfernen Sie die Datenträger auf diesem Knoten aus dem Speicher Wartungsmodus, indem Sie das folgende Cmdlet ausführen:

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Disable-StorageMaintenanceMode
   ```
7. Setzen Sie den Knoten fort, indem Sie das folgende Cmdlet ausführen:

   ```powershell
   Resume-ClusterNode
   ```
8. Überprüfen Sie den Status der Neusynchronisierungs Aufträge, indem Sie das folgende Cmdlet ausführen:

   ```powershell
   Get-StorageJob
   ```

### <a name="disabling-live-dumps"></a>Deaktivieren von livedumps
Um die Auswirkungen der Live dumpgenerierung auf Systeme zu mindern, die viel Arbeitsspeicher aufweisen und unter Belastung auftreten, können Sie die Live-dumpgenerierung zusätzlich deaktivieren. Unten sind drei Optionen angegeben.

>[!Caution]
>Dieses Verfahren kann die Erfassung von Diagnoseinformationen verhindern, die Microsoft-Support möglicherweise zur Untersuchung dieses Problems benötigt. Möglicherweise müssen Sie von einem Support-Agent aufgefordert werden, die Live-dumpgenerierung auf der Grundlage spezifischer Problem behandlungsszenarien erneut zu aktivieren.

Es gibt zwei Methoden zum Deaktivieren von livedumps, wie unten beschrieben.

#### <a name="method-1-recommended-in-this-scenario"></a>Methode 1 (in diesem Szenario empfohlen)
Führen Sie die folgenden Schritte aus, um alle Abbilder vollständig zu deaktivieren, einschließlich des systemweiten Live Abbilder:

1. Erstellen Sie den folgenden Registrierungsschlüssel: Hklm\system\currentcontrolset\control\crashcontrol\forcedumpsdeaktiviert
2. Erstellen Sie unter dem neuen **forcedumpsdeaktiviert** -Schlüssel eine REG_DWORD-Eigenschaft als "guardedhost", und legen Sie Ihren Wert auf "0x10000000" fest.
3. Wenden Sie den neuen Registrierungsschlüssel auf jeden Cluster Knoten an.

>[!NOTE]
>Sie müssen den Computer neu starten, damit die nRegistrierungseinstellung mit-Änderung wirksam wird.

Nachdem dieser Registrierungsschlüssel festgelegt wurde, schlägt die Erstellung des Live dumpbacks fehl und generiert den Fehler "STATUS_NOT_SUPPORTED".

#### <a name="method-2"></a>Methode 2
Standardmäßig lässt Windows-Fehlerberichterstattung nur einen livedump pro Berichtstyp pro Berichtstyp und 7 Tagen zu und nur 1 livedump pro Computer und 5 Tagen. Sie können dies ändern, indem Sie die folgenden Registrierungsschlüssel so festlegen, dass nur ein livedump auf dem Computer unbegrenzt zugelassen wird.
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v SystemThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v ComponentThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```

*Hinweis* Sie müssen den Computer neu starten, damit die Änderung wirksam wird.

### <a name="method-3"></a>Methode 3
Führen Sie das folgende Cmdlet aus, um die Cluster Generierung von livedumps (z. b. Wenn ein Ereignis 5120 protokolliert wird) zu deaktivieren:

```powershell
(Get-Cluster).DumpPolicy = ((Get-Cluster).DumpPolicy -band 0xFFFFFFFFFFFFFFFE)
```
Dieses Cmdlet wirkt sich sofort auf alle Cluster Knoten aus, ohne dass ein Computer neu gestartet wird.

## <a name="slow-io-performance"></a>Langsame EA-Leistung

Wenn eine langsame e/a-Leistung angezeigt wird, überprüfen Sie, ob der Cache in ihrer direkte Speicherplätze Konfiguration aktiviert ist. 

Es gibt zwei Möglichkeiten, um Folgendes zu überprüfen: 


1. Verwenden des Cluster Protokolls. Öffnen Sie das Cluster Protokoll im Text-Editor Ihrer Wahl, und suchen Sie nach "[= = = SBL Disks = = =]". Dabei handelt es sich um eine Liste der Datenträger auf dem Knoten, auf dem das Protokoll generiert wurde. 

     Beispiel für Cache aktivierte Datenträger: Beachten Sie, dass der Status "cachediskstateinitializedandbound" lautet und dass hier eine GUID vorhanden ist. 

   ```
   [=== SBL Disks ===]
    {26e2e40f-a243-1196-49e3-8522f987df76},3,false,true,1,48,{1ff348f1-d10d-7a1a-d781-4734f4440481},CacheDiskStateInitializedAndBound,1,8087,54,false,false,HGST    ,HUH721010AL4200 ,        7PG3N2ER,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    Cache nicht aktiviert: Hier sehen Sie, dass keine GUID vorhanden ist und der Status "cachediskstatonhybrid" lautet. 
    ```
   [=== SBL Disks ===]
    {426f7f04-e975-fc9d-28fd-72a32f811b7d},12,false,true,1,24,{00000000-0000-0000-0000-000000000000},CacheDiskStateNonHybrid,0,0,0,false,false,HGST    ,HUH721010AL4200 ,        7PGXXG6C,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    Cache nicht aktiviert: Wenn alle Datenträger denselben Typ haben, ist standardmäßig nicht aktiviert. Hier sehen Sie, dass keine GUID vorhanden ist und der Status cachediskstateineligibledatapartition ist. 
    ```
    {d543f90c-798b-d2fe-7f0a-cb226c77eeed},10,false,false,1,20,{00000000-0000-0000-0000-000000000000},CacheDiskStateIneligibleDataPartition,0,0,0,false,false,NVMe    ,INTEL SSDPE7KX02,  PHLF7330004V2P0LGN,0170,{79b4d631-976f-4c94-a783-df950389fd38},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0], 
    ```  
2. Verwenden von "Get-PhysicalDisk. xml" aus sddcdiagnosticinfo
    1. Öffnen Sie die XML-Datei mit "$d = Import-CliXML getphysicaldisk. xml".
    2. Führen Sie "ipmo-Speicher" aus.
    3. Führen Sie "$d" aus. Beachten Sie, dass die Verwendung automatisch ausgewählt wird, nicht im Journal, Sie sehen eine Ausgabe wie die folgende: 

   |FriendlyName|  SerialNumber| MediaType| CanPool| OperationalStatus| HealthStatus| Verwendung| Größe|
   |-----------|------------|---------| -------| -----------------| ------------| -----| ----|
   |Nvme Intel SSDPE7KX02| PHLF733000372P0LGN| SSD| False|   OK|                Fehlerfrei|      Automatische Auswahl von 1,82 TB|
   |Nvme Intel SSDPE7KX02 |PHLF7504008J2P0LGN| SSD|  False|    OK|                Fehlerfrei| Automatisch auswählen| 1,82 TB|
   |Nvme Intel SSDPE7KX02| PHLF7504005F2P0LGN| SSD|  False|  OK|                Fehlerfrei| Automatisch auswählen| 1,82 TB|
   |Nvme Intel SSDPE7KX02 |PHLF7504002A2P0LGN| SSD| False| OK|    Fehlerfrei| Automatisch auswählen| 1,82 TB|
   |Nvme Intel SSDPE7KX02| PHLF7504004T2P0LGN |SSD| False|OK|       Fehlerfrei| Automatisch auswählen| 1,82 TB|
   |Nvme Intel SSDPE7KX02 |PHLF7504002E2P0LGN| SSD| False| OK|      Fehlerfrei| Automatisch auswählen| 1,82 TB|
   |Nvme Intel SSDPE7KX02 |PHLF7330002Z2P0LGN| SSD| False| OK|      Fehlerfrei|Automatisch auswählen| 1,82 TB|
   |Nvme Intel SSDPE7KX02 |PHLF733000272P0LGN |SSD| False| OK|  Fehlerfrei| Automatisch auswählen| 1,82 TB|
   |Nvme Intel SSDPE7KX02 |PHLF7330001J2P0LGN |SSD| False| OK| Fehlerfrei| Automatisch auswählen| 1,82 TB|
   |Nvme Intel SSDPE7KX02| PHLF733000302P0LGN |SSD| False| OK|Fehlerfrei| Automatisch auswählen| 1,82 TB|
   |Nvme Intel SSDPE7KX02| PHLF7330004D2P0LGN |SSD| False| OK| Fehlerfrei| Automatisch auswählen |1,82 TB|

## <a name="how-to-destroy-an-existing-cluster-so-you-can-use-the-same-disks-again"></a>So zerstören Sie einen vorhandenen Cluster, sodass Sie die gleichen Datenträger wieder verwenden können

Wenn Sie in einem direkte Speicherplätze Cluster direkte Speicherplätze deaktivieren und den in [Clean Drives](deploy-storage-spaces-direct.md#step-31-clean-drives)beschriebenen Bereinigungs Vorgang verwenden, verbleibt der Cluster Speicherpool weiterhin in einem Offline Status, und die Integritätsdienst wird aus dem Cluster entfernt.

Der nächste Schritt besteht darin, den Phantom Speicherpool zu entfernen: 
   ```powershell
   Get-ClusterResource -Name "Cluster Pool 1" | Remove-ClusterResource
   ```

Wenn Sie nun **Get-PhysicalDisk** auf einem der Knoten ausführen, werden alle Datenträger im Pool angezeigt. Beispielsweise können Sie in einem Lab mit einem 4-Knoten-Cluster mit vier SAS-Datenträgern jeweils 100 GB für jeden Knoten darstellen. In diesem Fall, wenn Sie " **Get-PhysicalDisk" deaktiviert haben und "Get-PhysicalDisk**" ausführen, sollten Sie 4 Datenträger mit Ausnahme des lokalen Betriebssystem Datenträgers melden, wenn Sie "Get-PhysicalDisk" ausführen. Stattdessen wird stattdessen "16" gemeldet. Dies ist für alle Knoten im Cluster identisch. Wenn Sie einen **Get-Disk-** Befehl ausführen, werden die lokal angeschlossenen Datenträger als 0, 1, 2 usw. angezeigt, wie in der folgenden Beispielausgabe gezeigt:

|Number| Angezeigter Name| Seriennummer|HealthStatus|OperationalStatus|Gesamtgröße| Partitions Stil|
|-|-|-|-|-|-|-|-|
|0|MSFT Virtu...  ||Fehlerfrei | Online|  127 GB| GPT|
||MSFT Virtu... ||Fehlerfrei| Offline| 100 GB| STOFFES|
||MSFT Virtu... ||Fehlerfrei| Offline| 100 GB| STOFFES|
||MSFT Virtu... ||Fehlerfrei| Offline| 100 GB| STOFFES|
||MSFT Virtu... ||Fehlerfrei| Offline| 100 GB| STOFFES|
|1|MSFT Virtu...||Fehlerfrei| Offline| 100 GB| STOFFES|
||MSFT Virtu... ||Fehlerfrei| Offline| 100 GB| STOFFES|
|2|MSFT Virtu...||Fehlerfrei| Offline| 100 GB| STOFFES|
||MSFT Virtu... ||Fehlerfrei| Offline| 100 GB| STOFFES|
||MSFT Virtu... ||Fehlerfrei| Offline| 100 GB| STOFFES|
||MSFT Virtu... ||Fehlerfrei| Offline| 100 GB| STOFFES|
||MSFT Virtu... ||Fehlerfrei| Offline| 100 GB| STOFFES|
|4|MSFT Virtu...||Fehlerfrei| Offline| 100 GB| STOFFES|
|3|MSFT Virtu...||Fehlerfrei| Offline| 100 GB| STOFFES|
||MSFT Virtu... ||Fehlerfrei| Offline| 100 GB| STOFFES|
||MSFT Virtu... ||Fehlerfrei| Offline| 100 GB| STOFFES|
||MSFT Virtu... ||Fehlerfrei| Offline| 100 GB| STOFFES|


## <a name="error-message-about-unsupported-media-type-when-you-create-an-storage-spaces-direct-cluster-using-enable-clusters2d"></a>Fehlermeldung zu "nicht unterstützter Medientyp" beim Erstellen eines direkte Speicherplätze Clusters mithilfe von "Enable-ClusterS2D"  

Beim Ausführen des Cmdlets **enable-ClusterS2D** werden möglicherweise ähnliche Fehler angezeigt:

![Szenario 6-Fehlermeldung](media/troubleshooting/scenario-error-message.png)

Stellen Sie sicher, dass der HBA-Adapter im HBA-Modus konfiguriert ist, um dieses Problem zu beheben. Im RAID-Modus sollte kein HBA konfiguriert werden.  

## <a name="enable-clusterstoragespacesdirect-hangs-at-waiting-until-sbl-disks-are-surfaced-or-at-27"></a>"Enable-clusterstoragespacesdirect" reagiert bei "warten auf die Festplatte der SBL-Datenträger" oder bei 27%

Im Überprüfungsbericht werden die folgenden Informationen angezeigt:

    Disk <identifier> connected to node <nodename> returned a SCSI Port Association and the corresponding enclosure device could not be found. The hardware is not compatible with Storage Spaces Direct (S2D), contact the hardware vendor to verify support for SCSI Enclosure Services (SES). 


Das Problem liegt bei der HPE-SAS-Expander-Karte zwischen den Datenträgern und der HBA-Karte. Der SAS-Expander erstellt eine doppelte ID zwischen dem ersten Laufwerk, das mit dem Expander verbunden ist, und der Expander selbst.  Dies wurde in [HPE-SAS-Expander-Firmware aufgelöst: 4,02](https://support.hpe.com/hpsc/swd/public/detail?sp4ts.oid=7304566&swItemId=MTX_ef8d0bf4006542e194854eea6a&swEnvOid=4184#tab3).

## <a name="intel-ssd-dc-p4600-series-has-a-non-unique-nguid"></a>Intel SSD-DC P4600-Serie weist eine nicht eindeutige "nguid" auf.
Möglicherweise wird ein Problem auftreten, bei dem ein Gerät mit Intel SSD-DC P4600 eine ähnliche 16 Byte-nguid für mehrere Namespaces meldet, wie z. b. 0100000001000000e4d25c000014e214 oder 0100000001000000e4d25c0000eee214 im folgenden Beispiel.


|               UniqueId               | DeviceID | MediaType | BusType |               serialNumber               |      size      | canpool | FriendlyName | OperationalStatus |
|--------------------------------------|----------|-----------|---------|------------------------------------------|----------------|---------|--------------|-------------------|
|           5000 CCA251D12E30           |    0     |    HDD    |   SAS   |                 7PKR197G                 | 10000831348736 |  False  |     HGST     |  HUH721010AL4200  |
| EUI. 0100000001000000e4d25c000014e214 |    4     |    SSD    |  NVMe   | 0100_0000_0100_0000_E4D2_5C00_0014_E214. | 1600321314816  |  True   |    INTEL     |   SSDPE2KE016T7   |
| EUI. 0100000001000000e4d25c000014e214 |    5     |    SSD    |  NVMe   | 0100_0000_0100_0000_E4D2_5C00_0014_E214. | 1600321314816  |  True   |    INTEL     |   SSDPE2KE016T7   |
| EUI. 0100000001000000e4d25c0000eee214 |    6     |    SSD    |  NVMe   | 0100_0000_0100_0000_E4D2_5C00_00EE_E214. | 1600321314816  |  True   |    INTEL     |   SSDPE2KE016T7   |
| EUI. 0100000001000000e4d25c0000eee214 |    7     |    SSD    |  NVMe   | 0100_0000_0100_0000_E4D2_5C00_00EE_E214. | 1600321314816  |  True   |    INTEL     |   SSDPE2KE016T7   |

Aktualisieren Sie die Firmware auf den Intel-Laufwerken auf die neueste Version, um dieses Problem zu beheben.  Die Firmwareversion QDV101B1 von Mai 2018 ist bekannt, um dieses Problem zu beheben.

Die [Version vom Mai 2018 des Intel SSD Data Center-Tools](https://downloadmirror.intel.com/27778/eng/Intel_SSD_Data_Center_Tool_3_0_12_Release_Notes_330715-026.pdf) enthält ein Firmwareupdate, QDV101B1, für die P4600-Serie des Intel SSD-DC.


## <a name="physical-disk-healthy-and-operational-status-is-removing-from-pool"></a>Physischer Datenträger "fehlerfrei" und Betriebs Status "aus Pool entfernen" 

In einem Windows Server 2016 direkte Speicherplätze-Cluster kann der Integritäts Status für einen oder mehrere physische Datenträger als "fehlerfrei" angezeigt werden, während OperationalStatus "(aus Pool entfernen, OK)" lautet. 

Das "entfernen aus dem Pool" ist beabsichtigt, wenn " **Remove-PhysicalDisk** " aufgerufen wird, aber in "Health" gespeichert ist, um den Status beizubehalten und die Wiederherstellung zuzulassen, wenn der Entfernungs Vorgang Sie können den OperationalStatus mit einer der folgenden Methoden manuell in "fehlerfrei" ändern:

- Entfernen Sie den physischen Datenträger aus dem Pool, und fügen Sie ihn dann wieder hinzu.
- Führen Sie das [Skript Clear-PhysicalDiskHealthData. ps1](https://go.microsoft.com/fwlink/?linkid=2034205) aus, um die Absicht zu löschen. (Zum Herunterladen als verfügbar. TXT-Datei. Sie müssen Sie als speichern. PS1-Datei, bevor Sie Sie ausführen können.)

Im folgenden finden Sie einige Beispiele, die zeigen, wie das Skript ausgeführt wird:

- Verwenden Sie den **serialNumber** -Parameter, um den Datenträger anzugeben, der auf fehlerfrei festgelegt werden muss. Sie können die Seriennummer von **WMI MSFT_PhysicalDisk** oder **Get-PhysicalDisk**erhalten. (Für die unten stehende Seriennummer werden lediglich 0s verwendet.)

   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -SerialNumber 000000000000000 -Verbose -Force
    ```

- Verwenden Sie den **UniqueId** -Parameter, um den Datenträger anzugeben (wieder von **WMI MSFT_PhysicalDisk** oder **Get-PhysicalDisk**).

   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -UniqueId 00000000000000000 -Verbose -Force
   ```

## <a name="file-copy-is-slow"></a>Dateikopie ist langsam

Möglicherweise ist ein Problem mit dem Datei-Explorer aufgetreten, um eine große VHD auf den virtuellen Datenträger zu kopieren. der Kopiervorgang dauert länger als erwartet.

Das Verwenden des Datei-Explorers, Robocopy oder xcopy zum Kopieren einer großen VHD auf den virtuellen Datenträger ist keine empfohlene Methode für, da dies zu einer langsameren Leistungssteigerung führt. Der Kopiervorgang durchläuft nicht den direkte Speicherplätze Stapel, der sich unterhalb des Speicher Stapels befindet, und verhält sich stattdessen wie ein lokaler Kopiervorgang.

Wenn Sie die direkte Speicherplätze Leistung testen möchten, empfehlen wir die Verwendung von vmfleet und diskspd zum Laden und Belastungstest der Server, um eine Basislinie zu erhalten und die Erwartungen der direkte Speicherplätze Leistung festzulegen.

## <a name="expected-events-that-you-would-see-on-rest-of-the-nodes-during-the-reboot-of-a-node"></a>Erwartete Ereignisse, die während des Neustarts eines Knotens auf den restlichen Knoten angezeigt werden. 

Diese Ereignisse können sicher ignoriert werden: 

    Event ID 205: Windows lost communication with physical disk {XXXXXXXXXXXXXXXXXXXX }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

    Event ID 203: Windows lost communication with physical disk {xxxxxxxxxxxxxxxxxxxxxxxx }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

Wenn Sie Azure-VMS ausführen, können Sie dieses Ereignis ignorieren:

    Event ID 32: The driver detected that the device \Device\Harddisk5\DR5 has its write cache enabled. Data corruption may occur. 

## <a name="slow-performance-or-lost-communication-io-error-detached-or-no-redundancy-errors-for-deployments-that-use-intel-p3x00-nvme-devices"></a>Fehler bei der Leistung oder bei bereit Stellungen, bei denen Intel P3x00 nvme-Geräte verwendet werden, oder "verlorene Kommunikation", "e/a-Fehler", "getrennt" oder "keine Redundanz".

Wir haben ein kritisches Problem identifiziert, das sich auf einige direkte Speicherplätze Benutzer auswirkt, die Hardware auf der Grundlage der Intel P3x00-Familie von nvme-Geräten (nvme) mit Firmwareversionen vor dem Release 8 verwenden. 

>[!NOTE]
> Einzelne OEMs verfügen möglicherweise über Geräte, die auf der Intel P3x00-Familie von nvme-Geräten mit eindeutigen firmwareverzeichenfolgen basieren. Weitere Informationen zur neuesten Firmwareversion erhalten Sie von Ihrem OEM.

Wenn Sie in Ihrer Bereitstellung Hardware verwenden, die auf der Intel P3x00-Familie der nvme-Geräte basiert, wird empfohlen, dass Sie sofort die neueste verfügbare Firmware (mindestens Wartungs Release 8) anwenden. Dieser [Microsoft-Support Artikel](https://support.microsoft.com/help/4052341/slow-performance-or-lost-communication-io-error-detached-or-no-redunda) enthält weitere Informationen zu diesem Problem. 
