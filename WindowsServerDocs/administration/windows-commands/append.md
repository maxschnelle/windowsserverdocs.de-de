---
title: append
description: Windows-Befehls Thema für **Anfügen**, das es Programmen ermöglicht, Datendateien in angegebenen Verzeichnissen zu öffnen, als ob Sie sich im aktuellen Verzeichnis befinden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9c3fea20-9502-40ad-a442-7a927aad88eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 95bbc607ef297e7cf67da2e388884882356ef744
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851323"
---
# <a name="append"></a>append

Ermöglicht Programmen das Öffnen von Datendateien in angegebenen Verzeichnissen, als ob Sie sich im aktuellen Verzeichnis befinden. Bei Verwendung ohne Parameter zeigt **Anfügen** die angefügte Verzeichnisliste an.

> [!NOTE]
> Dieser Befehl wird in Windows 10 nicht unterstützt.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
append [[<Drive>:]<Path>[;...]] [/x[:on|:off]] [/path:[:on|:off] [/e] 
append ;
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `[\<Drive>:]<Path>` | Gibt ein anzufügende Laufwerk und Verzeichnis an. |
| `/x:on` | Wendet angefügte Verzeichnisse auf Datei suchen und starten von Anwendungen an. |
| `/x:off` | Wendet angefügte Verzeichnisse nur auf Anforderungen zum Öffnen von Dateien an. Die Option **/x: Off** ist die Standardeinstellung. |
| `/path:on` | Wendet angefügte Verzeichnisse auf Datei Anforderungen an, die bereits einen Pfad angeben. **/Path: on** ist die Standardeinstellung. |
| `/path:off` | Deaktiviert die Auswirkung von **/Path: on**. |
| `/e` | Speichert eine Kopie der angefügten Verzeichnisliste in einer Umgebungsvariablen mit dem Namen Append. **/e** kann nur verwendet werden, wenn Sie nach dem Starten des Systems das erste Mal **Anfügen** verwenden. |
| `;` | Löscht die angefügte Verzeichnisliste. |
| `/?` | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um die angefügte Verzeichnisliste zu löschen:

```
append ;
```

Geben Sie Folgendes ein, um eine Kopie des angefügten Verzeichnisses in einer Umgebungsvariablen namens "append" zu speichern:

```
append /e
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
