---
title: serverweroptin
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f3c0b0af-cafb-4f09-8b36-5a357ddf392d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 18b4a56888b3f23bf3bac4a12b2dba7079b50923
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834633"
---
# <a name="serverweroptin"></a>serverweroptin

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht es Ihnen, die Fehlerberichterstattung zu aktivieren.
## <a name="syntax"></a>Syntax
```
serverweroptin [/query] [/detailed] [/summary]
```
#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/Query "aus|überprüft die aktuelle Einstellung.|
|/Detailed|Sendet detaillierte Berichte automatisch.|
|/Summary|Sendet Zusammenfassungs Berichte automatisch.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele
Zum Überprüfen der aktuellen Einstellung geben Sie Folgendes ein:
```
serverweroptin /query
```
Geben Sie Folgendes ein, um automatisch ausführliche Berichte zu senden:
```
serverweroptin /detailed
```
Geben Sie zum automatischen Senden von Zusammenfassungs Berichten
```
serverweroptin /summary
```
## <a name="additional-references"></a>Weitere Verweise
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

