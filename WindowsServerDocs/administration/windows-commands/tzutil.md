---
title: tzutil
description: Referenz Artikel zu "TZUtil", in dem das Windows-Zeit Zonen Dienstprogramm angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bcf6e007-c9b6-4df5-83c5-ed7b4b1b5913
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 99d88057c88a55aaf529d238088f8422c33e9ba7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937294"
---
# <a name="tzutil"></a>tzutil

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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
|/s \<timeZoneID> [_dstoff]|Legt die aktuelle Zeitzone mithilfe der angegebenen Zeit Zonen-ID fest. Mit dem **_dstoff** Suffix werden die Anpassungen der Sommerzeit für die Zeitzone deaktiviert (falls zutreffend).|
|/l|Listet alle gültigen Zeit Zonen-IDs und anzeigen Amen auf. Ausgabe:<p>-   \<display name><br />-   \<time zone ID>|

## <a name="remarks"></a>Hinweise
Der Exitcode **0** gibt an, dass der Befehl erfolgreich abgeschlossen wurde.

## <a name="examples"></a>Beispiele
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
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

