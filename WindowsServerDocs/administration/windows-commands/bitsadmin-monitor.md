---
title: bitsadmin monitor
description: Referenz Thema für den Befehl bizadmin Monitor, mit dem Aufträge in der Übertragungs Warteschlange überwacht werden, deren Besitzer der aktuelle Benutzer ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4c8fa52f9fcf30a66b41c9cdbf7b7e1fab69f06e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717376"
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
| /Refresh | Optional. Aktualisiert die Daten in einem durch `<seconds>`angegebenen Intervall. Das Standard Aktualisierungs Intervall beträgt 5 Sekunden. Drücken Sie STRG + C, um die Aktualisierung zu verhindern. |

## <a name="examples"></a>Beispiele

Zum Überwachen der Übertragungs Warteschlange für Aufträge, die im Besitz des aktuellen Benutzers sind, und Aktualisieren der Informationen alle 60 Sekunden.

```
bitsadmin /monitor /refresh 60
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
