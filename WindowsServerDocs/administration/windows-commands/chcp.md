---
title: chcp
description: Windows-Befehle-Thema für CHCP, das die aktive Konsolen Codepage ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dc7b1c71-7b80-443d-9cf1-9bcf305aa1fd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e644cf8544d135c5d21c344b0fd0a3364c7f89c1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847943"
---
# <a name="chcp"></a>chcp

Ändert die aktive Konsolen Codepage. Bei Verwendung ohne Parameter zeigt **chcp** die Nummer der aktiven Konsolen Codepage an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
chcp [<NNN>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<nnn >|Gibt die Codepage an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

In der folgenden Tabelle werden die einzelnen unterstützten Codeseiten und deren Land/Region oder Sprache aufgeführt:

|Codepage|Land/Region oder Sprache|
|---------|--------------------------|
|437|USA|
|850|Mehrsprachig (lateinisch I)|
|852|Slawisch (Lateinisch II)|
|855|Kyrillisch (Russisch)|
|857|Türkisch|
|860|Portugiesisch|
|861|Isländisch|
|863|Französisch (Kanada)|
|865|Nordischen|
|866|Russisch|
|869|Modernes Griechisch|
|936|Chinesisch|

## <a name="remarks"></a>Hinweise

-   Nur die mit Windows installierte OEM-Codepage (Original Equipment Manufacturer) wird in einem Eingabe Aufforderungs Fenster, in dem Raster Schriftarten verwendet werden, ordnungsgemäß angezeigt. Andere Codepages werden im Vollbildmodus oder in Eingabe Aufforderungs Fenstern, die TrueType-Schriftarten verwenden, ordnungsgemäß angezeigt.
-   Sie müssen keine Codepages vorbereiten (wie in MS MS-DOS).
-   Programme, die Sie starten, nachdem Sie eine neue Codepage zugewiesen haben, verwenden die neue Codepage. Allerdings verwenden Programme (mit Ausnahme von "cmd. exe"), die Sie starten, bevor Sie die neue Codepage zuweisen, die ursprüngliche Codepage.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um die Einstellung der aktiven Codepage anzuzeigen:
```
chcp
```
Eine Meldung ähnlich der folgenden wird angezeigt:

`Active code page: 437`

Um die aktive Codepage in 850 (mehrsprachig) zu ändern, geben Sie Folgendes ein:
```
chcp 850
```
Wenn die angegebene Codepage ungültig ist, wird die folgende Fehlermeldung angezeigt:

`Invalid code page`

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
