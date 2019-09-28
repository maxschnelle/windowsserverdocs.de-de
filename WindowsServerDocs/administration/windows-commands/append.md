---
title: append
description: 'Thema für Windows-Befehle für '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c3fea20-9502-40ad-a442-7a927aad88eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fdc4243bee8055888b023a56921cef757dda6b7e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382752"
---
# <a name="append"></a>append



Ermöglicht Programmen das Öffnen von Datendateien in angegebenen Verzeichnissen, als ob Sie sich im aktuellen Verzeichnis befinden. Bei Verwendung ohne Parameter zeigt **Anfügen** die angefügte Verzeichnisliste an.

> [!NOTE]
> Dieser Befehl wird in Windows 10 nicht unterstützt.
>

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
append [[<Drive>:]<Path>[;...]] [/x[:on|:off]] [/path:[:on|:off] [/e] 
append ;
```

## <a name="parameters"></a>Parameter

|     Parameter     |                                                                                 Beschreibung                                                                                 |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [\<laufwerk >:] <Path> |                                                                 Gibt ein anzufügende Laufwerk und Verzeichnis an.                                                                  |
|       /x: ein       |                                                  Wendet angefügte Verzeichnisse auf Datei suchen und starten von Anwendungen an.                                                  |
|      /x: Off       |                                     Wendet angefügte Verzeichnisse nur auf Anforderungen zum Öffnen von Dateien an.</br>**/x: Off** ist die Standardeinstellung.                                     |
|     /Path: ein      |                               Wendet angefügte Verzeichnisse auf Datei Anforderungen an, die bereits einen Pfad angeben. **/Path: on** ist die Standardeinstellung.                               |
|     /Path: Off     |                                                                    Deaktiviert die Auswirkung von **/Path: on**.                                                                    |
|        /e         | Speichert eine Kopie der angefügten Verzeichnisliste in einer Umgebungsvariablen mit dem Namen Append. **/e** kann nur verwendet werden, wenn Sie nach dem Starten des Systems das erste Mal **Anfügen** verwenden. |
|         ;         |                                                                     Löscht die angefügte Verzeichnisliste.                                                                     |
|        /?         |                                                                    Zeigt die Hilfe an der Eingabeaufforderung an.                                                                     |

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die angefügte Verzeichnisliste zu löschen:
```
append ;
```
Geben Sie Folgendes ein, um eine Kopie des angefügten Verzeichnisses in einer Umgebungsvariablen namens "append" zu speichern:
```
append /e
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
