---
title: bitsadmin getreplyprogress
description: Windows-Befehle Thema **Bitsadmin Getreplyprogress** -Ruft die Größe und der Status, der die Antwort des Servers ab.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: aafecfb5873392ef86e6f7cceb139091b15e3b99
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852931"
---
# <a name="bitsadmin-getreplyprogress"></a>bitsadmin getreplyprogress

Ruft ab, die Größe und den Status der Serverantwort.

**BITS-Version 1.2 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetReplyProgress <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

Gilt nur für den Upload-Antwort-Aufträge.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft den Status der Antwort für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /GetReplyProgress myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)