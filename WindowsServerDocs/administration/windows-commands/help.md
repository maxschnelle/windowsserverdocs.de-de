---
title: help
description: Referenz Thema für den Help-Befehl, in dem eine Liste der verfügbaren Befehle oder ausführliche Hilfe Informationen zu einem angegebenen Befehl angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c65b5ac3-711a-4368-95b8-ba82e2d00713
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b73ef32b49b834a91f24e943749eb21398c8588
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818660"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
