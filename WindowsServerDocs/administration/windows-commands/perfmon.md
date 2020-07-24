---
title: perfmon
description: Referenz Artikel für den Perfmon-Befehl, der den Windows-Zuverlässigkeits-und Leistungs Monitor in einem bestimmten eigenständigen Modus startet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9a8d5eca-8473-463e-a6e0-7bbd590b18e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/25/2018
ms.openlocfilehash: a234c272d812ab225085d07ae66dcc6ecfaedba5
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86956612"
---
# <a name="perfmon"></a>perfmon

Starten Sie die Windows-Zuverlässigkeits-und Leistungsüberwachung in einem bestimmten eigenständigen Modus.

## <a name="syntax"></a>Syntax

```
perfmon </res|report|rel|sys>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| /res | Startet die Ressourcenansicht. |
| /Report ein | Startet den Datensammler Satz für die System Diagnose und zeigt einen Bericht der Ergebnisse an. |
| /rel | Startet den Zuverlässigkeits Monitor. |
| /sys | Startet den System Monitor. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Windows-Leistungsüberwachung](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc749154(v%3dws.11))
