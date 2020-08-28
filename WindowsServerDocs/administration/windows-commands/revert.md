---
title: umzukehren
description: Referenz Artikel für den revert-Befehl, mit dem ein Volume auf eine angegebene Schatten Kopie zurückgesetzt wird.
ms.topic: reference
ms.assetid: 75ad40e4-502a-401e-b11e-8b31e00424b5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cc80890604b5ad1a308d1cd4df9cd23465c970d2
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027278"
---
# <a name="revert"></a>umzukehren

Setzt ein Volume auf eine angegebene Schatten Kopie zurück. Dies wird nur für Schatten Kopien im Client zugänglichen Kontext unterstützt. Diese Schatten Kopien sind persistent und können nur vom Systemanbieter erstellt werden. Bei Verwendung ohne Parameter zeigt **Revert** die Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
revert <shadowcopyID>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| `<shadowcopyID>` | Gibt die Schattenkopiekennung an, auf der das Volume wieder hergestellt wird Wenn Sie diesen Parameter nicht verwenden, zeigt der Befehl die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
