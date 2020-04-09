---
title: bitadmin setcustomheaders
description: Windows-Befehls Thema für BI-admin setcustomheaders, das einer GET-Anforderung einen benutzerdefinierten HTTP-Header hinzufügt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5d97fae5f84637c80c3d1ef00aa36f09049bb17
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849613"
---
# <a name="bitsadmin-setcustomheaders"></a>bitadmin setcustomheaders

Fügen Sie einen benutzerdefinierten HTTP-Header zu einer GET-Anforderung hinzu.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetCustomHeaders <Job> <Header1> <Header2> <. . .>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Header1 Header2. . .|Die benutzerdefinierten Header für den Auftrag.|

## <a name="remarks"></a>Hinweise

-   Mithilfe dieses Schalters wird einer GET-Anforderung, die an einen HTTP-Server gesendet wird, ein benutzerdefinierter HTTP-Header hinzugefügt.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird ein benutzerdefinierter HTTP-Header für den Auftrag mit dem Namen *mydownloadjob*hinzugefügt.
```
C:\>bitsadmin / SetCustomHeaders myDownloadJob Accept-encoding:deflate/gzip
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)