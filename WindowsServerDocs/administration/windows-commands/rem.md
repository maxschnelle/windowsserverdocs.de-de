---
title: rem
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a45b585-a83c-4ff6-badd-ff40f34cec23
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 85c8a69bf21a386cd36e45bbca6dacd35aef2509
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847001"
---
# <a name="rem"></a>rem



Datensätze in den Kommentaren ("Hinweise") eine Batchdatei oder Konfiguration. SYS. Wenn kein Kommentar angegeben wird, **Rem** vertikalen Abstand hinzugefügt.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
rem [<Comment>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Kommentar >|Gibt eine Zeichenfolge, die als Kommentar enthalten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die **Rem** Befehl Kommentare nicht auf dem Bildschirm angezeigt. Verwenden Sie die **auf echo** Befehl in der Batchdatei oder Konfiguration. SYS-Datei, die Kommentare auf dem Bildschirm anzuzeigen.
-   Sie können kein Umleitungszeichen (**<** oder **>**) oder einer Pipe (**|**) in einem Batch-Datei-Kommentar.
-   Sie können zwar **Rem** ohne einen Kommentar zum vertikalen Abstand zu einer Batchdatei hinzufügen, können Sie auch leere Zeilen. Leere Zeilen werden ignoriert, wenn ein Batch-Anwendung verarbeitet wird.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel zeigt eine Batchdatei, die Hinweise für Kommentare und für den vertikalen Abstand verwendet:
```
@echo off
rem  This batch program formats and checks new disks.
rem  It is named Checknew.bat.
rem
rem echo Insert new disk in Drive B.
pause 
format b: /v chkdsk b: 
```
Sollen einen erläuternden Kommentar vor der **Eingabeaufforderung** in Ihre Konfiguration den Befehl. SYS-Datei, fügen Sie die folgenden Zeilen für die Konfiguration. SYS:
```
rem Set prompt to indicate current directory
prompt $p$g
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)