---
title: serverweroptin
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f3c0b0af-cafb-4f09-8b36-5a357ddf392d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6329552d3525a1330286e04c6400378b14039fbf
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821270"
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
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

