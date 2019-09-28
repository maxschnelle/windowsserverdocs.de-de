---
title: bdehdcfg-Neustart
description: 'Windows-Befehls Thema für bdehdcfg-Neustart: weist bdehdcfg darauf hin, dass der Computer nach Abschluss der Laufwerks Vorbereitung neu gestartet werden soll.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: e6c4e48b051f567c98ea679feaa22f995982a899
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382212"
---
# <a name="bdehdcfg-restart"></a>bdehdcfg: neu starten



Informiert das Befehlszeilen Tool bdehdcfg darüber, dass der Computer nach Abschluss der Laufwerks Vorbereitung neu gestartet werden soll. Ein Beispiel für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -restart
```

### <a name="parameters"></a>Parameter

Dieser Befehl erfordert keine zusätzlichen Parameter.

## <a name="remarks"></a>Hinweise

Wenn andere Benutzer auf dem Computer angemeldet sind und der Befehl **quiet** nicht angegeben ist, wird eine Eingabeaufforderung angezeigt, um zu bestätigen, dass der Computer neu gestartet werden muss.

## <a name="BKMK_Examples"></a>Beispiele

Das folgende Beispiel veranschaulicht die Verwendung des Befehls **Restart** .
```
bdehdcfg -target default -restart
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)