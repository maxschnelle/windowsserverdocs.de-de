---
title: bitsadmin getfilestransferred
description: 'Thema Windows-Befehle für **bizadmin getfilestransferred** : Ruft die Anzahl der für den angegebenen Auftrag übertragenen Dateien ab.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e282815c-938b-4ac0-a09d-9baafb656dcb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d02d9d7bc216a5ad7ca922e716c368f64c4b9a44
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381601"
---
# <a name="bitsadmin-getfilestransferred"></a>bitsadmin getfilestransferred



Ruft die Anzahl der Dateien ab, die für den angegebenen Auftrag übertragen wurden.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetFilesTransferred <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Anzahl der Dateien abgerufen, die im Auftrag mit dem Namen *mydownloadjob*übertragen wurden.
```
C:\>bitsadmin /GetFilesTransferred myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)