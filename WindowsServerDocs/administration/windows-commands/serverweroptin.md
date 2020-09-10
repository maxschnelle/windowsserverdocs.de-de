---
title: serverweroptin
description: Referenz Artikel für * * * *-
ms.topic: reference
ms.assetid: f3c0b0af-cafb-4f09-8b36-5a357ddf392d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 73bdce2a4b18f55239b61132df0417b02cb683c2
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637785"
---
# <a name="serverweroptin"></a>serverweroptin

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht es Ihnen, die Fehlerberichterstattung zu aktivieren.
## <a name="syntax"></a>Syntax
```
serverweroptin [/query] [/detailed] [/summary]
```
#### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|/Query "aus|überprüft die aktuelle Einstellung.|
|/Detailed|Sendet detaillierte Berichte automatisch.|
|/Summary|Sendet Zusammenfassungs Berichte automatisch.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="examples"></a>Beispiele
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
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

