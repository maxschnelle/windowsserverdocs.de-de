---
title: pause
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cab3afc3-d046-432f-a0bf-6282f0099032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 109d162e8d5c4bdd59871a21f16b6f568df4fbd6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861661"
---
# <a name="pause"></a>pause



Hält die Verarbeitung einer Batchdatei aus, und die folgende Eingabeaufforderung angezeigt:
```
Press any key to continue . . .
```
Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
pause
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Beim Ausführen der **anhalten** Befehl die folgende Meldung angezeigt:  
    ```
    Press any key to continue . . .
    ```  
-   Wenn Sie zum Beenden eines Batchprogramms STRG + C drücken, wird die folgende Meldung angezeigt:  
    ```
    Terminate batch job (Y/N)?
    ```  
    Wenn Sie Y (für Ja) als Reaktion auf diese Meldung klicken, gibt der Batch beendet und die Steuerung an das Betriebssystem.
-   Sie können zum Einfügen der **anhalten** Befehl, bevor Sie einen Abschnitt der Batch-Datei, die Sie möglicherweise nicht verarbeiten möchten. Wenn **anhalten** hält die Verarbeitung des Batchprogramms, können Sie STRG + C drücken und drücken Sie Y, um die Batchprogramm zu beenden.

## <a name="BKMK_examples"></a>Beispiele für

Um ein Batchprogramm erstellen, die den Benutzer auffordert, die Datenträger in einem dieser Laufwerke zu ändern, geben Sie Folgendes ein:
```
@echo off 
:Begin 
copy a:*.* 
echo Put a new disk into drive A 
pause 
goto begin
```
In diesem Beispiel werden alle Dateien auf dem Datenträger im Laufwerk einer im aktuellen Verzeichnis kopiert. Nachdem die Nachricht einfügen ein neues Datenträgers in Laufwerk A, aufgefordert werden, die **anhalten** Befehl hält die Verarbeitung, damit Sie Datenträger ändern können, und drücken Sie dann die eine beliebige Taste, um die Verarbeitung fortzusetzen. Das Batchprogramm, die in einer Endlosschleife ausgeführt wird – die **Goto beginnen** Befehl sendet den Befehlsinterpreter an die Begin-Bezeichnung der Batch-Datei. Um dieses Batchprogramm zu beenden, drücken Sie STRG + C drücken Sie anschließend Y.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)