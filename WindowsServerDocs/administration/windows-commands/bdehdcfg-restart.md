---
title: Bdehdcfg-Neustart
description: Windows-Befehle Thema Bdehdcfg-Neustarts – weist Bdehdcfg an, dass der Computer neu gestartet werden soll, nachdem die laufwerksvorbereitung abgeschlossen wurde.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a98b76bb-36f1-4790-b337-7dc35f606bc6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0f361db8fdf33bd414556575de75241f7dbd9327
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879461"
---
# <a name="bdehdcfg-restart"></a>Bdehdcfg: neu starten



Informiert dem Befehlszeilentool "Bdehdcfg", dass der Computer neu gestartet werden soll, nachdem die laufwerksvorbereitung abgeschlossen wurde. Ein Beispiel, wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -restart
```

### <a name="parameters"></a>Parameter

Dieser Befehl akzeptiert keine zusätzlichen Parameter.

## <a name="remarks"></a>Hinweise

Wenn andere Benutzer auf dem Computer angemeldet sind und die **quiet** Befehl nicht angegeben wird, eine Eingabeaufforderung angezeigt wird, um sicherzustellen, dass der Computer neu gestartet werden soll.

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel veranschaulicht die Verwendung der **Neustart** Befehl.
```
bdehdcfg -target default -restart
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)