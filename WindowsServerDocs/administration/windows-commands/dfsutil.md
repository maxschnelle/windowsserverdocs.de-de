---
title: Dfsutil
description: Referenz Artikel für den Dfsutil-Befehl, der DFS-Namespaces, Server und Clients verwaltet.
ms.topic: reference
ms.assetid: ef5093a4-0d24-4b21-9d04-59933ad98e2c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9fb3883403dd0f4a88b612655247c4f4a2df7de7
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635043"
---
# <a name="dfsutil"></a>Dfsutil

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der Dfsutil-Befehl verwaltet DFS-Namespaces,-Server und-Clients.

## <a name="functionality-available-in-powershell"></a>In PowerShell verfügbare Funktionalität

Das [DFSN](/powershell/module/dfsn/?view=win10-ps) -PowerShell-Modul bietet entsprechende Funktionen für die folgenden Dfsutil-Parameter.

| Parameter | Beschreibung |
| --------- | ----------- |
| root | Zeigt, erstellt, entfernt, importiert und exportiert Namespace Stämme. |
| link | Hiermit werden Ordner angezeigt, erstellt, entfernt oder verschoben (links). |
| target | Zeigt, erstellt oder entfernt den Ordner Ziel-oder Namespace Server. |
| property | Zeigt ein Ordner Ziel oder einen Namespace Server an oder ändert ihn. |
| server | Dient zum Anzeigen oder Ändern der Namespace Konfiguration. |
| Domäne | Zeigt alle domänenbasierten Namespaces in einer Domäne an. |

## <a name="functionality-available-only-in-dfsutil"></a>Funktionalität nur in Dfsutil verfügbar

Die folgende Funktionalität ist nur als Dfsutil-Parameter verfügbar:

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Client | Zeigt Client Informationen oder Registrierungsschlüssel an oder ändert Sie. |
| Diag | Ausführen von Diagnosen oder Anzeigen von dfsdirs/dfspath. |
| cache | Zeigt den Client Cache an oder leert ihn. |

Weitere Informationen zu den einzelnen Befehlen erhalten Sie, indem Sie auf einem Server, auf dem die DFS-Namespaces-Verwaltungs Tools installiert sind, eine Eingabeaufforderung öffnen und dann `dfsutil client /?` , `dfsutil diag /?` oder eingeben `dfsutil cache /?` .

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
