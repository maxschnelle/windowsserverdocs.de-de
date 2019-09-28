---
title: bizadmin getvalidationstate
description: 'Windows-Befehls Thema für **BITSAdmin getvalidationstate** -meldet den Status der Inhalts Überprüfung der angegebenen Datei innerhalb des Auftrags. '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca4269a596010258edd0479f5a7e9844bc9c98df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381259"
---
# <a name="bitsadmin-getvalidationstate"></a>bizadmin getvalidationstate



Meldet den Status der Inhalts Überprüfung der angegebenen Datei innerhalb des Auftrags.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetValidationState <Job> <file index> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Datei index|Beginnt bei 0|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Status der Inhalts Überprüfung der Datei 2 innerhalb des Auftrags mit dem Namen " *MyJob*" abgerufen.
```
C:\>bitsadmin /GetValidationState myJob 1
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)