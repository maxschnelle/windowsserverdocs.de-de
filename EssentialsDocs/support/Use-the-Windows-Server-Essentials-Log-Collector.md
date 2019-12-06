---
title: Verwenden des Windows Server Essentials-Protokollsammlers
description: Beschreibt die Verwendung von Windows Server Essentials
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
ms.openlocfilehash: df467921f8a8f5633d2b0bd792885fe2c9ae2212
ms.sourcegitcommit: a937eb17915a4a0e444a36ddb0fac9c9771cfbfa
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/06/2019
ms.locfileid: "74877905"
---
# <a name="use-the-windows-server-essentials-log-collector"></a>Verwenden des Windows Server Essentials-Protokollsammlers

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Bei der Behandlung von Computerproblemen werden Sie möglicherweise von einem Vertreter des Microsoft-Kunden Dienstanbieter und-Supports aufgefordert, Protokolle von Servern, Computern im Netzwerk oder beides mithilfe des Windows Server Essentials Log Collector zu erfassen.  
  
 Log Collector kopiert Programmprotokolle, Event-Reviewer-Protokolle und zugehörige Umgebungsinformationen in eine einzelne ZIP-Datei an einem angegebenen Speicherort. Sie können Log Collector direkt vom Server oder einem beliebigen Computer im Netzwerk oder mithilfe einer Remoteverbindung zu den Computern ausführen.  
  
> [!NOTE]
>Log Collector analysiert Netzwerkprobleme nicht und nimmt auch keine Änderungen an einem Server oder Computer im Netzwerk vor. Informationen zur Behandlung von Netzwerkproblemen finden Sie in der Hilfedokumentation für das Serverprodukt.  
>In diesem Handbuch werden die Computer in Ihrem Netzwerk, mit Ausnahme des Servers, als "Netzwerk Computer" bezeichnet.  
>[Herunterladen des Windows Server Essentials Log Collector-Installationspakets](https://www.microsoft.com/download/details.aspx?id=34821).  
  
 Zum Installieren und Ausführen von Log Collector führen Sie die Schritte in den folgenden Themen aus:  
  

1. [Installieren des Log Collector](Install-the-Windows-Server-Essentials-Log-Collector.md)  
  
2. [Ausführen des Protokoll Sammlers](Run-the-Windows-Server-Essentials-Log-Collector.md)  

3. [Installieren des Log Collector](../support/Install-the-Windows-Server-Essentials-Log-Collector.md)  
  
4. [Ausführen des Protokoll Sammlers](../support/Run-the-Windows-Server-Essentials-Log-Collector.md)  


## <a name="environment-information-collected"></a>Erfasste Umgebungsinformationen  
 Für jeden Netzwerkcomputer oder Server, den Sie angeben, erfasst Lob Collector folgende Umgebungsinformationen in der Protokollerfassungsdatei.  
  
-   Betriebssystemversion  
  
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
  
-   Server-Produkt Protokolle, von < ProgramData\>\Microsoft\Windows Server\Logs  
  
-   Geplante Aufgaben  
  
-   Setup-API-Protokolle  
  
-   Windows Update-Protokolle  
  
-   Datei mit den Integritätswarnungen  
  
-   Geräte-Infodatei  
  
-   Protokolldatei für Server-Sicherung  
  
-   Panther-Protokolldatei  
  
-   „Dienste“  
  
-   Registrierungsschlüssel aus  
  
    -   \\\ HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows Server \  
  
    -   \\\ HKEY_LOCAL_MACHINE \system\currentcontrolset\services\tvicesprovidersvc  
  
    -   \\\ HKEY_LOCAL_MACHINE \system\currentcontrolset\services\domainmanagerprovidersvc  
  
### <a name="network-computer-logs-and-registry-information"></a>Informationen zu Netzwerkcomputerprotokollen und -registrierung  
  
-   Netzwerk Computer-Produkt Protokolle bei < ProgramData\>\Microsoft\Windows Server\Logs  
  
-   Integritäts Warnungs Datei unter < ProgramData\>\Microsoft\Windows Server\Data  
  
-   Windows Update-Protokolle  
  
-   Setup-API-Protokolle  
  
-   Info zu geplanten Aufgaben  
  
-   Registrierungsschlüssel aus \\\ HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows Server \  
  
## <a name="logs-for-computers-that-do-not-run-a-version-of-the-windows-operating-system"></a>Protokolle für Computer, die keine Version des Windows-Betriebssystems ausführen  
 Log Collector erfasst nur Protokolldateien von Computern, die eine Version des Windows-Betriebssystems ausführen. Bei Nicht-Windows-Computern kopieren Sie die folgenden Protokolldateien manuell an den gleichen Speicherort, an dem die Log Collector-Dateien gespeichert sind.  
  
-   System.log  
  
-   Library/Logs/Windows Server.log  
  
-   Bibliothek/Protokolle/CrashReporter/Launchpad-< nnn-\> (Kopieren Sie alle Launchpad-< nnn-\>. Crash-Dateien)  
  
-   Bibliothek/Protokolle/diagnostikreports/Launchpad-< nnn-\> (Kopieren Sie alle Launchpad-< nnn-\>. Crash-Dateien)  
  
## <a name="see-also"></a>Weitere Informationen:  
  

-   [Problembehandlung für Log Collector-Fehler](Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

-   [Problembehandlung für Log Collector-Fehler](../support/Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

