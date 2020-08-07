---
title: color
description: Referenz Artikel für den Color-Befehl, mit dem die Vordergrund-und Hintergrundfarben im Eingabe Aufforderungs Fenster für die aktuelle Sitzung geändert werden.
ms.topic: article
ms.assetid: f5b67131-d196-45ec-a3f9-b5d9f091fd86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2534273eebe7f8596b0e8f2ab3c90cfdcf824d00
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892678"
---
# <a name="color"></a>color

Ändert die Vordergrund-und Hintergrundfarben im Eingabe Aufforderungs Fenster für die aktuelle Sitzung. Wenn Sie ohne Parameter verwendet **wird, werden** die standardmäßigen Vordergrund-und Hintergrundfarben des Eingabe Aufforderungs Fensters wieder hergestellt

## <a name="syntax"></a>Syntax

```
color [[<b>]<f>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<b>` | Gibt die Hintergrundfarbe an. |
| `<f>` | Gibt die Vordergrundfarbe an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

Hierbei gilt:

In der folgenden Tabelle werden gültige hexadezimale Ziffern aufgelistet, die Sie als Werte für und verwenden können `<b>` `<f>` :

| Wert | Color |
| ----- | ----- |
| 0 | Schwarz |
| 1 | Blau |
| 2 | Grün |
| 3 | Aqua |
| 4 | Red |
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
