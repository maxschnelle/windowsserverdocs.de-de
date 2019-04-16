---
title: Ereignisprotokollierung
description: Protokollierung von Windows Admin Center (Project Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d91b92cb3bba99ae4aa96a96650a251a6df4cea5
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/22/2018
ms.locfileid: "2074341"
---
# <a name="use-event-logging-in-windows-admin-center-to-gain-insight-into-management-activities-and-track-gateway-usage"></a>Verwenden der Protokollierung in Windows-Verwaltungskonsole Einblick in Management-Aktivitäten und Nachverfolgen Gateway Verwendungsanalyse

>Betrifft: Windows-Verwaltungskonsole, Windows-Verwaltungskonsole – Vorschau

Windows-Verwaltungskonsole schreibt Ereignisprotokolle finden Sie in der Management-Aktivitäten auf den Servern in Ihrer Umgebung durchgeführt werden können, als auch zum Windows-Verwaltungskonsole Probleme beheben von Problemen.

## <a name="gain-insight-into-management-activities-in-your-environment-through-user-action-logging"></a>Management von Aktivitäten in Ihrer Umgebung durch Benutzer Aktion Protokollierung Einblick

Windows-Verwaltungskonsole bietet einen Einblick in die Aktivitäten Management auf den Servern in Ihrer Umgebung von Protokollierungsaktionen an den **Microsoft-ServerManagementExperience** Ereignis Kanal im Ereignisprotokoll des verwalteten Servers an, mit EventID 4000 und SMEGateway Datenquelle. Windows-Verwaltungskonsole protokolliert nur Aktionen auf dem verwalteten Server, damit Sie nicht Ereignisse protokolliert sehen, wenn ein Benutzer einen Server für schreibgeschützte Zwecke greift auf.

Protokollierten Ereignisse enthalten die folgenden Informationen:

| Schlüssel           | Wert                                                                                              |
|---------------|----------------------------------------------------------------------------------------------------|
| PowerShell    | PowerShell-Skriptname, der auf dem Server ausgeführt wurde, wenn die Aktion ein PowerShell-Skripts ausgeführt wurde |
| CIM           | CIM-Anruf, der auf dem Server ausgeführt wurde, wenn die Aktion ein Anrufs CIM ausgeführt wurde.                        |
| Modul        | Tool (oder Modul), in der die Aktion ausgeführt wurde                                                     |
| Gateway       | Name des Windows-Verwaltungskonsole Gateway Computers, auf dem die Aktion ausgeführt wurde                     |
| UserOnGateway | Benutzernamen für den Zugriff auf das Gateway Windows Admin Center und die Aktion ausgeführt                    |
| UserOnTarget  | Benutzernamen für den Zugriff auf den verwalteten Zielserver, falls verschieden vom die UserOnGateway (d. h. der Benutzer mit dem Server mit den Anmeldeinformationen "Als verwalten" zugegriffen) |
| Delegierung    | Boolean: Wenn das Ziel verwaltete Server das Gateway vertraut und Anmeldeinformationen werden von der Clientcomputer des Benutzers delegiert             |
| RUNDEN          | Boolean: Wenn der Benutzer Zugriff auf den Server, die mit [runden](https://technet.microsoft.com/mt227395.aspx) Anmeldeinformationen                          |
| Datei          | Name der Datei hochgeladen, wenn die Aktion Dateiuploads war.                                |

## <a name="learn-about-windows-admin-center-activity-with-event-logging"></a>Erfahren Sie mehr über die Windows-Verwaltungskonsole dortigen ereignisprotokollierung

Windows-Verwaltungskonsole protokolliert Gateway Aktivitäten in der Event-Kanal auf dem Gatewaycomputer, mit denen Sie Probleme zu beheben und Metriken zur Verwendung anzeigen. Diese Ereignisse werden in der **Microsoft-ServerManagementExperience** -Kanal-Ereignis protokolliert.

[Weitere Informationen zur Problembehandlung für Windows-Verwaltungskonsole.](troubleshooting.md)
