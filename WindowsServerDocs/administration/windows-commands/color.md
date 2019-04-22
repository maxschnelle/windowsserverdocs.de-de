---
title: color
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: f8d23cc1bb5739b47c755d90c927cbcf82b8da7f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825021"
---
# <a name="color"></a>color



Änderungen, die die Vordergrund- und Farben im Eingabeaufforderungsfenster Befehl für die aktuelle Sitzung. Wenn Sie ohne Angabe von Parametern **Farbe** der Standard-Eingabeaufforderung Fenster Vordergrund- und Hintergrundfarben wiederhergestellt.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
color [[<B>]<F>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<B>|Gibt die Hintergrundfarbe an.|
|\<F>|Gibt an, die die Vordergrundfarbe darstellt.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die folgende Tabelle enthält gültige hexadezimale Ziffern, mit denen Sie als Werte für *B* und *F*.  
    |Wert|Farbe|
    |-----|-----|
    |0|Schwarz|
    |1|Blau|
    |2|Grün|
    |3|Aqua|
    |4|Rot|
    |5|Lila|
    |6|Gelb|
    |7|Weiß|
    |8|Grau|
    |9|Hellblau|
    |A|Hellgrün|
    |B|Hell aqua|
    |c|Hellrot|
    |D|Helles Lila|
    |E|Hosttags in Gelb|
    |V|Helle weiß|
-   Verwenden Sie keine Leerzeichen zwischen *B* und *F*.
-   Wenn Sie nur eine hexadezimale Ziffer angeben, wird die entsprechende Farbe verwendet, als Vordergrundfarbe und die Farbe des Hintergrunds, um die Standardfarbe festgelegt ist.
-   Um die Standardfarbe des Fensters Eingabeaufforderung festzulegen, klicken Sie auf der oberen linken Ecke von das Eingabeaufforderungsfenster aus, klicken Sie auf **Standardwerte**, klicken Sie auf die **Farben** Registerkarte, und klicken Sie dann auf die Farben, die Sie für die verwendenmöchten **Bildschirm Text** und **Bildschirm Hintergrund**.
-   Wenn *B* und *F* identisch sind, die **Farbe** auf 1 weißem und keine Änderung an der Vorder- oder die Farbe des Hintergrunds.

## <a name="BKMK_examples"></a>Beispiele für

Um die Hintergrundfarbe der Eingabeaufforderung im Fenster auf Grau und die Vordergrundfarbe auf Rot zu ändern, geben Sie Folgendes ein:
```
color 84
```
Um die Vordergrundfarbe des Eingabeaufforderung Hosttags in Gelb ändern möchten, geben Sie Folgendes ein:
```
color e
```

> [!NOTE]
> In diesem Beispiel wird der Hintergrund auf die Standardfarbe festgelegt, da nur eine hexadezimale Ziffer angegeben ist.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)