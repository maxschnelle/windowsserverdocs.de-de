---
title: bitsadmin getbytestotal
description: Thema Windows-Befehle für **bizadmin GetBytesTotal** -Ruft die Größe des angegebenen Auftrags ab.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 784e0bfa-7b09-4262-9104-adbc9beb479b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38b0f09e13919e0c75d2b7429dd66f765b434de5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381748"
---
# <a name="bitsadmin-getbytestotal"></a>bitsadmin getbytestotal



Ruft die Größe des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetBytesTotal <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Größe des Auftrags mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /GetBytesTotal myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)