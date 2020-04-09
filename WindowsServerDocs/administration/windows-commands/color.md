---
title: Farbe
description: Windows-Befehls Thema für Color, mit dem die Vordergrund-und Hintergrundfarben im Eingabe Aufforderungs Fenster für die aktuelle Sitzung geändert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f5b67131-d196-45ec-a3f9-b5d9f091fd86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0e89c20d90a3b812fa67b597c4c205d34e725785
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847483"
---
# <a name="color"></a>Farbe

Ändert die Vordergrund-und Hintergrundfarben im Eingabe Aufforderungs Fenster für die aktuelle Sitzung. Wenn Sie ohne Parameter verwendet **wird, werden** die standardmäßigen Vordergrund-und Hintergrundfarben des Eingabe Aufforderungs Fensters wieder hergestellt

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
color [[<B>]<F>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<B >|Gibt die Hintergrundfarbe an.|
|\<F >|Gibt die Vordergrundfarbe an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   In der folgenden Tabelle werden gültige hexadezimale Ziffern aufgelistet, die Sie als Werte für *B* und *F*verwenden können.

|Wert|Farbe|
|-----|-----|
|0|Black|
|1|Blau|
|2|Grün|
|3|CE|
|4|Rot|
|5|Violett|
|6|Gelb|
|7|Weiß|
|8|Grau|
|9|Hellblau|
|A|Hellgrün|
|B|Hell Aqua|
|A|Hellrot|
|D|Hell lila|
|E|Hellgelb|
|C|Helles Weiß|
    
-   Verwenden Sie keine Leerzeichen zwischen *B* und *F*.
-   Wenn Sie nur eine hexadezimale Ziffer angeben, wird die entsprechende Farbe als Vordergrundfarbe verwendet, und die Hintergrundfarbe wird auf die Standardfarbe festgelegt.
-   Um die standardmäßige Eingabe Aufforderungs Fenster Farbe festzulegen, klicken Sie auf die obere linke Ecke des Eingabe Aufforderungs Fensters, klicken Sie auf **Standardwerte**, klicken Sie auf die Registerkarte **Farben** , und klicken Sie dann auf die Farben, die Sie für den **Bildschirm Text** und den **Hintergrund Hintergrund**verwenden möchten.
-   Wenn *B* und *F* identisch sind, legt der **Color** -Befehl ERRORLEVEL auf 1 fest, und es wird keine Änderung an der Vorder-oder Hintergrundfarbe vorgenommen.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

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
