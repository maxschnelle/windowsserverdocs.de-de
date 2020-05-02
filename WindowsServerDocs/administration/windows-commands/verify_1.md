---
title: Überprüfen
description: Referenz Thema zur Überprüfung, das **cmd** mitteilt, ob die Dateien ordnungsgemäß auf einen Datenträger geschrieben werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dfe8bc91-d948-4e47-84ad-a79a60506ffa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f7fc35b37d5e0a429e1ecc2ebefc117804a0c645
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720295"
---
# <a name="verify"></a>Überprüfen



Weist **cmd** an, zu überprüfen, ob Ihre Dateien ordnungsgemäß auf einen Datenträger geschrieben wurden. Bei Verwendung ohne **Parameter zeigt die** aktuelle Einstellung an.



## <a name="syntax"></a>Syntax

```
verify [on | off]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\| [ein]|Schaltet die **Überprüfung** ein oder aus.|
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)