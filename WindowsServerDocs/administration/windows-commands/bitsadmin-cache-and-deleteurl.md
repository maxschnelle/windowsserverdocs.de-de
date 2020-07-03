---
title: biout admin Cache und DeleteUrl
description: Referenz Artikel für den bizadmin-Cache und den DeleteUrl-Befehl, der alle Cache Einträge für die angegebene URL löscht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e108b76b-fae9-4c16-bf4c-d74c9f025953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8d1ed4710bfeeefa721308c54075ddc8da5c5216
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923330"
---
# <a name="bitsadmin-cache-and-deleteurl"></a>biout admin Cache und DeleteUrl

Löscht alle Cache Einträge für die angegebene URL.

## <a name="syntax"></a>Syntax

```
bitsadmin /deleteURL URL
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| URL | Der Uniform Resource Locator, der eine Remote Datei identifiziert. |

## <a name="examples"></a>Beispiele

So löschen Sie alle Cache Einträge für `https://www.contoso.com/en/us/default.aspx` :

```
bitsadmin /deleteURL https://www.contoso.com/en/us/default.aspx
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "biout admin Cache"](bitsadmin-cache.md)
