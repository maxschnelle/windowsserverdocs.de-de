---
title: ktmutil
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 53bc56df-f0e5-443b-ab20-bbf8b11d4a9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 47b447165ee54e6839bb6338801c6703d818caa8
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724523"
---
# <a name="ktmutil"></a>ktmutil



Startet das Hilfsprogramm für den Kernel Transaktions-Manager. Bei Verwendung ohne Parameter zeigt " **ktmutil** " verfügbare Unterbefehle an.



## <a name="syntax"></a>Syntax

```
ktmutil list tms 
ktmutil list transactions [{TmGuid}]
ktmutil resolve complete {TmGuid} {RmGuid} {EnGuid}
ktmutil resolve commit {TxGuid}
ktmutil resolve rollback {TxGuid}
ktmutil force commit {??Guid}
ktmutil force rollback {??Guid}
ktmutil forget
```

### <a name="parameters"></a>Parameter

## <a name="remarks"></a>Bemerkungen

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine unzweifel hafte Transaktion mit der GUID 311a9209-03f4-11dc-918f-00188b8f707b für den Commit zu erzwingen:
```
ktmutil force commit {311a9209-03f4-11dc-918f-00188b8f707b}
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)