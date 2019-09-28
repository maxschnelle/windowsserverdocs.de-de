---
title: BI-admin setmaxdownloadtime
description: 'Windows-Befehls Thema für **bitadmin setmaxdownloadtime** : legt das Download Timeout in Sekunden fest.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 985453de5bd2f4a06b5635ae5b0a9794d30175b0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380556"
---
# <a name="bitsadmin-setmaxdownloadtime"></a>BI-admin setmaxdownloadtime



Legt das Download Timeout in Sekunden fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetMaxDownloadTime <Job> <Timeout>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Timeout|Das Timeout in Sekunden|

## <a name="remarks"></a>Hinweise

-   Nicht zutreffend

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird das Timeout für den Auftrag mit dem Namen *mydownloadjob* auf 10 Sekunden festgelegt.
```
C:\>bitsadmin /SetMaxDownloadTime myDownloadJob 10
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)