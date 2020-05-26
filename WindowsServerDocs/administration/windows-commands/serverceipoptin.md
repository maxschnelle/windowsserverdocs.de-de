---
title: serverceipoptin
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3d7d7fa7-0689-4797-b802-36fe260d21a0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45511ee5028779358c77e18c4e1c193dcd86fdfe
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821060"
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
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

