---
title: ktmutil
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 53bc56df-f0e5-443b-ab20-bbf8b11d4a9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d1a8fbc6360eca628d380a9c24612d952120162d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374785"
---
# <a name="ktmutil"></a>ktmutil



Startet das Hilfsprogramm für den Kernel Transaktions-Manager. Bei Verwendung ohne Parameter zeigt " **ktmutil** " verfügbare Unterbefehle an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

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

## <a name="parameters"></a>Parameter

## <a name="remarks"></a>Hinweise

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um eine unzweifel hafte Transaktion mit der GUID 311a9209-03f4-11dc-918f-00188b8f707b für den Commit zu erzwingen:
```
ktmutil force commit {311a9209-03f4-11dc-918f-00188b8f707b}
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)