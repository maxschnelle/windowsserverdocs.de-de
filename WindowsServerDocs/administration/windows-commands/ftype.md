---
title: ftype
description: Referenz Artikel für den ftype-Befehl, der den in Dateinamen Erweiterungs Zuordnungen verwendeten Dateityp anzeigt oder ändert.
ms.topic: reference
ms.assetid: 6fb53cee-9bed-44dd-af5d-bc7cec1dd114
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: db5781eccb4fc54fea42586b5e7aab779509bffd
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636658"
---
# <a name="ftype"></a>ftype

Zeigt Dateitypen an, die in Zuordnungen für Dateinamen Erweiterungen verwendet werden, oder ändert Sie. Wenn Sie ohne einen Zuweisungs Operator (=) verwendet wird, zeigt dieser Befehl die aktuelle geöffnete Befehls Zeichenfolge für den angegebenen Dateityp an. Bei Verwendung ohne Parameter zeigt dieser Befehl die Dateitypen an, für die geöffnete Befehls Zeichenfolgen definiert sind.

> [!NOTE]
> Dieser Befehl wird nur in cmd.exe unterstützt und ist in PowerShell nicht verfügbar.
> Obwohl Sie als Problem `cmd /c ftype` Umgehung verwenden können.

## <a name="syntax"></a>Syntax

```
ftype [<filetype>[=[<opencommandstring>]]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<filetype>` | Gibt den Dateityp an, der angezeigt oder geändert werden soll. |
| `<opencommandstring>` | Gibt die geöffnete Befehls Zeichenfolge an, die beim Öffnen von Dateien vom angegebenen Dateityp verwendet werden soll.|
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

In der folgenden Tabelle wird beschrieben, wie **ftype** Variablen in einer geöffneten Befehls Zeichenfolge ersetzt:

| Variable | Replacement value |
| -------- | ----------------- |
| `%0` oder `%1` | Wird durch den Dateinamen ersetzt, der durch die Zuordnung gestartet wird. |
| `%*` | Ruft alle Parameter ab. |
| `%2`, `%3`, ... | Ruft den ersten Parameter ( `%2` ), den zweiten Parameter ( `%3` ) usw. ab. |
| `%~<n>` | Ruft alle verbleibenden Parameter ab, beginnend mit dem *n*-ten Parameter, wobei *n* eine beliebige Zahl zwischen 2 und 9 sein kann. |

### <a name="examples"></a>Beispiele

Zum Anzeigen der aktuellen Dateitypen, für die geöffnete Befehls Zeichenfolgen definiert sind, geben Sie Folgendes ein:

```
ftype
```

Zum Anzeigen der aktuellen geöffneten Befehls Zeichenfolge für den *txtfile* -Dateityp geben Sie Folgendes ein:

```
ftype txtfile
```

Dieser Befehl erzeugt eine Ausgabe ähnlich der folgenden:

`txtfile=%SystemRoot%\system32\NOTEPAD.EXE %1`

Zum Löschen der geöffneten Befehls Zeichenfolge für einen Dateityp mit dem Namen *example*geben Sie Folgendes ein:

```
ftype example=
```

Geben Sie die folgenden Befehle ein, um die Dateinamenerweiterung. pl dem Dateityp Perl Script zuzuordnen und den Dateityp Perl Script zum Ausführen von PERL.EXE zu aktivieren:

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
