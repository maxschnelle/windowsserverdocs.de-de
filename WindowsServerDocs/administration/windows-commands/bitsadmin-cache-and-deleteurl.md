---
title: biout admin Cache und DeleteUrl
description: 'Windows-Befehls Thema für den **BI-admin-Cache und DeleteUrl** : Löscht alle Cache Einträge für die angegebene URL.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 869d3bc0f011cc82aaea9b7468667964051e1c00
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382057"
---
# <a name="bitsadmin-cache-and-deleteurl"></a>biout admin Cache und DeleteUrl



Löscht alle Cache Einträge für die angegebene URL.

## <a name="syntax"></a>Syntax

```
bitsadmin /DeleteURL url
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|URL|Der Uniform Resource Locator, der eine Remote Datei identifiziert.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden alle Cache Einträge für https://www.microsoft.com/en/us/default.aspx gelöscht.
```
C:\>bitsadmin /DeleteURL https://www.microsoft.com/en/us/default.aspx 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)