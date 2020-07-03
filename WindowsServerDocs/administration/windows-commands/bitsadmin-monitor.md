---
title: bitsadmin monitor
description: Referenz Artikel zum Befehl bizadmin Monitor, mit dem Aufträge in der Übertragungs Warteschlange überwacht werden, deren Besitzer der aktuelle Benutzer ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7ce08eccf46fc17086d216bc6797bec451ace7eb
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926497"
---
# <a name="bitsadmin-monitor"></a>bitsadmin monitor

Überwacht Aufträge in der Übertragungs Warteschlange, deren Besitzer der aktuelle Benutzer ist.

## <a name="syntax"></a>Syntax

```
bitsadmin /monitor [/allusers] [/refresh <seconds>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| /ALLUSERS | Dies ist optional. Überwacht Aufträge für alle Benutzer. Sie müssen über Administratorrechte verfügen, um diesen Parameter zu verwenden. |
| /Refresh | Dies ist optional. Aktualisiert die Daten in einem durch angegebenen Intervall `<seconds>` . Das Standard Aktualisierungs Intervall beträgt 5 Sekunden. Drücken Sie STRG + C, um die Aktualisierung zu verhindern. |

## <a name="examples"></a>Beispiele

Zum Überwachen der Übertragungs Warteschlange für Aufträge, die im Besitz des aktuellen Benutzers sind, und Aktualisieren der Informationen alle 60 Sekunden.

```
bitsadmin /monitor /refresh 60
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
