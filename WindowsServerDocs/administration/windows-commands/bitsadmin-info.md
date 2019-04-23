---
title: bitsadmin Informationen
description: Windows-Befehle Thema **zeigt zusammenfassende Informationen zu den angegebenen Auftrag.** -Bitsadmin-Informationen
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ee96c69e311600a53f04b1b883983718adf0f69
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851521"
---
# <a name="bitsadmin-info"></a>bitsadmin Informationen



Zeigt zusammenfassende Informationen über den angegebenen Auftrag.

## <a name="syntax"></a>Syntax

```
bitsadmin /Info <Job> [/verbose]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

Verwenden der / verbose Parameter, um ausführliche Informationen zum Auftrag bereitzustellen.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft Informationen über den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /Info myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)