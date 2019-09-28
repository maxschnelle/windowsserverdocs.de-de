---
title: bizadmin gettemporaryname
description: Windows-Befehls Thema für **bizadmin gettemporaryname** -meldet den temporären Dateinamen der angegebenen Datei innerhalb des Auftrags.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7b665fae4c0bfdd5ea04b929be49f9590430b358
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381299"
---
# <a name="bitsadmin-gettemporaryname"></a>bizadmin gettemporaryname



Meldet den temporären Dateinamen der angegebenen Datei innerhalb des Auftrags.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetTemporaryName <Job> <file index> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Datei index|Beginnt bei 0|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der temporäre Dateiname der Datei 2 für den Auftrag mit dem Namen *MyJob*gemeldet.
```
C:\>bitsadmin /GetTemporaryName myJob 1 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)