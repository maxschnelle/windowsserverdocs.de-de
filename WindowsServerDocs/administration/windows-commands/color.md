---
title: color
description: Referenz Artikel für den Color-Befehl, mit dem die Vordergrund-und Hintergrundfarben im Eingabe Aufforderungs Fenster für die aktuelle Sitzung geändert werden.
ms.topic: reference
ms.assetid: f5b67131-d196-45ec-a3f9-b5d9f091fd86
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: feb4d4a2de9491636a1c96b7a16c80e2e18f5865
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89629507"
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
| 4 | Rot |
| 5 | Purple |
| 6 | Gelb |
| 7 | White |
| 8 | Grau |
| 9 | Hellblau |
| a | Hellgrün |
| k | Hell Aqua |
| c | Hellrot |
| T | Hell lila |
| e | Hellgelb |
| f | Helles Weiß |

#### <a name="remarks"></a>Hinweise

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
