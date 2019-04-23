---
title: goto
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e0de1458-1f78-48ff-a746-c285a945a510
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f1ad0190519d58bd879ae391f378d800760c204f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857531"
---
# <a name="goto"></a>goto



Leitet cmd.exe an einer Marke in einem Batchprogramm. In einem Batchprogramm und **Goto** leitet die befehlsverarbeitung zu einer Zeile, die von einer Bezeichnung identifiziert wird. Wenn die Bezeichnung gefunden wird, setzt Verarbeitung fort, beginnend mit den Befehlen, die in der nächsten Zeile beginnen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
goto <Label> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Label>|Gibt eine Zeichenfolge, die als Bezeichnung in der Batch-Anwendung verwendet wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Arbeiten mit befehlserweiterungen

    Wenn befehlserweiterungen sind aktiviert (Standard), und Sie verwenden die **Goto** mit einer Bezeichnung Ziel des Befehls **: EOF**, Sie Nichtverwendung die Steuerung an das Ende des die aktuelle Batch-Skriptdatei, und beenden Sie die Batch-Skriptdatei ohne die Definition einer Bezeichnung. Bei Verwendung von **Goto** mit der **: EOF** Bezeichnung, müssen Sie einen Doppelpunkt vor der Marke einfügen. Zum Beispiel:  
    ```
    goto:EOF
    ```  
-   Mit gültigen *Bezeichnung* Werte

    Können Sie Leerzeichen in der *Bezeichnung* -Parameter, aber Sie darf keine andere Trennzeichen (z. B. ein Semikolon oder Gleichheitszeichen) enthalten.
-   Übereinstimmende *Bezeichnung* mit der Bezeichnung in der Batch-Anwendung

    Die *Bezeichnung* von Ihnen angegebene Wert muss eine Bezeichnung in der Batch-Anwendung entsprechen. Die Bezeichnung auf die Batch-Anwendung muss mit einem Doppelpunkt (:).) beginnen. Wenn eine Zeile mit einem Doppelpunkt beginnt, wird er als eine Bezeichnung behandelt, und alle Befehle in dieser Zeile werden ignoriert. Wenn Ihr Batchprogramm nicht mit die Bezeichnung, die Sie angeben enthält, in *Bezeichnung*, die Batch-Anwendung beendet und wird die folgende Meldung angezeigt:  
    ```
    Label not found
    ```  
-   Mithilfe von **Goto** für bedingte Vorgänge

    Sie können **Goto** mit anderen Befehlen zum Ausführen von bedingten Vorgängen. Weitere Informationen zur Verwendung von **Goto** bedingte finden Sie unter den [Wenn](if.md) -Befehlsreferenz.

## <a name="BKMK_examples"></a>Beispiele für

Die folgenden Batch-Anwendung formatiert eine Diskette in Laufwerk A als Systemdatenträger. Wenn der Vorgang erfolgreich ist, ist die **Goto** Befehl leitet die Verarbeitung der **: End** Bezeichnung:
```
echo off
format a: /s
if not errorlevel 1 goto end
echo An error occurred during formatting.
:end
echo End of batch program. 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

[Cmd](cmd.md)

[If](if.md)