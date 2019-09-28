---
title: bdehdcfg newdriveletter
description: 'Thema Windows-Befehle für bdehdcfg newdriveletter: weist dem Teil eines Laufwerks, das als Systemlaufwerk verwendet wird, einen neuen Laufwerk Buchstaben zu.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2abd4a686f358b5dd844514735edb3ffaa13845
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382229"
---
# <a name="bdehdcfg-newdriveletter"></a>bdehdcfg: newdriveletter



Weist dem Teil eines Laufwerks, das als Systemlaufwerk verwendet wird, einen neuen Laufwerk Buchstaben zu. Ein Beispiel für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -newdriveletter <DriveLetter>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<driveletter >|Definiert den Laufwerk Buchstaben, der dem angegebenen Ziellaufwerk zugewiesen wird.|

## <a name="remarks"></a>Hinweise

Als bewährte Vorgehensweise wird empfohlen, dem Systemlaufwerk keinen Laufwerk Buchstaben zuzuweisen.

## <a name="BKMK_Examples"></a>Beispiele

Im folgenden Beispiel wird gezeigt, wie dem Standard Laufwerk der Laufwerk Buchstabe P zugewiesen wird.
```
bdehdcfg -target default -newdriveletter P:
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)