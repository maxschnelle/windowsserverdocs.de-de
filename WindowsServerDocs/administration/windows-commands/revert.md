---
title: umzukehren
description: Referenz Artikel für den revert-Befehl, mit dem ein Volume auf eine angegebene Schatten Kopie zurückgesetzt wird.
ms.topic: reference
ms.assetid: 75ad40e4-502a-401e-b11e-8b31e00424b5
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3c909cec1e503552f68cad55489529585a5eaf51
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640622"
---
# <a name="revert"></a>umzukehren

Setzt ein Volume auf eine angegebene Schatten Kopie zurück. Dies wird nur für Schatten Kopien im Client zugänglichen Kontext unterstützt. Diese Schatten Kopien sind persistent und können nur vom Systemanbieter erstellt werden. Bei Verwendung ohne Parameter zeigt **Revert** die Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
revert <shadowcopyID>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<shadowcopyID>` | Gibt die Schattenkopiekennung an, auf der das Volume wieder hergestellt wird Wenn Sie diesen Parameter nicht verwenden, zeigt der Befehl die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
