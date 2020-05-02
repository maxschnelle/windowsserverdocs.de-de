---
title: assoc
description: Referenz Thema für den Befehl "Assoc", mit dem Dateinamen Erweiterungs Zuordnungen angezeigt oder geändert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 237bedda-b24c-4fec-a39c-9b7eacf96417
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f637e1f744ec412899320cfbb368633b222da8d3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718953"
---
# <a name="assoc"></a>assoc

Zeigt Zuordnungen für Dateinamen Erweiterungen an oder ändert diese. Bei Verwendung ohne Parameter zeigt **Assoc** eine Liste aller aktuellen Zuordnungen für Dateinamen Erweiterungen an.

> [!NOTE]
> Dieser Befehl wird nur in cmd unterstützt. EXE und ist in PowerShell nicht verfügbar.

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

### <a name="remarks"></a>Bemerkungen

- Um die Dateityp Zuordnung für eine Dateinamenerweiterung zu entfernen, fügen Sie nach dem Gleichheitszeichen ein Leerzeichen hinzu, indem Sie die Leertaste drücken.

- Verwenden Sie den **ftype** -Befehl, um aktuelle Dateitypen anzuzeigen, für die geöffnete Befehls Zeichenfolgen definiert sind.

- Um die Ausgabe von **Assoc** in eine Textdatei umzuleiten, verwenden `>` Sie den Umleitungs Operator.

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

Geben Sie Folgendes ein, um die Ausgabe von **Assoc** an die Datei "Assoc. txt" zu senden:

```
assoc>assoc.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [FTYPE-Befehl](ftype.md)
