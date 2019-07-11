---
title: Speicherung Datenbankmigrationsdienst bekannte Probleme
description: Bekannte Probleme und Supportinformationen zur Problembehandlung für Storage-Migration-Dienst, wie das Sammeln von Protokollen für Microsoft-Support.
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 07/09/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: 08156a09491d66016b5fcfe6056ed318d682b987
ms.sourcegitcommit: 514d659c3bcbdd60d1e66d3964ede87b85d79ca9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67735161"
---
# <a name="storage-migration-service-known-issues"></a>Speicherung Datenbankmigrationsdienst bekannte Probleme

Dieses Thema enthält Antworten auf die bekannten Probleme bei der Verwendung von [Speicherung Datenbankmigrationsdienst](overview.md) Servern zu migrieren.

## <a name="collecting-logs"></a> Sammeln von Protokolldateien bei der Arbeit mit Microsoft-Support

Die Storage-Migration-Dienst enthält die Ereignisprotokolle für den Orchestrator-Dienst und dem Anwendungsproxydienst. Der Server Urchestrator enthält immer beide Ereignisprotokolle und Zielserver mit dem anwendungsproxydienst installiert enthalten die Proxyprotokolle. Diese Protokolle befinden sich unter:

- Anwendungs- und Dienstprotokolle \ Microsoft \ Windows \ StorageMigrationService
- Anwendungs- und Dienstprotokolle \ Microsoft \ Windows \ StorageMigrationService-Proxy

Wenn Sie diese Protokolle für die Offlineanzeige sammeln oder an Microsoft Support senden müssen, ist es eine open-Source-PowerShell-Skripts auf GitHub verfügbar:

 [Storage-Migration-Dienst-Hilfsprogramm](https://aka.ms/smslogs) 

Infodatei für die Nutzung.

## <a name="storage-migration-service-doesnt-show-up-in-windows-admin-center-unless-managing-windows-server-2019"></a>Storage Migration-Dienst wird nicht in Windows Admin Center angezeigt, wenn die Verwaltung von Windows Server-2019

Wenn Sie die 1809-Version von Windows Admin Center zum Verwalten von einem Windows Server-2019 "Orchestrator" verwenden, werden keine die Tool-Option für Storage-Migration-Dienst angezeigt. 

Die Windows Admin Center Storage Migration Service-Erweiterung ist Version-Grenze für die alleinige Verwaltung von Windows Server-2019 Version 1809 oder höher. Wenn Sie ihn zum Verwalten von älteren Windows Server-Betriebssystemen oder Insider Preview-Versionen verwenden, wird das Tool nicht angezeigt. Dieses Verhalten ist entwurfsbedingt. 

Um zu beheben, verwenden, oder ein upgrade auf Windows Server-2019 Build 1809 oder höher.

## <a name="storage-migration-service-doesnt-let-you-choose-static-ip-on-cutover"></a>Speicherung Datenbankmigrationsdienst können nicht Sie statische IP-Adresse für die Umstellung auswählen.

Bei Verwendung der 0.57 Version von Storage Migration Service-Erweiterung in Windows Admin Center, und Sie die Umstellung Phase zu erreichen, können nicht Sie eine statische IP-Adresse für eine Adresse auswählen. Sie sind gezwungen, DHCP zu verwenden.

Zum Beheben dieses Problems in Windows Admin Center, suchen Sie unter **Einstellungen** > **Erweiterungen** für eine Benachrichtigung angezeigt wird die aktualisierte Version Speicherung Datenbankmigrationsdienst 0.57.2 für die Installation verfügbar ist. Sie müssen möglicherweise Ihre Registerkarte ' Browser ', für Windows-Admin Center neu zu starten.

## <a name="storage-migration-service-cutover-validation-fails-with-error-access-is-denied-for-the-token-filter-policy-on-destination-computer"></a>Speicherung Datenbankmigrationsdienst Umstellung Validierung schlägt fehl mit Fehler "Zugriff verweigert für die Richtlinie tokenfilter auf Zielcomputer"

Bei der Umstellung Überprüfung ausgeführt wird, wird die Fehlermeldung "Fehler: Zugriff für die Richtlinie tokenfilter auf Zielcomputer verweigert." Dies tritt auf, auch wenn Sie richtig lokale Administratoranmeldeinformationen für die sowohl die Quell-und Zielcomputer bereitgestellt.

Dieses Problem wird durch einen Codefehler in Windows Server-2019 verursacht. Das Problem treten auf, wenn Sie den Zielcomputer als ein Dienstorchestrator des Storage-Migration verwenden.

Um dieses Problem zu umgehen, installieren Sie den Storage-Migration-Dienst auf einem 2019 für Windows Server-Computer, der nicht die gewünschten Migrationsziel ist dann eine Verbindung mit diesem Server mit Windows Admin Center herstellen Sie, und führen Sie die Migration.

Wir haben dies in einer späteren Version von Windows Server behoben. Öffnen Sie eine Supportanfrage über [Microsoft-Support](https://support.microsoft.com) zum Anfordern einer Backport von diesem Fix erstellt werden.

## <a name="storage-migration-service-isnt-included-in-windows-server-2019-evaluation-edition"></a>Storage-Migration-Dienst ist in der Evaluierungsversion von Windows Server 2019 nicht enthalten.

Wenn Windows Admin Center zum Herstellen einer Verbindung mit einem [Evaluierungsversion von Windows Server 2019](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) gibt es keine Option zum Verwalten von Storage-Migration-Dienst. Storage-Migration-Dienst ist nicht auch in Rollen und Features enthalten.

Dieses Problem wird durch ein servicing Problem in die Evaluierungsmedien von Windows Server-2019 verursacht. 

Um dieses Problem zu umgehen, installieren Sie eine Verkaufsversion, MSDN, OEM oder einem Volume License-Version von Windows Server-2019 aus, und aktivieren Sie nicht. Arbeiten ohne Aktivierung alle Editionen von Windows Server im auswertungsmodus für 180 Tage. 

Wir haben dieses Problem in einer späteren Version von Windows Server-2019 behoben.  

## <a name="storage-migration-service-times-out-downloading-the-transfer-error-csv"></a>Storage Migration-Dienst ein Timeout auftritt, die Fehler beim Übertragen der CSV-Download

Wenn Windows Admin Center oder PowerShell verwenden die Übertragung Vorgänge ausführliche Fehler nur CSV-Protokoll herunterladen, erhalten Sie Fehler auf:

 >   Übertragungsprotokoll – überprüfen Sie, ob die Freigabe von Dateien in Ihrer Firewall zulässig ist. : Dieser Anforderungsvorgang gesendet, um die NET. TCP://localhost: 28940/Sms/Service/1/Übertragung hat keine empfangen eine Antwort innerhalb des konfigurierten Timeouts (00: 01:00). Die für diesen Vorgang zugewiesene Zeit war möglicherweise ein Teil eines längeren Timeouts. Dies kann sein, da der Dienst den Vorgang noch verarbeitet oder der Dienst eine Antwortnachricht senden konnte. Erhöhen Sie das Timeout des Vorgangs (durch Umwandeln des Kanals/Proxys in IContextChannel und Festlegen der OperationTimeout-Eigenschaft), und stellen Sie sicher, dass der Dienst an den Client eine Verbindung herstellen können.

Dieses Problem wird durch eine extrem hohe Anzahl von übertragenen Dateien verursacht, die in das Standardtimeout-einer Minute zulässig, die vom Speicherdienst für die Migration nicht gefiltert werden können. 

Um dieses Problem zu umgehen:

1. Bearbeiten Sie auf dem Orchestrator-Computer die *%SYSTEMROOT%\SMS\Microsoft.StorageMigration.Service.exe.config* Datei mithilfe von Notepad.exe, um die "SendTimeout" vom Standardwert eine Minute in 10 Minuten zu ändern.

   ```
     <bindings>
      <netTcpBinding>
        <binding name="NetTcpBindingSms"
                 sendTimeout="00:01:00"
   ```

2. Starten Sie den Dienst "Storage-Migration-Dienst" auf dem Orchestrator-Computer neu. 
3. Starten Sie Regedit.exe, auf dem Orchestrator-computer
4. Suchen Sie den folgenden Registrierungsunterschlüssel, und klicken Sie darauf: 

   `HKEY_LOCAL_MACHINE\\Software\\Microsoft\\SMSPowershell`

5. Zeigen Sie im Menü „Bearbeiten“ auf „Neu“, und klicken Sie dann auf „DWORD-Wert“. 
6. Geben Sie "WcfOperationTimeoutInMinutes" für den Namen des den DWORD-Wert ein, und drücken Sie dann die EINGABETASTE.
7. Mit der rechten Maustaste "WcfOperationTimeoutInMinutes", und klicken Sie dann auf ändern. 
8. Klicken Sie im Feld Basis auf "Decimal"
9. Klicken Sie im Datenfeld "Wert" Geben Sie "10", und klicken Sie dann auf OK.
10. Beenden Sie den Registrierungs-Editor.
11. Es wurde versucht, die die Fehler nur CSV-Datei erneut herunterladen. 

Ändern Sie dieses Verhalten in einer späteren Version von Windows Server-2019 geplant.  

## <a name="cutover-fails-when-migrating-between-networks"></a>Umstellung schlägt fehl, wenn die Migration zwischen Netzwerken

Bei der Migration zu einem Zielcomputer ausgeführt wird, in einem anderen Netzwerk als die Quelle, z. B. einer Azure-IaaS-Instanz kann Umstellung abgeschlossen, wenn die Quelle eine statische IP-Adresse verwendet wurde. 

Dieses Verhalten ist beabsichtigt, um Konnektivitätsprobleme nach der Migration von Benutzern, Anwendungen und Skripts, die eine Verbindung über IP-Adresse zu verhindern. Wenn die IP-Adresse aus dem alten Quellcomputer in das neue Ziel verschoben wird, wird nicht sie die neuen Netzwerk-Subnetz-Informationen und vielleicht DNS und WINS-übereinstimmen.

Dieses Problem umgehen, führen Sie eine Migration auf einem Computer im selben Netzwerk. Klicken Sie dann diesen Computer zu einem neuen Netzwerk verschieben und seine IP-Informationen zuweisen. Z. B. bei der Migration zu Azure IaaS, zunächst zu einem lokalen virtuellen Computer migrieren und dann die Verwendung von Azure Migrate die VM nach Azure verschoben.  

Wir haben dieses Problem behoben, in einer späteren Version von Windows Admin Center. Wir werden jetzt können Sie Migrationen an, die Netzwerkeinstellungen des Zielservers nicht ändern. Die aktualisierte Erweiterung werden hier aufgelistet, bei der Veröffentlichung. 

## <a name="validation-warnings-for-destination-proxy-and-credential-administrative-privileges"></a>Warnungen für die Ziel-Proxy und Anmeldeinformationen über Administratorrechte

Bei der Überprüfung eines Übertragungsauftrag des, sehen Sie die folgenden Warnungen:

 > **Die Anmeldeinformationen über Administratorrechte verfügt.**
 > Warnung: Aktion nicht remote verfügbar.
 > **Der Zielproxy wird registriert.**
 > Warnung: Der Zielproxy wurde nicht gefunden.

Wenn Sie die Storage-Migration-Dienstproxy-Dienst nicht auf dem Zielcomputer Windows Server-2019 installiert haben oder der Ziel-Computer, Windows Server 2016 oder Windows Server 2012 R2 befindet, ist dieses Verhalten beabsichtigt. Wir empfehlen die Migration zu einem 2019 für Windows Server-Computer mit dem Proxy für die deutlich verbesserte übertragungsleistung installiert.  

## <a name="certain-files-do-not-inventory-or-transfer-error-5-access-is-denied"></a>Bestimmte Dateien nicht inventarisiert oder übertragen, 5-Fehler "Zugriff verweigert"

Bei der Inventur oder Übertragung der Dateien aus der Quelle an die Zielcomputer verwendet werden sollen, nicht Dateien, die aus denen ein Benutzer Berechtigungen für Administratoren-Gruppe entfernt wurde migriert. Untersuchen die Storage-Migration-Dienst-Proxy-Debug zeigt:

  Protokollname:      Microsoft-Windows-StorageMigrationService-Proxy/Debug Source:        Microsoft-Windows-StorageMigrationService-Proxy Date:          2/26/2019 9:00:04 Uhr-Ereignis-ID:      10000 Aufgabenkategorie: Keine Ebene:         Fehlerschlüsselwörter:      
  Benutzer:          Netzwerkcomputer-Dienst: srv1.contoso.com Beschreibung:

  02/26/2019-09:00:04.860 [Aufgabenschema] Fehler beim Übertragen der für \\srv1.contoso.com\public\indy.png: (5) Zugriff wird verweigert.
Stapelüberwachung: Am Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.OpenFile (String FileName, DesiredAccess DesiredAccess, ShareMode ShareMode, CreationDisposition CreationDisposition, FlagsAndAttributes FlagsAndAttributes) an Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetTargetFile (Zeichenfolgenpfad) am Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetTargetFile ("FileInfo"-Datei) an Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.InitializeSourceFileInfo() am Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.Transfer() an Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.TryTransfer() [d:\os\src\base\dms\proxy\transfer\transferproxy\FileTransfer.cs::TryTransfer::55]


Dieses Problem wird durch einen Codefehler im Storage-Migration-Dienst verursacht, in dem die Sicherung Berechtigung nicht aufgerufen wurde. 

Um dieses Problem zu beheben, installieren [Windows Update 2 April 2019 – KB4490481 (OS Build 17763.404)](https://support.microsoft.com/help/4490481/windows-10-update-kb4490481) auf dem Orchestrator-Computer und dem Zielcomputer, wenn der Dienst gibt es installiert ist. Stellen Sie sicher, dass die Benutzer-Konto des Quellstandorts-Migration ein lokaler Administrator auf dem Quellcomputer und der Speicherung Datenbankmigrationsdienst Orchestrator ist. Stellen Sie sicher, dass das Benutzerkonto des Ziel-Migration ein lokaler Administrator auf dem Zielcomputer und der Speicherung Datenbankmigrationsdienst Orchestrator ist. 

## <a name="dfsr-hashes-mismatch-when-using-storage-migration-service-to-preseed-data"></a>DFSR-Hashes Konflikt, wenn Storage-Migration-Dienst zum Seeding von Daten

Wenn Sie den Storage-Migration-Dienst zum Übertragen von Dateien an ein neues Ziel verwenden, klicken Sie dann konfigurieren die DFS-Replikation (DFSR) zum Replizieren von Daten mit einem vorhandenen DFSR-Server über Presseded Replikation oder DFSR-Datenbank beim Klonen, alle Dateien Experiemce einen hash Konflikt und werden erneut repliziert werden. Die Datenströme, Sicherheitsdatenströme, Größen und Attribute, die alle perfekt abgeglichen wird, nach der Verwendung von SMS an sie übertragen werden. Examing zeigt die Dateien mit ICACLS oder das Debugprotokoll der DFSR-Datenbank zum Klonen:

Quelldatei:

  Icacls d:\test\Source:

  icacls d:\test\thatcher.png /save out.txt /t thatcher.png D:AI(A;;FA;;;BA)(A;;0x1200a9;;;DD)(A;;0x1301bf;;;DU)(A;ID;FA;;;BA)(A;ID;FA;;;SY)(A;ID;0x1200a9;;;BU)

Zieldatei:

  icacls d:\test\thatcher.png /save out.txt /t thatcher.png D:AI(A;;FA;;;BA)(A;;0x1301bf;;;DU)(A;;0x1200a9;;;DD)(A;ID;FA;;;BA)(A;ID;FA;;;SY)(A;ID;0x1200a9;;;BU)**S:PAINO_ACCESS_CONTROL**

DFSR-Debugprotokoll:

  20190308 10:18:53.116 3948 DBCL 4045 [Warnung] stimmt nicht überein. DBClone::IDTableImportUpdate Datensatz wurde gefunden. 

  Lokale ACL-Hash: 1BCDFE03-A18BCE01-D1AE9859-23A0A5F6 LastWriteTime:20190308 18:09:44.876 FileSizeLow:1131654 FileSizeHigh:0 Attribute: 32 

  Klonen Sie ACL-Hash:**DDC4FCE4-DDF329C4-977CED6D-F4D72A5B** LastWriteTime:20190308 18:09:44.876 FileSizeLow:1131654 FileSizeHigh:0 Attribute: 32 

Dieses Problem wird durch einen Codefehler in einer Bibliothek, die vom Speicherdienst Migration verwendet werden, um die sicherheitsüberwachung ACLs (SACL) festgelegt, verursacht. Eine SACL ungleich Null ist versehentlich festgelegt werden, wenn die SACL leer ist, wurde führende DFSR einen Hash-Konflikt ordnungsgemäß zu identifizieren. 

Zur Umgehung dieses Problem, weiterhin mit Robocopy für [vorabseedings DFSR-als auch DFSR-Datenbank Klonvorgänge](../dfs-replication/preseed-dfsr-with-robocopy.md) anstelle von dem Storage-Migration-Dienst. Wir werden das Problem zu untersuchen und zum Beheben dieses Problems in einer späteren Version von Windows Server und möglicherweise einen Windows Update-bereitgestellt werden soll. 

## <a name="error-404-when-downloading-csv-logs"></a>Fehler 404 beim Herunterladen der CSV-Protokolle

Beim Versuch, die die Übertragung oder Fehler Protokolle am Ende der einem Übertragungsvorgang herunterzuladen, erhalten Sie Fehler auf:

  $jobname: Übertragungsprotokoll: Ajax-Fehler 404

Dieser Fehler wird erwartet, wenn Sie die Firewallregel "Datei- und Druckerfreigabe (SMB eingehend)" auf dem OrchestratorServer nicht aktiviert haben. Dateidownloads Windows Admin Center müssen Port TCP/445 (SMB) auf verbundenen Computern.  

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-when-transfering-from-windows-server-2008-r2"></a>Fehler "konnte nicht transfer Speicher auf einem der Endpunkte" beim Übertragen von Windows Server 2008 R2

Beim Versuch, Daten von einem Windows Server 2008 R2-Quellcomputer zu übertragen, erhalten keine Datenübertragungen und Sie zu einem Fehler:  

  Speicherkonto konnte nicht auf einem der Endpunkte übertragen werden.
0x9044

Dieser Fehler wird erwartet, wenn es sich bei Ihrem Windows Server 2008 R2-Computer mit allen kritischen und wichtigen Updates über Windows Update ist nicht alle Patches installiert. Unabhängig von der Speicherung Datenbankmigrationsdienst empfehlen wir grundsätzlich die Patchen von eines Windows Server 2008 R2-Computers aus Sicherheitsgründen wie das Betriebssystem nicht zu die sicherheitsverbesserungen neuerer Versionen von Windows Server enthält.

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-and-check-if-the-source-device-is-online---we-couldnt-access-it"></a>Fehler "konnte nicht transfer Speicher auf einem der Endpunkte" und "Überprüfen ist das Quellgerät online - konnte nicht wir darauf zugreifen."

Beim Versuch, Daten von einem Quellcomputer zu übertragen, werden einige oder alle Freigaben nicht, mit der Zusammenfassung Fehler übertragen:

   Speicherkonto konnte nicht auf einem der Endpunkte übertragen werden.
0x9044

Untersuchen die Details der SMB-Übertragung wird Fehler angezeigt:

   Überprüfen Sie, wenn das Quellgerät online - ist es darauf zugreifen konnte nicht.

Zeigt das StorageMigrationService/Admin-Ereignisprotokoll untersucht:

   Speicherkonto konnte nicht übertragen werden.

   Auftrag: Job1 ID:  
   Status: Fehler: 36931 Fehlermeldung angezeigt: 

   Leitfaden: Prüfen Sie die ausführliche Fehlermeldung, und stellen Sie sicher, dass die Übertragung Anforderungen erfüllt werden. Der Übertragungsauftrag konnten keine Quell- und Ziel-Computer übertragen. Dies möglicherweise daran, dass der Orchestrator-Computer konnten keine Computer Quell- oder Zielschema, möglicherweise aufgrund einer Firewallregel erreichen oder Berechtigungen fehlt.

Untersuchen die StorageMigrationService-Proxy/Debug Protokoll zeigt:

   Fehler beim Überprüfen von 07/02/2019-13:35:57.231 [Aufgabenschema] übertragen. ErrorCode: 40961, Quellendpunkt ist nicht erreichbar oder nicht vorhanden ist, Datenquellen-Anmeldeinformationen sind ungültig oder authentifizierter Benutzer verfügt nicht über ausreichende Berechtigungen für den Zugriff.
am Microsoft.StorageMigration.Proxy.Service.Transfer.TransferOperation.Validate() am Microsoft.StorageMigration.Proxy.Service.Transfer.TransferRequestHandler.ProcessRequest ("FileTransferRequest FileTransferRequest", "Guid" operationId "")    [d:\os\src\base\dms\proxy\transfer\transferproxy\TransferRequestHandler.cs::

Dieser Fehler wird erwartet, verfügt Ihr Migrationskonto nicht mindestens Lesezugriff auf die SMB-Freigaben. Zur Umgehung dieses Fehlers fügen Sie eine Sicherheitsgruppe mit den Konto des Quellstandorts-Migration auf die SMB-Freigaben auf dem Quellcomputer hinzu, und lesen, ändern oder Vollzugriff zu gewähren. Nachdem die Migration abgeschlossen ist, können Sie dieser Gruppe entfernen. Eine zukünftige Version von Windows Server kann dieses Verhalten dahingehend, dass nicht mehr explizite Berechtigungen für die Quellfreigaben ändern.

## <a name="see-also"></a>Siehe auch

- [Übersicht über Storage-Migration Service](overview.md)
