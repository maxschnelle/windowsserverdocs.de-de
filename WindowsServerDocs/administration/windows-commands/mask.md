---
title: mask
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 816bcd932091b33ed897add5a13603e3a1eea925
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724011"
---
# <a name="mask"></a>mask



Entfernt Hardware Schatten Kopien, die mithilfe des **Import** -Befehls importiert wurden.



## <a name="syntax"></a>Syntax

```
mask <ShadowSetID>
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|Shadow-TID|Entfernt Schatten Kopien, die zur angegebenen Schattenkopiesatz-ID gehören.|

## <a name="remarks"></a>Bemerkungen

-   Anstelle von *Shadow* TID*können Sie einen vorhandenen Alias oder eine Umgebungsvariable verwenden. Verwenden **Sie hinzufügen** ohne Parameter, um vorhandene Aliase anzuzeigen.

## <a name="examples"></a>Beispiele

Um die importierte Schatten Kopie% Import_1% zu entfernen, geben Sie Folgendes ein:
```
mask %Import_1%
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)