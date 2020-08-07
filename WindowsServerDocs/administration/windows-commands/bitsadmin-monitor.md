---
title: bitsadmin monitor
description: Referenz Artikel zum Befehl bizadmin Monitor, mit dem Aufträge in der Übertragungs Warteschlange überwacht werden, deren Besitzer der aktuelle Benutzer ist.
ms.topic: article
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3ba2cb315fb0696b8363506669aa41f1693bb758
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893662"
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
| /ALLUSERS | Optional. Überwacht Aufträge für alle Benutzer. Sie müssen über Administratorrechte verfügen, um diesen Parameter zu verwenden. |
| /Refresh | Optional. Aktualisiert die Daten in einem durch angegebenen Intervall `<seconds>` . Das Standard Aktualisierungs Intervall beträgt 5 Sekunden. Drücken Sie STRG + C, um die Aktualisierung zu verhindern. |

## <a name="examples"></a>Beispiele

Zum Überwachen der Übertragungs Warteschlange für Aufträge, die im Besitz des aktuellen Benutzers sind, und Aktualisieren der Informationen alle 60 Sekunden.

```
bitsadmin /monitor /refresh 60
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
