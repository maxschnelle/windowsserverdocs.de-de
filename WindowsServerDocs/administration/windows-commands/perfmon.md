---
title: perfmon
description: Referenz Artikel für den Perfmon-Befehl, der den Windows-Zuverlässigkeits-und Leistungs Monitor in einem bestimmten eigenständigen Modus startet.
ms.topic: reference
ms.assetid: 9a8d5eca-8473-463e-a6e0-7bbd590b18e1
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/25/2018
ms.openlocfilehash: c68f0c2160621ed38ea013697f178ec461c8d44c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627446"
---
# <a name="perfmon"></a>perfmon

Starten Sie die Windows-Zuverlässigkeits-und Leistungsüberwachung in einem bestimmten eigenständigen Modus.

## <a name="syntax"></a>Syntax

```
perfmon </res|report|rel|sys>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /res | Startet die Ressourcenansicht. |
| /Report ein | Startet den Datensammler Satz für die System Diagnose und zeigt einen Bericht der Ergebnisse an. |
| /rel | Startet den Zuverlässigkeits Monitor. |
| /sys | Startet den System Monitor. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Windows-Leistungsüberwachung](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc749154(v%3dws.11))
