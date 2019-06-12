---
title: Verwenden des Windows Server Essentials-Protokollsammlers
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6985518-b42d-4cfb-9761-eaa75306b6d7
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ba5c0de9d8689c63c95ea3410a74fc9a7289aeab
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435990"
---
# <a name="use-the-windows-server-essentials-log-collector"></a>Verwenden des Windows Server Essentials-Protokollsammlers

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Wenn Sie Probleme mit dem behandeln möchten, unter Umständen einem Vertreter des Microsoft-Kundendienst und Support zu erfassen Protokolle von Servern, Computern im Netzwerk oder beides mit der Windows Server Essentials Log Collector erforderlich.  
  
 Log Collector kopiert Programmprotokolle, Event-Reviewer-Protokolle und zugehörige Umgebungsinformationen in eine einzelne ZIP-Datei an einem angegebenen Speicherort. Sie können Log Collector direkt vom Server oder einem beliebigen Computer im Netzwerk oder mithilfe einer Remoteverbindung zu den Computern ausführen.  
  
> [!NOTE]
> - Log Collector analysiert Netzwerkprobleme nicht und nimmt auch keine Änderungen an einem Server oder Computer im Netzwerk vor. Informationen zur Behandlung von Netzwerkproblemen finden Sie in der Hilfedokumentation für das Serverprodukt.  
>   -   In diesem Handbuch werden die Computer in Ihrem Netzwerk, anders als Ihr Server, Netzwerkcomputer aufgerufen.  
>   -   [Herunterladen des Windows Server Essentials Log Collector-Installationspakets](https://go.microsoft.com/fwlink/?LinkID=266341).  
  
 Zum Installieren und Ausführen von Log Collector führen Sie die Schritte in den folgenden Themen aus:  
  

1.  [Installieren des Log Collectors](Install-the-Windows-Server-Essentials-Log-Collector.md)  
  
2.  [Führen Sie den Log Collector](Run-the-Windows-Server-Essentials-Log-Collector.md)  

1.  [Installieren des Log Collectors](../support/Install-the-Windows-Server-Essentials-Log-Collector.md)  
  
2.  [Führen Sie den Log Collector](../support/Run-the-Windows-Server-Essentials-Log-Collector.md)  

  
## <a name="environment-information-collected"></a>Erfasste Umgebungsinformationen  
 Für jeden Netzwerkcomputer oder Server, den Sie angeben, erfasst Lob Collector folgende Umgebungsinformationen in der Protokollerfassungsdatei.  
  
-   Version des Betriebssystems  
  
-   CPU-Hersteller und -Beschreibung  
  
-   Speichermenge und -zuweisung  
  
-   Netzwerkadapter, die an TCP/IP gebunden sind  
  
-   Locale  
  
-   Prozesse  
  
-   Speicherkonfiguration  
  
-   Informationen zur Hostdatei  
  
-   Ereignisprotokolle, einschließlich Anwendung, System, Windows Server und Media Center  
  
-   Dienststeuerungs-Manager-Meldungen  
  
-   Neustartereignisse und Windows Update-Ereignisse  
  
-   Systemfehler und Anwendungsfehler  
  
## <a name="services-information-collected"></a>Gesammelte Dienstinformationen  
  
### <a name="server-services"></a>Server-Dienste  
  
-   Windows Server-Dienst für die Clientcomputersicherung  
  
-   Windows Server-Anbieterdienst für die Clientcomputersicherung  
  
-   Anbieter für Windows Server-Geräte  
  
-   Windows Server-Domänennamenverwaltung  
  
-   Dienstanbieterregistrierung von Windows Server  
  
-   Windows Server-Einstellungsanbieter  
  
-   UPnP-Gerätedienst von Windows Server  
  
-   Windows Server-Verwaltungsanbieter für Remotewebzugriff  
  
-   Integritätsdienst von Windows Server  
  
-   Windows Server-Speicherdienst  
  
-   SQM-Dienst von Windows Server  
  
### <a name="network-computer-services"></a>Netzwerkcomputerdienste  
  
-   Windows Server-Anbieterdienst für die Clientcomputersicherung  
  
-   Integritätsdienst von Windows Server  
  
-   Dienstanbieterregistrierung von Windows Server  
  
-   SQM-Dienst von Windows Server  
  
## <a name="logs-and-registry-information-collected"></a>Erfasste Protokolle und Registrierungsinformationen  
 Für jeden angegebenen Netzwerkcomputer oder Server sammelt Log Collector folgende Protokoll- und Registrierungsinformationen vom Server und Netzwerkcomputer.  
  
### <a name="server-logs-and-registry-information"></a>Server-Protokoll- und Registrierungsinformationen  
  
-   Server-Produktprotokolle aus < ProgramData\>\Microsoft\Windows Server\Logs  
  
-   Geplante Aufgaben  
  
-   Setup-API-Protokolle  
  
-   Windows Update-Protokolle  
  
-   Datei mit den Integritätswarnungen  
  
-   Geräte-Infodatei  
  
-   Protokolldatei für Server-Sicherung  
  
-   Panther-Protokolldatei  
  
-   Dienste  
  
-   Registrierungsschlüssel aus  
  
    -   \\\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\  
  
    -   \\\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DevicesProviderSvc  
  
    -   \\\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DomainManagerProviderSvc  
  
### <a name="network-computer-logs-and-registry-information"></a>Informationen zu Netzwerkcomputerprotokollen und -registrierung  
  
-   Netzwerkcomputer-Produktprotokolle < ProgramData\>\Microsoft\Windows Server\Logs  
  
-   Integritätswarnungsdatei < ProgramData\>\Microsoft\Windows Server\Data  
  
-   Windows Update-Protokolle  
  
-   Setup-API-Protokolle  
  
-   Info zu geplanten Aufgaben  
  
-   Registrierungsschlüssel aus \\\HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows Server\  
  
## <a name="logs-for-computers-that-do-not-run-a-version-of-the-windows-operating-system"></a>Protokolle für Computer, die keine Version des Windows-Betriebssystems ausführen  
 Log Collector erfasst nur Protokolldateien von Computern, die eine Version des Windows-Betriebssystems ausführen. Bei Nicht-Windows-Computern kopieren Sie die folgenden Protokolldateien manuell an den gleichen Speicherort, an dem die Log Collector-Dateien gespeichert sind.  
  
-   System.log  
  
-   Library/Logs/Windows Server.log  
  
-   Library/Logs/CrashReporter/LaunchPad-< Nnn\> (Kopieren Sie alle Launchpad-< Nnn\>.crash-Dateien)  
  
-   Bibliothek/Protokolle/DiagnosticReports/LaunchPad-< Nnn\> (Kopieren Sie alle Launchpad-< Nnn\>.crash-Dateien)  
  
## <a name="see-also"></a>Siehe auch  
  

-   [Problembehandlung bei der Log Collector-Fehler](Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

-   [Problembehandlung bei der Log Collector-Fehler](../support/Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

