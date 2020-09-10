---
title: rem
description: Referenz Artikel für den REM-Befehl, der Kommentare in einem Skript, in einem Batch oder in einer config.sys Datei aufzeichnet.
ms.topic: reference
ms.assetid: 1a45b585-a83c-4ff6-badd-ff40f34cec23
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c56595a45eba3fd841f1f455c189164b240191e8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640650"
---
# <a name="rem"></a>rem

Zeichnet Kommentare in einem Skript, in einem Batch oder in einer config.sys Datei auf. Wenn kein Kommentar angegeben wird, fügt **REM** den vertikalen Abstand hinzu.

## <a name="syntax"></a>Syntax

```
rem [<comment>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<comment>` | Gibt eine Zeichenfolge an, die als Kommentar eingeschlossen werden soll. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Der **REM** -Befehl zeigt keine Kommentare auf dem Bildschirm an. Wenn Sie Kommentare auf dem Bildschirm anzeigen möchten, müssen Sie den Befehl **Echo on** in Ihre Datei einschließen.

- Ein Umleitungs Zeichen ( `<` oder `>` ) oder eine Pipe () kann nicht `|` in einem Batchdatei Kommentar verwendet werden.

- Obwohl Sie **REM** ohne einen Kommentar zum Hinzufügen von vertikaler Abstände zu einer Batchdatei verwenden können, können Sie auch leere Zeilen verwenden. Leere Zeilen werden ignoriert, wenn ein Batch-Programm verarbeitet wird.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den vertikalen Abstand durch Batchdatei Kommentare hinzuzufügen:

```
@echo off
rem  This batch program formats and checks new disks.
rem  It is named Checknew.bat.
rem
rem echo Insert new disk in Drive B.
pause
format b: /v chkdsk b:
```

Geben Sie Folgendes ein, um einen erklärenden Kommentar vor dem **Eingabe** Aufforderungs Befehl in einer config.sys Datei einzufügen:

```
rem Set prompt to indicate current directory
prompt $p$g
```

Geben Sie Folgendes ein, um einen Kommentar zum Funktionsumfang eines Skripts bereitzustellen:

```
rem The commands in this script set up 3 drives.
rem The first drive is a primary partition and is
rem assigned the letter D. The second and third drives
rem are logical partitions, and are assigned letters
rem E and F.
create partition primary size=2048
assign d:
create partition extended
create partition logical size=2048
assign e:
create partition logical
assign f:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)