---
title: Bitsadmin getmaxdownloadtime
description: Windows-Befehle Thema **Bitsadmin Getmaxdownloadtime** -Ruft die Downloadtimeout in Sekunden ab.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdce64f6-7125-489d-be3c-4af1dfc8c46a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d067d6a0821d9af4784c02c6a332e8eddd2352c0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434943"
---
# <a name="bitsadmin-getmaxdownloadtime"></a>Bitsadmin getmaxdownloadtime

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ruft das Downloadtimeout in Sekunden ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetMaxDownloadtime <Job> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

-   N\/A

## <a name="BKMK_examples"></a>Beispiele für
Im folgenden Beispiel wird der maximalen Downloadzeit für den Auftrag mit dem Namen *MyDownloadJob* in Sekunden.

```
C:\>bitsadmin /GetMaxDownloadtime myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)


