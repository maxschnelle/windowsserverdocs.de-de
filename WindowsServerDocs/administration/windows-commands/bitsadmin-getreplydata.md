---
title: bitsadmin getreplydata
description: 'Thema Windows-Befehle für **BITSAdmin getreplydata** : Ruft die Antwortdaten des Servers im Hexadezimal Format ab.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 819f97d5-b255-4b2d-9f63-0daa73915434
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7ebd3ee77e5d442467f49bb209c560f089f2271b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381279"
---
# <a name="bitsadmin-getreplydata"></a>bitsadmin getreplydata

Ruft die Antwortdaten des Servers im Hexadezimal Format ab.

**Bits 1,2 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetReplyData <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Nur für Upload-Antwort-Aufträge gültig.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden die Antwortdaten für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /GetReplyData myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)