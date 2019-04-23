---
title: ftype
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6fb53cee-9bed-44dd-af5d-bc7cec1dd114
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c29ca0aa027d11fa8f981134e5367021227d3096
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881681"
---
# <a name="ftype"></a>ftype



Zeigt oder ändert die Dateitypen aufgeführt, die in Dateinamenerweiterungen verwendet werden. Ohne Angabe von Zuweisungsoperator (**=**), **Ftype** zeigt die aktuellen Befehl Öffnen-Zeichenfolge für den angegebenen Dateityp. Wenn Sie ohne Angabe von Parametern **Ftype** zeigt die Dateitypen, die open definiert sind.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
ftype [<FileType>[=[<OpenCommandString>]]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<FileType>|Gibt den Dateityp zum Anzeigen oder ändern.|
|\<OpenCommandString>|Gibt an, die Befehlszeichenfolge, die beim Öffnen von Dateien mit den angegebenen Dateityp zu verwendende öffnen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

In der folgende Tabelle wird beschrieben, wie **Ftype** ersetzt Variablen in einer Befehlszeichenfolge öffnen:

|Variable|Ersatzwert|
|--------|-----------------|
|%0 oder %1|Ruft ab, mit dem Namen der Datei gestartet wird, über die Zuordnung ersetzt.|
|%*|Ruft alle Parameter an.|
|%2, %3, ...|Ruft ab, der erste Parameter (%2), zweiten Parameter (%3) und So weiter.|
|%~\<N>|Ruft die restlichen Parameter, beginnend mit der *N*-ten Parameter, in denen *N* kann eine beliebige Anzahl von 2 bis 9 sein.|

## <a name="BKMK_examples"></a>Beispiele für

Um die aktuellen Dateitypen anzuzeigen, die Befehl zum Öffnen von Zeichenfolgen definiert haben, geben Sie Folgendes ein:
```
ftype
```
Zum Anzeigen der aktuellen Befehl Öffnen-Zeichenfolge für die *Txtfile* Dateityp, Typ:
```
ftype txtfile
```
Dieser Befehl erzeugt eine Ausgabe ähnlich der folgenden:
```
txtfile=%SystemRoot%\system32\NOTEPAD.EXE %1
```
So löschen Sie die Befehlszeichenfolge, die für einen Dateityp mit dem Namen öffnen *Beispiel*, Typ:
```
ftype example=
```
Ordnen Sie die PL-Dateinamenerweiterung mit dem Dateityp PerlScript, und aktivieren den Dateityp von PerlScript PERL ausgeführt. EXE-Datei, geben Sie die folgenden Befehle:
```
assoc .pl=PerlScript 
ftype PerlScript=perl.exe %1 %*
```
Um die Notwendigkeit, geben Sie die PL-Dateinamenerweiterung beim Aufrufen eines Perl-Skripts zu vermeiden, geben Sie Folgendes ein:
```
set PATHEXT=.pl;%PATHEXT%
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)