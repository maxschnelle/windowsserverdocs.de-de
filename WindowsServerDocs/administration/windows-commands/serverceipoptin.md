---
title: serverceipoptin
description: Referenz Artikel für serverceipoptin, mit dem Sie am Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP) teilnehmen können.
ms.topic: reference
ms.assetid: 3d7d7fa7-0689-4797-b802-36fe260d21a0
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6df387158a9630ab767dda655346836355fae936
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389168"
---
# <a name="serverceipoptin"></a>serverceipoptin

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht die Teilnahme am Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP).

## <a name="syntax"></a>Syntax

```
serverceipoptin [/query] [/enable] [/disable]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /Query "aus | Überprüft die aktuelle Einstellung. |
| /enable | Aktiviert die Teilnahme an CEIP. |
| /Disable | Deaktiviert die Teilnahme an CEIP. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Zum Überprüfen der aktuellen Einstellungen geben Sie Folgendes ein:

```
serverceipoptin /query
```

Geben Sie Folgendes ein, um die Teilnahme zu aktivieren:

```
serverceipoptin /enable
```

Geben Sie Folgendes ein, um die Teilnahme zu deaktivieren:

```
serverceipoptin /disable
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
