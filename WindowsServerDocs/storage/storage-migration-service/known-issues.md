---
title: Bekannte Probleme bei Storage Migration Service
description: Bekannte Probleme und Problembehandlung für den Speicher Migrationsdienst, z. b. das Sammeln von Protokollen für Microsoft-Support.
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 02/10/2020
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: 77a23e5787283aa93d6f2f303cf45b461ccf52dd
ms.sourcegitcommit: f0fcfee992b76f1ad5dad460d4557f06ee425083
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2020
ms.locfileid: "77125111"
---
# <a name="storage-migration-service-known-issues"></a>Bekannte Probleme bei Storage Migration Service

Dieses Thema enthält Antworten auf bekannte Probleme bei der Verwendung von [Storage Migration Service](overview.md) zum Migrieren von Servern.

Storage Migration Service wird in zwei Teilen veröffentlicht: der-Dienst in Windows Server und die Benutzeroberfläche im Windows Admin Center. Der Dienst ist in Windows Server, langfristig Wartungs Kanal sowie Windows Server, halbjährlicher Kanal, verfügbar. Obwohl Windows Admin Center als separater Download verfügbar ist. Wir schließen auch regelmäßig Änderungen an kumulativen Updates für Windows Server ein, die über Windows Update veröffentlicht werden. 

Beispielsweise enthält Windows Server, Version 1903, neue Features und Korrekturen für den Speicher Migrationsdienst, die auch für Windows Server 2019 und Windows Server, Version 1809, verfügbar sind, indem Sie [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)installieren.

## <a name="collecting-logs"></a>Sammeln von Protokolldateien beim Arbeiten mit Microsoft-Support

Der Speicher Migrationsdienst enthält Ereignisprotokolle für den Orchestrator-Dienst und den Proxy Dienst. Der Orchestrator-Server enthält immer Ereignisprotokolle, und Zielserver, auf denen der Proxy Dienst installiert ist, enthalten die Proxy Protokolle. Diese Protokolle befinden sich unter:

- Anwendungs-und Dienst Protokolle \ Microsoft \ Windows \ storagemigrationservice
- Anwendungs-und Dienst Protokolle \ Microsoft \ Windows \ storagemigrationservice-Proxy

Wenn Sie diese Protokolle für die Offline Anzeige oder zum Senden an Microsoft-Support erfassen müssen, ist auf GitHub ein Open-Source-PowerShell-Skript verfügbar:

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

 >   Übertragungsprotokoll: Überprüfen Sie, ob die Dateifreigabe in der Firewall zulässig ist. : Dieser Anforderungs Vorgang, der an net. TCP://localhost: 28940/SMS/Service/1/Transfer gesendet wurde, hat innerhalb des konfigurierten Timeouts (00:01:00) keine Antwort empfangen. Die für diesen Vorgang vorgesehene Zeit war möglicherweise Teil eines längeren Timeouts. Die Ursache dafür könnte sein, dass der Dienst den Vorgang immer noch verarbeitet oder dass der Dienst keine Antwortmeldung senden konnte. Erhöhen Sie das Timeout für den Vorgang (indem Sie den Kanal/Proxy in IContextChannel umwandeln und die Eigenschaft OperationTimeout festlegen), und stellen Sie sicher, dass der Dienst eine Verbindung mit dem Client herstellen kann.

Dieses Problem wird durch eine extrem große Anzahl übertragener Dateien verursacht, die nicht in dem vom Speicher Migrationsdienst zulässigen Standard Timeout von einer Minute gefiltert werden können. 

So umgehen Sie dieses Problem:

1. Bearbeiten Sie auf dem Orchestrator-Computer die Datei *%systemroot%\SMS\Microsoft.StorageMigration.Service.exe.config* mithilfe von "Notepad. exe", um "SendTimeout" von der 1-minütigen Standardeinstellung in 10 Minuten zu ändern.

   ```
     <bindings>
      <netTcpBinding>
        <binding name="NetTcpBindingSms"
                 sendTimeout="00:01:00"
   ```

2. Starten Sie den Dienst "Storage Migration Service" auf dem Orchestrator-Computer neu. 
3. Starten Sie auf dem Orchestrator-Computer "regedit. exe".
4. Suchen Sie den folgenden Registrierungsunterschlüssel, und klicken Sie darauf: 

   `HKEY_LOCAL_MACHINE\Software\Microsoft\SMSPowershell`

5. Zeigen Sie im Menü „Bearbeiten“ auf „Neu“, und klicken Sie dann auf „DWORD-Wert“. 
6. Geben Sie "wcfoperationtimeoutinminutes" als Namen für das DWORD ein, und drücken Sie dann die EINGABETASTE.
7. Klicken Sie mit der rechten Maustaste auf "wcfoperationtimeoutinminutes", und klicken Sie dann auf ändern. 
8. Klicken Sie im Feld Base Data auf "Decimal".
9. Geben Sie im Feld Wertdaten den Wert "10" ein, und klicken Sie dann auf OK.
10. Beenden Sie den Registrierungs-Editor.
11. Es wird erneut versucht, die CSV-Datei mit Fehlern herunterzuladen. 

Wir beabsichtigen, dieses Verhalten in einer späteren Version von Windows Server 2019 zu ändern.  

## <a name="validation-warnings-for-destination-proxy-and-credential-administrative-privileges"></a>Validierungs Warnungen für den Ziel Proxy und Administratorrechte für Anmelde Informationen

Beim Validieren eines Übertragungs Auftrags werden folgende Warnungen angezeigt:

 > **Die Anmelde Informationen verfügen über Administratorrechte.**
 > Warnung: die Aktion ist nicht Remote verfügbar.
 > **Der Ziel Proxy ist registriert.**
 > Warnung: der Ziel Proxy wurde nicht gefunden.

Wenn Sie den Speicher Migrationsdienst-Proxy Dienst auf dem Windows Server 2019-Zielcomputer nicht installiert haben, oder wenn der Zielcomputer Windows Server 2016 oder Windows Server 2012 R2 ist, ist dieses Verhalten Entwurfs bedingt. Es wird empfohlen, zu einem Windows Server 2019-Computer zu migrieren, auf dem der Proxy installiert ist  

## <a name="certain-files-do-not-inventory-or-transfer-error-5-access-is-denied"></a>Bestimmte Dateien werden nicht inventarisiert oder übertragen, Fehler 5: "Zugriff verweigert"

Bei der Inventarisierung oder Übertragung von Dateien von einer Quell-auf einen Zielcomputer können Dateien, von denen ein Benutzer die Administrator Gruppenberechtigungen entfernt hat, nicht migriert werden. Überprüfen des Speicher Migrations Dienstanbieter: Proxy Debug zeigt Folgendes an:

  Protokoll Name: Microsoft-Windows-storagemigrationservice-Proxy/debugquelle: Microsoft-Windows-storagemigrationservice-Proxy Date: 2/26/2019 9:00:04 am Ereignis-ID: 10000 Aufgaben Kategorie: keine Ebene: Fehler Schlüsselwörter:      
  Benutzer: Netzwerkdienst Computer: SRV1.contoso.com Beschreibung:

  02/26/2019-09:00:04.860 [Fehler] Übertragungsfehler für \\SRV1. ". com\public\indy.png: (5)" wurde verweigert.
Stapel Überwachung: bei Microsoft. storagemigration. Proxy. Service. Transfer. filedirutils. OpenFile (Zeichenfolge Dateiname, desiredAccess desiredAccess, share Mode Share Mode, kreationdisposition erationdisposition, flagsandattribute flagsandattribute) unter Microsoft. storagemigration. Proxy. Service. Transfer. filedirutils. gettargetfile (Zeichen folgen Pfad) bei Microsoft. storagemigration. Proxy. Service. Transfer. filedirutils. gettargetfile (FileInfo-Datei) unter Microsoft. storagemigration. Proxy. Service. Transfer. Filetransfer. initializesourcefileingefo () bei Microsoft. storagemigration. Proxy. Service. Transfer. Filetransfer. Transfer () at Microsoft. storagemigration. Proxy. Service. Transfer. Filetransfer. trytransfer () [d:\os\src\base\dms\proxy\transfer\transferproxy\filetransfer.cs:: trytransfer:: 55]


Dieses Problem wird durch einen Code Fehler im Speicher Migrationsdienst verursacht, bei dem die Sicherungs Berechtigung nicht aufgerufen wurde. 

Um dieses Problem zu beheben, installieren Sie [Windows Update 2. April 2019 – KB4490481 (OS Build 17763,404)](https://support.microsoft.com/help/4490481/windows-10-update-kb4490481) auf dem Orchestrator-Computer und dem Zielcomputer, wenn der Proxy Dienst dort installiert ist. Stellen Sie sicher, dass das Benutzerkonto der Quell Migration ein lokaler Administrator auf dem Quellcomputer und der Orchestrator für den Speicher Migrationsdienst ist. Stellen Sie sicher, dass das Benutzerkonto für die Ziel Migration ein lokaler Administrator auf dem Zielcomputer und der Orchestrator für den Speicher Migrationsdienst ist. 

## <a name="dfsr-hashes-mismatch-when-using-storage-migration-service-to-preseed-data"></a>Nicht übereinstimmende DFSR-Hashes bei der Verwendung von Storage Migration Service zum vorab Seed von Daten

Wenn Sie den Speicher Migrationsdienst zum Übertragen von Dateien an ein neues Ziel verwenden, können Sie die DFS-Replikation (DFSR) zum Replizieren dieser Daten mit einem vorhandenen DFSR-Server über die vorab bereitgestellte Replikation oder das Klonen von DFSR-Datenbanken konfigurieren. nicht übereinstimmende und werden erneut repliziert. Die Datenströme, Sicherheitsdaten Ströme, Größen und Attribute werden nach der Verwendung von SMS für die Übertragung der Datenströme angezeigt. Wenn Sie die Dateien mit icacls oder dem Klon Debugprotokoll der DFSR-Datenbank untersuchen, werden folgende

Quelldatei:

  icacls d:\test\quelle:

  icacls d:\test\thatcher.png/Save out. txt/t Thatcher. png d:Ai (A;; FA;;; BA) (A;; 0 x1200a9;;;D D) (A;; 0 x1301bf;;;D U) (A; ID; FA;;; BA) (A; ID; FA;;; SY) (A; ID; 0x1200a9;;; ECM

Zieldatei:

  icacls d:\test\thatcher.png/Save out. txt/t Thatcher. png d:Ai (A;; FA;;; BA) (A;; 0 x1301bf;;;D U) (A;; 0 x1200a9;;;D D) (A; ID; FA;;; BA) (A; ID; FA;;; SY) (A; ID; 0x1200a9;;; BU)**S: PAINO_ACCESS_CONTROL**

DFSR-Debugprotokoll:

  20190308 10:18:53.116 3948 dbcl 4045 [warn] dbclone:: idtableimportupdate-Konflikt Daten Satz gefunden. 

  Lokaler ACL-Hash: 1bcdfe03-A18BCE01-D1AE9859-23a0a5f 6 LastWrite-Time: 20190308 18:09:44.876 filesizelow: 1131654 filesizehigh: 0 Attribute: 32 

  Klon-ACL-Hash:**DDC4FCE4-DDF329C4-977ced6d-F4D72A5B** LastWrite-Time: 20190308 18:09:44.876 filesizelow: 1131654 filesizehigh: 0 Attribute: 32 

Dieses Problem wurde durch das [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) -Update behoben.

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-when-transferring-from-windows-server-2008-r2"></a>Fehler "der Speicher konnte bei der Übertragung von Windows Server 2008 R2 nicht an einen der Endpunkte übertragen werden.

Beim Versuch, Daten von einem Windows Server 2008 R2-Quellcomputer zu übertragen, erhalten Sie keine Datenübertragungen, und Sie erhalten eine Fehlermeldung:  

  Der Speicher konnte auf keinem der Endpunkte übertragen werden.
0x9044

Dieser Fehler wird erwartet, wenn Ihr Windows Server 2008 R2-Computer nicht vollständig mit allen kritischen und wichtigen Updates von Windows Update gepatcht ist. Unabhängig vom Speicher Migrationsdienst empfehlen wir immer, einen Windows Server 2008 R2-Computer zu Sicherheitszwecken zu patchen, da dieses Betriebssystem nicht die Sicherheitsverbesserungen von neueren Versionen von Windows Server enthält.

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-and-check-if-the-source-device-is-online---we-couldnt-access-it"></a>Fehler "der Speicher konnte nicht an einen der Endpunkte übertragen werden", und "Überprüfen Sie, ob das Quellgerät Online ist-wir konnten nicht darauf zugreifen."

Beim Versuch, Daten von einem Quellcomputer zu übertragen, werden einige oder alle Freigaben nicht übertragen, zusammenfassende Fehler:

   Der Speicher konnte auf keinem der Endpunkte übertragen werden.
0x9044

Die Überprüfung der Details zur SMB-Übertragung zeigt Folgendes

   Überprüfen Sie, ob das Quellgerät Online ist-wir konnten nicht darauf zugreifen.

Die Untersuchung des storagemigrationservice/Admin-Ereignis Protokolls zeigt Folgendes:

   Speicher konnte nicht übertragen werden.

   Job: den job1-ID:  
   Status: Fehler: 36931 Fehlermeldung: 

   Leitfaden: Überprüfen Sie den detaillierten Fehler, und stellen Sie sicher, dass die Übertragungsanforderungen erfüllt sind. Der Übertragungs Auftrag konnte keine Quell-und Zielcomputer übertragen. Dies kann darauf zurückzuführen sein, dass der Orchestrator-Computer keinen Quell-oder Zielcomputer erreichen konnte, möglicherweise aufgrund einer Firewallregel oder fehlender Berechtigungen.

Die Untersuchung des storagemigrationservice-Proxy/Debug-Protokolls zeigt Folgendes:

   07/02/2019-13:35:57.231 [Fehler] Fehler bei der Überprüfung der Übertragung. ErrorCode: 40961, der Quell Endpunkt ist nicht erreichbar oder nicht vorhanden, oder die Quell Anmelde Informationen sind ungültig, oder der authentifizierte Benutzer verfügt nicht über ausreichende Zugriffsberechtigungen.
bei Microsoft. storagemigration. Proxy. Service. Transfer. transferoperation. Validate () bei Microsoft. storagemigration. Proxy. Service. Transfer. transferrequesthandler. ProcessRequest (filetransferrequest filetransferrequest, GUID operationId)    [d:\os\src\base\dms\proxy\transfer\transferproxy\transferrequesthandler.cs::

Dies war ein Code Fehler, der Manifest, wenn Ihr Migrations Konto nicht mindestens über Leseberechtigungen für die SMB-Freigaben verfügt. Dieses Problem wurde zuerst im kumulativen Update [4520062](https://support.microsoft.com/help/4520062/windows-10-update-kb4520062)behoben. 

## <a name="error-0x80005000-when-running-inventory"></a>Fehler 0x80005000 beim Ausführen des Inventars.

Nach der Installation von [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) und dem Versuch, das Inventar auszuführen, schlägt die Inventur mit Fehlern fehl

  Ausnahme von HRESULT: 0x80005000
  
  Protokoll Name: Microsoft-Windows-storagemigrationservice/Administrator Quelle: Microsoft-Windows-storagemigrationservice Date: 9/9/2019 5:21:42 pm Ereignis-ID: 2503 Aufgaben Kategorie: keine Ebene: Fehler Schlüsselwörter:      
  Benutzer: Netzwerkdienst Computer: FS02. TailwindTraders.net Description: die Computer konnten nicht inventarisiert werden.
Auftrag: foo2 ID: 20ac3f75-4945-41d1-9a79-d11dbb57798b State: failed Error: Fehlermeldung: 36934 Fehlermeldung: Fehler bei Inventur für alle Geräte Anleitung: Überprüfen Sie den detaillierten Fehler, und stellen Sie sicher, dass die Inventur Anforderungen erfüllt sind. Der Auftrag konnte keinen der angegebenen Quellcomputer inventarisieren. Dies kann darauf zurückzuführen sein, dass der Orchestrator-Computer ihn nicht über das Netzwerk erreichen konnte, möglicherweise aufgrund einer Firewallregel oder fehlender Berechtigungen.
  
  Protokoll Name: Microsoft-Windows-storagemigrationservice/Administrator Quelle: Microsoft-Windows-storagemigrationservice Date: 9/9/2019 5:21:42 pm Ereignis-ID: 2509 Aufgaben Kategorie: keine Ebene: Fehler Schlüsselwörter:      
  Benutzer: Netzwerkdienst Computer: FS02. TailwindTraders.net Description: der Computer konnte nicht inventarisiert werden.
Auftrag: foo2 Computer: FS01. TailwindTraders.net State: failed Error:-2147463168 Error Message: Anleitung: Überprüfen Sie den detaillierten Fehler, und stellen Sie sicher, dass die Inventur Anforderungen erfüllt sind. Das Inventar konnte keine Aspekte des angegebenen Quell Computers ermitteln. Dies kann daran liegen, dass fehlende Berechtigungen oder Berechtigungen für die Quelle oder einen gesperrten Firewallport vorhanden sind.
  
Dieser Fehler wird durch einen Code Fehler im Speicher Migrationsdienst verursacht, wenn Sie Migrations Anmelde Informationen in Form eines Benutzer Prinzipal namens (User Principal Name, UPN) bereitstellen, z. b. "meghan@contoso.com". Der Orchestrator-Dienst des Speicher Migrations Dienstanbieter kann dieses Format nicht ordnungsgemäß analysieren, was zu einem Fehler bei einer Domänen Suche führt, die zur Unterstützung der Cluster Migration in KB4512534 und 19h1 hinzugefügt wurde.

Um dieses Problem zu umgehen, geben Sie Anmelde Informationen im Format "Domäne \ Benutzer" an, z. b. "contoso\meghan".

## <a name="error-serviceerror0x9006-or-the-proxy-isnt-currently-available-when-migrating-to-a-windows-server-failover-cluster"></a>Fehler "ServiceError0x9006" oder "der Proxy ist zurzeit nicht verfügbar." beim Migrieren zu einem Windows Server-Failovercluster

Wenn Sie versuchen, Daten auf einen Cluster Datei Server zu übertragen, erhalten Sie folgende Fehlermeldung: 

   Stellen Sie sicher, dass der Proxy Dienst installiert ist und ausgeführt wird, und wiederholen Sie dann den Vorgang. Der Proxy ist zurzeit nicht verfügbar.
0x9006 ServiceError0x9006, Microsoft. storagemigration. Commands. unregistersmsproxycommand

Dieser Fehler wird erwartet, wenn die Datei Server Ressource vom ursprünglichen Windows Server 2019-Cluster Besitzer Knoten auf einen neuen Knoten verschoben wurde und die Proxy Funktion für den Speicher Migrationsdienst nicht auf diesem Knoten installiert wurde.

Um dieses Problem zu umgehen, verschieben Sie die Ressource des Ziel Dateiservers zurück auf den ursprünglichen Besitzer Cluster Knoten, der bei der ersten Konfiguration der Übertragungs Paare verwendet wurde.

Als Alternative Problem Umgehung:

1. Installieren Sie das Feature "Speicher Migrationsdienst-Proxy" auf allen Knoten in einem Cluster.
2. Führen Sie den folgenden PowerShell-Befehl für den Speicher Migrationsdienst auf dem Orchestrator-Computer aus: 

   ```PowerShell
   Register-SMSProxy -ComputerName *destination server* -Force
   ```
## <a name="error-dll-was-not-found-when-running-inventory-from-a-cluster-node"></a>Fehler "dll wurde nicht gefunden" beim Ausführen des Inventars von einem Cluster Knoten

Wenn Sie versuchen, eine Inventur mit dem Speicher Migrationsdienst auszuführen und ein Windows Server-Failovercluster mit der allgemeinen Datei Server Quelle zu verwenden, erhalten Sie die folgenden Fehler:

    DLL not found
    [Error] Failed device discovery stage VolumeInfo with error: (0x80131524) Unable to load DLL 'Microsoft.FailoverClusters.FrameworkSupport.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)   

Um dieses Problem zu umgehen, installieren Sie die Failovercluster-Verwaltungs Tools (RSAT-Clustering-Mgmt) auf dem Server, auf dem der Orchestrator für den Speicher Migrationsdienst ausgeführt wird. 

## <a name="error-there-are-no-more-endpoints-available-from-the-endpoint-mapper-when-running-inventory-against-a-windows-server-2003-source-computer"></a>Fehler "Es sind keine weiteren Endpunkte von der Endpunkt Zuordnung verfügbar", wenn die Inventur auf einem Windows Server 2003-Quellcomputer ausgeführt wird.

Wenn Sie versuchen, die Inventur mit dem für den Speicher Migrationsdienst Orchestrator-Server mit dem kumulativen Update für [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) oder später auszuführen, erhalten Sie die folgende Fehlermeldung:

    There are no more endpoints available from the endpoint mapper  

Um dieses Problem zu umgehen, deinstallieren Sie das kumulative Update KB4512534 (und ggf. das kumulative Update) vorübergehend über den Orchestrator-Computer des Speicher Migrations Dienstanbieter. Installieren Sie nach Abschluss der Migration das aktuellste kumulative Update neu.  

Beachten Sie, dass es unter bestimmten Umständen dazu führen kann, dass der Speicher Migrationsdienst nicht mehr gestartet wird, wenn Sie KB4512534 oder seine ersetzenden Updates deinstallieren Um dieses Problem zu beheben, können Sie die Speicher Migrationsdienst-Datenbank sichern und löschen:

1.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, bei der Sie ein Mitglied der Administratoren auf dem Orchestrator-Server für den Speicher Migrationsdienst sind, und führen Sie Folgendes aus:

     ```
     TAKEOWN /d y /a /r /f c:\ProgramData\Microsoft\StorageMigrationService
     
     MD c:\ProgramData\Microsoft\StorageMigrationService\backup

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService\* /grant Administrators:(GA)

     XCOPY c:\ProgramData\Microsoft\StorageMigrationService\* .\backup\*

     DEL c:\ProgramData\Microsoft\StorageMigrationService\* /q

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService  /GRANT networkservice:F /T /C

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService /GRANT networkservice:(GA) /T /C
     ```
   
2.  Starten Sie den Dienst "Storage Migration Service", mit dem eine neue Datenbank erstellt wird.

## <a name="error-clusctl_resource_netname_repair_vco-failed-against-netname-resource-and-windows-server-2008-r2-cluster-cutover-fails"></a>Fehler "Fehler beim CLUSCTL_RESOURCE_NETNAME_REPAIR_VCO für die NetName-Ressource", und der Windows Server 2008 R2-Cluster-cudever schlägt fehl

Bei dem Versuch, einen Ausschneiden einer Windows Server 2008 R2-Cluster Quelle auszuführen, bleibt die Ausschneide in der Phase "Umbenennen des Quell Computers..." hängen. und Sie erhalten die folgende Fehlermeldung:

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

Dieses Problem wird durch eine fehlende API in älteren Versionen von Windows Server verursacht. Zurzeit gibt es keine Möglichkeit, Windows Server 2008-und Windows Server 2003-Cluster zu migrieren. Sie können eine Inventur und Übertragung ohne Probleme auf Windows Server 2008 R2-Clustern durchführen und dann die Umstellung manuell durchführen, indem Sie die Ressource "NetName" und die IP-Adresse des Cluster Quelldatei Servers manuell ändern und dann den Ziel Cluster NetName und IP ändern. Adresse, die der ursprünglichen Quelle entspricht. 

## <a name="cutover-hangs-on-38-mapping-network-interfaces-on-the-source-computer"></a>Die Umstellung hängt von "38% Mapping Network Interfaces on the Source Computer..." ab. 

Wenn Sie versuchen, einen Ausschneide eines Quell Computers auszuführen, wenn der Quellcomputer für die Verwendung einer neuen statischen (nicht DHCP-) IP-Adresse auf einer oder mehreren Netzwerkschnittstellen festgelegt wurde, bleibt der Ausschneide Schritt in der Phase "38% Mapping Network Interfaces on the Source comnputer..." und Sie erhalten die folgende Fehlermeldung im SMS-Ereignisprotokoll:

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

Die Untersuchung des Quell Computers zeigt, dass die ursprüngliche IP-Adresse nicht geändert werden kann. 

Dieses Problem tritt nicht auf, wenn Sie auf dem Windows Admin Center-Bildschirm "Konfiguration konfigurieren" die Option "DHCP verwenden" ausgewählt haben, nur wenn Sie eine neue statische IP-Adresse, ein Subnetz und ein Gateway angeben. 

Dieses Problem wird durch eine Regression in der [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) -Aktualisierung verursacht. Es gibt zurzeit zwei Problem Umgehungen für dieses Problem:

  - Vor dem Ausschneiden: Wenn Sie keine neue statische IP-Adresse auf dem Cutover festgelegt haben, wählen Sie "DHCP verwenden" aus, und stellen Sie sicher, dass ein DHCP-Bereich dieses Subnetz abdeckt. SMS konfiguriert den Quellcomputer für die Verwendung von DHCP auf Quellcomputer Schnittstellen, und die überschneidet wird normal fortgesetzt. 
  
  - Wenn das Ausschneiden bereits unterbrochen ist: Melden Sie sich beim Quellcomputer an, und aktivieren Sie DHCP auf seinen Netzwerkschnittstellen, nachdem Sie sichergestellt haben, dass ein DHCP-Bereich dieses Subnetz abdeckt. Wenn der Quellcomputer eine von DHCP bereitgestellte IP-Adresse erhält, fährt SMS mit der Kürzung fort.
  
Wenn beide Problem Umgehungen abgeschlossen sind, können Sie nach Abschluss des Ausschnitts eine statische IP-Adresse auf dem alten Quellcomputer festlegen, und Sie können DHCP nicht mehr verwenden.   

## <a name="slower-than-expected-re-transfer-performance"></a>Langsamer als erwartete erneute Übertragungsleistung

Nachdem Sie eine Übertragung abgeschlossen und dann eine nachfolgende erneute Übertragung derselben Daten ausgeführt haben, wird die Übertragungszeit möglicherweise nicht wesentlich verbessert, auch wenn sich in der Zwischenzeit nur wenige Daten auf dem Quell Server geändert haben.

Dies ist das erwartete Verhalten beim Übertragen einer sehr großen Anzahl von Dateien und von untergeordneten Ordnern. Die Größe der Daten ist nicht relevant. Wir haben zunächst Verbesserungen an diesem Verhalten in [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) vorgenommen und optimieren weiterhin die Übertragungsleistung. Um die Leistung weiter zu optimieren, lesen Sie [Optimieren von Inventur-und Übertragungsleistung](https://docs.microsoft.com/windows-server/storage/storage-migration-service/faq#optimizing-inventory-and-transfer-performance).

## <a name="data-does-not-transfer-user-renamed-when-migrating-to-or-from-a-domain-controller"></a>Die Daten werden nicht übertragen, der Benutzer wurde bei der Migration zu oder von einem Domänen Controller umbenannt.

Nach dem Starten der Übertragung von oder zu einem Domänen Controller:

 1. Es werden keine Daten migriert, und auf dem Ziel werden keine Freigaben erstellt.
 2. Im Windows Admin Center wird ein rotes Fehler Symbol ohne Fehlermeldung angezeigt.
 3. Mindestens ein AD-Benutzer und eine lokale Domänen Gruppe haben den Namen und/oder das Anmelde Attribut vor Windows 2000 geändert.
 4. Das Ereignis 3509 wird im SMS-Orchestrator angezeigt:
 
 Protokoll Name: Microsoft-Windows-storagemigrationservice/Administrator Quelle: Microsoft-Windows-storagemigrationservice Date: 1/10/2020 2:53:48 pm Ereignis-ID: 3509 Aufgaben Kategorie: keine Ebene: Fehler Schlüsselwörter:      
 Benutzer: Netzwerkdienst Computer: orc2019-RTM.Corp.contoso.com Description: der Speicher für einen Computer konnte nicht übertragen werden.

 Auftrag: dctest3 Computer: dc02-2019.Corp.contoso.com Zielcomputer: DC03-2019.Corp.contoso.com Status: Fehler: 53251 Fehlermeldung: Fehler bei der Migration lokaler Konten mit Fehler System. Ausnahme:-2147467259 bei Microsoft. storagemigration. Service. devicehelper. MigrateSecurity (idevicerecord sourcedevicerecord, idevicerecord destinationdevicerecord, transferconfiguration config, GUID proxyid, CancellationToken canceltoken)

Dies ist das erwartete Verhalten, wenn Sie versucht haben, von oder zu einem Domänen Controller mit Storage Migration Service zu migrieren und die Option "Benutzer und Gruppen migrieren" zum Umbenennen oder wieder verwenden von Konten verwendet haben. anstatt "Benutzer und Gruppen übertragen" auszuwählen. Die DC-Migration wird für [Storage Migration Service nicht unterstützt](faq.md). Da ein Domänen Controller nicht über echte lokale Benutzer und Gruppen verfügt, werden diese Sicherheits Prinzipale von Storage Migration Service wie bei der Migration zwischen zwei Mitglieds Servern behandelt, und es wird versucht, ACLs als angewiesen zu ändern. Dies führt zu den Fehlern und verkopierten oder kopierten Konten. 

Wenn Sie die Übertragung bereits einmal ausgeführt haben, gehen Sie wie folgt vor:

 1. Verwenden Sie den folgenden AD PowerShell-Befehl für einen Domänen Controller, um geänderte Benutzer oder Gruppen zu suchen (Ändern von searchbase entsprechend dem Domänen Namen Ihres Domänen Namens): 

    ```PowerShell
    Get-ADObject -Filter 'Description -like "*storage migration service renamed*"' -SearchBase 'DC=<domain>,DC=<TLD>' | ft name,distinguishedname
    ```
   
 2. Bearbeiten Sie für alle Benutzer, die mit Ihrem ursprünglichen Namen zurückgegeben werden, ihren "Benutzer Anmelde Namen (Pre-Windows 2000)", um das zufällige Zeichen Suffix zu entfernen, das von Storage Migration Service hinzugefügt wurde, sodass sich dieser Verlierer anmelden kann.
 3. Bearbeiten Sie für alle Gruppen, die mit Ihrem ursprünglichen Namen zurückgegeben werden, ihren "Gruppennamen (Pre-Windows 2000)", um das zufällige Zeichen Suffix zu entfernen, das von Storage Migration Service hinzugefügt wurde.
 4. Für alle deaktivierten Benutzer oder Gruppen, deren Namen jetzt ein durch Storage Migration Service hinzugefügtes Suffix enthalten, können Sie diese Konten löschen. Sie können überprüfen, ob Benutzerkonten zu einem späteren Zeitpunkt hinzugefügt wurden, da Sie nur die Gruppe "Domänen Benutzer" enthalten und ein erstelltes Datum/Uhrzeit-Wert für die Übertragungs Start Zeit des Speicher Migrations dienstan
 
 Wenn Sie Storage Migration Service mit Domänen Controllern zu Übertragungszwecken verwenden möchten, stellen Sie sicher, dass Sie immer "Benutzer und Gruppen nicht übertragen" im Windows Admin Center auf der Seite "Übertragungs Einstellungen" auswählen.
 
 ## <a name="error-53-failed-to-inventory-all-specified-devices-when-running-inventory"></a>Fehler 53: "Fehler beim Inventarisieren aller angegebenen Geräte" beim Ausführen des Inventars. 

Wenn Sie versuchen, die Inventur auszuführen, erhalten Sie Folgendes:

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

Zu diesem Zeitpunkt versucht der Speicher Migrationsdienst-Orchestrator, die Quellcomputer Konfiguration zu ermitteln, um die Konfiguration des Quell Computers zu bestimmen, wird jedoch vom Quell Server abgelehnt, was besagt, dass der Registrierungs Pfad nicht vorhanden ist. Folgende Ursachen sind möglich:

 - Der Remote Registrierungsdienst wird auf dem Quellcomputer nicht ausgeführt.
 - die Firewall lässt keine Remote Registrierungs Verbindungen mit dem Quell Server vom Orchestrator zu.
 - Das Quell Migrations Konto verfügt nicht über Remote Registrierungs Berechtigungen zum Herstellen einer Verbindung mit dem Quellcomputer.
 - Das Quell Migrations Konto verfügt nicht über Leseberechtigungen in der Registrierung des Quell Computers unter "HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows NT\CurrentVersion" oder unter "HKEY_LOCAL_MACHINE \system\currentcontrolset\services\". LanManServer

## <a name="see-also"></a>Siehe auch

- [Übersicht über den Speicher Migrationsdienst](overview.md)
