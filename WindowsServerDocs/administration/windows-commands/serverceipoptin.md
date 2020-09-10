---
title: serverceipoptin
description: Referenz Artikel für * * * *-
ms.topic: reference
ms.assetid: 3d7d7fa7-0689-4797-b802-36fe260d21a0
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 691b2e072d6581f8f8760e20d4ba8f09500ed169
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89638979"
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

