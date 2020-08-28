---
title: color
description: Referenz Artikel für den Color-Befehl, mit dem die Vordergrund-und Hintergrundfarben im Eingabe Aufforderungs Fenster für die aktuelle Sitzung geändert werden.
ms.topic: reference
ms.assetid: f5b67131-d196-45ec-a3f9-b5d9f091fd86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3ce7aa8e927e3796917d2720495f394636d9c240
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028458"
---
# <a name="color"></a>color

Ändert die Vordergrund-und Hintergrundfarben im Eingabe Aufforderungs Fenster für die aktuelle Sitzung. Wenn Sie ohne Parameter verwendet **wird, werden** die standardmäßigen Vordergrund-und Hintergrundfarben des Eingabe Aufforderungs Fensters wieder hergestellt

## <a name="syntax"></a>Syntax

```
color [[<b>]<f>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<b>` | Gibt die Hintergrundfarbe an. |
| `<f>` | Gibt die Vordergrundfarbe an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

Hierbei gilt:

In der folgenden Tabelle werden gültige hexadezimale Ziffern aufgelistet, die Sie als Werte für und verwenden können `<b>` `<f>` :

| Wert | Farbe |
| ----- | ----- |
| 0 | Schwarz |
| 1 | Blau |
| 2 | Grün |
| 3 | Aqua |
| 4 | Rot |
| 5 | Purple |
| 6 | Gelb |
| 7 | White |
| 8 | Grau |
| 9 | Hellblau |
| a | Hellgrün |
| b | Hell Aqua |
| c | Hellrot |
| d | Hell lila |
| e | Hellgelb |
| f | Helles Weiß |

#### <a name="remarks"></a>Bemerkungen

- Verwenden Sie keine Leerzeichen zwischen `<b>` und `<f>` .

- Wenn Sie nur eine hexadezimale Ziffer angeben, wird die entsprechende Farbe als Vordergrundfarbe verwendet, und die Hintergrundfarbe wird auf die Standardfarbe festgelegt.

- Wenn Sie die standardmäßige Eingabe Aufforderungs Fenster Farbe festlegen möchten, wählen Sie die linke obere Ecke des **Eingabe** Aufforderungs Fensters aus, wählen Sie **Standard**aus, wählen Sie die Registerkarte **Farben** aus, und wählen Sie dann die Farben aus, die Sie für den **Bildschirm Text** und den **Bildschirmhintergrund**verwenden möchten.

- Wenn `<b>` und `<f>` den gleichen Farbwert haben, wird ERRORLEVEL auf festgelegt `1` , und es wird keine Änderung an der Vorder-oder Hintergrundfarbe vorgenommen.

## <a name="examples"></a>Beispiele

Wenn Sie die Hintergrundfarbe des Eingabe Aufforderungs Fensters in grau und die Vordergrundfarbe in Rot ändern möchten, geben Sie Folgendes ein:

```
color 84
```

Geben Sie Folgendes ein, um die Vordergrundfarbe des Eingabe Aufforderungs Fensters in hellgelb zu ändern

```
color e
```

> [!NOTE]
> In diesem Beispiel wird der Hintergrund auf die Standardfarbe festgelegt, da nur eine hexadezimale Ziffer angegeben wird.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
