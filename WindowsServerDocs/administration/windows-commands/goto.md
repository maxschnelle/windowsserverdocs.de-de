---
title: goto
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e0de1458-1f78-48ff-a746-c285a945a510
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dd61575b8b31ed47463db464f4aad0a048e755b2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725007"
---
# <a name="goto"></a>goto



Leitet "cmd. exe" an eine gekennzeichnete Zeile in einem Batch-Programm weiter. In einem Batch Programm leitet **goto** die Befehls Verarbeitung an eine Zeile weiter, die durch eine Bezeichnung gekennzeichnet ist. Wenn die Bezeichnung gefunden wird, wird die Verarbeitung fortgesetzt, beginnend mit den Befehlen, die in der nächsten Zeile beginnen.



## <a name="syntax"></a>Syntax

```
goto <Label> 
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Bezeichnung>|Gibt eine Text Zeichenfolge an, die im Batch Programm als Bezeichnung verwendet wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

-   Arbeiten mit Befehls Erweiterungen

    Wenn Befehls Erweiterungen aktiviert sind (Standardeinstellung), und Sie den **goto** -Befehl mit der Ziel Bezeichnung **: EOF**verwenden, übertragen Sie die Steuerung an das Ende der aktuellen Batch Skriptdatei und beenden die Batch Skriptdatei, ohne eine Bezeichnung zu definieren. Wenn Sie " **goto** " mit der Bezeichnung " **: EOF** " verwenden, müssen Sie vor der Bezeichnung einen Doppelpunkt einfügen. Beispiel:  
    ```
    goto:EOF
    ```  
-   Verwenden gültiger *Label* Bezeichnungs Werte

    Sie können Leerzeichen im *Label* -Parameter verwenden, aber Sie können keine anderen Trennzeichen (z. b. Semikolons oder Gleichheitszeichen) einschließen.
-   Übereinstimmende *Bezeichnung* mit der Bezeichnung im Batch-Programm

    Der von Ihnen angegebene Bezeichnungs *Wert muss mit einer Bezeichnung im* Batch Programm identisch sein. Die Bezeichnung im Batch Programm muss mit einem Doppelpunkt (:) beginnen. Wenn eine Zeile mit einem Doppelpunkt beginnt, wird Sie als Bezeichnung behandelt, und alle Befehle in dieser Zeile werden ignoriert. Wenn das Batch Programm nicht die Bezeichnung enthält, die Sie in der *Bezeichnung*angegeben haben, wird das Batch Programm angehalten und zeigt die folgende Meldung an:  
    ```
    Label not found
    ```  
-   Verwenden von **goto** für bedingte Vorgänge

    Sie können " **goto** " mit anderen Befehlen verwenden, um bedingte Vorgänge auszuführen. Weitere Informationen zur Verwendung von **goto** für bedingte Vorgänge finden Sie in der [if](if.md) -Befehlsreferenz.

## <a name="examples"></a>Beispiele

Das folgende Batch Programm formatiert einen Datenträger in Laufwerk a als System Datenträger. Wenn der Vorgang erfolgreich ist, leitet der **goto** -Befehl die Verarbeitung an die **: End** -Bezeichnung weiter:
```
echo off
format a: /s
if not errorlevel 1 goto end
echo An error occurred during formatting.
:end
echo End of batch program. 
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Cmd](cmd.md)

[If](if.md)