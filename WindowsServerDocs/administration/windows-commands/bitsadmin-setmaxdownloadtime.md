---
title: BI-admin setmaxdownloadtime
description: Windows-Befehls Thema für bistiadmin setmaxdownloadtime, das das Download Timeout in Sekunden festlegt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fd44011cd14d575a9c3798ede45641fac4c3dc75
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849373"
---
# <a name="bitsadmin-setmaxdownloadtime"></a>BI-admin setmaxdownloadtime

Legt das Download Timeout in Sekunden fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetMaxDownloadTime <Job> <Timeout>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Timeout|Das Timeout in Sekunden|

## <a name="remarks"></a>Hinweise

-   N/V

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird das Timeout für den Auftrag mit dem Namen *mydownloadjob* auf 10 Sekunden festgelegt.
```
C:\>bitsadmin /SetMaxDownloadTime myDownloadJob 10
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)