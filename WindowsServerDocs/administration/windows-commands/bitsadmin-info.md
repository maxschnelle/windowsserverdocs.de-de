---
title: bitsadmin Informationen
description: Das Thema Windows-Befehle für **zeigt zusammenfassende Informationen zum angegebenen Auftrag an.** -bizadmin-Informationen
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b6710d73860315fcd13670669871cd310ffb41c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381076"
---
# <a name="bitsadmin-info"></a>bitsadmin Informationen



Zeigt zusammenfassende Informationen zum angegebenen Auftrag an.

## <a name="syntax"></a>Syntax

```
bitsadmin /Info <Job> [/verbose]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Verwenden Sie den/Verbose-Parameter, um ausführliche Informationen zum Auftrag bereitzustellen.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden Informationen zum Auftrag mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /Info myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)