---
title: Bekannte Probleme bei Storage Migration Service
description: Bekannte Probleme und Problembehandlung für den Speicher Migrationsdienst, z. b. das Sammeln von Protokollen für Microsoft-Support.
author: nedpyle
ms.author: nedpyle
manager: tiaascs
ms.date: 07/29/2020
ms.topic: article
ms.openlocfilehash: 6c3ca3a44665bab08c58853d569823f88c908f35
ms.sourcegitcommit: f89639d3861c61620275c69f31f4b02fd48327ab
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/29/2020
ms.locfileid: "91517516"
---
# <a name="storage-migration-service-known-issues"></a>Bekannte Probleme bei Storage Migration Service

Dieses Thema enthält Antworten auf bekannte Probleme bei der Verwendung von [Storage Migration Service](overview.md) zum Migrieren von Servern.

Storage Migration Service wird in zwei Teilen veröffentlicht: der-Dienst in Windows Server und die Benutzeroberfläche im Windows Admin Center. Der Dienst ist in Windows Server, langfristig Wartungs Kanal sowie Windows Server, halbjährlicher Kanal, verfügbar. Obwohl Windows Admin Center als separater Download verfügbar ist. Wir schließen auch regelmäßig Änderungen an kumulativen Updates für Windows Server ein, die über Windows Update veröffentlicht werden.

Beispielsweise enthält Windows Server, Version 1903, neue Features und Korrekturen für den Speicher Migrationsdienst, die auch für Windows Server 2019 und Windows Server, Version 1809, verfügbar sind, indem Sie [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)installieren.

## <a name="how-to-collect-log-files-when-working-with-microsoft-support"></a><a name="collecting-logs"></a> Sammeln von Protokolldateien beim Arbeiten mit Microsoft-Support

Der Speicher Migrationsdienst enthält Ereignisprotokolle für den Orchestrator-Dienst und den Proxy Dienst. Der Orchestrator-Server enthält immer Ereignisprotokolle, und Zielserver, auf denen der Proxy Dienst installiert ist, enthalten die Proxy Protokolle. Diese Protokolle befinden sich unter:

- Anwendungs-und Dienst Protokolle \ Microsoft \ Windows \ storagemigrationservice
- Anwendungs-und Dienst Protokolle \ Microsoft \ Windows \ storagemigrationservice-Proxy

Wenn Sie diese Protokolle für die Offline Anzeige oder das Senden an Microsoft-Support erfassen müssen, ist auf GitHub ein Open-Source-PowerShell-Skript verfügbar:

 [Hilfsprogramm für den Speicher Migrationsdienst](https://aka.ms/smslogs)

Lesen Sie die Informationen zur Verwendung.

## <a name="storage-migration-service-doesnt-show-up-in-windows-admin-center-unless-managing-windows-server-2019"></a>Der Speicher Migrationsdienst wird nicht im Windows Admin Center angezeigt, es sei denn, Windows Server 2019 wird verwaltet.

Wenn Sie die Version 1809 von Windows Admin Center zum Verwalten eines Windows Server 2019 Orchestrator verwenden, wird die Option Tool für Storage Migration Service nicht angezeigt.

Die Windows Admin Center Storage Migration Service-Erweiterung ist nur für die Verwaltung der Betriebssysteme Windows Server 2019, Version 1809 oder höher, Versions gebunden. Wenn Sie damit ältere Windows Server-Betriebssysteme oder Insider-Vorschau Versionen verwalten, wird das Tool nicht angezeigt. Dieses Verhalten ist beabsichtigt.

Verwenden Sie zum Auflösen von Windows Server 2019 Build 1809 oder höher, oder führen Sie ein Upgrade durch.

## <a name="storage-migration-service-cutover-validation-fails-with-error-access-is-denied-for-the-token-filter-policy-on-destination-computer"></a>Die Überprüfung des Speicher Migrationsdienst-cutovers schlägt mit dem Fehler "Zugriff wird für die tokenfilterrichtlinie auf dem Zielcomputer verweigert" fehl

Beim Ausführen der Überprüfung des cutovers erhalten Sie den Fehler "Fehler: der Zugriff wird für die tokenfilterrichtlinie auf dem Zielcomputer verweigert". Dies geschieht auch, wenn Sie sowohl für den Quell-als auch für den Zielcomputer die richtigen lokalen Administrator Anmelde Informationen angegeben haben

Dieses Problem wurde im [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) -Update behoben.

## <a name="storage-migration-service-isnt-included-in-windows-server-2019-evaluation-or-windows-server-2019-essentials-edition"></a>Storage Migration Service ist nicht in Windows Server 2019 Evaluation oder Windows Server 2019 Essentials Edition enthalten.

Wenn Sie Windows Admin Center verwenden, um eine Verbindung mit einer [Windows Server 2019-Evaluierungsversion](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) oder Windows Server 2019 Essentials Edition herzustellen, gibt es keine Option zum Verwalten des Speicher Migrations Dienstanbieter. Storage Migration Service ist auch nicht in Rollen und Features enthalten.

Dieses Problem wird durch ein Wartungsproblem in den Evaluierungs Medien von Windows Server 2019 und Windows Server 2019 Essentials verursacht.

Um dieses Problem für die Evaluierung zu umgehen, installieren Sie eine Einzelhandels-, MSDN-, OEM-oder Volumenlizenz Version von Windows Server 2019, und aktivieren Sie Sie nicht. Ohne Aktivierung werden alle Editionen von Windows Server 180 Tage lang im Evaluierungs Modus ausgeführt.

Dieses Problem wurde in einem späteren Release von Windows Server behoben.

## <a name="storage-migration-service-times-out-downloading-the-transfer-error-csv"></a>Timeout des Speicher Migrations Dienstanbieter beim Herunterladen des Übertragungsfehler-CSV

Wenn Sie das Windows Admin Center oder PowerShell verwenden, um das CSV-Protokoll mit ausführlichen Fehlern bei der Übertragungs Operation herunterzuladen, erhalten Sie folgende Fehlermeldung:

```
Transfer Log - Please check file sharing is allowed in your firewall. : This request operation sent to net.tcp://localhost:28940/sms/service/1/transfer did not receive a reply within the configured timeout (00:01:00). The time allotted to this operation may have been a portion of a longer timeout. This may be because the service is still processing the operation or because the service was unable to send a reply message. Please consider increasing the operation timeout (by casting the channel/proxy to IContextChannel and setting the OperationTimeout property) and ensure that the service is able to connect to the client.
```

Dieses Problem wird durch eine extrem große Anzahl übertragener Dateien verursacht, die nicht in dem vom Speicher Migrationsdienst zulässigen Standard Timeout von einer Minute gefiltert werden können.

So umgehen Sie dieses Problem:

1. Bearbeiten Sie auf dem Orchestrator-Computer die Datei *% systemroot% \SMS\Microsoft.StorageMigration.Service.exe.config* mit Notepad.exe, um "SendTimeout" von der 1-minütigen Standardeinstellung in 10 Minuten zu ändern.

    ```
    <bindings>
      <netTcpBinding>
        <binding name="NetTcpBindingSms"
                 sendTimeout="00:10:00"
    ```

2. Starten Sie den Dienst "Storage Migration Service" auf dem Orchestrator-Computer neu.

3. Starten Sie auf dem Orchestrator-Computer Regedit.exe

4. Erstellen Sie den folgenden Registrierungs Unterschlüssel, falls er nicht bereits vorhanden ist:

    `HKEY_LOCAL_MACHINE\Software\Microsoft\SMSPowershell`

5. Zeigen Sie im Menü „Bearbeiten“ auf „Neu“, und klicken Sie dann auf „DWORD-Wert“.

6. Geben Sie "wcfoperationtimeoutinminutes" als Namen für das DWORD ein, und drücken Sie dann die EINGABETASTE.

7. Klicken Sie mit der rechten Maustaste auf "wcfoperationtimeoutinminutes", und klicken Sie dann auf ändern.

8. Klicken Sie im Feld Base Data auf "Decimal".

9. Geben Sie im Feld Wertdaten den Wert "10" ein, und klicken Sie dann auf OK.

10. Beenden Sie den Registrierungs-Editor.

11. Es wird erneut versucht, die CSV-Datei mit Fehlern herunterzuladen.

Wenn Sie eine extrem große Anzahl von Dateien migrieren, müssen Sie dieses Timeout möglicherweise auf mehr als 10 Minuten erhöhen. 

## <a name="validation-warnings-for-destination-proxy-and-credential-administrative-privileges"></a>Validierungs Warnungen für den Ziel Proxy und Administratorrechte für Anmelde Informationen

Beim Validieren eines Übertragungs Auftrags werden folgende Warnungen angezeigt:

```
The credential has administrative privileges.
Warning: Action isn't available remotely.
The destination proxy is registered.
Warning: The destination proxy wasn't found.
```

Wenn Sie den Speicher Migrationsdienst-Proxy Dienst auf dem Windows Server 2019-Zielcomputer nicht installiert haben, oder wenn der Zielcomputer Windows Server 2016 oder Windows Server 2012 R2 ist, ist dieses Verhalten Entwurfs bedingt. Es wird empfohlen, zu einem Windows Server 2019-Computer zu migrieren, auf dem der Proxy installiert ist

## <a name="certain-files-dont-inventory-or-transfer-error-5-access-is-denied"></a>Bestimmte Dateien werden nicht inventarisiert oder übertragen, Fehler 5: "Zugriff verweigert"

Bei der Inventarisierung oder Übertragung von Dateien von einer Quell-auf einen Zielcomputer können Dateien, von denen ein Benutzerberechtigungen für die Administratoren Gruppe entfernt hat, nicht migriert werden. Überprüfen des Speicher Migrations Dienstanbieter: Proxy Debug zeigt Folgendes an:

```
Log Name: Microsoft-Windows-StorageMigrationService-Proxy/Debug
Source: Microsoft-Windows-StorageMigrationService-Proxy
Date: 2/26/2019 9:00:04 AM
Event ID: 10000
Task Category: None
Level: Error
Keywords:
User: NETWORK SERVICE
Computer: srv1.contoso.com
Description:

02/26/2019-09:00:04.860 [Error] Transfer error for \\srv1.contoso.com\public\indy.png: (5) Access is denied.
Stack Trace:
at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.OpenFile(String fileName, DesiredAccess desiredAccess, ShareMode shareMode, CreationDisposition creationDisposition, FlagsAndAttributes flagsAndAttributes)
at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetTargetFile(String path)
at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetTargetFile(FileInfo file)
at Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.InitializeSourceFileInfo()
     at Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.Transfer()
at Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.TryTransfer()
```

Dieses Problem wird durch einen Code Fehler im Speicher Migrationsdienst verursacht, bei dem die Sicherungs Berechtigung nicht aufgerufen wurde.

Um dieses Problem zu beheben, installieren Sie [Windows Update 2. April 2019 – KB4490481 (OS Build 17763,404)](https://support.microsoft.com/help/4490481/windows-10-update-kb4490481) auf dem Orchestrator-Computer und dem Zielcomputer, wenn der Proxy Dienst dort installiert ist. Stellen Sie sicher, dass das Benutzerkonto der Quell Migration ein lokaler Administrator auf dem Quellcomputer und der Orchestrator für den Speicher Migrationsdienst ist. Stellen Sie sicher, dass das Benutzerkonto für die Ziel Migration ein lokaler Administrator auf dem Zielcomputer und der Orchestrator für den Speicher Migrationsdienst ist.

## <a name="dfsr-hashes-mismatch-when-using-storage-migration-service-to-preseed-data"></a>Nicht übereinstimmende DFSR-Hashes bei der Verwendung von Storage Migration Service zum vorab Seed von Daten

Wenn Sie den Speicher Migrationsdienst zum Übertragen von Dateien an ein neues Ziel verwenden, können Sie DFS-Replikation für die Replikation dieser Daten mit einem vorhandenen Server durch die vorab bereitgestellte Replikation oder das Klonen von DFS-Replikation-Datenbank verwenden, dass alle Dateien einen Hash Konflikt haben und erneut repliziert werden. Die Datenströme, Sicherheitsdaten Ströme, Größen und Attribute werden nach der Verwendung von Storage Migration Service für die Übertragung von vollständig abgeglichen. Wenn Sie die Dateien mit icacls oder dem DFS-Replikation-Daten Bank Klon-Debugprotokoll untersuchen, werden

### <a name="source-file"></a>Quelldatei
```
  icacls d:\test\Source:

  icacls d:\test\thatcher.png /save out.txt /t thatcher.png
  D:AI(A;;FA;;;BA)(A;;0x1200a9;;;DD)(A;;0x1301bf;;;DU)(A;ID;FA;;;BA)(A;ID;FA;;;SY)(A;ID;0x1200a9;;;BU)
```

### <a name="destination-file"></a>Zieldatei

```
  icacls d:\test\thatcher.png /save out.txt /t thatcher.png
  D:AI(A;;FA;;;BA)(A;;0x1301bf;;;DU)(A;;0x1200a9;;;DD)(A;ID;FA;;;BA)(A;ID;FA;;;SY)(A;ID;0x1200a9;;;BU)**S:PAINO_ACCESS_CONTROL**
```
### <a name="dfsr-debug-log"></a>DFSR-Debugprotokoll

```
   20190308 10:18:53.116 3948 DBCL  4045 [WARN] DBClone::IDTableImportUpdate Mismatch record was found.

   Local ACL hash:1BCDFE03-A18BCE01-D1AE9859-23A0A5F6
   LastWriteTime:20190308 18:09:44.876
   FileSizeLow:1131654
   FileSizeHigh:0
   Attributes:32

   Clone ACL hash:**DDC4FCE4-DDF329C4-977CED6D-F4D72A5B**
   LastWriteTime:20190308 18:09:44.876
   FileSizeLow:1131654
   FileSizeHigh:0
   Attributes:32
```

Dieses Problem wird durch das [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) -Update behoben.

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-when-transferring-from-windows-server-2008-r2"></a>Fehler "der Speicher konnte bei der Übertragung von Windows Server 2008 R2 nicht an einen der Endpunkte übertragen werden.

Beim Versuch, Daten von einem Windows Server 2008 R2-Quellcomputer zu übertragen, erhalten Sie keine Datenübertragungen, und Sie erhalten eine Fehlermeldung:

```
Couldn't transfer storage on any of the endpoints.
0x9044
```

Dieser Fehler wird erwartet, wenn Ihr Windows Server 2008 R2-Computer nicht vollständig mit allen kritischen und wichtigen Updates von Windows Update gepatcht ist. Es ist besonders wichtig, einen Windows Server 2008 R2-Computer aus Sicherheitsgründen aktualisieren zu lassen, da dieses Betriebssystem nicht die Sicherheitsverbesserungen von neueren Versionen von Windows Server enthält.

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-and-check-if-the-source-device-is-online---we-couldnt-access-it"></a>Fehler "der Speicher konnte nicht an einen der Endpunkte übertragen werden", und "Überprüfen Sie, ob das Quellgerät Online ist-wir konnten nicht darauf zugreifen."

Beim Versuch, Daten von einem Quellcomputer zu übertragen, werden einige oder alle Freigaben mit dem folgenden Fehler nicht übertragen:

```
Couldn't transfer storage on any of the endpoints.
0x9044
```

Die Überprüfung der Details zur SMB-Übertragung zeigt Folgendes

```
Check if the source device is online - we couldn't access it.
```

Die Untersuchung des storagemigrationservice/Admin-Ereignis Protokolls zeigt Folgendes:

```
Couldn't transfer storage.

Job: Job1
ID:
State: Failed
Error: 36931
Error Message:

Guidance: Check the detailed error and make sure the transfer requirements are met. The transfer job couldn't transfer any source and destination computers. This could be because the orchestrator computer couldn't reach any source or destination computers, possibly due to a firewall rule, or missing permissions.
```

Die Untersuchung des storagemigrationservice-Proxy/Debug-Protokolls zeigt Folgendes:

```
07/02/2019-13:35:57.231 [Error] Transfer validation failed. ErrorCode: 40961, Source endpoint is not reachable, or doesn't exist, or source credentials are invalid, or authenticated user doesn't have sufficient permissions to access it.
at Microsoft.StorageMigration.Proxy.Service.Transfer.TransferOperation.Validate()
at Microsoft.StorageMigration.Proxy.Service.Transfer.TransferRequestHandler.ProcessRequest(FileTransferRequest fileTransferRequest, Guid operationId)
```

Dies war ein Code Fehler, der Manifest, wenn Ihr Migrations Konto nicht mindestens über Leseberechtigungen für die SMB-Freigaben verfügt. Dieses Problem wurde zuerst im kumulativen Update [4520062](https://support.microsoft.com/help/4520062/windows-10-update-kb4520062)behoben.

## <a name="error-0x80005000-when-running-inventory"></a>Fehler 0x80005000 beim Ausführen des Inventars.

Nach der Installation von [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) und dem Versuch, das Inventar auszuführen, schlägt die Inventur mit Fehlern fehl

```
EXCEPTION FROM HRESULT: 0x80005000

Log Name:      Microsoft-Windows-StorageMigrationService/Admin
Source:        Microsoft-Windows-StorageMigrationService
Date:          9/9/2019 5:21:42 PM
Event ID:      2503
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      FS02.TailwindTraders.net
Description:
Couldn't inventory the computers.
Job: foo2
ID: 20ac3f75-4945-41d1-9a79-d11dbb57798b
State: Failed
Error: 36934
Error Message: Inventory failed for all devices
Guidance: Check the detailed error and make sure the inventory requirements are met. The job couldn't inventory any of the specified source computers. This could be because the orchestrator computer couldn't reach it over the network, possibly due to a firewall rule or missing permissions.

Log Name:      Microsoft-Windows-StorageMigrationService/Admin
Source:        Microsoft-Windows-StorageMigrationService
Date:          9/9/2019 5:21:42 PM
Event ID:      2509
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      FS02.TailwindTraders.net
Description:
Couldn't inventory a computer.
Job: foo2
Computer: FS01.TailwindTraders.net
State: Failed
Error: -2147463168
Error Message:
Guidance: Check the detailed error and make sure the inventory requirements are met. The inventory couldn't determine any aspects of the specified source computer. This could be because of missing permissions or privileges on the source or a blocked firewall port.

Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Debug
Source:        Microsoft-Windows-StorageMigrationService-Proxy
Date:          2/14/2020 1:18:21 PM
Event ID:      10000
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      2019-rtm-orc.ned.contoso.com
Description:
02/14/2020-13:18:21.097 [Erro] Failed device discovery stage SystemInfo with error: (0x80005000) Unknown error (0x80005000)
```

Dieser Fehler wird durch einen Code Fehler im Speicher Migrationsdienst verursacht, wenn Sie Migrations Anmelde Informationen in Form eines Benutzer Prinzipal namens (User Principal Name, UPN) bereitstellen, z meghan@contoso.com . b. "". Der Orchestrator-Dienst des Speicher Migrations Dienstanbieter kann dieses Format nicht ordnungsgemäß analysieren, was zu einem Fehler bei einer Domänen Suche führt, die zur Unterstützung der Cluster Migration in KB4512534 und 19h1 hinzugefügt wurde.

Um dieses Problem zu umgehen, geben Sie Anmelde Informationen im Format "Domäne \ Benutzer" an, z. b. "contoso\meghan".

## <a name="error-serviceerror0x9006-or-the-proxy-isnt-currently-available-when-migrating-to-a-windows-server-failover-cluster"></a>Fehler "ServiceError0x9006" oder "der Proxy ist zurzeit nicht verfügbar." beim Migrieren zu einem Windows Server-Failovercluster

Wenn Sie versuchen, Daten auf einen Cluster Datei Server zu übertragen, erhalten Sie folgende Fehlermeldung:

```
Make sure the proxy service is installed and running, and then try again. The proxy isn't currently available.
0x9006
ServiceError0x9006,Microsoft.StorageMigration.Commands.UnregisterSmsProxyCommand
```

Dieser Fehler wird erwartet, wenn die Datei Server Ressource vom ursprünglichen Windows Server 2019-Cluster Besitzer Knoten auf einen neuen Knoten verschoben wurde und die Proxy Funktion für den Speicher Migrationsdienst nicht auf diesem Knoten installiert wurde.

Um dieses Problem zu umgehen, verschieben Sie die Ressource des Ziel Dateiservers zurück auf den ursprünglichen Besitzer Cluster Knoten, der bei der ersten Konfiguration der Übertragungs Paare verwendet wurde.

Als Alternative Problem Umgehung:

1. Installieren Sie das Feature "Speicher Migrationsdienst-Proxy" auf allen Knoten in einem Cluster.
2. Führen Sie den folgenden PowerShell-Befehl für den Speicher Migrationsdienst auf dem Orchestrator-Computer aus:

   ```PowerShell
   Register-SMSProxy -ComputerName <destination server> -Force
   ```
## <a name="error-dll-was-not-found-when-running-inventory-from-a-cluster-node"></a>Fehler "dll wurde nicht gefunden" beim Ausführen des Inventars von einem Cluster Knoten

Wenn Sie versuchen, eine Inventur mit dem Speicher Migrationsdienst auszuführen und ein Windows Server-Failovercluster mit der allgemeinen Datei Server Quelle zu verwenden, erhalten Sie die folgenden Fehler:

```
DLL not found
[Error] Failed device discovery stage VolumeInfo with error: (0x80131524) Unable to load DLL 'Microsoft.FailoverClusters.FrameworkSupport.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)
```

Um dieses Problem zu umgehen, installieren Sie die Failovercluster-Verwaltungs Tools (RSAT-Clustering-Mgmt) auf dem Server, auf dem der Orchestrator für den Speicher Migrationsdienst ausgeführt wird.

## <a name="error-there-are-no-more-endpoints-available-from-the-endpoint-mapper-when-running-inventory-against-a-windows-server-2003-source-computer"></a>Fehler "Es sind keine weiteren Endpunkte von der Endpunkt Zuordnung verfügbar", wenn die Inventur auf einem Windows Server 2003-Quellcomputer ausgeführt wird.

Wenn Sie versuchen, eine Inventur mit dem Speicher Migrationsdienst-Orchestrator für einen Windows Server 2003-Quellcomputer auszuführen, erhalten Sie die folgende Fehlermeldung:

```
There are no more endpoints available from the endpoint mapper
```

Dieses Problem wird durch das [KB4537818](https://support.microsoft.com/help/4537818/windows-10-update-kb4537818) -Update behoben.

## <a name="uninstalling-a-cumulative-update-prevents-storage-migration-service-from-starting"></a>Beim Deinstallieren eines kumulativen Updates wird der Speicher Migrationsdienst nicht gestartet.

Durch das Deinstallieren von kumulativen Windows Server-Updates kann der Speicher Migrationsdienst nicht mehr gestartet werden. Um dieses Problem zu beheben, können Sie die Speicher Migrationsdienst-Datenbank sichern und löschen:

1. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, bei der Sie ein Mitglied der Administratoren auf dem Orchestrator-Server für den Speicher Migrationsdienst sind, und führen Sie Folgendes aus:

     ```DOS
     TAKEOWN /d y /a /r /f c:\ProgramData\Microsoft\StorageMigrationService

     MD c:\ProgramData\Microsoft\StorageMigrationService\backup

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService\* /grant Administrators:(GA)

     XCOPY c:\ProgramData\Microsoft\StorageMigrationService\* .\backup\*

     DEL c:\ProgramData\Microsoft\StorageMigrationService\* /q

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService  /GRANT networkservice:F /T /C

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService /GRANT networkservice:(GA) /T /C
     ```

2. Starten Sie den Dienst "Storage Migration Service", mit dem eine neue Datenbank erstellt wird.

## <a name="error-clusctl_resource_netname_repair_vco-failed-against-netname-resource-and-windows-server-2008-r2-cluster-cutover-fails"></a>Fehler "Fehler beim CLUSCTL_RESOURCE_NETNAME_REPAIR_VCO für die NetName-Ressource", und der Windows Server 2008 R2-Cluster-cudever schlägt fehl

Bei dem Versuch, einen Ausschneiden einer Windows Server 2008 R2-Cluster Quelle auszuführen, bleibt die Ausschneide in der Phase "Umbenennen des Quell Computers..." hängen. und Sie erhalten die folgende Fehlermeldung:

```
Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Debug
Source:        Microsoft-Windows-StorageMigrationService-Proxy
Date:          10/17/2019 6:44:48 PM
Event ID:      10000
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      WIN-RNS0D0PMPJH.contoso.com
Description:
10/17/2019-18:44:48.727 [Erro] Exception error: 0x1. Message: Control code CLUSCTL_RESOURCE_NETNAME_REPAIR_VCO failed against netName resource 2008r2FS., stackTrace:    at Microsoft.FailoverClusters.Framework.ClusterUtils.NetnameRepairVCO(SafeClusterResourceHandle netNameResourceHandle, String netName)
at Microsoft.FailoverClusters.Framework.ClusterUtils.RenameFSNetName(SafeClusterHandle ClusterHandle, String clusterName, String FsResourceId, String NetNameResourceId, String newDnsName, CancellationToken ct)
at Microsoft.StorageMigration.Proxy.Cutover.CutoverUtils.RenameFSNetName(NetworkCredential networkCredential, Boolean isLocal, String clusterName, String fsResourceId, String nnResourceId, String newDnsName, CancellationToken ct)    [d:\os\src\base\dms\proxy\cutover\cutoverproxy\CutoverUtils.cs::RenameFSNetName::1510]
```

Dieses Problem wird durch eine fehlende API in älteren Versionen von Windows Server verursacht. Zurzeit gibt es keine Möglichkeit, Windows Server 2008-und Windows Server 2003-Cluster zu migrieren. Sie können eine Inventur und Übertragung ohne Probleme auf Windows Server 2008 R2-Clustern durchführen und dann die Umstellung manuell durchführen, indem Sie die Ressource NetName und IP-Adresse des Cluster Quelldatei Servers manuell ändern und dann den NetName und die IP-Adresse des Ziel Clusters entsprechend der ursprünglichen Quelle ändern.

## <a name="cutover-hangs-on-38-mapping-network-interfaces-on-the-source-computer-when-using-static-ips"></a>Die Umstellung hängt von "38% Mapping Network Interfaces on the Source Computer..." ab. bei Verwendung statischer IPS

Wenn Sie versuchen, einen Ausschneide Bereich eines Quell Computers auszuführen, wenn der Quellcomputer für die Verwendung einer neuen statischen (nicht DHCP-) IP-Adresse auf einer oder mehreren Netzwerkschnittstellen festgelegt wurde, bleibt die Ausschneide in der Phase "38% Mapping Netzwerkschnittstellen auf dem Quellcomputer..." hängen. und Sie erhalten den folgenden Fehler im Ereignisprotokoll für den Speicher Migrationsdienst:

```
Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Admin
Source:        Microsoft-Windows-StorageMigrationService-Proxy
Date:          11/13/2019 3:47:06 PM
Event ID:      20494
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      orc2019-rtm.corp.contoso.com
Description:
Couldn't set the IP address on the network adapter.

Computer: fs12.corp.contoso.com
Adapter: microsoft hyper-v network adapter
IP address: 10.0.0.99
Network mask: 16
Error: 40970
Error Message: Unknown error (0xa00a)

Guidance: Confirm that the Netlogon service on the computer is reachable through RPC and that the credentials provided are correct.
```

Die Untersuchung des Quell Computers zeigt, dass die ursprüngliche IP-Adresse nicht geändert werden kann.

Dieses Problem tritt nicht auf, wenn Sie auf dem Windows Admin Center-Bildschirm "Konfigurieren des Windows Admin Centers" die Option "DHCP verwenden" ausgewählt haben, nur wenn Sie eine neue statische IP-Adresse angeben.

Für dieses Problem gibt es zwei Lösungen:

1. Dieses Problem wurde zuerst durch das [KB4537818](https://support.microsoft.com/help/4537818/windows-10-update-kb4537818) -Update gelöst. Der vorherige Code Fehler verhinderte die Verwendung statischer IP-Adressen.

2. Wenn Sie auf den Netzwerkschnittstellen des Quell Computers keine Standard-Gateway-IP-Adresse angegeben haben, tritt dieses Problem auch mit dem KB4537818-Update auf. Um dieses Problem zu umgehen, legen Sie eine gültige Standard-IP-Adresse auf den Netzwerkschnittstellen fest, indem Sie das Applet Network Connections (NCPA.CPL) oder das PowerShell-Cmdlet Set-nettroute verwenden.

## <a name="slower-than-expected-re-transfer-performance"></a>Langsamer als erwartete erneute Übertragungsleistung

Nachdem Sie eine Übertragung abgeschlossen und dann eine nachfolgende erneute Übertragung derselben Daten ausgeführt haben, wird die Übertragungszeit möglicherweise nicht wesentlich verbessert, auch wenn sich in der Zwischenzeit nur wenige Daten auf dem Quell Server geändert haben.

Dies ist das erwartete Verhalten beim Übertragen einer sehr großen Anzahl von Dateien und von untergeordneten Ordnern. Die Größe der Daten ist nicht relevant. Wir haben zunächst Verbesserungen an diesem Verhalten in [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) vorgenommen und optimieren weiterhin die Übertragungsleistung. Um die Leistung weiter zu optimieren, lesen Sie [Optimieren von Inventur-und Übertragungsleistung](./faq.md#optimizing-inventory-and-transfer-performance).

## <a name="data-does-not-transfer-user-renamed-when-migrating-to-or-from-a-domain-controller"></a>Die Daten werden nicht übertragen, der Benutzer wurde bei der Migration zu oder von einem Domänen Controller umbenannt.

Nach dem Starten der Übertragung von oder zu einem Domänen Controller:

 1. Es werden keine Daten migriert, und auf dem Ziel werden keine Freigaben erstellt.
 2. Im Windows Admin Center wird ein rotes Fehler Symbol ohne Fehlermeldung angezeigt.
 3. Mindestens ein AD-Benutzer und eine lokale Domänen Gruppe haben den Namen und/oder das Anmelde Attribut vor Windows 2000 geändert.

 4. Das Ereignis 3509 wird im Orchestrator für den Speicher Migrationsdienst angezeigt:

    ```
    Log Name:      Microsoft-Windows-StorageMigrationService/Admin
    Source:        Microsoft-Windows-StorageMigrationService
    Date:          1/10/2020 2:53:48 PM
    Event ID:      3509
    Task Category: None
    Level:         Error
    Keywords:
    User:          NETWORK SERVICE
    Computer:      orc2019-rtm.corp.contoso.com
    Description:
    Couldn't transfer storage for a computer.

    Job: dctest3
    Computer: dc02-2019.corp.contoso.com
    Destination Computer: dc03-2019.corp.contoso.com
    State: Failed
    Error: 53251
    Error Message: Local accounts migration failed with error System.Exception: -2147467259
        at Microsoft.StorageMigration.Service.DeviceHelper.MigrateSecurity(IDeviceRecord sourceDeviceRecord, IDeviceRecord destinationDeviceRecord, TransferConfiguration config, Guid proxyId, CancellationToken cancelToken)
    ```

    Dies ist das erwartete Verhalten, wenn Sie versucht haben, von oder zu einem Domänen Controller mit Storage Migration Service zu migrieren und die Option "Benutzer und Gruppen migrieren" zum Umbenennen oder wieder verwenden von Konten verwendet haben. anstatt "Benutzer und Gruppen übertragen" auszuwählen. Die DC-Migration wird für [Storage Migration Service nicht unterstützt](faq.md). Da ein Domänen Controller nicht über echte lokale Benutzer und Gruppen verfügt, werden diese Sicherheits Prinzipale von Storage Migration Service wie bei der Migration zwischen zwei Mitglieds Servern behandelt, und es wird versucht, ACLs als angewiesen zu ändern. Dies führt zu den Fehlern und verkopierten oder kopierten Konten.

Wenn Sie die Übertragung bereits einmal ausgeführt haben, gehen Sie wie folgt vor:

 1. Verwenden Sie den folgenden AD PowerShell-Befehl für einen Domänen Controller, um geänderte Benutzer oder Gruppen zu suchen (Ändern von searchbase entsprechend dem definierten Domänen Namen):

    ```PowerShell
    Get-ADObject -Filter 'Description -like "*storage migration service renamed*"' -SearchBase 'DC=<domain>,DC=<TLD>' | ft name,distinguishedname
    ```

 2. Bearbeiten Sie für alle Benutzer, die mit Ihrem ursprünglichen Namen zurückgegeben werden, ihren "Benutzer Anmelde Namen (Pre-Windows 2000)", um das zufällige Zeichen Suffix zu entfernen, das von Storage Migration Service hinzugefügt wurde, sodass sich dieser Benutzer anmelden kann.

 3. Bearbeiten Sie für alle Gruppen, die mit Ihrem ursprünglichen Namen zurückgegeben werden, ihren "Gruppennamen (Pre-Windows 2000)", um das zufällige Zeichen Suffix zu entfernen, das von Storage Migration Service hinzugefügt wurde.

 4. Für alle deaktivierten Benutzer oder Gruppen, deren Namen jetzt ein durch Storage Migration Service hinzugefügtes Suffix enthalten, können Sie diese Konten löschen. Sie können überprüfen, ob Benutzerkonten zu einem späteren Zeitpunkt hinzugefügt wurden, da Sie nur die Gruppe "Domänen Benutzer" enthalten und ein erstelltes Datum/Uhrzeit-Wert für die Übertragungs Start Zeit des Speicher Migrations dienstan

    Wenn Sie Storage Migration Service mit Domänen Controllern zu Übertragungszwecken verwenden möchten, stellen Sie sicher, dass Sie immer "Benutzer und Gruppen nicht übertragen" im Windows Admin Center auf der Seite "Übertragungs Einstellungen" auswählen.

## <a name="error-53-failed-to-inventory-all-specified-devices-when-running-inventory"></a>Fehler 53: "Fehler beim Inventarisieren aller angegebenen Geräte" beim Ausführen des Inventars.

Wenn Sie versuchen, die Inventur auszuführen, erhalten Sie Folgendes:

```
Failed to inventory all specified devices

Log Name:      Microsoft-Windows-StorageMigrationService/Admin
Source:        Microsoft-Windows-StorageMigrationService
Date:          1/16/2020 8:31:17 AM
Event ID:      2516
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      ned.corp.contoso.com
Description:
Couldn't inventory files on the specified endpoint.
Job: ned1
Computer: ned.corp.contoso.com
Endpoint: hithere
State: Failed
File Count: 0
File Size in KB: 0
Error: 53
Error Message: Endpoint scan failed
Guidance: Check the detailed error and make sure the inventory requirements are met. This could be because of missing permissions on the source computer.

Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Debug
Source:        Microsoft-Windows-StorageMigrationService-Proxy
Date:          1/16/2020 8:31:17 AM
Event ID:      10004
Task Category: None
Level:         Critical
Keywords:
User:          NETWORK SERVICE
Computer:      ned.corp.contoso.com
Description:
01/16/2020-08:31:17.031 [Crit] Consumer Task failed with error:The network path was not found.
. StackTrace=   at Microsoft.Win32.RegistryKey.Win32ErrorStatic(Int32 errorCode, String str)
    at Microsoft.Win32.RegistryKey.OpenRemoteBaseKey(RegistryHive hKey, String machineName, RegistryView view)
    at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetEnvironmentPathFolders(String ServerName, Boolean IsServerLocal)
    at Microsoft.StorageMigration.Proxy.Service.Discovery.ScanUtils.<ScanSMBEndpoint>d__3.MoveNext()
    at Microsoft.StorageMigration.Proxy.EndpointScanOperation.Run()
    at Microsoft.StorageMigration.Proxy.Service.Discovery.EndpointScanRequestHandler.ProcessRequest(EndpointScanRequest scanRequest, Guid operationId)
    at Microsoft.StorageMigration.Proxy.Service.Discovery.EndpointScanRequestHandler.ProcessRequest(Object request)
    at Microsoft.StorageMigration.Proxy.Common.ProducerConsumerManager`3.Consume(CancellationToken token)

01/16/2020-08:31:10.015 [Erro] Endpoint Scan failed. Error: (53) The network path was not found.
Stack trace:
    at Microsoft.Win32.RegistryKey.Win32ErrorStatic(Int32 errorCode, String str)
    at Microsoft.Win32.RegistryKey.OpenRemoteBaseKey(RegistryHive hKey, String machineName, RegistryView view)
```

Zu diesem Zeitpunkt versucht der Speicher Migrationsdienst-Orchestrator, die Quellcomputer Konfiguration zu ermitteln, um die Konfiguration des Quell Computers zu bestimmen, wird jedoch vom Quell Server abgelehnt, was besagt, dass der Registrierungs Pfad nicht vorhanden ist. Mögliche Ursachen:

 - Der Remote Registrierungsdienst wird nicht auf dem Quellcomputer ausgeführt.
 - die Firewall lässt keine Remote Registrierungs Verbindungen mit dem Quell Server vom Orchestrator zu.
 - Das Quell Migrations Konto verfügt nicht über Remote Registrierungs Berechtigungen zum Herstellen einer Verbindung mit dem Quellcomputer.
 - Das Quell Migrations Konto verfügt nicht über Leseberechtigungen in der Registrierung des Quell Computers unter "HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows NT\CurrentVersion" oder unter "HKEY_LOCAL_MACHINE \system\currentcontrolset\services\lanmanserver".

## <a name="cutover-hangs-on-38-mapping-network-interfaces-on-the-source-computer"></a>Die Umstellung hängt von "38% Mapping Network Interfaces on the Source Computer..." ab.

Bei dem Versuch, einen Ausschneide Versuch eines Quell Computers auszuführen, bleibt die Ausschneide in der Phase "38% Mapping Netzwerkschnittstellen auf dem Quellcomputer..." hängen. und Sie erhalten den folgenden Fehler im Ereignisprotokoll für den Speicher Migrationsdienst:

```
Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Admin
Source:        Microsoft-Windows-StorageMigrationService-Proxy
Date:          1/11/2020 8:51:14 AM
Event ID:      20505
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      nedwardo.contosocom
Description:
Couldn't establish a CIM session with the computer.

Computer: 172.16.10.37
User Name: nedwardo\MsftSmsStorMigratSvc
Error: 40970
Error Message: Unknown error (0xa00a)

Guidance: Confirm that the Netlogon service on the computer is reachable through RPC and that the credentials provided are correct.
```

Dieses Problem wird durch Gruppenrichtlinie verursacht, bei der der folgende Registrierungs Wert auf dem Quellcomputer festgelegt wird: "HKEY_LOCAL_MACHINE \software\microsoft\windows\currentversion\policies\system\localaccountdekenfilterpolicy = 0"

Diese Einstellung ist nicht Bestandteil von Standard Gruppenrichtlinie, sondern ein Add-on, das mit dem [Microsoft Security Compliance Toolkit](https://www.microsoft.com/download/details.aspx?id=55319)konfiguriert wurde:

- Windows Server 2012 R2: "Computerkonfiguration\Administrative vorlagen\scm: Pass-the-Hash-entschärf\uac-Einschränkungen auf lokale Konten bei Netzwerk Anmeldungen anwenden"

- Windows Server 2016: "Computerkonfiguration\Administrative vorlagen\ms sicherheitssteuerungssteuerungs\uac-Einschränkungen auf lokale Konten bei Netzwerk Anmeldungen anwenden"

Sie kann auch mithilfe Gruppenrichtlinie Einstellungen mit einer benutzerdefinierten Registrierungs Einstellung festgelegt werden. Sie können das gpresult-Tool verwenden, um zu bestimmen, welche Richtlinie diese Einstellung auf den Quellcomputer anwendet.

Der Speicher Migrationsdienst aktiviert vorübergehend [localaccountdekenfilterpolicy](https://support.microsoft.com/help/951016/description-of-user-account-control-and-remote-restrictions-in-windows) als Teil des Ausschneide Prozesses und entfernt ihn anschließend. Wenn Gruppenrichtlinie ein in Konflikt stehender Gruppenrichtlinie Objekt (GPO) anwendet, wird der Speicher Migrationsdienst überschrieben und ein Ausschneide Vorgang verhindert.

Um dieses Problem zu umgehen, verwenden Sie eine der folgenden Optionen:

1. Verschieben Sie den Quellcomputer temporär aus der Active Directory Organisationseinheit, die dieses widersprüchliche GPO anwendet.
2. Deaktivieren Sie das GPO, das diese widersprüchliche Richtlinie anwendet, vorübergehend.
3. Temporäres Erstellen eines neuen Gruppenrichtlinien Objekts, das diese Einstellung auf deaktiviert festlegt und für bestimmte Organisationseinheiten der Quell Server gilt, die Vorrang vor anderen GPOs haben.

## <a name="inventory-or-transfer-fail-when-using-credentials-from-a-different-domain"></a>Inventar oder Übertragung schlägt fehl, wenn Anmelde Informationen aus einer anderen Domäne verwendet werden

Wenn Sie versuchen, eine Inventur oder Übertragung mit dem Speicher Migrationsdienst auszuführen und einen Windows-Server zu verwenden, während Sie die Migrations Anmelde Informationen von einer anderen Domäne als dem Zielserver verwenden, erhalten Sie die folgenden Fehler:
```
Exception from HRESULT:0x80131505

The server was unable to process the request due to an internal error

04/28/2020-11:31:01.169 [Error] Failed device discovery stage SystemInfo with error: (0x490) Could not find computer object 'myserver' in Active Directory    [d:\os\src\base\dms\proxy\discovery\discoveryproxy\DeviceDiscoveryOperation.cs::TryStage::1042]
```

Das weitere untersuchen der Protokolle zeigt, dass sich das Migrations Konto und der migrierte Server in unterschiedlichen Domänen befinden:

```
06/25/2020-10:11:16.543 [Info] Creating new job=NedJob user=**CONTOSO**\ned
[d:\os\src\base\dms\service\StorageMigrationService.IInventory.cs::CreateJob::133]
```

```
GetOsVersion(fileserver75.**corp**.contoso.com)    [d:\os\src\base\dms\proxy\common\proxycommon\CimSessionHelper.cs::GetOsVersion::66] 06/25/2020-10:20:45.368 [Info] Computer 'fileserver75.corp.contoso.com': OS version
```

Dieses Problem wird durch einen Code Fehler im Speicher Migrationsdienst verursacht. Um dieses Problem zu umgehen, verwenden Sie die Anmelde Informationen für die Migration aus derselben Domäne, zu der der Quell-und Zielcomputer gehören. Wenn der Quell-und Zielcomputer z. b. zur Domäne "Corp.contoso.com" in der Gesamtstruktur "contoso.com" gehören, verwenden Sie "corp\myaccount", um die Migration auszuführen, nicht die Anmelde Informationen "contoso\myaccount".

## <a name="inventory-fails-with-element-not-found"></a>Inventur schlägt fehl, weil das Element nicht gefunden wurde.

Betrachten Sie das folgende Szenario:

Sie verfügen über einen Quell Server mit einem DNS-Hostnamen und Active Directory Namen mit mehr als 15 Unicode-Zeichen, z. b. "iamaverylongcomputername". In Windows konnte der Legacy-NetBIOS-Name nicht so festgelegt werden, dass er so lange festgelegt wird, und warnte, als der Server benannt wurde, dass der NetBIOS-Name auf 15 Unicode-breit Zeichen gekürzt wird (Beispiel: "iamaverylongcom"). Wenn Sie versuchen, diesen Computer zu inventarisieren, erhalten Sie im Windows Admin Center und im Ereignisprotokoll Folgendes:

```DOS
"Element not found"
========================

Log Name:      Microsoft-Windows-StorageMigrationService/Admin
Source:        Microsoft-Windows-StorageMigrationService
Date:          4/10/2020 10:49:19 AM
Event ID:      2509
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      WIN-6PJAG3DHPLF.corp.contoso.com
Description:
Couldn't inventory a computer.

Job: longnametest
Computer: iamaverylongcomputername.corp.contoso.com
State: Failed
Error: 1168
Error Message:

Guidance: Check the detailed error and make sure the inventory requirements are met. The inventory couldn't determine any aspects of the specified source computer. This could be because of missing permissions or privileges on the source or a blocked firewall port.
```

Dieses Problem wird durch einen Code Fehler im Speicher Migrationsdienst verursacht. Die einzige Problem Umgehung besteht darin, den Computer so umzubenennen, dass er den gleichen Namen wie der NetBIOS-Name hat, und dann mit [netdom computername/Add](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc835082(v=ws.11)) einen alternativen Computernamen hinzuzufügen, der den längeren Namen enthält, der vor dem Start des Inventars verwendet wurde. Storage Migration Service unterstützt die Migration alternativer Computernamen.

## <a name="storage-migration-service-inventory-fails-with-a-parameter-cannot-be-found-that-matches-parameter-name-includedfsn"></a>Die Inventur des Speicher Migrations Dienstanbieter schlägt fehl, weil kein Parameter gefunden wurde, der mit dem Parameternamen "includedfsn" übereinstimmt. 

Wenn Sie die Version 2009 von Windows Admin Center zum Verwalten eines Windows Server 2019 Orchestrator verwenden, erhalten Sie die folgende Fehlermeldung, wenn Sie versuchen, eine Inventur für einen Quellcomputer durchführen zu können:

```
Remote exception : a parameter cannot be found that matches parameter name 'IncludeDFSN'" 
```

Aktualisieren Sie die Erweiterung "Storage Migration Service" auf mindestens Version 1.113.0 im Windows Admin Center, um das Problem zu beheben. Das Update sollte automatisch im Feed angezeigt werden und zur Installation aufgefordert werden.


## <a name="see-also"></a>Weitere Informationen

- [Übersicht über den Speicher Migrationsdienst](overview.md)
