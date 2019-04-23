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
ms.openlocfilehash: 868f7ac58a69c067681bf0597524fbaa5a25984f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842421"
---
#<a name="bitsadmin-getmaxdownloadtime"></a>Bitsadmin getmaxdownloadtime

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
[Befehlszeilensyntax](command-line-syntax-key.md)


