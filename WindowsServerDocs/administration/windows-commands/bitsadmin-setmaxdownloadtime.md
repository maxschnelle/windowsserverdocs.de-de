---
title: Bitsadmin setmaxdownloadtime
description: Windows-Befehle Thema **Bitsadmin Setmaxdownloadtime** -Downloadtimeout in Sekunden festgelegt.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f13b44429bec2718af1a648f273fead18d4e9e08
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830991"
---
# <a name="bitsadmin-setmaxdownloadtime"></a>Bitsadmin setmaxdownloadtime



Die Downloadtimeout festgelegt in Sekunden.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetMaxDownloadTime <Job> <Timeout>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Zeitüberschreitung|Das Timeout in Sekunden|

## <a name="remarks"></a>Hinweise

-   Nicht zutreffend

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird das Timeout für den Auftrag mit dem Namen *MyDownloadJob* auf 10 Sekunden.
```
C:\>bitsadmin /SetMaxDownloadTime myDownloadJob 10
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)