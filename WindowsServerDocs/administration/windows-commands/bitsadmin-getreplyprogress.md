---
title: bitsadmin getreplyprogress
description: 'Thema Windows-Befehle für **BITSAdmin getreplyprogress** : Ruft die Größe und den Fortschritt der Serverantwort ab.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f7cb0b4-ad95-44fd-a35d-0ddf5fc0b0d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c791fe98271b497e5ecf48338ab3bbb0cc50de98
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381239"
---
# <a name="bitsadmin-getreplyprogress"></a>bitsadmin getreplyprogress

Ruft die Größe und den Fortschritt der Serverantwort ab.

**Bits 1,2 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetReplyProgress <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="remarks"></a>Hinweise

Nur für Upload-Antwort-Aufträge gültig.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Antwortstatus des Auftrags mit dem Namen " *mydownloadjob*" abgerufen.
```
C:\>bitsadmin /GetReplyProgress myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)