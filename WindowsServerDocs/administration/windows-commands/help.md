---
title: help
description: Referenz Artikel für den Help-Befehl, der eine Liste der verfügbaren Befehle oder ausführliche Hilfe Informationen zu einem angegebenen Befehl anzeigt.
ms.topic: reference
ms.assetid: c65b5ac3-711a-4368-95b8-ba82e2d00713
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5e1ee94be773d546b2ef441d370c7cb91ee6c167
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634624"
---
# <a name="help"></a>help

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Liste der verfügbaren Befehle oder ausführliche Hilfe Informationen zu einem angegebenen Befehl an. Wenn Sie ohne Parameter verwendet wird, werden die einzelnen Systembefehle in der **Hilfe** aufgeführt und kurz beschrieben.

## <a name="syntax"></a>Syntax

```
help [<command>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<command>` | Gibt den Befehl an, für den ausführliche Hilfe Informationen angezeigt werden sollen. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen zum **Robocopy** -Befehl anzuzeigen:

```
help robocopy
```

Geben Sie Folgendes ein, um eine Liste aller in DiskPart verfügbaren Befehle anzuzeigen:

```
help
```

Geben Sie Folgendes ein, um ausführliche Hilfe Informationen zur Verwendung des Befehls **create partition primary** in DiskPart anzuzeigen:

```
help create partition primary
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
