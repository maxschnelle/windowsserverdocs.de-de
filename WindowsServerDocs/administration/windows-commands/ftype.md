---
title: ftype
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6fb53cee-9bed-44dd-af5d-bc7cec1dd114
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eb4a9fa3105247695f1a50e5fc483ce608cd4816
ms.sourcegitcommit: 7116460855701eed4e09d615693efa4fffc40006
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83433124"
---
# <a name="ftype"></a>ftype



Zeigt Dateitypen an, die in Zuordnungen für Dateinamen Erweiterungen verwendet werden, oder ändert Sie. Bei Verwendung ohne Zuweisungs Operator ( **=** ) zeigt **ftype** die aktuelle geöffnete Befehls Zeichenfolge für den angegebenen Dateityp an. Bei Verwendung ohne Parameter zeigt **ftype** die Dateitypen an, für die geöffnete Befehls Zeichenfolgen definiert sind.

> [!NOTE]
> Dieser Befehl wird nur in cmd unterstützt. EXE und ist in PowerShell nicht verfügbar.  
> Obwohl Sie als Problem `cmd /c ftype` Umgehung verwenden können.


## <a name="syntax"></a>Syntax

```
ftype [<FileType>[=[<OpenCommandString>]]]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Filetype->|Gibt den Dateityp an, der angezeigt oder geändert werden soll.|
|\<Opencommandstring->|Gibt die geöffnete Befehls Zeichenfolge an, die beim Öffnen von Dateien vom angegebenen Dateityp verwendet werden soll.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

In der folgenden Tabelle wird beschrieben, wie **ftype** Variablen in einer geöffneten Befehls Zeichenfolge ersetzt:

|Variable|Replacement value|
|--------|-----------------|
|%0 oder %1|Wird durch den Dateinamen ersetzt, der durch die Zuordnung gestartet wird.|
|%*|Ruft alle Parameter ab.|
|%2, %3,...|Ruft den ersten Parameter (%2), den zweiten Parameter (%3) usw. ab.|
|%~\<N>|Ruft alle verbleibenden Parameter ab, beginnend mit dem *n*-ten Parameter, wobei *N* eine beliebige Zahl zwischen 2 und 9 sein kann.|

## <a name="examples"></a>Beispiele

Zum Anzeigen der aktuellen Dateitypen, für die geöffnete Befehls Zeichenfolgen definiert sind, geben Sie Folgendes ein:
```
ftype
```
Zum Anzeigen der aktuellen geöffneten Befehls Zeichenfolge für den *txtfile* -Dateityp geben Sie Folgendes ein:
```
ftype txtfile
```
Dieser Befehl erzeugt eine Ausgabe ähnlich der folgenden:
```
txtfile=%SystemRoot%\system32\NOTEPAD.EXE %1
```
Zum Löschen der geöffneten Befehls Zeichenfolge für einen Dateityp mit dem Namen *example*geben Sie Folgendes ein:
```
ftype example=
```
Um die Dateinamenerweiterung. pl dem Dateityp PerlScript zuzuordnen, und aktivieren Sie den Dateityp Perl Script, um perl auszuführen. EXE, geben Sie die folgenden Befehle ein:
```
assoc .pl=PerlScript 
ftype PerlScript=perl.exe %1 %*
```
Wenn Sie die Dateinamenerweiterung. pl beim Aufrufen eines Perl-Skripts nicht eingeben müssen, geben Sie Folgendes ein:
```
set PATHEXT=.pl;%PATHEXT%
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
