---
title: ktmutil
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 7af47ab8697345b81018c2539e0c451359bd2a2f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826461"
---
# <a name="ktmutil"></a>ktmutil



Vom Kerneltransaktions-Manager-Dienstprogramm gestartet. Wenn Sie ohne Angabe von Parametern **Ktmutil** verfügbaren Unterbefehle angezeigt.

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

## <a name="BKMK_examples"></a>Beispiele für

Um eine Transaktion ist zweifelhaft mit GUID 311a9209-03f4-11dc-918f-00188b8f707b einen commit für zu erzwingen, geben Sie Folgendes ein:
```
ktmutil force commit {311a9209-03f4-11dc-918f-00188b8f707b}
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)