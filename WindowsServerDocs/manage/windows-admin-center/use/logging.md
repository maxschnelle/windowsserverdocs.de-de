---
title: Protokollierung
description: Ereignisprotokollierung von Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d91b92cb3bba99ae4aa96a96650a251a6df4cea5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849301"
---
# <a name="use-event-logging-in-windows-admin-center-to-gain-insight-into-management-activities-and-track-gateway-usage"></a>Verwenden Sie die ereignisprotokollierung in Windows Admin Center Einblick in den Management-Aktivitäten und Gateway-Verwendung nachverfolgen

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Windows Admin Center schreibt Ereignisprotokolle finden Sie in der Management-Aktivitäten, die für die Server in Ihrer Umgebung ausgeführt werden können, als auch können Sie die Windows Admin Center-Probleme zu beheben.

## <a name="gain-insight-into-management-activities-in-your-environment-through-user-action-logging"></a>Gewinnen von Einblicken in den Management-Aktivitäten in Ihrer Umgebung über die Benutzer-Aktion-Protokollierung

Windows Admin Center bietet einen Einblick in den Management-Aktivitäten, die auf den Servern in Ihrer Umgebung ausgeführt werden, durch die der Protokollierungsaktionen, die die **Microsoft-ServerManagementExperience** ereigniskanal im Ereignisprotokoll der verwalteten Server, mit der EventID-4000 und Quelle SMEGateway. Windows Admin Center protokolliert Aktionen, die nur auf dem verwalteten Server, damit Sie nicht, dass Ereignisse protokolliert sehen, wenn ein Benutzer für nur-Lese Zwecke auf einen Server zugreift.

Protokollierte Ereignisse umfassen die folgende Informationen an:

| Key           | Wert                                                                                              |
|---------------|----------------------------------------------------------------------------------------------------|
| PowerShell    | Namen der PowerShell-Skripts, die auf dem Server ausgeführt wurde, wenn die Aktion ein PowerShell-Skript ausgeführt wurde. |
| CIM           | CIM-Aufruf, der auf dem Server ausgeführt wurde, wenn die Aktion einen CIM-Aufruf ausgeführt wurde.                        |
| Modul        | -Tool (oder Moduls), in dem die Aktion ausgeführt wurde                                                     |
| Gateway       | Name des Gatewaycomputers Windows Admin Center, in dem die Aktion ausgeführt wurde                     |
| UserOnGateway | Benutzername für das Gateway Windows Admin Center zugreifen, und führen die Aktion                    |
| UserOnTarget  | Benutzername, den Zugriff auf die verwalteten Ziel-Server verwendet wird, falls diese von der UserOnGateway (d. h. der Benutzer, der mit dem Server mithilfe von "Verwalten als" Anmeldeinformationen zugegriffen) |
| Delegierung    | Boolescher Wert: Wenn der verwaltete Server vertraut, das Gateway und Anmeldeinformationen werden von Client-Computer des Benutzers delegiert             |
| LAPS          | Boolescher Wert: Wenn der Benutzer dem Server mit Zugriff auf [LAPS](https://technet.microsoft.com/mt227395.aspx) Anmeldeinformationen                          |
| Datei          | Name der Datei hochgeladen, wenn die Aktion eine Datei hoch war.                                |

## <a name="learn-about-windows-admin-center-activity-with-event-logging"></a>Erfahren Sie mehr über Windows Admin Center-Aktivität, bei der Protokollierung von Komponentenereignissen

Windows Admin Center protokolliert die Gateway-Aktivität an den ereigniskanal auf dem Gatewaycomputer zum Behandeln von Problemen und Anzeigen von Metriken auf der Nutzung. Diese Ereignisse werden protokolliert, um die **Microsoft-ServerManagementExperience** Ereignis-Kanal.

[Weitere Informationen zur Problembehandlung bei Windows Admin Center.](troubleshooting.md)
