---
title: "\"Direkte Speicherplätze\", Problembehandlung"
description: Erfahren Sie, wie Sie Probleme bei Ihrem "direkte Speicherplätze"-Bereitstellung.
keywords: Speicherplätze
ms.prod: windows-server-threshold
ms.author: ''
ms.technology: storage-spaces
ms.topic: article
author: kaushika-msft
ms.date: 10/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: ecf3cb5703a90976dce15abbd0c9fdd1d4aa24ec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812631"
---
# <a name="troubleshoot-storage-spaces-direct"></a>Problembehandlung für Speicherplätze direkt

Verwenden Sie die folgende Informationen, um die "direkte Speicherplätze"-Bereitstellung zu beheben.

Starten Sie in der Regel die folgenden Schritte aus:

1. Vergewissern Sie sich, dass das Modell SSD für Windows Server 2016 mithilfe von Windows Server-Katalog zertifiziert ist. Vergewissern Sie sich beim Anbieter, dass die Laufwerke für "direkte Speicherplätze" unterstützt werden.
2. Überprüfen Sie den Speicher für alle fehlerhaften Laufwerke. Verwenden Sie Speicher-Management-Software zum Überprüfen des Status der Laufwerke an. Wenn die Laufwerke fehlerhaft, arbeiten Sie mit Ihrem Anbieter sind. 
3. Aktualisieren Sie den Speicher und Laufwerksfirmware bei Bedarf.
   Stellen Sie sicher, dass die neuesten Windows-Updates auf allen Knoten installiert sind. Sie erhalten die neuesten Updates für Windows Server 2016 von [ https://aka.ms/update2016 ](https://aka.ms/update2016).
4. Aktualisieren Sie Netzwerkadapter-Treiber und Firmware.
5. Ausführen der clustervalidierung, lesen Sie den Storage Space-Direct-Abschnitt, und stellen Sie sicher, die Laufwerke, die verwendet werden, für den Cache ordnungsgemäß gemeldet werden und keine Fehler.

Wenn weiterhin Probleme auftreten, überprüfen Sie die folgenden Szenarios.

## <a name="virtual-disk-resources-are-in-no-redundancy-state"></a>Virtuelle Festplattenressourcen befinden sich in Zustand keine Redundanz
Die Knoten eines "direkte Speicherplätze"-Systems, die unerwartet aufgrund eines Fehlers Absturz oder Stromausfall neu starten. Klicken Sie dann eine oder mehrere virtuelle Datenträger kann nicht online geschaltet, und finden Sie in der Beschreibung "nicht genügend Redundanzinformationen."
    
|FriendlyName|ResiliencySettingName| OperationalStatus| HealthStatus| IsManualAttach|Größe| PSComputerName|
|------------|---------------------| -----------------| ------------| --------------|-----| --------------|
|Disk4| Spiegelung| OK|  Fehlerfrei| True|  10 TB|  Node-01.conto...|
|Disk3         |Spiegelung                 |OK                          |Fehlerfrei       |True            |10 TB | Node-01.conto...|
|Disk2         |Spiegelung                 |Keine Redundanz               |Unhealthy     |True            |10 TB | Node-01.conto...|
|Disk1         |Spiegelung                 |{No Redundancy, InService}  |Unhealthy     |True            |10 TB | Node-01.conto...| 

Darüber hinaus wird nach einem Versuch, den virtuellen Datenträger online zu schalten, die folgende Informationen im Clusterprotokoll (DiskRecoveryAction) protokolliert.  

```
[Verbose] 00002904.00001040::YYYY/MM/DD-12:03:44.891 INFO [RES] Physical Disk <DiskName>: OnlineThread: SuGetSpace returned 0.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 WARN [RES] Physical Disk < DiskName>: Underlying virtual disk is in 'no redundancy' state; its volume(s) may fail to mount.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 ERR [RES] Physical Disk <DiskName>: Failing online due to virtual disk in 'no redundancy' state. If you would like to attempt to online the disk anyway, first set this resource's private property 'DiskRecoveryAction' to 1. We will try to bring the disk online for recovery, but even if successful, its volume(s) or CSV may be unavailable. 
``` 

Die **keine Redundanz-Betriebsstatus** kann auftreten, wenn ein Datenträger ausgefallen oder das System nicht auf Daten auf dem virtuellen Datenträger zugreifen kann. Dieses Problem kann auftreten, wenn ein Neustart auf einem Knoten, während der Wartung auf den Knoten auftritt.
    
Um dieses Problem zu beheben, gehen Sie folgendermaßen vor:

1. Entfernen Sie die betroffenen virtuellen Datenträger aus CSV-Datei. Platzieren Sie sie in der Gruppe "Verfügbarer Speicherplatz" im Cluster wird, und starten, als eine ResourceType der "Physikalischer Datenträger".

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. Führen Sie den folgenden Befehl auf jedem Datenträger, die in einem Zustand keine Redundanz ist, auf dem Knoten, der Besitzer die verfügbaren Speichergruppe ist. Um den Knoten zu identifizieren,, die Gruppe "Verfügbarer Speicherplatz darin" kann den folgenden Befehl ausführen.

   ```powershell
   Get-ClusterGroup
   ```
3. Legen Sie die Datenträger-Wiederherstellungsaktion an, und starten Sie den Datenträger.
   ```powershell
   Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 1
   Start-ClusterResource -Name "VdiskName"
   ```
4. Eine Reparatur sollte automatisch gestartet werden. Warten Sie, bis die Reparatur abgeschlossen. Es kann in den Standbymodus wechseln und erneut starten. Um den Fortschritt zu überwachen: 
    - Führen Sie **Get-StorageJob** zum Überwachen des Status der Reparatur und um festzustellen, wann sie abgeschlossen ist.
    - Führen Sie **Get-VirtualDisk** und stellen Sie sicher, dass der Speicherplatz einer HealthStatus der Integrität zurückgibt.
5. Sind nach der Reparatur abgeschlossen ist und die virtuellen Datenträger fehlerfrei, Änderung, die Parameter für die virtuellen Datenträger zu sichern.

   ```powershell
    Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 0
   ```
6. Führen Sie die Datenträger offline und anschließend wieder online ist, erneut aus, um die DiskRecoveryAction wirksam werden:

   ```powershell
   Stop-ClusterResource "VdiskName"
   Start-ClusterResource "VdiskName"
   ``` 
7. Fügen Sie die betroffenen virtuellen Datenträger wieder zum CSV hinzu.

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```

**DiskRecoveryAction** ist ein außer Kraft setzen-Schalter, die es ermöglicht, das Volume Speicherplatz im Lese-/ Schreibmodus ohne Überprüfungen anfügen. Die Eigenschaft können Sie Sie der Diagnose in warum ein Volume online geschaltet wird nicht. Es ist sehr ähnlich, in den Wartungsmodus wechseln, aber Sie können es aufrufen, für eine Ressource in einem fehlerhaften Zustand. Darüber hinaus können Sie die Daten zugegriffen wird, können hilfreich in Situationen, z. B. "Keine Redundanz", in dem Sie Zugriff erhalten auf alle Daten können, und kopieren Sie ihn. Die DiskRecoveryAction-Eigenschaft wurde in dem 22. Februar 2018, Update, KB 4077525 hinzugefügt.
    
    
## <a name="detached-status-in-a-cluster"></a>Getrennten Status in einem cluster 

Beim Ausführen der **Get-VirtualDisk** -Cmdlet, der OperationalStatus lautet für eine oder mehrere "direkte Speicherplätze" virtuelle Datenträger wird getrennt. Die HealthStatus jedoch gemeldet, indem die **Get-PhysicalDisk** Cmdlet gibt an, dass alle physischen Datenträger in einem fehlerfreien Zustand.

Im folgenden ist ein Beispiel der Ausgabe der **Get-VirtualDisk** Cmdlet.

|FriendlyName|  ResiliencySettingName|  OperationalStatus|   HealthStatus|  IsManualAttach|  Größe|   PSComputerName|
|-|-|-|-|-|-|-|
|Disk4|         Spiegelung|                 OK|                  Fehlerfrei|       True|            10 TB|  Node-01.conto...|
|Disk3|         Spiegelung|                 OK|                  Fehlerfrei|       True|            10 TB|  Node-01.conto...|
|Disk2|         Spiegelung|                 „Getrennt“|            Unbekannt|       True|            10 TB|  Node-01.conto...|
|Disk1|         Spiegelung|                 „Getrennt“|            Unbekannt|       True|            10 TB|  Node-01.conto...| 


Darüber hinaus können die folgenden Ereignisse auf den Knoten protokolliert werden:

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

Die **getrennten Betriebsstatus** kann auftreten, wenn die dirty Region tracking (DRT) Protokoll voll ist. Speicherplätze verwendet dirty Region tracking (DRT) für die gespiegelten Speicherbereichen, stellen Sie sicher, dass bei ein Stromausfall, alle ausgeführten Aktualisierungen von Metadaten so protokolliert werden, um sicherzustellen, dass der tatsächlich belegte Speicherplatz wiederholen oder Rückgängig-Vorgänge aus, um den Speicherplatz eine flexible wiederherstellen zu können und einen konsistenten Zustand, wenn die Stromversorgung wiederhergestellt ist und das System wieder hochgefahren. Wenn das DRT-Protokoll voll ist, kann nicht der virtuelle Datenträger online geschaltet werden, bis die DRT-Metadaten synchronisiert ist und geleert wird. Dieser Prozess erfordert das Ausführen einer vollständigen Überprüfung, die mehrere Stunden in Anspruch nehmen kann.
    
Um dieses Problem zu beheben, gehen Sie folgendermaßen vor:
1. Entfernen Sie die betroffenen virtuellen Datenträger aus CSV-Datei.

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. Führen Sie die folgenden Befehle auf alle Datenträger, der nicht in den Onlinestatus wechselt. 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 7
   Start-ClusterResource -Name "VdiskName"
   ``` 
3. Führen Sie den folgenden Befehl auf jedem Knoten, in dem das getrennte Volume online ist. 

   ```powershell
   Get-ScheduledTask -TaskName "Data Integrity Scan for Crash Recovery" | Start-ScheduledTask 
   ```
   Diese Aufgabe sollte auf allen Knoten initiiert werden, auf denen das getrennte Volume online ist. Eine Reparatur sollte automatisch gestartet werden. Warten Sie, bis die Reparatur abgeschlossen. Es kann in den Standbymodus wechseln und erneut starten. Um den Fortschritt zu überwachen: 
   - Führen Sie **Get-StorageJob** zum Überwachen des Status der Reparatur und um festzustellen, wann sie abgeschlossen ist.
   -  Führen Sie **Get-VirtualDisk** und prüfen, ob der Speicherplatz HealthStatus von fehlerfrei zurückgegeben.
    - Die "Integrität überprüfen für abstürzen Datenwiederherstellung" ist eine Aufgabe, die nicht als eines Speicherauftrags angezeigt wird, und es ist kein Fortschrittsanzeige. Wenn die Aufgabe angezeigt werden ausgeführt, er ausgeführt wird. Wenn der Vorgang abgeschlossen ist, wird die abgeschlossene angezeigt.
    
       Darüber hinaus können Sie den Status des ein aktuell ausgeführter zeitplantask anzeigen, indem Sie mit dem folgenden Cmdlet: 
       ```powershell
       Get-ScheduledTask | ? State -eq running
       ``` 
4. Sobald die "Integrität überprüfen für abstürzen Datenwiederherstellung" abgeschlossen ist, sind die Reparatur abgeschlossen ist und die virtuellen Datenträger fehlerfrei, Änderung, die Parameter für die virtuellen Datenträger zu sichern. 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 0 
   ```
5. Fügen Sie die betroffenen virtuellen Datenträger wieder zum CSV hinzu.    

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```  
**DiskRunChkdsk Wert 7** wird verwendet, fügen Sie das Volume Speicherplatz und die Partition im schreibgeschützten Modus. Dies ermöglicht Leerzeichen, die selbst ermitteln und betriebssystembereich, indem Sie eine Reparatur auslösen. Repair führt automatisch bereitgestellt. Außerdem können Sie Zugriff auf die Daten, die für den Zugriff auf alle Daten, die Sie kopieren können hilfreich sein kann. Für einige fehlerbedingungen, wie z. B. ein vollständiges DRT-Protokoll müssen Sie die Datenintegritätsüberprüfung für Wiederherstellung nach einem Systemabsturz geplante Aufgabe ausführen.
    
**Datenintegritätsüberprüfung für die Wiederherstellung nach einem Systemabsturz Aufgabe** wird verwendet, um ein vollständiger dirty Region tracking (DRT)-Protokoll zu löschen. Diese Aufgabe kann mehrere Stunden in Anspruch nehmen. Die "Integrität überprüfen für abstürzen Datenwiederherstellung" ist eine Aufgabe, die nicht als eines Speicherauftrags angezeigt wird, und es ist kein Fortschrittsanzeige. Wenn die Aufgabe angezeigt werden ausgeführt, er ausgeführt wird. Wenn der Vorgang abgeschlossen ist, wird als abgeschlossen angezeigt. Wenn Sie den Vorgang abbrechen oder Neustart eines Knotens aus, während diese Aufgabe ausgeführt wird, müssen die Aufgabe von vorn zu beginnen.

Weitere Informationen finden Sie unter [Problembehandlung von "direkte Speicherplätze" Integritäts- und Betriebsstatus](storage-spaces-states.md).
    
## <a name="event-5120-with-statusiotimeout-c00000b5"></a>Ereignis 5120 mit STATUS_IO_TIMEOUT c00000b5 

>[! Wichtige} um die Wahrscheinlichkeit, dass diese Symptome auftreten, beim Anwenden des Updates mit der Behebung zu reduzieren, ist es wird empfohlen, das folgende Verfahren für den Speicherwartungsmodus zu verwenden, um die Installation der [18. Oktober 2018, kumulatives Update für Windows Server 2016 ](https://support.microsoft.com/help/4462928) oder eine höhere Version, wenn die Knoten derzeit ein kumulatives Update für Windows Server 2016 installiert haben, die freigegeben wurde [8. Mai 2018](https://support.microsoft.com/help/4103723) zu [am 9. Oktober 2018](https://support.microsoft.com/help/KB4462917).

Nach dem Neustart eines Knotens unter Windows Server 2016 mit dem kumulativen Update, die von veröffentlicht wurden, erhalten Sie möglicherweise Ereignis 5120 mit STATUS_IO_TIMEOUT c00000b5 [8. Mai 2018 KB 4103723](https://support.microsoft.com/help/4103723) zu [9. Oktober 2018 KB 4462917](https://support.microsoft.com/help/4462917)installiert.

Wenn Sie den Knoten neu starten, wird Ereignis 5120 wird im Systemereignisprotokoll protokolliert und beinhaltet eine der folgenden Fehlercodes:

```
Event Source: Microsoft-Windows-FailoverClustering
Event ID: 5120
Description:    Cluster Shared Volume 'CSVName' ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_IO_TIMEOUT(c00000b5)'. All I/O will temporarily be queued until a path to the volume is reestablished. 

Cluster Shared Volume ‘CSVName’ ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_CONNECTION_DISCONNECTED(c000020c)'. All I/O will temporarily be queued until a path to the volume is reestablished.    
```

Wenn ein Ereignis 5120 protokolliert wird, wird ein live-Speicherabbild generiert, um Debuginformationen zu sammeln, die möglicherweise dazu führen, dass zusätzliche Symptome oder haben eine Auswirkung auf die Leistung. Generieren von der live-Dump erstellt eine kurze Pause, um eine Momentaufnahme des Speichers, der die Speicherabbilddatei schreiben zu aktivieren. Systeme, die viel Arbeitsspeicher und ausgelastet sind möglicherweise auf den Knoten Clustermitgliedschaft und auch dazu führen, dass das folgende Ereignis 1135 protokolliert werden.

```
Event source: Microsoft-Windows-FailoverClustering
Event ID: 1135  
Description: Cluster node 'NODENAME'was removed from the active failover cluster membership. The Cluster service on this node may have stopped. This could also be due to the node having lost communication with other active nodes in the failover cluster. Run the Validate a Configuration wizard to check your network configuration. If the condition persists, check for hardware or software errors related to the network adapters on this node. Also check for failures in any other network components to which the node is connected such as hubs, switches, or bridges.
```

Das kumulative Update der 8. Mai 2018, SMB robuste behandelt, die für die SMB-Netzwerk-Sitzungen von "direkte Speicherplätze" innerhalb des Clusters hinzufügen wurde eine Änderung eingeführt. Dies erfolgte, um resilienz bei vorübergehenden Netzwerkfehlern verbessern und zu verbessern, wie RoCE Überlastung des Netzwerks behandelt.

Diese Verbesserungen erhöht auch versehentlich Timeouts bei der SMB-Verbindungen versuchen, eine Verbindung herzustellen und wartet auf Timeout, wenn ein Knoten neu gestartet wird. Diese Probleme können es sich um ein System auswirken, der ausgelastet ist. Bei ungeplanten Ausfallzeiten haben e/a-Pausen von bis zu 60 Sekunden auch festgestellt wurde, während das System, Verbindungen mit Timeout wartet.

Um dieses Problem zu beheben, installieren die [18. Oktober 2018, kumulatives Update für Windows Server 2016](https://support.microsoft.com/help/4462928) oder eine höhere Version.

*Beachten Sie* dieses Update richtet die Timeouts CSV mit SMB-Verbindungstimeouts, um dieses Problem zu beheben. Es implementiert nicht die Änderungen live Dump-Generierung im Problemumgehungsabschnitt erwähnten zu deaktivieren.
    
### <a name="shutdown-process-flow"></a>Herunterfahren-Prozessablauf:

1. Führen Sie das Get-VirtualDisk-Cmdlet aus, und stellen Sie sicher, dass die HealthStatus fehlerfrei ist.
2. Das folgende Cmdlet ausführen, um den Knoten zu leeren:

   ```powershell
   Suspend-ClusterNode -Drain
   ```
3. Fügen Sie die Datenträger auf diesem Knoten in den Wartungsmodus für Speicher, durch das folgende Cmdlet ausführen: 

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Enable-StorageMaintenanceMode
   ```
4. Führen Sie die **Get-PhysicalDisk** -Cmdlet, und stellen Sie sicher, dass der OperationalStatus Wert im Wartungsmodus.
5. Führen Sie die **Restart-Computer** Cmdlet, um die Knoten neu gestartet werden.
6. Nach dem Neustart des Knotens entfernen Sie die Datenträger auf diesem Knoten aus dem Wartungsmodus Speicher, indem Sie das folgende Cmdlet ausführen:

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Disable-StorageMaintenanceMode
   ```
7. Fortsetzen des Knotens durch Ausführen des folgenden Cmdlets:

   ```powershell
   Resume-ClusterNode
   ```
8. Überprüfen Sie den Status der Aufträge für die erneute Synchronisierung, indem Sie das folgende Cmdlet ausführen:

   ```powershell
   Get-StorageJob
   ```

### <a name="disabling-live-dumps"></a>Deaktivieren die live-dumps
Um die Auswirkungen der live-Dump-Generierung auf Systemen zu verringern, die viel Arbeitsspeicher und ausgelastet sind, sollten Sie außerdem live Dump-Generierung zu deaktivieren. Drei Optionen sind nachfolgend aufgeführt.

>[!Caution]
>Dieses Verfahren kann die Sammlung von Diagnoseinformationen vermeiden, die Microsoft-Support möglicherweise, um dieses Problem zu untersuchen muss. Ein Support-Agent möglicherweise aufgefordert, die basierend auf bestimmten Problembehandlungsszenarien live Dump-Generierung erneut zu aktivieren.

Es gibt zwei Methoden zum Deaktivieren von live-Dumps, wie unten beschrieben.

#### <a name="method-1-recommended-in-this-scenario"></a>Methode 1 (in diesem Szenario empfohlen)
Gehen Sie folgendermaßen vor, um alle Abbilder, einschließlich der live-Dumps systemweite, vollständig zu deaktivieren:

1. Erstellen Sie den folgenden Registrierungsschlüssel: HKLM\System\CurrentControlSet\Control\CrashControl\ForceDumpsDisabled
2. Unter der neuen **ForceDumpsDisabled** Schlüssel, erstellen Sie eine REG_DWORD-Eigenschaft als GuardedHost und legen Sie dessen Wert auf 0 x 10000000.
3. Wenden Sie den neuen Registrierungsschlüssel auf jedem Clusterknoten an.

>[!NOTE]
>Sie haben zum Neustart des Computers für die %nRegistrierungseinstellung mit Änderung wirksam wird.

Wenn dieser Registrierungsschlüssel festgelegt ist, live ist Speicherabbild fehl und generiert einen Fehler "" Status_Not_Supported "zurück".

#### <a name="method-2"></a>Methode 2
Standardmäßig wird das Windows-Fehlerberichterstattung nur eine LiveDump pro Typ pro sieben Tage lang und nur 1 LiveDump pro Computer pro 5 Tage ermöglichen. Sie können ändern, die die folgenden Registrierungsschlüssel, immer nur eine LiveDump auf dem Computer zuzulassen.
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v SystemThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v ComponentThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```

*Beachten Sie* man Neustart des Computers, damit die Änderung wirksam wird.

### <a name="method-3"></a>Methode 3
Um die Cluster-Generierung von live Dumps (z. B. wenn ein Ereignis 5120 angemeldet ist) zu deaktivieren, führen Sie das folgende Cmdlet aus:

```powershell
(Get-Cluster).DumpPolicy = ((Get-Cluster).DumpPolicy -band 0xFFFFFFFFFFFFFFFE)
```
Dieses Cmdlet hat eine unmittelbare Auswirkung auf alle Knoten des Clusters ohne einen Neustart des Computers.
    
## <a name="slow-io-performance"></a>E/a-Leistung

Wenn Sie e/a-Leistung angezeigt werden, überprüfen Sie, ob der Cache in Ihrer Konfiguration mit "direkte Speicherplätze" aktiviert ist. 

Es gibt zwei Möglichkeiten, um zu überprüfen: 
     
 
1. Verwenden das Cluster-Protokoll. Öffnen Sie das Clusterprotokoll in Text-Editor Ihrer Wahl, und suchen Sie nach "[==== SBL Datenträger ====]." Dies wird eine Liste mit den Datenträger auf dem Knoten sein, die für das Protokoll generiert wurde. 

     Cache aktiviert, Datenträger-Beispiel: Beachten Sie hier, dass der Status CacheDiskStateInitializedAndBound ist und hier eine GUID, die vorhanden ist ist. 

   ```
   [=== SBL Disks ===]
    {26e2e40f-a243-1196-49e3-8522f987df76},3,false,true,1,48,{1ff348f1-d10d-7a1a-d781-4734f4440481},CacheDiskStateInitializedAndBound,1,8087,54,false,false,HGST    ,HUH721010AL4200 ,        7PG3N2ER,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    Der Cache nicht aktiviert: Hier sehen wir, es wird keine GUID vorhanden, und der Zustand ist CacheDiskStateNonHybrid. 
    ```
   [=== SBL Disks ===]
    {426f7f04-e975-fc9d-28fd-72a32f811b7d},12,false,true,1,24,{00000000-0000-0000-0000-000000000000},CacheDiskStateNonHybrid,0,0,0,false,false,HGST    ,HUH721010AL4200 ,        7PGXXG6C,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    Der Cache nicht aktiviert: Wenn alle Datenträger für den gleichen Typ Fall sind ist standardmäßig nicht aktiviert. Hier sehen wir, es wird keine GUID vorhanden, und der Zustand ist CacheDiskStateIneligibleDataPartition. 
    ```
    {d543f90c-798b-d2fe-7f0a-cb226c77eeed},10,false,false,1,20,{00000000-0000-0000-0000-000000000000},CacheDiskStateIneligibleDataPartition,0,0,0,false,false,NVMe    ,INTEL SSDPE7KX02,  PHLF7330004V2P0LGN,0170,{79b4d631-976f-4c94-a783-df950389fd38},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0], 
    ```  
2. Verwenden Get-PhysicalDisk.xml aus der SDDCDiagnosticInfo
    1. Öffnen Sie die XML-Datei mit "$d Import-Clixml GetPhysicalDisk.XML ="
    2. Führen Sie "Ipmo Storage"
    3. Führen Sie "$d". Beachten Sie, dass die Auslastung automatisch auswählen, nicht Buch.-Sie ist, wird etwa folgende Ausgabe angezeigt: 

   |FriendlyName|  SerialNumber| MediaType| CanPool| OperationalStatus| HealthStatus| Verwendung| Größe|
   |-----------|------------|---------| -------| -----------------| ------------| -----| ----|
   |NVMe INTEL SSDPE7KX02| PHLF733000372P0LGN| SSD| False|   OK|                Fehlerfrei|      Automatische Auswahl 1,82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504008J2P0LGN| SSD|  False|    OK|                Fehlerfrei| Automatische Auswahl| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7504005F2P0LGN| SSD|  False|  OK|                Fehlerfrei| Automatische Auswahl| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504002A2P0LGN| SSD| False| OK|    Fehlerfrei| Automatische Auswahl| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7504004T2P0LGN |SSD| False|OK|       Fehlerfrei| Automatische Auswahl| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504002E2P0LGN| SSD| False| OK|      Fehlerfrei| Automatische Auswahl| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7330002Z2P0LGN| SSD| False| OK|      Fehlerfrei|Automatische Auswahl| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF733000272P0LGN |SSD| False| OK|  Fehlerfrei| Automatische Auswahl| 1.82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7330001J2P0LGN |SSD| False| OK| Fehlerfrei| Automatische Auswahl| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF733000302P0LGN |SSD| False| OK|Fehlerfrei| Automatische Auswahl| 1.82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7330004D2P0LGN |SSD| False| OK| Fehlerfrei| Automatische Auswahl |1.82 TB|
    
## <a name="how-to-destroy-an-existing-cluster-so-you-can-use-the-same-disks-again"></a>Wie Sie einen vorhandenen Cluster zu löschen, damit Sie die gleichen Datenträger erneut verwenden zu können

In einem Cluster "direkte Speicherplätze" nachdem Sie Sie deaktivieren "direkte Speicherplätze" und verwenden Sie den Cleanup-Prozess beschrieben, die [Laufwerke reinigen](deploy-storage-spaces-direct.md#step-31-clean-drives)clusterspeicherpools bleibt weiterhin im Status "Offline" und dem Health-Dienst wird aus entfernt -Cluster.

Der nächste Schritt besteht phantom Speicherpool zu entfernen: 
   ```powershell
   Get-ClusterResource -Name "Cluster Pool 1" | Remove-ClusterResource
   ```

Nun, wenn das Ausführen **Get-PhysicalDisk** auf einen beliebigen Knoten, sehen Sie alle Datenträger, die im Pool wurden. Z. B. in einem Lab mit einem 4-Knoten-Cluster mit 4-SAS-Datenträgern, jeweils 100GB für jeden Knoten angezeigt werden soll. In diesem Fall nach Storage Space Direct deaktiviert ist, die entfernt die SBL (Storage Bus Layer) jedoch bewirkt, dass den Filter, wenn das Ausführen **Get-PhysicalDisk**, meldet sie 4 Datenträger mit Ausnahme der lokalen Betriebssystem-Datenträgers. Stattdessen hat es stattdessen gemeldet 16. Dies ist für alle Knoten im Cluster identisch. Beim Ausführen einer **Get-Disk** Befehl sehen Sie die lokal angeschlossenen Datenträger, die als 0, 1, 2 und So weiter, wie in dieser Beispielausgabe gezeigt:

|Number| Angezeigter Name| Seriennummer|HealthStatus|OperationalStatus|Gesamtgröße| Partitionstyp|
|-|-|-|-|-|-|-|-|
|0|Msft-Virtu...  ||Fehlerfrei | Online|  127 GB| GPT|
||Msft-Virtu... ||Fehlerfrei| Offline| 100 GB| RAW|
||Msft-Virtu... ||Fehlerfrei| Offline| 100 GB| RAW|
||Msft-Virtu... ||Fehlerfrei| Offline| 100 GB| RAW|
||Msft-Virtu... ||Fehlerfrei| Offline| 100 GB| RAW|
|1|Msft-Virtu...||Fehlerfrei| Offline| 100 GB| RAW|
||Msft-Virtu... ||Fehlerfrei| Offline| 100 GB| RAW|
|2|Msft-Virtu...||Fehlerfrei| Offline| 100 GB| RAW|
||Msft-Virtu... ||Fehlerfrei| Offline| 100 GB| RAW|
||Msft-Virtu... ||Fehlerfrei| Offline| 100 GB| RAW|
||Msft-Virtu... ||Fehlerfrei| Offline| 100 GB| RAW|
||Msft-Virtu... ||Fehlerfrei| Offline| 100 GB| RAW|
|4|Msft-Virtu...||Fehlerfrei| Offline| 100 GB| RAW|
|3|Msft-Virtu...||Fehlerfrei| Offline| 100 GB| RAW|
||Msft-Virtu... ||Fehlerfrei| Offline| 100 GB| RAW|
||Msft-Virtu... ||Fehlerfrei| Offline| 100 GB| RAW|
||Msft-Virtu... ||Fehlerfrei| Offline| 100 GB| RAW|

    
## <a name="error-message-about-unsupported-media-type-when-you-create-an-storage-spaces-direct-cluster-using-enable-clusters2d"></a>Fehlermeldung über "unsupported Media Type" beim Erstellen eines "direkte Speicherplätze"-Clusters mit der Enable-ClusterS2D  

Sie möglicherweise Fehlermeldungen, die etwa wie folgt angezeigt, beim Ausführen der **Enable-ClusterS2D** Cmdlet:

![Szenario 6-Fehlermeldung](media/troubleshooting/scenario-error-message.png)

Um dieses Problem zu beheben, stellen Sie sicher, dass der Adapter HBA HBA-Modus konfiguriert ist. Keine HBA sollte im RAID-Modus konfiguriert werden.  
    
## <a name="enable-clusterstoragespacesdirect-hangs-at-waiting-until-sbl-disks-are-surfaced-or-at-27"></a>Enable-ClusterStorageSpacesDirect hängt "wartet, bis SBL Datenträger tauchen" höchstens 27 %

Sie sehen, dass die folgende Informationen in den Validierungsbericht:

    Disk <identifier> connected to node <nodename> returned a SCSI Port Association and the corresponding enclosure device could not be found. The hardware is not compatible with Storage Spaces Direct (S2D), contact the hardware vendor to verify support for SCSI Enclosure Services (SES). 
    
  
Das Problem ist mit der Karte der HPE SAS-Expander, die sich zwischen der Datenträger, und die HBA-Karte. Der SAS-Erweiterung erstellt eine doppelte ID zwischen das erste Laufwerk das Expander-Steuerelement und das Expander-Steuerelement selbst verbunden.  Dies wurde behoben [HPE Smart Array SAS-Expander Firmware des Controllers: 4.02](https://support.hpe.com/hpsc/swd/public/detail?sp4ts.oid=7304566&swItemId=MTX_ef8d0bf4006542e194854eea6a&swEnvOid=4184#tab3).
    
## <a name="intel-ssd-dc-p4600-series-has-a-non-unique-nguid"></a>Intel SSD DC P4600-Serie hat einen nicht eindeutigen NGUID
Möglicherweise scheint, in denen ein Gerät der Serie Intel SSD DC P4600 meldet ähnliche 16 Byte NGUID für mehrere Namespaces wie z. B. 0100000001000000E4D25C000014E214 oder 0100000001000000E4D25C0000EEE214 im folgenden Beispiel werden Fehler angezeigt.

|uniqueid| Geräte-ID |MediaType| BusType| serialNumber| size|canpool| friendlyname| OperationalStatus|
|-|-|-|-|-|-|-|-|-
|5000CCA251D12E30| 0| HDD| SAS| 7PKR197G|                  10000831348736 |False|HGST| HUH721010AL4200| OK|
|eui.0100000001000000E4D25C000014E214 |4|SSD| NVMe|   0100_0000_0100_0000_E4D2_5C00_0014_E214.|1600321314816|True| INTEL| SSDPE2KE016T7|  OK|
|eui.0100000001000000E4D25C000014E214 |5|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_0014_E214.|  1600321314816|    True| INTEL| SSDPE2KE016T7|  OK|
|eui.0100000001000000E4D25C0000EEE214| 6|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_00EE_E214.|  1600321314816|    True| INTEL| SSDPE2KE016T7|  OK|
|eui.0100000001000000E4D25C0000EEE214| 7|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_00EE_E214.|  1600321314816|    True| INTEL| SSDPE2KE016T7|  OK|

Um dieses Problem zu beheben, aktualisieren Sie die Firmware auf den Intel-Laufwerken auf die neueste Version aus.  Firmwareversion wird QDV101B1 ab Mai 2018 bezeichnet, um dieses Problem zu beheben.

Die [Mai 2018-Version von Intel SSD Data Center Tool](https://downloadmirror.intel.com/27778/eng/Intel_SSD_Data_Center_Tool_3_0_12_Release_Notes_330715-026.pdf) ein Firmwareupdate QDV101B1, für die Reihe Intel SSD DC P4600 enthält.

    
## <a name="physical-disk-healthy-and-operational-status-is-removing-from-pool"></a>Physischer Datenträger "Fehlerfrei" und Betriebsstatus ist "Aus Pool entfernen" 

In einem Windows Server 2016 "direkte Speicherplätze"-Cluster können Sie die HealthStatus für physischen Datenträger von einem oder mehreren als "Fehlerfrei", finden Sie unter zwar der OperationalStatus lautet "(Entfernen aus Pool OK)." 

"Aus Pool entfernen" wird ein Intent-Objekt festgelegt, wenn **Remove-PhysicalDisk** aufgerufen, aber in Health Zustand verwaltet und Wiederherstellung zulassen, wenn der Entfernungsvorgang nicht gespeichert. Sie können manuell die OperationalStatus fehlerfrei mit einem der folgenden Methoden ändern:

- Entfernen Sie den physischen Datenträger aus dem Pool, und fügen Sie ihn anschließend wieder.
- Führen Sie die [Clear-PhysicalDiskHealthData.ps1 Skript](https://go.microsoft.com/fwlink/?linkid=2034205) die Absicht zu löschen. (Als zum Download zur Verfügung. ein. TXT-Datei. Müssen Sie ihn als speichern ein. PS1-Datei, bevor Sie ausgeführt werden kann.)

Hier sind einige Beispiele, die zeigt, wie das Skript auszuführen:

- Verwenden der **SerialNumber** Parameter, um den Datenträger angeben, Sie fehlerfrei festlegen müssen. Sie können die Seriennummer aus abrufen **WMI MSFT_PhysicalDisk** oder **Get-PhysicalDIsk**. (Wir nur 0 s für die Seriennummer unten verwenden.)
   
   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -SerialNumber 000000000000000 -Verbose -Force
    ```

- Verwenden der **UniqueId** Parameter, um den Datenträger angeben (erneut über **WMI MSFT_PhysicalDisk** oder **Get-PhysicalDIsk**).

   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -UniqueId 00000000000000000 -Verbose -Force
   ```

## <a name="file-copy-is-slow"></a>Kopieren von Dateien ist langsam.

Sie möglicherweise ein Problem mit der Datei-Explorer zum Kopieren einer großen VHD auf den virtuellen Datenträger gesehen – Kopieren der Datei dauert länger als erwartet.

Mithilfe des Datei-Explorers ist Robocopy oder Xcopy auf eine große VHD auf den virtuellen Datenträger kopieren nicht empfohlenen Methode zur wie dies langsamer als die erwartete Leistung führt. Der Kopiervorgang geht nicht über den "direkte Speicherplätze"-Stapel, die niedriger ist, auf den Speicherstapel und stattdessen verhält sich wie ein Prozess für die lokale Kopie.

Wenn Sie "direkte Speicherplätze"-Leistung testen möchten, empfiehlt sich VMFleet und Diskspd auf auslastungs- und Belastungstests Server zum Abrufen einer Baseline und Festlegen von Erwartungen für die "direkte Speicherplätze"-Leistung.

## <a name="expected-events-that-you-would-see-on-rest-of-the-nodes-during-the-reboot-of-a-node"></a>Ereignisse, die auch auf die übrigen Knoten, beim Neustart eines Knotens angezeigt werden zu erwarten. 

Es ist sicherer, diese Ereignisse ignoriert: 

    Event ID 205: Windows lost communication with physical disk {XXXXXXXXXXXXXXXXXXXX }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

    Event ID 203: Windows lost communication with physical disk {xxxxxxxxxxxxxxxxxxxxxxxx }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

Wenn Sie virtuelle Azure-Computer ausführen, können Sie dieses Ereignis ignorieren:

    Event ID 32: The driver detected that the device \Device\Harddisk5\DR5 has its write cache enabled. Data corruption may occur. 
    
## <a name="slow-performance-or-lost-communication-io-error-detached-or-no-redundancy-errors-for-deployments-that-use-intel-p3x00-nvme-devices"></a>Langsame Leistung oder "Lost Communication," "-e/a-Fehler", "Getrennt" oder "No-Redundanz" Fehler bei Bereitstellungen, verwenden Intel P3x00 NVMe-Geräte,

Wir haben ein schwerwiegendes Problem identifiziert, die einige Benutzer mit "direkte Speicherplätze" wirkt sich auf, die Hardware, die basierend auf der Intel P3x00 Gerätefamilie NVM Express (NVMe) mit Versionen vor "Wartungsversion 8." verwenden 

>[!NOTE]
> Einzelne OEMs möglicherweise Geräte, die auf der Intel P3x00-Familie NVMe-Geräte mit eindeutigen Firmware Versionszeichenfolgen basieren. Wenden Sie sich an Ihren OEM, Weitere Informationen, die neueste Version der Firmware.

Wenn Sie Hardware in Ihrer Bereitstellung basierend auf der Intel P3x00-Produktfamilie NVMe-Geräte verwenden, es wird empfohlen, sofortiges Anwenden von der neuesten Firmware (mindestens Wartung Version 8). Dies [Microsoft Support-Artikel](https://support.microsoft.com/en-us/help/4052341/slow-performance-or-lost-communication-io-error-detached-or-no-redunda) enthält zusätzliche Informationen zu diesem Problem. 
