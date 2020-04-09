---
title: ftype
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6fb53cee-9bed-44dd-af5d-bc7cec1dd114
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f982f68f25a4decbc9c572b533fa1ecc5e893a8c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842703"
---
# <a name="ftype"></a>ftype



Zeigt Dateitypen an, die in Zuordnungen für Dateinamen Erweiterungen verwendet werden, oder ändert Sie. Wenn Sie ohne einen Zuweisungs Operator ( **=** ) verwendet wird, zeigt **ftype** die aktuelle geöffnete Befehls Zeichenfolge für den angegebenen Dateityp an. Bei Verwendung ohne Parameter zeigt **ftype** die Dateitypen an, für die geöffnete Befehls Zeichenfolgen definiert sind.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
ftype [<FileType>[=[<OpenCommandString>]]]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<filetype->|Gibt den Dateityp an, der angezeigt oder geändert werden soll.|
|\<opencommandstring >|Gibt die geöffnete Befehls Zeichenfolge an, die beim Öffnen von Dateien vom angegebenen Dateityp verwendet werden soll.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

In der folgenden Tabelle wird beschrieben, wie **ftype** Variablen in einer geöffneten Befehls Zeichenfolge ersetzt:

|Variable|Replacement value|
|--------|-----------------|
|%0 oder %1|Wird durch den Dateinamen ersetzt, der durch die Zuordnung gestartet wird.|
|%*|Ruft alle Parameter ab.|
|%2, %3,...|Ruft den ersten Parameter (%2), den zweiten Parameter (%3) usw. ab.|
|%~\<N >|Ruft alle verbleibenden Parameter ab, beginnend mit dem *n*-ten Parameter, wobei *N* eine beliebige Zahl zwischen 2 und 9 sein kann.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)