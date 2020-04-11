---
title: Dfsutil
description: Windows-Befehls Thema für Dfsutil, das DFS-Namespaces,-Server und-Clients verwaltet. Dfsutil-Befehle verwenden die ursprüngliche verteiltes Dateisystem Terminologie, wobei die aktualisierte Terminologie für DFS-Namespaces als Erklärung für die meisten Befehle bereitgestellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ef5093a4-0d24-4b21-9d04-59933ad98e2c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 47d468ee122dc78cc880f4a9bc0705354e0b5214
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122555"
---
# <a name="dfsutil"></a>Dfsutil

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der Dfsutil-Befehl verwaltet DFS-Namespaces,-Server und-Clients.

>[!NOTE]
>Das **PowerShell-Modul für DFS-Namespaces** stellt Ersetzungen für einige der Dfsutil-Parameter bereit, während andere weiterhin Dfsutil verwenden müssen. Weitere Informationen zu den aktualisierten PowerShell-Entsprechungen finden Sie unter [DFSN](https://docs.microsoft.com/powershell/module/dfsn/?view=win10-ps).

## <a name="parameters-available-in-powershell"></a>In PowerShell verfügbare Parameter

Sie können die folgenden Parameter in PowerShell verwenden:

| Parameter | Beschreibung |
| --------- | ----------- |
| root | Zeigt, erstellt, entfernt, importiert und exportiert Namespace Stämme. |
| Link | Hiermit werden Ordner angezeigt, erstellt, entfernt oder verschoben (links). |
| target | Zeigt, erstellt oder entfernt den Ordner Ziel-oder Namespace Server. |
| property | Zeigt ein Ordner Ziel oder einen Namespace Server an oder ändert ihn. |
| Server | Dient zum Anzeigen oder Ändern der Namespace Konfiguration. |
| Domäne | Zeigt alle domänenbasierten Namespaces in einer Domäne an. |

## <a name="parameters-only-available-in-dfsutil"></a>Parameter sind nur in Dfsutil verfügbar.

Die folgenden Parameter können nur von DFSUtil verwendet werden.

| Parameter | Beschreibung |
| --------- | ----------- |
| client | Zeigt Client Informationen oder Registrierungsschlüssel an oder ändert Sie. |
| Diag | Ausführen von Diagnosen oder Anzeigen von dfsdirs/dfspath. |
| Cache | Zeigt den Client Cache an oder leert ihn. |

Weitere Informationen zu den einzelnen Befehlen erhalten Sie, indem Sie auf einem Server, auf dem die DFS-Namespaces-Verwaltungs Tools installiert sind, eine Eingabeaufforderung öffnen und dann `dfsutil client /?`, `dfsutil diag /?`oder `dfsutil cache /?`eingeben.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)