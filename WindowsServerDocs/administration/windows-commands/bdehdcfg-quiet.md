---
title: bdehdcfg quiet
description: 'Windows-Befehls Thema für bdehdcfg quiet: weist bdehdcfg an, nicht alle Aktionen und Fehler anzuzeigen.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f75b702-890b-4ff9-805c-edf5cadd8822
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d59a14e34200e3fa8e18e36e166ef62ceca1afe7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382218"
---
# <a name="bdehdcfg-quiet"></a>bdehdcfg: Quiet



Informiert das Befehlszeilen Tool bdehdcfg, dass alle Aktionen und Fehler nicht in der Befehlszeilenschnittstelle angezeigt werden. Ein Beispiel für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -quiet
```

### <a name="parameters"></a>Parameter

Dieser Befehl erfordert keine zusätzlichen Parameter.

## <a name="remarks"></a>Hinweise

Wenn Ja/Nein (J/N)-Eingabeaufforderungen während der Laufwerksvorbereitung angezeigt wurden, wird eine „Ja“-Antwort angenommen. Um einen Fehler anzuzeigen, der während der Laufwerksvorbereitung aufgetreten ist, überprüfen Sie das Systemereignisprotokoll im **Microsoft-Windows-BitLocker-DrivePreparationTool**-Ereignisanbieter.

## <a name="BKMK_Examples"></a>Beispiele

Im folgenden Beispiel wird die Verwendung des **quiet** -Befehls veranschaulicht.
```
bdehdcfg -target default -quiet
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)