---
title: assoc
description: Windows-Befehls Thema für Assoc, das Dateinamen Erweiterungs Zuordnungen anzeigt oder ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 237bedda-b24c-4fec-a39c-9b7eacf96417
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 442ba244a7325425df29a1ebdcdb8bc107095ebe
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851293"
---
# <a name="assoc"></a>assoc

Zeigt Zuordnungen für Dateinamen Erweiterungen an oder ändert diese. Bei Verwendung ohne Parameter zeigt **Assoc** eine Liste aller aktuellen Zuordnungen für Dateinamen Erweiterungen an.

> [!NOTE]
> Dieser Befehl wird nur in cmd unterstützt. EXE und ist in PowerShell nicht verfügbar.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
assoc [<.ext>[=[<FileType>]]]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<.ext>` | Gibt die Dateinamenerweiterung an. |
| `<FileType>` | Gibt den Dateityp an, der der angegebenen Dateinamenerweiterung zugeordnet werden soll. |
| `/?` | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Hinweise

- Um die Dateityp Zuordnung für eine Dateinamenerweiterung zu entfernen, fügen Sie nach dem Gleichheitszeichen ein Leerzeichen hinzu, indem Sie die Leertaste drücken.

- Verwenden Sie den **ftype** -Befehl, um aktuelle Dateitypen anzuzeigen, für die geöffnete Befehls Zeichenfolgen definiert sind.

- Um die Ausgabe von **Assoc** in eine Textdatei umzuleiten, verwenden Sie den **>** -Umleitungs Operator.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um die aktuelle Dateityp Zuordnung für die Dateinamenerweiterung. txt anzuzeigen:

```
assoc .txt
```

Um die Dateityp Zuordnung für die Dateinamenerweiterung. bak zu entfernen, geben Sie Folgendes ein:

```
assoc .bak= 
```

> [!NOTE]
> Achten Sie darauf, nach dem Gleichheitszeichen ein Leerzeichen hinzuzufügen.

Geben Sie Folgendes ein, um die Ausgabe von **Assoc** auf einem Bildschirm anzuzeigen:

```
assoc | more
```

Geben Sie Folgendes ein, um die Ausgabe von **Assoc** an die Datei "Assoc. txt" zu senden:

```
assoc>assoc.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
