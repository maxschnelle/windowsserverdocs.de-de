---
title: biout admin Cache und DELETE
description: Windows-Befehls Thema für den **bistiadmin-Cache und DELETE** -löscht einen bestimmten Cache Eintrag.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 22540273-55a5-46ea-869b-6df2aa6808a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87c3ffd7e0c9c43e8e2eb6e5d5a1d98610a4d9ad
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382075"
---
# <a name="bitsadmin-cache-and-delete"></a>biout admin Cache und DELETE



Löscht einen bestimmten Cache Eintrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /Cache /Delete RecordID 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Datensatz|Die GUID, die dem Cache Eintrag zugeordnet ist.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Cache Eintrag mit dem Datensatz did {6511b595-E195-40A2-b47702 e8e2f 8F} gelöscht.
```
C:\>bitsadmin /Cache /Delete {6511FB02-E195-40A2-B595-E8E2F8F47702} 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)