---
title: assoc
description: Referenz Artikel für den Befehl "Assoc", mit dem Dateinamen Erweiterungs Zuordnungen angezeigt oder geändert werden.
ms.topic: reference
ms.assetid: 237bedda-b24c-4fec-a39c-9b7eacf96417
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1ce1ee97dd386757ab5802ac2f493e25635ff66f
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633440"
---
# <a name="assoc"></a>assoc

Zeigt Zuordnungen für Dateinamen Erweiterungen an oder ändert diese. Bei Verwendung ohne Parameter zeigt **Assoc** eine Liste aller aktuellen Zuordnungen für Dateinamen Erweiterungen an.

> [!NOTE]
> Dieser Befehl wird nur in cmd.exe unterstützt und ist in PowerShell nicht verfügbar.
> Obwohl Sie als Problem `cmd /c assoc` Umgehung verwenden können.

## <a name="syntax"></a>Syntax

```
assoc [<.ext>[=[<filetype>]]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<.ext>` | Gibt die Dateinamenerweiterung an. |
| `<filetype>` | Gibt den Dateityp an, der der angegebenen Dateinamenerweiterung zugeordnet werden soll. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="remarks"></a>Hinweise

- Um die Dateityp Zuordnung für eine Dateinamenerweiterung zu entfernen, fügen Sie nach dem Gleichheitszeichen ein Leerzeichen hinzu, indem Sie die Leertaste drücken.

- Verwenden Sie den **ftype** -Befehl, um aktuelle Dateitypen anzuzeigen, für die geöffnete Befehls Zeichenfolgen definiert sind.

- Um die Ausgabe von **Assoc** in eine Textdatei umzuleiten, verwenden Sie den `>` Umleitungs Operator.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die aktuelle Dateityp Zuordnung für die Dateinamenerweiterung. txt anzuzeigen:

```
assoc .txt
```

Um die Dateityp Zuordnung für die Dateinamenerweiterung. bak zu entfernen, geben Sie Folgendes ein:

```
assoc .bak=
```

> [!NOTE]
> Stellen Sie sicher, dass Sie nach dem Gleichheitszeichen ein Leerzeichen einfügen.

Geben Sie Folgendes ein, um die Ausgabe von **Assoc** auf einem Bildschirm anzuzeigen:

```
assoc | more
```

Um die Ausgabe von **Assoc** an die Datei assoc.txt zu senden, geben Sie Folgendes ein:

```
assoc>assoc.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [FTYPE-Befehl](ftype.md)
