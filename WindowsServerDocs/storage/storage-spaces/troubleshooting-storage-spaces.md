---
title: "\"Direkte Speicherplätze\", Problembehandlung"
description: Hier erfahren Sie, wie Sie Ihre Bereitstellung mit direkten Speicherplätzen zu beheben.
keywords: Speicherplätze
ms.prod: windows-server-threshold
ms.author: ''
ms.technology: storage-spaces
ms.topic: article
author: kaushika-msft
ms.date: 10/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: c7c9573732ff1cf5a998588b1aec81915c227ee2
ms.sourcegitcommit: 5d55c3ebd1ceee7229ea9a9989c69cf93757ed88
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2019
ms.locfileid: "9256933"
---
# Problembehandlung für Storage Spaces Direct

Verwenden Sie die folgende Informationen, um Ihre Bereitstellung mit direkten Speicherplätzen zu beheben.

Starten Sie in der Regel mit den folgenden Schritten:

1. Stellen Sie sicher, dass der Hersteller/Modell des SSD für Windows Server 2016 unter Verwendung von Windows Server-Katalog zertifiziert wurde. Vergewissern Sie sich beim Anbieter, dass die Laufwerke für Storage Spaces Direct unterstützt werden.
2. Untersuchen Sie den Speicher für alle fehlerhafte Laufwerke. Verwenden Sie zum Überprüfen des Status der Laufwerke Speicher-Management-Software. Wenn die Laufwerke fehlerhaft, arbeiten Sie mit Ihrem Anbieter sind. 
3. Aktualisieren Sie den Speicher und steuern Sie Firmware bei Bedarf zu.
   Stellen Sie sicher, dass die neuesten Windows-Updates auf allen Knoten installiert werden. Sie erhalten die neuesten Updates für Windows Server 2016 von [https://aka.ms/update2016](https://aka.ms/update2016).
4. Netzwerkadapter-Treiber und Firmware zu aktualisieren.
5. Ausführen der clustervalidierung und Lesen Sie den Abschnitt direkte Speicherplatz, sicherzustellen, dass die Laufwerke werden für den Cache verwendete korrekt gemeldet werden und keine Fehler.

Wenn weiterhin Probleme auftreten, überprüfen Sie die folgenden Szenarien.

## Virtuelle Datenträgerressourcen befinden sich im Zustand ohne Redundanz
Der Knoten für ein "direkte Speicherplätze" System unerwartet aufgrund eines Fehlers Absturz oder Stromausfall nicht neu starten. Anschließend einem oder mehreren der virtuellen Laufwerke möglicherweise nicht online geschaltet, und Sie sehen die Beschreibung "nicht genügend Redundanzinformationen."
    
|FriendlyName|ResiliencySettingName| OperationalStatus| HealthStatus| IsManualAttach|Size| PSComputerName|
|------------|---------------------| -----------------| ------------| --------------|-----| --------------|
|Disk4| Spiegel| OK|  Healthy| Wahr|  10 TB|  Knoten-01.conto …|
|Disk3         |Spiegel                 |OK                          |Healthy       |Wahr            |10 TB | Knoten-01.conto …|
|Lesen der 2         |Spiegel                 |Keine Redundanz               |Unhealthy     |Wahr            |10 TB | Knoten-01.conto …|
|Disk1         |Spiegel                 |{Keine Redundanz InService}  |Unhealthy     |Wahr            |10 TB | Knoten-01.conto …| 

Nach dem Versuch, den virtuellen Datenträger online zu schalten, wird darüber hinaus die folgende Informationen im Ereignisprotokoll Cluster (DiskRecoveryAction) protokolliert.  

```
[Verbose] 00002904.00001040::YYYY/MM/DD-12:03:44.891 INFO [RES] Physical Disk <DiskName>: OnlineThread: SuGetSpace returned 0.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 WARN [RES] Physical Disk < DiskName>: Underlying virtual disk is in 'no redundancy' state; its volume(s) may fail to mount.
[Verbose] 00002904.00001040:: YYYY/MM/DD -12:03:44.891 ERR [RES] Physical Disk <DiskName>: Failing online due to virtual disk in 'no redundancy' state. If you would like to attempt to online the disk anyway, first set this resource's private property 'DiskRecoveryAction' to 1. We will try to bring the disk online for recovery, but even if successful, its volume(s) or CSV may be unavailable. 
``` 

Der **Nein Redundanz Betriebsstatus** kann auftreten, wenn ein Datenträger fehlgeschlagen ist oder wenn das System nicht auf Daten auf den virtuellen Datenträger zugreifen kann. Dieses Problem kann auftreten, wenn ein Neustart auf einem Knoten während der Wartung auf den Knoten auftritt.
    
Um dieses Problem zu beheben, gehen Sie folgendermaßen vor:

1. Entfernen Sie die betroffenen virtuellen Datenträger aus dem freigegebenen Clustervolume. Dies wird platzieren Sie sie in der Gruppe "Verfügbaren Speicher" im Cluster und angezeigt werden sollen als eine ResourceType von "Physical Disk".

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. Führen Sie auf dem Knoten, der verfügbaren Speichergruppe besitzt den folgenden Befehl auf jedem Datenträger, die in einem Nein Redundanz Zustand befindet. Um die Knoten identifizieren Sie die Gruppe "Verfügbaren Speicher" ist kann den folgenden Befehl ausführen.

   ```powershell
   Get-ClusterGroup
   ```
3. Setzen Sie die Datenträger-Wiederherstellung-Aktion aus, und starten Sie den Datenträger.
   ```powershell
   Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 1
   Start-ClusterResource -Name "VdiskName"
   ```
4. Eine Reparatur sollte automatisch gestartet werden. Warten Sie, bis die Reparatur zum Abschließen. Es kann in einen angehaltenen Zustand wechseln und erneut starten. Um den Fortschritt überwachen: 
    - Führen Sie **Get-StorageJob** Überwachen des Status der Reparatur und anzuzeigen, wenn er abgeschlossen ist.
    - Führen Sie **Get-VirtualDisk** , und überprüfen Sie, ob der Platz HealthStatus von fehlerfrei zurückgibt.
5. Nach der Reparatur sind abgeschlossen ist und die virtuellen Datenträger fehlerfrei, Änderung, die die virtuellen Datenträger-Parameter zurück.

   ```powershell
    Get-ClusterResource "VdiskName" | Set-ClusterParameter -Name DiskRecoveryAction -Value 0
   ```
6. Führen Sie die Datenträger offline und anschließend wieder online erneut aus, um die DiskRecoveryAction wirksam haben:

   ```powershell
   Stop-ClusterResource "VdiskName"
   Start-ClusterResource "VdiskName"
   ``` 
7. Die betroffenen virtuellen Datenträger wieder zu CSV hinzufügen.

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```

**DiskRecoveryAction** ist eine Überschreibung Switch, die das Volume Platz im Lese-/ Schreibzugriff-Modus ohne jegliche Überprüfung anfügen. Die Eigenschaft ermöglicht Ihnen Diagnose in warum ein Volume online geschaltet wird nicht. Es ist sehr ähnlich Wartungsmodus, jedoch können Sie sie auf eine Ressource im Fehlerstatus aufrufen. Außerdem können Sie die auf diese Daten zugreifen in Situationen, z. B. "Nein Redundanz hilfreich können", in denen erhalten Sie Zugriff auf alle Daten können, und kopieren Sie sie. Die Eigenschaft DiskRecoveryAction wurde in der Februar 22. Mai 2018, Update, KB 4077525 hinzugefügt.
    
    
## Getrennte Status in einem cluster 

Wenn Sie das Cmdlet **Get-VirtualDisk** ausführen, ist der OperationalStatus für "direkte Speicherplätze" virtuellen Festplatten getrennt. Allerdings kennzeichnet die HealthStatus gemeldet werden, indem Sie das Cmdlet **Get-PhysicalDisk** , dass alle physischen Datenträger in einem fehlerfreien Zustand.

Im folgenden ist ein Beispiel für die Ausgabe des Cmdlets **Get-VirtualDisk** .

|FriendlyName|  ResiliencySettingName|  OperationalStatus|   HealthStatus|  IsManualAttach|  Size|   PSComputerName|
|-|-|-|-|-|-|-|
|Disk4|         Spiegel|                 OK|                  Healthy|       Wahr|            10 TB|  Knoten-01.conto …|
|Disk3|         Spiegel|                 OK|                  Healthy|       Wahr|            10 TB|  Knoten-01.conto …|
|Lesen der 2|         Spiegel|                 Getrennt|            Unknown|       Wahr|            10 TB|  Knoten-01.conto …|
|Disk1|         Spiegel|                 Getrennt|            Unknown|       Wahr|            10 TB|  Knoten-01.conto …| 


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

Der **Getrennten Betriebsstatus** kann auftreten, wenn die veralteten Bereich (DRT) tracking Protokoll voll ist. "Speicherplätze" verwendet veralteten Bereich tracking (DRT) für gespiegelte Leerzeichen, stellen Sie sicher, dass bei einem Stromausfall alle Flight Updates für die Metadaten so angemeldet sind, stellen Sie sicher, dass der Speicherplatz wiederherstellen oder verwendet Rückgängigmachen, um den Speicherplatz wieder eine flexible machen können und konsistenten Zustand, wenn die Stromversorgung wiederhergestellt, und das System wieder eingeblendet wird. Wenn das Protokoll DRT voll ist, kann nicht der virtuelle Datenträger online geschaltet werden, bis die DRT Metadaten synchronisiert und geleert ist. Dieser Vorgang erfordert das Ausführen einer vollständigen Überprüfung, die dies kann mehrere Stunden dauern.
    
Um dieses Problem zu beheben, gehen Sie folgendermaßen vor:
1. Entfernen Sie die betroffenen virtuellen Datenträger aus dem freigegebenen Clustervolume.

   ```powershell
   Remove-ClusterSharedVolume -name "VdiskName"
   ``` 
2. Führen Sie die folgenden Befehle auf jedem Datenträger, die nicht online stammen. 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 7
   Start-ClusterResource -Name "VdiskName"
   ``` 
3. Führen Sie den folgenden Befehl auf jedem Knoten, in denen das getrennte Volume online ist. 

   ```powershell
   Get-ScheduledTask -TaskName "Data Integrity Scan for Crash Recovery" | Start-ScheduledTask 
   ```
   Diese Aufgabe sollte auf allen Knoten initiiert werden, auf denen das getrennte Volume online ist. Eine Reparatur sollte automatisch gestartet werden. Warten Sie, bis die Reparatur zum Abschließen. Es kann in einen angehaltenen Zustand wechseln und erneut starten. Um den Fortschritt überwachen: 
   - Führen Sie **Get-StorageJob** Überwachen des Status der Reparatur und anzuzeigen, wenn er abgeschlossen ist.
   -  Führen Sie **Get-VirtualDisk** , und stellen Sie sicher, dass der Platz HealthStatus von fehlerfrei zurückgibt.
    - Die "Integrität Scannen für Absturz-Wiederherstellung" ist eine Aufgabe, die als Speicher Auftrag angezeigt wird, und es gibt keine Statusanzeige. Wenn die Aufgabe angezeigt wird als ausgeführt, es ausgeführt wird. Wenn es abgeschlossen ist, wird die abgeschlossene angezeigt.
    
       Darüber hinaus können Sie den Status einer ausgeführten Planungsaufgabe anzeigen, indem Sie mit dem folgenden Cmdlet: 
       ```powershell
       Get-ScheduledTask | ? State -eq running
       ``` 
4. Sobald die "Integrität Scannen für Absturz-Wiederherstellung" abgeschlossen ist, sind die Reparatur abgeschlossen ist und die virtuellen Laufwerke fehlerfrei, Änderung, die die virtuellen Datenträger-Parameter zurück. 

   ```powershell
   Get-ClusterResource -Name "VdiskName" | Set-ClusterParameter DiskRunChkDsk 0 
   ```
5. Die betroffenen virtuellen Datenträger wieder zu CSV hinzufügen.    

   ```powershell
   Add-ClusterSharedVolume -name "VdiskName"
   ```  
**DiskRunChkdsk Wert 7** wird verwendet, das Volume Speicherplatz anhängen und die Partition im schreibgeschützten Modus. Dadurch können Speicherplätze selbst ermitteln, automatische Fehlerbehebung durch eine Reparatur auslösen. Führt die Reparatur automatisch, sobald Sie bereitgestellt. Außerdem können Sie Zugriff auf die Daten, die auf Daten zugreifen, die Sie zum Kopieren von hilfreich sein kann. Für einige Bedingungen Fehlertoleranz, z. B. ein vollständiges DRT-Protokoll müssen Sie die Datenintegrität gesucht Wiederherstellung geplante Aufgabe ausführen.
    
**Datenintegrität überprüft, auf die Wiederherstellung Aufgabe** dient zum Synchronisieren und eine vollständige veralteten Bereich (DRT) tracking-Protokoll löschen. Dieser Vorgang kann mehrere Stunden dauern. Die "Integrität Scannen für Absturz-Wiederherstellung" ist eine Aufgabe, die als Speicher Auftrag angezeigt wird, und es gibt keine Statusanzeige. Wenn die Aufgabe angezeigt wird als ausgeführt, es ausgeführt wird. Wenn es abgeschlossen ist, zeigen sie als abgeschlossen. Wenn Sie den Vorgang abbrechen oder neu starten ein Knotens, während diese Aufgabe ausgeführt wird, müssen die Aufgabe über von vorn beginnen.

Weitere Informationen finden Sie in der [Problembehandlung für "direkte Speicherplätze" Integrität- und Betriebsstatus](storage-spaces-states.md).
    
## Ereignis 5120 mit STATUS_IO_TIMEOUT c00000b5 

> [!Important]
> Um die Wahrscheinlichkeit, dass diese Symptome beim Anwenden einer Aktualisierung mit dem Update auftreten zu reduzieren, wird empfohlen, die nachfolgend Speichermodus-Wartung verwenden, um das [18. Oktober 2018 kumulative Update für Windows Server 2016](https://support.microsoft.com/help/4462928) oder höher installieren Wenn die Knoten derzeit installiert haben, ein veröffentlichtes Windows Server 2016 Kumulatives Update von [8 Mai 2018](https://support.microsoft.com/help/4103723) , [9. Oktober 2018](https://support.microsoft.com/help/KB4462917).

Sie erhalten möglicherweise Ereignis 5120 mit STATUS_IO_TIMEOUT c00000b5 nach dem Neustart eines Knotens unter Windows Server 2016 mit kumulative Update, die [möglicherweise 8 2018 KB 4103723](https://support.microsoft.com/help/4103723) , [9. Oktober 2018 KB 4462917](https://support.microsoft.com/help/4462917) installiert freigegeben wurden.

Wenn Sie den Knoten neu starten, wird Ereignis 5120 Systemereignisprotokoll angemeldet ist und eine der folgenden Fehlercodes enthält:

```
Event Source: Microsoft-Windows-FailoverClustering
Event ID: 5120
Description:    Cluster Shared Volume 'CSVName' ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_IO_TIMEOUT(c00000b5)'. All I/O will temporarily be queued until a path to the volume is reestablished. 

Cluster Shared Volume ‘CSVName’ ('Cluster Virtual Disk (CSVName)') has entered a paused state because of 'STATUS_CONNECTION_DISCONNECTED(c000020c)'. All I/O will temporarily be queued until a path to the volume is reestablished.    
```

Wenn ein Ereignis 5120 protokolliert wird, wird ein live Dump generiert, um Debuginformationen zu sammeln, die möglicherweise zusätzliche Symptome verursachen oder eine Auswirkung auf die Leistung haben. Generieren das live-Speicherabbild erstellt eine kurze Pause zum Erstellen einer Momentaufnahme der Speicher zum Schreiben der Dumpdatei aktivieren. Systeme, die viel Speicher und Belastung sind möglicherweise Knoten aus Clustermitgliedschaft löschen und auch dazu führen, dass die folgenden Ereignis 1135 protokolliert werden.

```
Event source: Microsoft-Windows-FailoverClustering
Event ID: 1135  
Description: Cluster node 'NODENAME'was removed from the active failover cluster membership. The Cluster service on this node may have stopped. This could also be due to the node having lost communication with other active nodes in the failover cluster. Run the Validate a Configuration wizard to check your network configuration. If the condition persists, check for hardware or software errors related to the network adapters on this node. Also check for failures in any other network components to which the node is connected such as hubs, switches, or bridges.
```

Eine Änderung wurde im kumulativen Update 8 Mai 2018 SMB robustes behandelt, die für den "direkte Speicherplätze" innerhalb des Clusters SMB-Netzwerk-Sitzungen hinzufügen eingeführt. Dies wurde zur Optimierung der resilienz, um die vorübergehende Netzwerkfehlern zu verbessern, wie RoCE eine netzwerküberlastung behandelt.

Diese Verbesserungen erhöht auch versehentlich Timeouts Wenn SMB-Verbindungen erneut eine Verbindung herzustellen und wartet abbricht, wenn ein Knoten neu gestartet wird. Diese Probleme können es sich um ein System auswirken, die Belastung ist. Bei ungeplanten Ausfällen haben auch e/a-Pausen von bis zu 60 Sekunden beobachtet wurde, während das System Verbindungen mit Timeout wartet.

Um dieses Problem zu beheben, installieren Sie dem [18. Oktober 2018, kumulative Update für Windows Server 2016](https://support.microsoft.com/help/4462928) oder höher.

*Hinweis:* Dieses Update richtet die CSV-Timeouts mit SMB-Verbindungstimeouts zur Behebung dieses Problems. Die Änderungen zum Deaktivieren von live Dump-Generation, die im Abschnitt Abhilfe erwähnt wird nicht implementiert.
    
### Prozess-Flow Herunterfahren:

1. Führen Sie das Cmdlet Get-VirtualDisk, und stellen Sie sicher, dass der Wert HealthStatus fehlerfrei ist.
2. Ausgeglichen des Knotens durch Ausführen des folgenden Cmdlet:

   ```powershell
   Suspend-ClusterNode -Drain
   ```
3. Platzieren Sie die Datenträger auf diesem Knoten im Speicher Wartungsmodus durch Ausführen des folgenden Cmdlet: 

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Enable-StorageMaintenanceMode
   ```
4. Führen Sie das Cmdlet **Get-PhysicalDisk** , und stellen Sie sicher, dass der OperationalStatus Wert im Wartungsmodus.
5. Führen Sie das Cmdlet " **Computer neu starten** ", um die Knoten neu zu starten.
6. Nach dem Neustart Knoten entfernen Sie die Datenträger auf diesem Knoten aus dem Speicher Wartungsmodus durch Ausführen des folgenden Cmdlet:

   ```powershell
   Get-StorageFaultDomain -type StorageScaleUnit | Where-Object {$_.FriendlyName -eq "<NodeName>"} | Disable-StorageMaintenanceMode
   ```
7. Fortsetzen des Knotens durch Ausführen des folgenden Cmdlet:

   ```powershell
   Resume-ClusterNode
   ```
8. Überprüfen Sie den Status der neu synchronisierten Aufträgen, indem Sie das folgende Cmdlet ausführen:

   ```powershell
   Get-StorageJob
   ```

### Deaktivieren live-Speicherabbilder
Um den Effekt live Dump Generation auf Systemen zu verringern, die viel Speicher und Belastung sind, sollten Sie außerdem live Dump Generation deaktivieren. Drei Optionen unten.

>[!Caution]
>Bei diesem Verfahren kann die Sammlung von Diagnoseinformationen verhindern, die Microsoft-Support benötigen möglicherweise, dieses Problem zu untersuchen. Einem Support-Mitarbeiter möglicherweise aufgefordert, basierend auf bestimmten zur Problembehandlung Szenarien live Dump Generation erneut zu aktivieren.

Es gibt zwei Methoden zur Deaktivierung von live Abbilder, wie unten beschrieben.

#### Methode 1 (in diesem Szenario empfohlen)
Gehen Sie folgendermaßen vor, um alle Abbilder, einschließlich live Speicherabbilder systemweiten, vollständig zu deaktivieren:

1. Erstellen Sie den folgenden Registrierungsschlüssel: HKLM\System\CurrentControlSet\Control\CrashControl\ForceDumpsDisabled
2. Erstellen Sie eine REG_DWORD-Eigenschaft als GuardedHost, und legen Sie den Wert auf 0 x 10000000, unter dem neuen **ForceDumpsDisabled** -Schlüssel.
3. Wenden Sie den neuen Registrierungsschlüssel auf jedem Clusterknoten.

>[!NOTE]
>Sie haben zum Neustarten des Computers für die Nregistry Änderung wirksam wird.

Nach Abschluss dieser Registrierungsschlüssel fest, live wird Dump Erstellung fehl, und einen Fehler "" Status_Not_Supported "zurück" generieren.

#### Methode 2
Standardmäßig wird das Windows-Fehlerberichterstattung nur eine LiveDump pro Berichtstyp pro 7 Tage und nur 1 LiveDump pro Computer pro bis zu fünf Tage ermöglichen. Sie können ändern, durch Festlegen der folgenden Registrierungsschlüssel für immer nur eine LiveDump auf dem Computer zulassen.
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v SystemThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```
```
reg add "HKLM\Software\Microsoft\Windows\Windows Error Reporting\FullLiveKernelReports" /v ComponentThrottleThreshold /t REG_DWORD /d 0xFFFFFFFF /f
```

*Hinweis:* Sie haben zum Neustarten des Computers für die Änderung wirksam wird.

### Methode 3
Führen Sie zum Deaktivieren der Cluster-Generierung von live Speicherabbilder (z. B. wenn ein Ereignis 5120 angemeldet ist), das folgende Cmdlet aus:

```powershell
(Get-Cluster).DumpPolicy = ((Get-Cluster).DumpPolicy -band 0xFFFFFFFFFFFFFFFE)
```
Dieses Cmdlet verfügt über eine sofortige Auswirkung auf alle Clusterknoten, ohne einen Neustart des Computers.
    
## Geringer e/a-Leistung

Wenn Sie mit geringer e/a-Leistung angezeigt werden, überprüfen Sie, ob der Cache in Ihrer Konfiguration der "direkte Speicherplätze" aktiviert ist. 

Es gibt zwei Möglichkeiten überprüfen: 
     
 
1. Verwenden das Cluster-Protokoll. Öffnen Sie das Clusterprotokoll in beliebigen Texteditor, und suchen Sie nach "[=== SBL Datenträger ===]." Dies ist eine Liste mit den Datenträger auf den Knoten, aus denen das Protokoll auf generiert wurde. 

     Cache aktiviert Datenträger-Beispiel: Beachten Sie, dass der Zustand CacheDiskStateInitializedAndBound und hier eine GUID, die vorhanden sind ist. 

   ```
   [=== SBL Disks ===]
    {26e2e40f-a243-1196-49e3-8522f987df76},3,false,true,1,48,{1ff348f1-d10d-7a1a-d781-4734f4440481},CacheDiskStateInitializedAndBound,1,8087,54,false,false,HGST    ,HUH721010AL4200 ,        7PG3N2ER,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    Cache ist nicht aktiviert: Hier sehen wir keine GUID vorhanden vorhanden ist und der Zustand ist CacheDiskStateNonHybrid. 
    ```
   [=== SBL Disks ===]
    {426f7f04-e975-fc9d-28fd-72a32f811b7d},12,false,true,1,24,{00000000-0000-0000-0000-000000000000},CacheDiskStateNonHybrid,0,0,0,false,false,HGST    ,HUH721010AL4200 ,        7PGXXG6C,A21D,{d5e27a3b-42fb-410a-81c6-9d8cc12da20c},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0],
    ```

    Cache ist nicht aktiviert: Wenn alle Laufwerke den gleichen Typ sind Fall ist standardmäßig nicht aktiviert. Hier sehen Sie keine GUID vorhanden vorhanden ist und der Zustand ist CacheDiskStateIneligibleDataPartition. 
    ```
    {d543f90c-798b-d2fe-7f0a-cb226c77eeed},10,false,false,1,20,{00000000-0000-0000-0000-000000000000},CacheDiskStateIneligibleDataPartition,0,0,0,false,false,NVMe    ,INTEL SSDPE7KX02,  PHLF7330004V2P0LGN,0170,{79b4d631-976f-4c94-a783-df950389fd38},[R/M 0 R/U 0 R/T 0 W/M 0 W/U 0 W/T 0], 
    ```  
2. Mithilfe von Get-PhysicalDisk.xml aus der SDDCDiagnosticInfo
    1. Öffnen Sie die XML-Datei mit "$d Import-Clixml GetPhysicalDisk.XML ="
    2. Führen Sie "Ipmo Speicher"
    3. Führen Sie "$d". Beachten Sie, dass Nutzung ist automatische Auswahl nicht Journal Sie sehen die Ausgabe wie folgt aus: 

   |FriendlyName|  SerialNumber| MediaType| CanPool| OperationalStatus| HealthStatus| Verwendungszweck| Size|
   |-----------|------------|---------| -------| -----------------| ------------| -----| ----|
   |NVMe INTEL SSDPE7KX02| PHLF733000372P0LGN| SSD| False|   OK|                Healthy|      Automatische Auswahl 1,82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504008J2P0LGN| SSD|  False|    OK|                Healthy| Automatische Auswahl| 1,82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7504005F2P0LGN| SSD|  False|  OK|                Healthy| Automatische Auswahl| 1,82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504002A2P0LGN| SSD| False| OK|    Healthy| Automatische Auswahl| 1,82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7504004T2P0LGN |SSD| False|OK|       Healthy| Automatische Auswahl| 1,82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7504002E2P0LGN| SSD| False| OK|      Healthy| Automatische Auswahl| 1,82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7330002Z2P0LGN| SSD| False| OK|      Healthy|Automatische Auswahl| 1,82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF733000272P0LGN |SSD| False| OK|  Healthy| Automatische Auswahl| 1,82 TB|
   |NVMe INTEL SSDPE7KX02 |PHLF7330001J2P0LGN |SSD| False| OK| Healthy| Automatische Auswahl| 1,82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF733000302P0LGN |SSD| False| OK|Healthy| Automatische Auswahl| 1,82 TB|
   |NVMe INTEL SSDPE7KX02| PHLF7330004D2P0LGN |SSD| False| OK| Healthy| Automatische Auswahl |1,82 TB|
    
## Wie Sie einen vorhandenen Cluster zu löschen, damit Sie die gleichen Datenträger erneut verwenden können

In einem "direkte Speicherplätze"-Cluster, sobald Sie "direkte Speicherplätze" deaktivieren und die Bereinigungsprozesses in [Bereinigen von Laufwerken](deploy-storage-spaces-direct.md#step-31-clean-drives)beschriebenen gruppierten Speicherpool im Offline-Status verbleibt und der Zustandsdienst wird vom Cluster entfernt.

Der nächste Schritt ist die phantom Speicherpool zu entfernen: 
   ```powershell
   Get-ClusterResource -Name "Cluster Pool 1" | Remove-ClusterResource
   ```

Nun, wenn Sie **Get-PhysicalDisk** auf allen Knoten ausführen, alle Datenträger sehen Sie, die im Pool waren. Z. B. in einem Labor mit einem 4-Knoten-Cluster mit 4 SAS-Datenträgern, jeweils 100GB zu jedem Knoten angezeigt. In diesem Fall sollten sie nach direkte Speicherplatz die entfernt die SBL (Speicher-Bus-Ebene), aber den Filter verlässt deaktivieren, wenn Sie **Get-PhysicalDisk**ausführen, 4 Datenträger, die den lokalen Betriebssystem-Datenträger ausschließen melden. Stattdessen es 16 statt ausgegeben. Dies gilt für alle Knoten im Cluster. Wenn Sie einen **Get-Disk** -Befehl ausführen, sehen Sie die lokal angeschlossenen Datenträger als 0, 1, 2 usw. nummeriert, wie in dieser Beispielausgabe gezeigt:

|Zahl| Anzeigename| Seriennummer|HealthStatus|OperationalStatus|Gesamtgröße| Partitionsstil|
|-|-|-|-|-|-|-|-|
|0|Msft virtuellen …  ||Healthy | Online|  127 GB| GPT|
||Msft virtuellen … ||Healthy| Offline| 100 GB| RAW|
||Msft virtuellen … ||Healthy| Offline| 100 GB| RAW|
||Msft virtuellen … ||Healthy| Offline| 100 GB| RAW|
||Msft virtuellen … ||Healthy| Offline| 100 GB| RAW|
|1|Msft virtuellen …||Healthy| Offline| 100 GB| RAW|
||Msft virtuellen … ||Healthy| Offline| 100 GB| RAW|
|2|Msft virtuellen …||Healthy| Offline| 100 GB| RAW|
||Msft virtuellen … ||Healthy| Offline| 100 GB| RAW|
||Msft virtuellen … ||Healthy| Offline| 100 GB| RAW|
||Msft virtuellen … ||Healthy| Offline| 100 GB| RAW|
||Msft virtuellen … ||Healthy| Offline| 100 GB| RAW|
|4|Msft virtuellen …||Healthy| Offline| 100 GB| RAW|
|3|Msft virtuellen …||Healthy| Offline| 100 GB| RAW|
||Msft virtuellen … ||Healthy| Offline| 100 GB| RAW|
||Msft virtuellen … ||Healthy| Offline| 100 GB| RAW|
||Msft virtuellen … ||Healthy| Offline| 100 GB| RAW|

    
## Fehlermeldung über "nicht unterstützte Medientyp" beim Erstellen eines "direkte Speicherplätze" Clusters mit Enable-ClusterS2D  

Wenn Sie das Cmdlet " **Enable-ClusterS2D** " Ausführen möglicherweise Fehler ähnlich wie folgt angezeigt:

![Szenario 6-Fehlermeldung](media/troubleshooting/scenario-error-message.png)

Um dieses Problem zu beheben, stellen Sie sicher, dass die HBA-Adapter HBA-Modus konfiguriert ist. Keine HBA sollte im RAID-Modus konfiguriert werden.  
    
## Enable-ClusterStorageSpacesDirect oder des Gerätetreibers am 'werden warten bis SBL Datenträger dargestellt' oder 27 %

Sehen Sie die folgende Informationen in der Prüfbericht ein:

    Disk <identifier> connected to node <nodename> returned a SCSI Port Association and the corresponding enclosure device could not be found. The hardware is not compatible with Storage Spaces Direct (S2D), contact the hardware vendor to verify support for SCSI Enclosure Services (SES). 
    
  
Liegt ein Problem mit der Karte der HPE SAS-einer Erweiterung, die zwischen den Laufwerken und HBA-Karte befindet. Einer der SAS-Erweiterung erstellt eine doppelte ID zwischen dem ersten Laufwerk den einer Erweiterung und die einer Erweiterung selbst.  Dies wurde behoben [HPE Smart Array-Controller SAS-einer Erweiterung Firmware: 4.02](https://support.hpe.com/hpsc/swd/public/detail?sp4ts.oid=7304566&swItemId=MTX_ef8d0bf4006542e194854eea6a&swEnvOid=4184#tab3).
    
## Intel SSD DC P4600 Reihe verfügt über eine nicht eindeutige NGUID
Sie möglicherweise ein Problem sehen, scheint, in denen ein Intel SSD DC P4600 Reihe Gerät ähnliche 16 Byte NGUID für mehrere Namespaces, z. B. 0100000001000000E4D25C000014E214 oder 0100000001000000E4D25C0000EEE214 im folgenden Beispiel Berichte werden.

|UniqueID| Geräte-ID |MediaType| BusType| Seriennummer| size|canpool| FriendlyName| OperationalStatus|
|-|-|-|-|-|-|-|-|-
|5000CCA251D12E30| 0| HDD| SAS| 7PKR197G|                  10000831348736 |False|HGST| HUH721010AL4200| OK|
|EUI.0100000001000000E4D25C000014E214 |4|SSD| NVMe|   0100_0000_0100_0000_E4D2_5C00_0014_E214.|1600321314816|Wahr| INTEL| SSDPE2KE016T7|  OK|
|EUI.0100000001000000E4D25C000014E214 |5|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_0014_E214.|  1600321314816|    Wahr| INTEL| SSDPE2KE016T7|  OK|
|EUI.0100000001000000E4D25C0000EEE214| 6|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_00EE_E214.|  1600321314816|    Wahr| INTEL| SSDPE2KE016T7|  OK|
|EUI.0100000001000000E4D25C0000EEE214| 7|        SSD|       NVMe|    0100_0000_0100_0000_E4D2_5C00_00EE_E214.|  1600321314816|    Wahr| INTEL| SSDPE2KE016T7|  OK|

Um dieses Problem zu beheben, aktualisieren Sie die Firmware auf den Intel-Laufwerken auf die neueste Version.  Firmware-Version wird QDV101B1 von Mai 2018 bezeichnet, um dieses Problem zu beheben.

Die [Mai 2018 Version des Tools Intel SSD Daten Center](https://downloadmirror.intel.com/27778/eng/Intel_SSD_Data_Center_Tool_3_0_12_Release_Notes_330715-026.pdf) enthält ein Firmwareupdate QDV101B1, für die Intel SSD DC P4600-Reihe.

    
## Physische Datenträger "Fehlerfrei", und als Betriebsstatus ist "Entfernen von Pool" 

In einem Cluster mit Windows Server 2016 Storage Spaces Direct möglicherweise Sie die HealthStatus für physische Datenträger von einem oder mehreren als "Fehlerfrei" angezeigt, während der OperationalStatus "(Entfernen von Pool, OK)." wird 

"Entfernen von Pool" wird beim **Entfernen-PhysicalDisk** aufgerufen wird, Health Zustand verwaltet und Wiederherstellung zulassen, wenn der Vorgang zum Entfernen fehlschlägt gespeichert ein Intent festgelegt. Sie können die OperationalStatus manuell in fehlerfrei mit einer der folgenden Methoden ändern:

- Entfernen Sie die physische Festplatte aus dem Pool, und fügen Sie es wieder.
- Führen Sie das [Skript löschen PhysicalDiskHealthData.ps1](https://go.microsoft.com/fwlink/?linkid=2034205) die Absicht deaktivieren. (Verfügbar für den Download als ein. TXT-Datei. Sie müssen es als speichern ein. PS1-Datei, bevor Sie ausgeführt werden können.)

Hier sind einige Beispiele, wie Sie das Skript ausführen:

- Verwenden Sie den **Seriennummer** -Parameter, um den Datenträger anzugeben, die, den Sie benötigen, um fehlerfrei festlegen. Sie können die Seriennummer von **MSFT_PhysicalDisk WMI-** oder **Get-PhysicalDIsk**abrufen. (Wir nur 0 s für die Seriennummer unten verwenden.)
   
   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -SerialNumber 000000000000000 -Verbose -Force
    ```

- Verwenden Sie den **UniqueId** -Parameter, um den Datenträger (erneut aus **MSFT_PhysicalDisk WMI-** oder **Get-PhysicalDIsk**) anzugeben.

   ```powershell
   Clear-PhysicalDiskHealthData -Intent -Policy -UniqueId 00000000000000000 -Verbose -Force
   ```

## Kopieren von Dateien ist langsam

Sie möglicherweise ein Problem mit der Datei-Explorer, um eine große virtuelle Festplatte auf den virtuellen Datenträger zu kopieren gesehen: Kopieren der Datei dauert länger als erwartet.

Mit dem Datei-Explorer, ist Robocopy "oder" Xcopy ", um eine große virtuelle Festplatte auf den virtuellen Datenträger zu kopieren keine empfohlene Methode, um dies dauert länger als der erwarteten Leistung führt wird. Der Kopiervorgang geht nicht durch den "direkte Speicherplätze" Stapel, die befindet sich unten auf der Speicherstapel und stattdessen verhält sich wie eine lokale Kopie-Prozess.

Wenn Sie "direkte Speicherplätze" Leistung testen möchten, empfehlen wir die Verwendung von VMFleet und Diskspd geladen und Belastungstests Server eine Grundlinie abrufen und Festlegen von Erwartungen an die "direkte Speicherplätze" Leistung.

## Erwartet Ereignisse, die Sie auf den Rest der Knoten, während der Neustart eines Knotens sehen würde. 

Es ist sicherer, ignorieren Sie diese Ereignisse: 

    Event ID 205: Windows lost communication with physical disk {XXXXXXXXXXXXXXXXXXXX }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

    Event ID 203: Windows lost communication with physical disk {xxxxxxxxxxxxxxxxxxxxxxxx }. This can occur if a cable failed or was disconnected, or if the disk itself failed. 

Wenn Sie Azure-VMs ausführen, können Sie dieses Ereignis ignorieren:

    Event ID 32: The driver detected that the device \Device\Harddisk5\DR5 has its write cache enabled. Data corruption may occur. 
    
## Langsam oder "Lost Communication," "E/a-Fehler", "Getrennt," oder "No Redundanz"-Fehler für Bereitstellungen, die Intel P3x00 NVMe-Geräte verwenden

Wir haben ein wichtige Problem identifiziert, das einige "direkte Speicherplätze" Benutzer betrifft, die mithilfe von Hardware, die basierend auf der Intel P3x00 Gerätefamilie NVM Express (NVMe) mit Firmware-Versionen vor "Wartung Release 8". 

>[!NOTE]
> Einzelne OEMs können Geräte verfügen, die auf die Gerätefamilie Intel P3x00 NVMe-Geräte mit eindeutige Firmware Versionszeichenfolgen basieren. Weitere Informationen der neuesten Firmwareversion erhalten Sie von Ihrem OEM.

Wenn Sie Hardware in Ihrer Bereitstellung basierend auf der Gerätefamilie Intel P3x00 NVMe-Geräte verwenden, empfehlen wir, dass Sie sofort die neuesten Firmware anwenden (mindestens Wartung Version 8). Diese [Microsoft-Support-Artikel](https://support.microsoft.com/en-us/help/4052341/slow-performance-or-lost-communication-io-error-detached-or-no-redunda) enthält zusätzlichen Informationen zu diesem Problem. 
