---
title: serverweroptin
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3c0b0af-cafb-4f09-8b36-5a357ddf392d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a7d5791e059d31e416f848f6e8df648c8f9bd27d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371021"
---
# <a name="serverweroptin"></a>serverweroptin

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht es Ihnen, die Fehlerberichterstattung zu aktivieren.
## <a name="syntax"></a>Syntax
```
serverweroptin [/query] [/detailed] [/summary]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/Query "aus|überprüft die aktuelle Einstellung.|
|/Detailed|Sendet detaillierte Berichte automatisch.|
|/Summary|Sendet Zusammenfassungs Berichte automatisch.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="BKMK_Examples"></a>Beispiele
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
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

