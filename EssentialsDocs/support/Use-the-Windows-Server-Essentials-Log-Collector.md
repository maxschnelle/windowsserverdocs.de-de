---
title: Verwenden Sie die Windows Server Essentials Log Collector
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.openlocfilehash: d003c6a45159548f7e34d86ca242f74868659d2f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="use-the-windows-server-essentials-log-collector"></a>Verwenden Sie die Windows Server Essentials Log Collector

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Sie bei der Behandlung von Computerproblemen können Sie von einem Vertreter des Microsoft-Kundendienst und Support aufgefordert, Protokolle von Servern, Computern im Netzwerk oder beides mit der Windows Server Essentials Log Collector zu erfassen.  
  
 Der Log Collector kopiert programmprotokolle, Event-Reviewer-Protokolle und zugehörige Umgebungsinformationen in einer einzelnen Zip-Datei an einem angegebenen Speicherort. Sie können den Log Collector direkt vom Server oder von einem beliebigen Computer im Netzwerk oder mithilfe einer Remoteverbindung zu den Computern ausführen.  
  
> [!NOTE]
>  -   Der Log Collector analysiert Netzwerkprobleme oder nehmen Sie Änderungen an einem Server oder Computer im Netzwerk nicht. Informationen zur Behandlung von Netzwerkproblemen finden Sie in der Hilfedokumentation für das Serverprodukt.  
> -   In diesem Handbuch werden die Computer in Ihrem Netzwerk, anders als Ihr Server, Netzwerkcomputer aufgerufen.  
> -   [Herunterladen des Windows Server Essentials Log Collector-Installationspakets](https://go.microsoft.com/fwlink/?LinkID=266341).  
  
 Installieren und Ausführen von Log Collector, führen Sie die Schritte in den folgenden Themen:  
  

1.  [Installieren Sie den Log Collector](Install-the-Windows-Server-Essentials-Log-Collector.md)  
  
2.  [Führen Sie den Log Collector](Run-the-Windows-Server-Essentials-Log-Collector.md)  

1.  [Installieren Sie den Log Collector](../support/Install-the-Windows-Server-Essentials-Log-Collector.md)  
  
2.  [Führen Sie den Log Collector](../support/Run-the-Windows-Server-Essentials-Log-Collector.md)  

  
## <a name="environment-information-collected"></a>Erfasste Umgebungsinformationen  
 Für jeden Computer im Netzwerk oder der Server, den Sie angeben, den Log Collector sammelt die folgenden Umgebungsinformationen und verschiebt sie in der protokollerfassungsdatei.  
  
-   Version des Betriebssystems  
  
-   CPU-Hersteller und Beschreibung  
  
-   Speichermenge und-Zuweisung  
  
-   Netzwerkadapter, die an TCP/IP gebunden sind  
  
-   Gebietsschema  
  
-   Prozesse  
  
-   Speicherkonfiguration  
  
-   Informationen zur Hostdatei  
  
-   Ereignisprotokolle, einschließlich Anwendung, System, Windows Server und Media Center  
  
-   Dienststeuerungs-Manager-Nachrichten  
  
-   Neustartereignisse und Windows Update-Ereignisse  
  
-   Systemfehler und Anwendungsfehler  
  
## <a name="services-information-collected"></a>Gesammelte Dienstinformationen  
  
### <a name="server-services"></a>Server-Dienste  
  
-   Windows Server Client Computer Backup Service  
  
-   Windows Server Client Computer Backup Provider Service  
  
-   Windows-Geräte-Anbieter  
  
-   Windows Server-Domänennamenverwaltung  
  
-   Dienstanbieterregistrierung von Windows Server  
  
-   Windows Server-Einstellungsanbieter  
  
-   Windows-Serverdienst UPnP-Gerät  
  
-   Anbieter für Windows Server Remote Web Access-Verwaltung  
  
-   Windows Server-Integritätsdienst  
  
-   Windows Server-Speicherdienst  
  
-   SQM-Dienst von Windows Server  
  
### <a name="network-computer-services"></a>Netzwerkcomputerdienste  
  
-   Windows Server Client Computer Backup Provider Service  
  
-   Windows Server-Integritätsdienst  
  
-   Dienstanbieterregistrierung von Windows Server  
  
-   SQM-Dienst von Windows Server  
  
## <a name="logs-and-registry-information-collected"></a>Protokolle und die gesammelten Informationen in der Registrierung  
 Für jeden Computer im Netzwerk oder der angegebene Server sammelt Log Collector Protokoll-und Registrierungsinformationen vom Server und Computer im Netzwerk wie folgt.  
  
### <a name="server-logs-and-registry-information"></a>Informationen zur Registrierung und SQL Server  
  
-   Server-Produktprotokolle aus < ProgramData\ > \Microsoft\Windows Server\Logs  
  
-   Geplante Aufgaben  
  
-   API-Setup-Protokollen  
  
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
  
### <a name="network-computer-logs-and-registry-information"></a>Netzwerkcomputerprotokollen und Registrierungsinformationen  
  
-   Netzwerkcomputer-Produktprotokolle am < ProgramData\ > \Microsoft\Windows Server\Logs  
  
-   Integritätswarnungsdatei < ProgramData\ > \Microsoft\Windows Server\Data  
  
-   Windows Update-Protokolle  
  
-   API-Setup-Protokollen  
  
-   Info zu geplanten Aufgaben  
  
-   Registrierungsschlüssel aus \\\HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows Server\  
  
## <a name="logs-for-computers-that-do-not-run-a-version-of-the-windows-operating-system"></a>Protokolle für Computer, auf denen eine Version von Windows-Betriebssystem nicht ausgeführt werden.  
 Der Log Collector ist nicht Protokolldateien von Computern sammeln, die eine Version von Windows-Betriebssystem nicht ausgeführt werden. Kopieren Sie für nicht-Windows-Computer die folgenden Protokolldateien manuell an demselben Speicherort, in dem Sie die Log Collector-Dateien gespeichert werden.  
  
-   System.log  
  
-   Bibliothek/Protokolle/Windows Server.log  
  
-   Library/Logs/CrashReporter/LaunchPad-< Nnn\ > (Kopieren Sie alle Launchpad-< Nnn\ > .crash-Dateien)  
  
-   Bibliothek/Protokolle/DiagnosticReports/LaunchPad-< Nnn\ > (Kopieren Sie alle Launchpad-< Nnn\ > .crash-Dateien)  
  
## <a name="see-also"></a>Siehe auch  
  

-   [Problembehandlung für Log Collector-Fehler](Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

-   [Problembehandlung für Log Collector-Fehler](../support/Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

