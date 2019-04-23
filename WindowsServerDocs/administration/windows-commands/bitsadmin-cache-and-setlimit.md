---
title: Bitsadmin-Cache und setlimit
description: Windows-Befehle Thema **Bitsadmin Cache und Setlimit** -legt das Limit der Cache-Größe.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d0b72c5ec6c779fa4ce3fa038352836cd9456ac
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852591"
---
# <a name="bitsadmin-cache-and-setlimit"></a>Bitsadmin-Cache und setlimit



Legt das Limit der Cache-Größe.

## <a name="syntax"></a>Syntax

```
bitsadmin /Cache /SetLimit Percent
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Prozent|Das CacheLimit, definiert als Prozentsatz der gesamte Festplattenspeicherplatz...|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel schränkt die Cachegröße auf 50 %.
```
C:\>bitsadmin /Cache /SetLimit 50 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)