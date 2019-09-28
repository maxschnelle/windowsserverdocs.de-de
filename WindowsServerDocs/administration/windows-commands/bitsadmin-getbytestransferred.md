---
title: bitsadmin getbytestransferred
description: 'Thema Windows-Befehle für **bizadmin getbytestransferred** : Ruft die Anzahl der für den angegebenen Auftrag übertragenen Bytes ab.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f690fa55a4ac5ae31223794c5e7eabc0c982c2ce
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381734"
---
# <a name="bitsadmin-getbytestransferred"></a>bitsadmin getbytestransferred



Ruft die Anzahl der Bytes ab, die für den angegebenen Auftrag übertragen wurden.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetBytesTransferred <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Anzahl der Bytes abgerufen, die für den Auftrag mit dem Namen *mydownloadjob*übertragen werden.
```
C:\>bitsadmin /GetBytesTransferred myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)