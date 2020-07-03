---
title: revert
description: Referenz Artikel für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75ad40e4-502a-401e-b11e-8b31e00424b5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8d2d8bfbfa10df9776e849b1450c2fce47c097b7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933041"
---
# <a name="revert"></a>revert



Setzt ein Volume auf eine angegebene Schatten Kopie zurück. Dies wird nur für Schatten Kopien im Client zugänglichen Kontext unterstützt. Diese Schatten Kopien sind persistent und können nur vom Systemanbieter erstellt werden. Bei Verwendung ohne Parameter zeigt **Revert** die Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
revert <ShadowCopyID>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<ShadowCopyID>|Gibt die Schattenkopiekennung an, auf der das Volume wieder hergestellt wird|

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)