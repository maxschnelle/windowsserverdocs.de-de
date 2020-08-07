---
title: serverceipoptin
description: Referenz Artikel für * * * *-
ms.topic: article
ms.assetid: 3d7d7fa7-0689-4797-b802-36fe260d21a0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 47928232de399baf1f8351f865fbff18f1126340
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882755"
---
# <a name="serverceipoptin"></a>serverceipoptin

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht die Teilnahme am Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP).
## <a name="syntax"></a>Syntax
```
serverceipoptin [/query] [/enable] [/disable]
```
#### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|/Query "aus|überprüft die aktuelle Einstellung.|
|/enable|Ermöglicht die Teilnahme.|
|/Disable|Deaktiviert die Teilnahme.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="examples"></a>Beispiele
Zum Überprüfen der aktuellen Einstellungen geben Sie Folgendes ein:
```
serverceipoptin /query
```
Geben Sie zum Aktivieren der Teilnahme Folgendes ein:
```
serverceipoptin /enable
```
Zum Deaktivieren der Teilnahme geben Sie Folgendes ein:
```
serverceipoptin /disable
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

