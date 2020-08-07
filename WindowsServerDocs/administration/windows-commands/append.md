---
title: append
description: Referenz Artikel für den Befehl anfügen, mit dem Programme Datendateien in angegebenen Verzeichnissen öffnen können, als ob Sie sich im aktuellen Verzeichnis befinden.
ms.topic: article
ms.assetid: 9c3fea20-9502-40ad-a442-7a927aad88eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 887d058baf333f068b2e1fb557f085f0cfe58615
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895578"
---
# <a name="append"></a>append

Ermöglicht Programmen das Öffnen von Datendateien in angegebenen Verzeichnissen, als ob Sie sich im aktuellen Verzeichnis befinden. Bei Verwendung ohne Parameter zeigt **Anfügen** die angefügte Verzeichnisliste an.

> [!NOTE]
> Dieser Befehl wird in Windows 10 nicht unterstützt.

## <a name="syntax"></a>Syntax

```
append [[<drive>:]<path>[;...]] [/x[:on|:off]] [/path:[:on|:off] [/e]
append ;
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `[\<drive>:]<path>` | Gibt ein anzufügende Laufwerk und Verzeichnis an. |
| /x: ein | Wendet angefügte Verzeichnisse auf Datei suchen und starten von Anwendungen an. |
| /x: Off | Wendet angefügte Verzeichnisse nur auf Anforderungen zum Öffnen von Dateien an. Die Option **/x: Off** ist die Standardeinstellung. |
| /Path: ein | Wendet angefügte Verzeichnisse auf Datei Anforderungen an, die bereits einen Pfad angeben. **/Path: on** ist die Standardeinstellung. |
| /Path: Off | Deaktiviert die Auswirkung von **/Path: on**. |
| /e | Speichert eine Kopie der angefügten Verzeichnisliste in einer Umgebungsvariablen mit dem Namen Append. **/e** kann nur verwendet werden, wenn Sie nach dem Starten des Systems das erste Mal **Anfügen** verwenden. |
| ; | Löscht die angefügte Verzeichnisliste. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die angefügte Verzeichnisliste zu löschen:

```
append ;
```

Geben Sie Folgendes ein, um eine Kopie des angefügten Verzeichnisses in einer Umgebungsvariablen namens " *Anfügen*" zu speichern:

```
append /e
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
