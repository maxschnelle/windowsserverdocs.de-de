---
title: rem
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1a45b585-a83c-4ff6-badd-ff40f34cec23
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94428e6d5ec6fdb482a5d0d15bd1120e45ffea80
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836113"
---
# <a name="rem"></a>rem



Zeichnet Kommentare (Hinweise) in einer Batchdatei oder-Konfiguration auf. Einsetzt. Wenn kein Kommentar angegeben wird, fügt **REM** den vertikalen Abstand hinzu.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
rem [<Comment>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Kommentar >|Gibt eine Zeichenfolge an, die als Kommentar eingeschlossen werden soll.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Der **REM** -Befehl zeigt keine Kommentare auf dem Bildschirm an. Sie müssen den Befehl **Echo on** in Ihrem Batch oder in der Konfiguration verwenden. SYS-Datei zum Anzeigen von Kommentaren auf dem Bildschirm.
-   Ein Umleitungs Zeichen ( **<** oder **>** ) oder eine Pipe ( **|** ) kann nicht in einem Batchdatei Kommentar verwendet werden.
-   Obwohl Sie **REM** ohne einen Kommentar zum Hinzufügen von vertikaler Abstände zu einer Batchdatei verwenden können, können Sie auch leere Zeilen verwenden. Leere Zeilen werden ignoriert, wenn ein Batch-Programm verarbeitet wird.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Das folgende Beispiel zeigt eine Batchdatei, die Hinweise auf Kommentare und einen vertikalen Abstand verwendet:
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)