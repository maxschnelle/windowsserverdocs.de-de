---
title: bitsadmin geterror
description: 'Windows-Befehls Thema für **bizadmin getError** : Ruft ausführliche Fehlerinformationen für den angegebenen Auftrag ab.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0f9bd607886d00ede4e1da91ed73eff2794db6ce
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381643"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror



Ruft ausführliche Fehlerinformationen für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetError <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden die Fehlerinformationen für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /GetError myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)