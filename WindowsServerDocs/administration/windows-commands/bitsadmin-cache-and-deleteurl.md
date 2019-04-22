---
title: Bitsadmin-Cache und deleteurl
description: Windows-Befehle Thema **Bitsadmin Cache und Deleteurl** -löscht alle Einträge im Cache für die angegebene URL.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e108b76b-fae9-4c16-bf4c-d74c9f025953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a831c49e1461761cb7466b46e7a5ad8e037f4ec9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816651"
---
# <a name="bitsadmin-cache-and-deleteurl"></a>Bitsadmin-Cache und deleteurl



Löscht alle Einträge im Cache für die angegebene URL.

## <a name="syntax"></a>Syntax

```
bitsadmin /DeleteURL url
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|URL|Der Uniform Resource Locator, die eine entfernte Datei identifiziert.|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel löscht alle Cacheeinträge für https://www.microsoft.com/en/us/default.aspx
```
C:\>bitsadmin /DeleteURL https://www.microsoft.com/en/us/default.aspx 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)