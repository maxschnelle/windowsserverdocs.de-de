---
title: Verwenden der Remotezugriffsüberwachung und Ressourcenerfassung
description: Dieses Thema ist Teil des Leitfadens für die Remote Zugriffs Überwachung und-Kontoführung in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 92519b49-0df4-43c1-9717-f13570644212
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 03d367f2f981ca3ed649f1ca4d5eca23967c9cfc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860513"
---
# <a name="use-remote-access-monitoring-and-accounting"></a>Verwenden der Remotezugriffsüberwachung und Ressourcenerfassung

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Die Überwachung des Remotezugriffs meldet Remotebenutzeraktivitäten und den Status der DirectAccess- und VPN-Verbindungen. Sie zeichnet die Anzahl und die Dauer der Clientverbindungen (und weitere Statistiken) auf und überwacht den Betriebsstatus des Servers. Eine benutzerfreundliche Überwachungskonsole stellt Ihnen eine Ansicht der gesamten Remotezugriffinfrastruktur bereit. Die Überwachungsansichten sind für einzelne Server-, Cluster- und Konfigurationen für mehrere Standorte.  
  
**Hinweis:** Durch Windows Server 2012 werden DirectAccess und RRAS (Routing and Remote Access Service, Routing- und RAS-Dienst) zu einer einzigen Remotezugriffsrolle zusammengefasst.  
  
> [!NOTE]  
> Über dieses Thema hinaus sind die folgenden Themen zur Überwachung des Remotezugriffs verfügbar.  
>   
> -   [Überwachen der vorhandenen Last auf dem Remotezugriffsserver](Monitor-the-existing-load-on-the-Remote-Access-server.md)  
> -   [Überwachen des Konfigurationsverteilungsstatus des Remotezugriffsservers](Monitor-the-configuration-distribution-status-of-the-Remote-Access-server.md)  
> -   [Überwachen des Betriebs Status des Remote Zugriffs Servers und seiner Komponenten](Monitor-the-operations-status-of-the-Remote-Access-server-and-its-components.md)  
> -   [Identifizieren und Beheben von Betriebsproblemen auf dem Remotezugriffsserver](Identify-and-resolve-Remote-Access-server-operations-problems.md)  
> -   [Überwachen der Aktivitäten und des Status von verbundenen Remoteclients](Monitor-connected-remote-clients-for-activity-and-status.md)  
> -   [Erstellen eines Nutzungsberichts für Remoteclients mithilfe von Verlaufsdaten](Generate-a-usage-report-for-remote-clients-using-historical-data.md)  

## <a name="in-this-guide"></a>In diesem Handbuch  
Dieses Dokument enthält Anweisungen zur Nutzung der Überwachungsfunktionen des Remotezugriffs mit der DirectAccess-Verwaltungskonsole und den entsprechenden Windows PowerShell-Cmdlets, die als Teil der Remotezugriffs-Serverrolle bereitgestellt werden.  
  
Es werden folgende Überwachungs- und Ressourcenerfassungsszenarios erläutert:  
  
1.  Überwachen der vorhandenen Last auf dem Remotezugriffsserver  
  
2.  Überwachen des Konfigurationsverteilungsstatus des Remotezugriffsservers  
  
3.  Überwachen des Betriebsstatus des Remotezugriffsservers und dessen Komponenten  
  
4.  Identifizieren und Beheben von Betriebsproblemen auf dem Remotezugriffsserver  
  
5.  Überwachen der Aktivitäten und des Status von verbundenen Remoteclients  
  
6.  Erstellen eines Nutzungsberichts für die Remoteclients mithilfe von Verlaufsdaten  
  
### <a name="understand-monitoring-and-accounting"></a>Grundlagen von Überwachung und Ressourcenerfassung  
Bevor Sie mit den Überwachungs- und Ressourcenüberwachungsaufgaben für Remoteclients beginnen, müssen Sie den Unterschied zwischen den beiden Komponenten verstehen.  
  
-   Die**Überwachung** zeigt die aktiv zu einem bestimmten Zeitpunkt verbundenen Benutzer an.  
  
-   Die **Ressourcenerfassung** erfasst einen Verlauf der Benutzer, die eine Verbindung zum Unternehmensnetzwerk hergestellt haben und ihre Nutzungsdetails (zu Kompatibilitäts- und Prüfzwecken).  
  
Die Remoteclientüberwachung basiert auf Verbindungen. Es gibt zwei Arten von Tunnelverbindungen, die von DirectAccess-Clients aufgebaut werden können:  
  
-   **Computer-Tunneldatenverkehrverbindungen**: Dieser Tunnel wird vom Computer im Systemkontext aufgebaut, um auf Server zuzugreifen, die für die Namenauflösung, Authentifizierung, Aktualisierung der Wartung usw. erforderlich sind.  
  
-   **Benutzer-Tunneldatenverkehrverbindungen**: Dieser Tunnel wird auf dem Computer vom Benutzerkonto in einem Benutzerkontext aufgebaut, wenn der Benutzer versucht, auf eine Ressource im Unternehmensnetzwerk zuzugreifen. Je nach Bereitstellungsanforderungen muss ein Benutzer möglicherweise sichere Anmeldungsinformationen angeben (z. B. mit einer Smartcard oder einem Einmalkennwort), um auf Ressourcen im Unternehmensnetzwerk zuzugreifen.  
  
Für DirectAccess wird eine Verbindung durch die IP-Adresse des Remoteclients eindeutig identifiziert. Wenn ein Computertunnel beispielsweise für einen Clientcomputer geöffnet wurde und ein Benutzer über diesen Computer verbunden ist, verwenden sie die gleiche Verbindung. Wenn der Benutzer die Verbindung trennt und erneut herstellt, während der Computertunnel noch aktiv ist, handelt es sich um eine einzelne Verbindung.  
  


