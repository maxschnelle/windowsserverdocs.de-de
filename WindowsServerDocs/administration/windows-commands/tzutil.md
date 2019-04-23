---
title: tzutil
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 41a46ea7974b67cc557973484428480e7beb5484
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876801"
---
# <a name="tzutil"></a>tzutil

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Die Zeit wird die Windows-Hilfsprogramm Zone. 
## <a name="syntax"></a>Syntax
```
tzutil [/?] [/g] [/s <timeZoneID>[_dstoff]] [/l]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
|/g|Zeigt die aktuelle Zeitzone-ID an.|
|/s \<timeZoneID>[_dstoff]|Legt die aktuelle Zeitzone, die mithilfe der angegebenen Zeitzone-ID. Die **_dstoff** Suffix deaktiviert Anpassungen für die Sommerzeit für die Zeitzone, (falls zutreffend).|
|/l|Listet alle gültige Uhrzeit zone IDs und Anzeigenamen. Die Ausgabe werden:<br /><br />-   \<der Anzeigename ><br />-   \<Zeitzonen-ID >|

## <a name="remarks"></a>Hinweise
Ein Exitcode **0** gibt den Befehl wurde erfolgreich abgeschlossen.

## <a name="BKMK_Examples"></a>Beispiele für
Wenn die aktuelle Zeitzone-ID anzeigen möchten, geben Sie Folgendes ein:
```
tzutil /g
```
Um die aktuelle Zeitzone Pacific Standard Time festzulegen, geben Sie Folgendes ein:
```
tzutil /s Pacific Standard time
```
Die aktuelle Zeitzone Pacific Standard Time festgelegt, und Deaktivieren von Sommerzeit Anpassungen aus, geben Sie Folgendes ein:
```
tzutil /s Pacific Standard time_dstoff
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Befehlszeilensyntax](command-line-syntax-key.md)

