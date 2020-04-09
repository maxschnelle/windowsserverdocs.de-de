---
title: tzutil
description: Windows-Befehls Thema für TZUtil, das das Windows-Zeit Zonen-Hilfsprogramm anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bcf6e007-c9b6-4df5-83c5-ed7b4b1b5913
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 330ee1eb4318df5aca1a5bb1a456711cd103c467
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832343"
---
# <a name="tzutil"></a>tzutil

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt das Windows-Zeit Zonen Dienstprogramm an. 

## <a name="syntax"></a>Syntax
```
tzutil [/?] [/g] [/s <timeZoneID>[_dstoff]] [/l]
```
#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
|/g|Zeigt die aktuelle Zeit Zonen-ID an.|
|/s \<TimeZoneId > [_dstoff]|Legt die aktuelle Zeitzone mithilfe der angegebenen Zeit Zonen-ID fest. Mit dem **_dstoff** Suffix werden die Anpassungen der Sommerzeit für die Zeitzone deaktiviert (falls zutreffend).|
|/l|Listet alle gültigen Zeit Zonen-IDs und anzeigen Amen auf. Die Ausgabe lautet wie folgt:<p>-   \<anzeigen Amen ><br />-   \<Zeit Zonen-ID >|

## <a name="remarks"></a>Hinweise
Der Exitcode **0** gibt an, dass der Befehl erfolgreich abgeschlossen wurde.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele
Geben Sie Folgendes ein, um die aktuelle Zeit Zonen-ID anzuzeigen:
```
tzutil /g
```
Um die aktuelle Zeitzone auf Pacific Normalzeit festzulegen, geben Sie Folgendes ein:
```
tzutil /s Pacific Standard time
```
Geben Sie Folgendes ein, um die aktuelle Zeitzone auf Pacific Normalzeit festzulegen und die Anpassungen der Sommerzeit zu deaktivieren:
```
tzutil /s Pacific Standard time_dstoff
```
## <a name="additional-references"></a>Weitere Verweise
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

