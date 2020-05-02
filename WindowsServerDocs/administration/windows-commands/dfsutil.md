---
title: Dfsutil
description: Referenz Thema für Dfsutil, das DFS-Namespaces, Server und Clients verwaltet. Dfsutil-Befehle verwenden die ursprüngliche verteiltes Dateisystem Terminologie, wobei die aktualisierte Terminologie für DFS-Namespaces als Erklärung für die meisten Befehle bereitgestellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ef5093a4-0d24-4b21-9d04-59933ad98e2c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 999eef79227d4531ba724c9cac40127297ea38a0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719514"
---
# <a name="dfsutil"></a>Dfsutil

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der Dfsutil-Befehl verwaltet DFS-Namespaces,-Server und-Clients.

>[!NOTE]
>Das **PowerShell-Modul für DFS-Namespaces** stellt Ersetzungen für einige der Dfsutil-Parameter bereit, während andere weiterhin Dfsutil verwenden müssen. Weitere Informationen zu den aktualisierten PowerShell-Entsprechungen finden Sie unter [DFSN](https://docs.microsoft.com/powershell/module/dfsn/?view=win10-ps).

## <a name="parameters-available-in-powershell"></a>In PowerShell verfügbare Parameter

Sie können die folgenden Parameter in PowerShell verwenden:

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| root | Zeigt, erstellt, entfernt, importiert und exportiert Namespace Stämme. |
| link | Hiermit werden Ordner angezeigt, erstellt, entfernt oder verschoben (links). |
| target | Zeigt, erstellt oder entfernt den Ordner Ziel-oder Namespace Server. |
| property | Zeigt ein Ordner Ziel oder einen Namespace Server an oder ändert ihn. |
| server | Dient zum Anzeigen oder Ändern der Namespace Konfiguration. |
| Domäne | Zeigt alle domänenbasierten Namespaces in einer Domäne an. |

## <a name="parameters-only-available-in-dfsutil"></a>Parameter sind nur in Dfsutil verfügbar.

Die folgenden Parameter können nur von DFSUtil verwendet werden.

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Client | Zeigt Client Informationen oder Registrierungsschlüssel an oder ändert Sie. |
| Diag | Ausführen von Diagnosen oder Anzeigen von dfsdirs/dfspath. |
| cache | Zeigt den Client Cache an oder leert ihn. |

Weitere Informationen zu den einzelnen Befehlen erhalten Sie, indem Sie auf einem Server, auf dem die DFS-Namespaces-Verwaltungs Tools installiert sind, `dfsutil client /?`eine `dfsutil diag /?`Eingabeaufforderung `dfsutil cache /?`öffnen und dann, oder eingeben.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)