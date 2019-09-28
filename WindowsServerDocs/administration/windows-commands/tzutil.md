---
title: tzutil
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bcf6e007-c9b6-4df5-83c5-ed7b4b1b5913
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 347254bd5a00a8bfb4a80f20d518f1e0e8b593bf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392303"
---
# <a name="tzutil"></a>tzutil

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt das Windows-Zeit Zonen Dienstprogramm an. 
## <a name="syntax"></a>Syntax
```
tzutil [/?] [/g] [/s <timeZoneID>[_dstoff]] [/l]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
|/g|Zeigt die aktuelle Zeit Zonen-ID an.|
|/s \<timezoneid > [_dstoff]|Legt die aktuelle Zeitzone mithilfe der angegebenen Zeit Zonen-ID fest. Das Suffix **_dstoff** deaktiviert die Sommerzeit Anpassungen für die Zeitzone (falls zutreffend).|
|/l|Listet alle gültigen Zeit Zonen-IDs und anzeigen Amen auf. Die Ausgabe lautet wie folgt:<br /><br />-    @ no__t-1anzeige Name ><br />-    @ no__t-1 Zeit Zonen-ID >|

## <a name="remarks"></a>Hinweise
Der Exitcode **0** gibt an, dass der Befehl erfolgreich abgeschlossen wurde.

## <a name="BKMK_Examples"></a>Beispiele
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
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

