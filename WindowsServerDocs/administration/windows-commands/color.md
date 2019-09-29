---
title: color
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5b67131-d196-45ec-a3f9-b5d9f091fd86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed792e4626897945e688f1c54767d7680ade6d99
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379239"
---
# <a name="color"></a>color



Ändert die Vordergrund-und Hintergrundfarben im Eingabe Aufforderungs Fenster für die aktuelle Sitzung. Wenn Sie ohne Parameter verwendet **wird, werden** die standardmäßigen Vordergrund-und Hintergrundfarben des Eingabe Aufforderungs Fensters wieder hergestellt

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
color [[<B>]<F>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<B >|Gibt die Hintergrundfarbe an.|
|\<F >|Gibt die Vordergrundfarbe an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die folgende Tabelle enthält gültige hexadezimale Ziffern, mit denen Sie als Werte für *B* und *F*.

|Wert|Farbe|
|-----|-----|
|0|Schwarz|
|1|Blau|
|2|Grün|
|3|CE|
|4|Rot|
|5|Viol|
|6|Gelb|
|7|Weiß|
|8|Grau|
|9|Hellblau|
|A|Hellgrün|
|B|Hell Aqua|
|c|Hellrot|
|D|Hell lila|
|E|Hellgelb|
|V|Helles Weiß|
    
-   Verwenden Sie keine Leerzeichen zwischen *B* und *F*.
-   Wenn Sie nur eine hexadezimale Ziffer angeben, wird die entsprechende Farbe als Vordergrundfarbe verwendet, und die Hintergrundfarbe wird auf die Standardfarbe festgelegt.
-   Wenn Sie die standardmäßige Eingabe Aufforderungs Fenster-Farbe festlegen möchten, klicken Sie auf die linke obere Ecke des Eingabe Aufforderungs Fensters, klicken Sie auf **Standardwerte**, klicken Sie auf die Registerkarte **Farben** , und klicken Sie dann auf die Farben, die Sie für den **Bildschirm Text** und den **Bildschirmhintergrund** .
-   Wenn *B* und *F* identisch sind, legt der **Color** -Befehl ERRORLEVEL auf 1 fest, und es wird keine Änderung an der Vorder-oder Hintergrundfarbe vorgenommen.

## <a name="BKMK_examples"></a>Beispiele

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

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
