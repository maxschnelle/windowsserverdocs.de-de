---
title: assoc
description: Referenz Artikel für den Befehl "Assoc", mit dem Dateinamen Erweiterungs Zuordnungen angezeigt oder geändert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 237bedda-b24c-4fec-a39c-9b7eacf96417
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6e6d72dce2a3e820b52a33bf11dbf38890278fb8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924043"
---
# <a name="assoc"></a>assoc

Zeigt Zuordnungen für Dateinamen Erweiterungen an oder ändert diese. Bei Verwendung ohne Parameter zeigt **Assoc** eine Liste aller aktuellen Zuordnungen für Dateinamen Erweiterungen an.

> [!NOTE]
> Dieser Befehl wird nur in cmd.exe unterstützt und ist in PowerShell nicht verfügbar.

## <a name="syntax"></a>Syntax

```
assoc [<.ext>[=[<filetype>]]]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
