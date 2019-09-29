---
title: bizadmin-Cache und Info
description: Windows-Befehls Thema für den **bistiadmin-Cache und Info** -Dumps einen bestimmten Cache Eintrag.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 11963ff5640ef30e597e5e802778aff121c0efb3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381966"
---
# <a name="bitsadmin-cache-and-info"></a>bizadmin-Cache und Info



Sichert einen bestimmten Cache Eintrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /Cache /Info RecordID [/Verbose] 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Datensatz|Die GUID, die dem Cache Eintrag zugeordnet ist.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Cache Eintrag mit dem Datensatz did {6511b595-E195-40A2-b47702 e8e2f 8F} Abbilder.
```
C:\>bitsadmin /Cache /Info {6511FB02-E195-40A2-B595-E8E2F8F47702} 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)