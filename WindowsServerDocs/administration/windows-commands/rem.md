---
title: rem
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1a45b585-a83c-4ff6-badd-ff40f34cec23
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d115548f15ff45087a771458062da8a3ef919eb3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722462"
---
# <a name="rem"></a>rem



Zeichnet Kommentare (Hinweise) in einer Batchdatei oder-Konfiguration auf. Einsetzt. Wenn kein Kommentar angegeben wird, fügt **REM** den vertikalen Abstand hinzu.



## <a name="syntax"></a>Syntax

```
rem [<Comment>]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Kommentar>|Gibt eine Zeichenfolge an, die als Kommentar eingeschlossen werden soll.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

-   Der **REM** -Befehl zeigt keine Kommentare auf dem Bildschirm an. Sie müssen den Befehl **Echo on** in Ihrem Batch oder in der Konfiguration verwenden. SYS-Datei zum Anzeigen von Kommentaren auf dem Bildschirm.
-   Ein Umleitungs Zeichen (**<** oder **>**) oder eine Pipe (**|**) kann nicht in einem Batchdatei Kommentar verwendet werden.
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
, Wenn ein erklärender Kommentar vor dem **Eingabe** Aufforderungs Befehl in der Konfiguration enthalten sein soll. SYS-Datei, fügen Sie der Konfigurationsdatei die folgenden Zeilen hinzu. Einsetzt
```
rem Set prompt to indicate current directory
prompt $p$g
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)