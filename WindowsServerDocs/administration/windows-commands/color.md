---
title: color
description: Referenz Artikel für den Color-Befehl, mit dem die Vordergrund-und Hintergrundfarben im Eingabe Aufforderungs Fenster für die aktuelle Sitzung geändert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f5b67131-d196-45ec-a3f9-b5d9f091fd86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 93c51fdbf1909adfda06730c3a517f602f8024b8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929803"
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
| 1 | Blue |
| 2 | Grün |
| 3 | Aqua |
| 4 | Red |
| 5 | Purple |
| 6 | Yellow |
| 7 | White |
| 8 | Grau |
| 9 | Hellblau |
| eine | Hellgrün |
| k | Hell Aqua |
| c | Hellrot |
| d | Hell lila |
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
