---
title: biout admin Cache und setLimit
description: 'Windows-Befehls Thema für **bitadmin-Cache und setLimit** : legt das Cache Größenlimit fest.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 88a10ce8599202e237daa6822cf62806d3c21429
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381937"
---
# <a name="bitsadmin-cache-and-setlimit"></a>biout admin Cache und setLimit



Legt die Cache Größenbeschränkung fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /Cache /SetLimit Percent
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Prozenti|Der als Prozentsatz des gesamten Festplatten Speichers definierte Cache Limit.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Cache Größe auf 50% beschränkt.
```
C:\>bitsadmin /Cache /SetLimit 50 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)