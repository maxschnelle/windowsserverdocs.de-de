---
title: rem
description: Referenz Artikel für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1a45b585-a83c-4ff6-badd-ff40f34cec23
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5161a3ba0904396f29b7c567e3a16da5f95e5271
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933498"
---
# <a name="rem"></a>rem



Zeichnet Kommentare (Hinweise) in einer Batchdatei oder CONFIG.SYS auf. Wenn kein Kommentar angegeben wird, fügt **REM** den vertikalen Abstand hinzu.



## <a name="syntax"></a>Syntax

```
rem [<Comment>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Comment>|Gibt eine Zeichenfolge an, die als Kommentar eingeschlossen werden soll.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Der **REM** -Befehl zeigt keine Kommentare auf dem Bildschirm an. Sie müssen den Befehl **Echo on** in der Batch-oder CONFIG.SYS Datei verwenden, um Kommentare auf dem Bildschirm anzuzeigen.
-   Ein Umleitungs Zeichen ( **<** oder **>** ) oder eine Pipe () kann nicht **|** in einem Batchdatei Kommentar verwendet werden.
-   Obwohl Sie **REM** ohne einen Kommentar zum Hinzufügen von vertikaler Abstände zu einer Batchdatei verwenden können, können Sie auch leere Zeilen verwenden. Leere Zeilen werden ignoriert, wenn ein Batch-Programm verarbeitet wird.

## <a name="examples"></a>Beispiele

So zeigen Sie eine Batchdatei an, in der Hinweise für Kommentare und für den vertikalen Abstand verwendet werden:
```
@echo off
rem  This batch program formats and checks new disks.
rem  It is named Checknew.bat.
rem
rem echo Insert new disk in Drive B.
pause
format b: /v chkdsk b:
```
Fügen Sie CONFIG.SYS die folgenden Zeilen hinzu, um einen erläuternden Kommentar vor dem **Eingabe** Aufforderungs Befehl in der CONFIG.SYS-Datei einzufügen:
```
rem Set prompt to indicate current directory
prompt $p$g
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)