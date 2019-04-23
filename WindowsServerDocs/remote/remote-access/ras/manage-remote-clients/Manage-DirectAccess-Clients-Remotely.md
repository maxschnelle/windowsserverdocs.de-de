---
title: Remote-Verwaltung von DirectAccess-Clients
description: Dieses Thema ist Teil des Leitfadens verwalten DirectAccess-Clients Remote in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 36255d80-a13e-4af7-a5c0-ab4c8f302622
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 736495ff5d1d5d3ba73fa86e6030606da92271de
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832751"
---
# <a name="manage-directaccess-clients-remotely"></a>Remote-Verwaltung von DirectAccess-Clients

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die Überwachung des Remotezugriffs meldet Remotebenutzeraktivitäten und den Status der DirectAccess- und VPN-Verbindungen. Sie zeichnet die Anzahl und die Dauer der Clientverbindungen (und weitere Statistiken) auf und überwacht den Betriebsstatus des Servers. Eine benutzerfreundliche Überwachungskonsole stellt Ihnen eine Ansicht der gesamten Remotezugriffinfrastruktur bereit. Die Überwachungsansichten sind für einzelne Server-, Cluster- und Konfigurationen für mehrere Standorte.  
  
**Hinweis**: Windows Server 2016 werden DirectAccess "und" Remote Access Service (RAS) in einer einzigen remotezugriffsrolle zusammengefasst.  
  
## <a name="in-this-guide"></a>Inhalt dieser Anleitung  
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
  


