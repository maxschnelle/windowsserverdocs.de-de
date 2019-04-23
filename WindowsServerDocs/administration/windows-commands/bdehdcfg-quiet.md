---
title: quiet bdehdcfg
description: Windows-Befehle Thema Bdehdcfg Quiet - nennt Bdehdcfg nicht alle Aktionen und Fehler angezeigt.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 0f0d98f6ae76e9bf6357689c97e091766b9645c2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865751"
---
# <a name="bdehdcfg-quiet"></a>Bdehdcfg: quiet



Informiert das Befehlszeilentool "Bdehdcfg", die alle Aktionen und Fehler nicht in der Befehlszeilenschnittstelle angezeigt werden. Ein Beispiel, wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -quiet
```

### <a name="parameters"></a>Parameter

Dieser Befehl akzeptiert keine zusätzlichen Parameter.

## <a name="remarks"></a>Hinweise

Wenn Ja/Nein (J/N)-Eingabeaufforderungen während der Laufwerksvorbereitung angezeigt wurden, wird eine „Ja“-Antwort angenommen. Um einen Fehler anzuzeigen, der während der Laufwerksvorbereitung aufgetreten ist, überprüfen Sie das Systemereignisprotokoll im **Microsoft-Windows-BitLocker-DrivePreparationTool**-Ereignisanbieter.

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel veranschaulicht die Verwendung der **quiet** Befehl.
```
bdehdcfg -target default -quiet
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)