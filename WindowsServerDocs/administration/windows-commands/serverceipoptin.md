---
title: serverceipoptin
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3d7d7fa7-0689-4797-b802-36fe260d21a0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c0625694053a2d673cd86e12d6f6d54662a6c81d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834679"
---
# <a name="serverceipoptin"></a>serverceipoptin

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht die Teilnahme am Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP).
## <a name="syntax"></a>Syntax
```
serverceipoptin [/query] [/enable] [/disable]
```
#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/Query "aus|überprüft die aktuelle Einstellung.|
|/enable|Ermöglicht die Teilnahme.|
|/Disable|Deaktiviert die Teilnahme.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele
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
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

