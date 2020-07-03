---
title: Überprüfen
description: Referenz Artikel zur Überprüfung, der **cmd** mitteilt, ob die Dateien ordnungsgemäß auf einen Datenträger geschrieben werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dfe8bc91-d948-4e47-84ad-a79a60506ffa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1455705d409e0273e85135a183279835e7238d7a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931317"
---
# <a name="verify"></a>Überprüfen



Weist **cmd** an, zu überprüfen, ob Ihre Dateien ordnungsgemäß auf einen Datenträger geschrieben wurden. Bei Verwendung ohne **Parameter zeigt die** aktuelle Einstellung an.



## <a name="syntax"></a>Syntax

```
verify [on | off]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[ein \| ]|Schaltet die **Überprüfung** ein oder aus.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die aktuelle **Verify** -Einstellung anzuzeigen:
```
verify
```
Geben Sie Folgendes ein, um die Einstellung **überprüfen** für zu aktivieren:
```
Verify on
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)