---
title: Speicherung Datenbankmigrationsdienst bekannte Probleme
description: Bekannte Probleme und Supportinformationen zur Problembehandlung für Storage-Migration-Dienst, wie das Sammeln von Protokollen für Microsoft-Support.
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 02/27/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: f5fefab2c1b7ba8b62ffd6734217eab9a13ae95e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888871"
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

Wir möchten in einer späteren Version von Windows Server dieses Problem zu beheben. Öffnen Sie eine Supportanfrage über [Microsoft-Support](https://support.microsoft.com) zum Anfordern einer Backport von diesem Fix erstellt werden.

## <a name="storage-migration-service-isnt-included-in-windows-server-2019-evaluation-edition"></a>Storage-Migration-Dienst ist in der Evaluierungsversion von Windows Server 2019 nicht enthalten.

Wenn Windows Admin Center zum Herstellen einer Verbindung mit einem [Evaluierungsversion von Windows Server 2019](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) gibt es keine Option zum Verwalten von Storage-Migration-Dienst. Storage-Migration-Dienst ist nicht auch in Rollen und Features enthalten.

Dieses Problem wird durch ein servicing Problem in die Evaluierungsmedien von Windows Server-2019 verursacht. 

Um dieses Problem zu umgehen, installieren Sie eine Verkaufsversion, MSDN, OEM oder einem Volume License-Version von Windows Server-2019 aus, und aktivieren Sie nicht. Arbeiten ohne Aktivierung alle Editionen von Windows Server im auswertungsmodus für 180 Tage. 

Wir haben dieses Problem in einer späteren Version von Windows Server-2019 behoben.  

## <a name="storage-migration-service-times-out-downloading-the-transfer-error-csv"></a>Storage Migration-Dienst ein Timeout auftritt, die Fehler beim Übertragen der CSV-Download

Wenn Windows Admin Center oder PowerShell verwenden die Übertragung Vorgänge ausführliche Fehler nur CSV-Protokoll herunterladen, erhalten Sie Fehler auf:

 >   Übertragungsprotokoll – überprüfen Sie, ob die Freigabe von Dateien in Ihrer Firewall zulässig ist. : Dieser Anforderungsvorgang gesendet, um die NET. TCP://localhost: 28940/Sms/Service/1/Übertragung hat keine empfangen eine Antwort innerhalb des konfigurierten Timeouts (00: 01:00). Die Zeit, die für diesen Vorgang zugewiesene Zeitraum war möglicherweise ein Teil eines längeren Zeitlimits. Dies kann sein, da der Dienst den Vorgang noch verarbeitet oder der Dienst eine Antwortnachricht senden konnte. Erhöhen Sie das Timeout des Vorgangs (durch Umwandeln des Kanals/Proxys in IContextChannel und Festlegen der OperationTimeout-Eigenschaft), und stellen Sie sicher, dass der Dienst an den Client eine Verbindung herstellen können.

Dieses Problem wird durch eine extrem hohe Anzahl von übertragenen Dateien verursacht, die in das Standardtimeout-einer Minute zulässig, die vom Speicherdienst für die MIgration nicht gefiltert werden können. 

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

Bei der Migration zu einem virtuellen Zielcomputer kann nicht auf einem anderen Netzwerk als die Quelle, z. B. eine Azure-IaaS-Instanz, Umstellung abgeschlossen, wenn die Quelle eine statische IP-Adresse verwendet wurde. 

Dieses Verhalten ist beabsichtigt, um Konnektivitätsprobleme nach der Migration von Benutzern, Anwendungen und Skripts, die eine Verbindung über IP-Adresse zu verhindern. Wenn die IP-Adresse aus dem alten Quellcomputer in das neue Ziel verschoben wird, wird nicht sie die neuen Netzwerk-Subnetz-Informationen und vielleicht DNS und WINS-übereinstimmen.

Dieses Problem umgehen, führen Sie eine Migration auf einem Computer im selben Netzwerk. Klicken Sie dann diesen Computer zu einem neuen Netzwerk verschieben und seine IP-Informationen zuweisen. Z. B. bei der Migration zu Azure IaaS, zunächst zu einem lokalen virtuellen Computer migrieren und dann die Verwendung von Azure Migrate die VM nach Azure verschoben.  

Wir haben dieses Problem in einer späteren Version von Windows Server-2019 behoben. Wir werden jetzt können Sie Migrationen an, die Netzwerkeinstellungen des Zielservers nicht ändern. Wir können ein Update der vorhandenen Version von Windows Server-2019 im Rahmen des normalen monatlichen Updatezyklus freigeben. 


## <a name="see-also"></a>Siehe auch

- [Übersicht über Storage-Migration Service](overview.md)