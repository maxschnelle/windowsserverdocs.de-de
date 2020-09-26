---
title: serverweroptin
description: Referenz Artikel für den Befehl "serverweroptin", mit dem Sie die Fehlerberichterstattung aktivieren können.
ms.topic: reference
ms.assetid: f3c0b0af-cafb-4f09-8b36-5a357ddf392d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c8a2fe32634704a22f12430b8516ed7f6cae4e82
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389132"
---
# <a name="serverweroptin"></a>serverweroptin

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht es Ihnen, die Fehlerberichterstattung zu aktivieren.

## <a name="syntax"></a>Syntax

```
serverweroptin [/query] [/detailed] [/summary]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /Query "aus | Überprüft die aktuelle Einstellung. |
| /Detailed | Gibt an, dass detaillierte Berichte automatisch gesendet werden. |
| /Summary | Gibt an, dass Zusammenfassungs Berichte automatisch gesendet werden sollen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Zum Überprüfen der aktuellen Einstellung geben Sie Folgendes ein:

```
serverweroptin /query
```

Geben Sie Folgendes ein, um automatisch ausführliche Berichte zu senden:

```
serverweroptin /detailed
```

Geben Sie zum automatischen Senden von Zusammenfassungs Berichten Folgendes ein:

```
serverweroptin /summary
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
