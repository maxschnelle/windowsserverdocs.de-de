---
title: Bitsadmin setcustomheaders
description: Windows-Befehle Thema **Bitsadmin Setcustomheaders** – eine GET-Anforderung einen benutzerdefinierten HTTP-Header hinzugefügt.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6d90ac2d23b852ae0c2114e7cd5a9c9e6382ce8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853851"
---
# <a name="bitsadmin-setcustomheaders"></a>Bitsadmin setcustomheaders



Fügen Sie einen benutzerdefinierten HTTP-Header für eine GET-Anforderung hinzu.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetCustomHeaders <Job> <Header1> <Header2> <. . .>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Header1 Header2 . . .|Die benutzerdefinierten Header für den Auftrag|

## <a name="remarks"></a>Hinweise

-   Dieser Schalter wird verwendet, um einen benutzerdefinierten HTTP-Header eine GET-Anforderung gesendet, um einen HTTP-Server hinzufügen.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel fügt einen benutzerdefinierten HTTP-Header für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin / SetCustomHeaders myDownloadJob "Accept-encoding:deflate/gzip"
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)