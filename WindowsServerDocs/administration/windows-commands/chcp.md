---
title: chcp
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc7b1c71-7b80-443d-9cf1-9bcf305aa1fd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 622d4b64128c7e39cc761e4f5e9d69cf54383760
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819201"
---
# <a name="chcp"></a>chcp



Ändert die Codepage für die aktive Konsole. Wenn Sie ohne Angabe von Parametern **Chcp** zeigt die Anzahl der die Codepage für die aktive Konsole.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
chcp [<NNN>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<NNN>|Gibt die Codepage an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

Die folgende Tabelle enthält jede unterstützte Code Seite und die Sprache/Land oder die Sprache:

|Codepage|Land/Region oder Sprache|
|---------|--------------------------|
|437|USA|
|850|Mehrsprachige (Lateinisch I)|
|852|Altslawisch (Lateinisch II)|
|855|Kyrillisch (Russisch)|
|857|Türkisch|
|860|Portugiesisch|
|861|Isländisch|
|863|Französisch (Kanada)|
|865|Nordisch|
|866|Russisch|
|869|Neugriechisch|
|936|Chinesisch|

## <a name="remarks"></a>Hinweise

-   Nur die Originalgerätehersteller (OEM)-Codepage, die mit Windows installiert ist, wird ordnungsgemäß in einem Eingabeaufforderungsfenster aus, die Rasterschriftarten verwendet angezeigt. Anderen Codepages werden korrekt angezeigt, in den Vollbildmodus oder in den Eingabeaufforderungsfenstern, die TrueType-Schriftarten verwenden.
-   Sie müssen nicht-Codepages (wie in der MS-DOS) vorbereiten.
-   Programme, die Sie, nachdem Sie Starten einer neue Verwendung des Code-Seite weisen Sie die neue Seite. Allerdings weisen Sie Programme (mit Ausnahme von Cmd.exe), die Sie vor dem Starten der neue Code-Seite verwendet die ursprüngliche Codepage.

## <a name="BKMK_examples"></a>Beispiele für

Um die aktiven codepageeinstellung anzuzeigen, geben Sie Folgendes ein:
```
chcp
```
Es wird eine Meldung ähnlich der folgenden angezeigt:

`Active code page: 437`

Um die aktiven Codepage 850 (Multilingual) ändern, geben Sie Folgendes ein:
```
chcp 850
```
Wenn die angegebene Codepage ungültig ist, wird die folgende Fehlermeldung angezeigt:

`Invalid code page`

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
