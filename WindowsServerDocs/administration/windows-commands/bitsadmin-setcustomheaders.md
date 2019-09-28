---
title: bitadmin setcustomheaders
description: Windows-Befehls Thema für **bitionadmin setcustomheaders** -Hinzufügen eines benutzerdefinierten HTTP-Headers zu einer GET-Anforderung.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 45e3a5178df69b84618966ca0fcd9cc1e6d0e449
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380639"
---
# <a name="bitsadmin-setcustomheaders"></a>bitadmin setcustomheaders



Fügen Sie einen benutzerdefinierten HTTP-Header zu einer GET-Anforderung hinzu.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetCustomHeaders <Job> <Header1> <Header2> <. . .>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Header1 Header2. . .|Die benutzerdefinierten Header für den Auftrag.|

## <a name="remarks"></a>Hinweise

-   Mithilfe dieses Schalters wird einer GET-Anforderung, die an einen HTTP-Server gesendet wird, ein benutzerdefinierter HTTP-Header hinzugefügt.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird ein benutzerdefinierter HTTP-Header für den Auftrag mit dem Namen *mydownloadjob*hinzugefügt.
```
C:\>bitsadmin / SetCustomHeaders myDownloadJob "Accept-encoding:deflate/gzip"
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)