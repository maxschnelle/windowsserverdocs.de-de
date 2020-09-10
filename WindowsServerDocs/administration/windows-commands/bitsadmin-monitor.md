---
title: bitsadmin monitor
description: Referenz Artikel zum Befehl bizadmin Monitor, mit dem Aufträge in der Übertragungs Warteschlange überwacht werden, deren Besitzer der aktuelle Benutzer ist.
ms.topic: reference
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2245d9e4375130877755f96eed42a46a479742f3
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631472"
---
# <a name="bitsadmin-monitor"></a>bitsadmin monitor

Überwacht Aufträge in der Übertragungs Warteschlange, deren Besitzer der aktuelle Benutzer ist.

## <a name="syntax"></a>Syntax

```
bitsadmin /monitor [/allusers] [/refresh <seconds>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| /ALLUSERS | (Optional) Überwacht Aufträge für alle Benutzer. Sie müssen über Administratorrechte verfügen, um diesen Parameter zu verwenden. |
| /Refresh | (Optional) Aktualisiert die Daten in einem durch angegebenen Intervall `<seconds>` . Das Standard Aktualisierungs Intervall beträgt 5 Sekunden. Drücken Sie STRG + C, um die Aktualisierung zu verhindern. |

## <a name="examples"></a>Beispiele

Zum Überwachen der Übertragungs Warteschlange für Aufträge, die im Besitz des aktuellen Benutzers sind, und Aktualisieren der Informationen alle 60 Sekunden.

```
bitsadmin /monitor /refresh 60
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
