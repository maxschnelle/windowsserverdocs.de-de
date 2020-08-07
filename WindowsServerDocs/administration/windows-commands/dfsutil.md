---
title: Dfsutil
description: Referenz Artikel für den Dfsutil-Befehl, der DFS-Namespaces, Server und Clients verwaltet.
ms.topic: article
ms.assetid: ef5093a4-0d24-4b21-9d04-59933ad98e2c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f31af9f557271182980a367ebf5e2233788fcc31
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891027"
---
# <a name="dfsutil"></a>Dfsutil

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der Dfsutil-Befehl verwaltet DFS-Namespaces,-Server und-Clients.

## <a name="functionality-available-in-powershell"></a>In PowerShell verfügbare Funktionalität

Das [DFSN](/powershell/module/dfsn/?view=win10-ps) -PowerShell-Modul bietet entsprechende Funktionen für die folgenden Dfsutil-Parameter.

| Parameter | BESCHREIBUNG |
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
