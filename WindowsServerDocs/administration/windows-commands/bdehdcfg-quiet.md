---
title: bdehdcfg quiet
description: Windows-Befehls Thema für **bdehdcfg quiet**, das bdehdcfg anweist, nicht alle Aktionen und Fehler anzuzeigen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7f75b702-890b-4ff9-805c-edf5cadd8822
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e9c24d8861476e6c1578af8245236d699b6ef6db
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851043"
---
# <a name="bdehdcfg-quiet"></a>bdehdcfg: Quiet

Informiert das Befehlszeilen Tool bdehdcfg, dass alle Aktionen und Fehler nicht in der Befehlszeilenschnittstelle angezeigt werden. Ein Beispiel für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -quiet
```

#### <a name="parameters"></a>Parameter

Dieser Befehl erfordert keine zusätzlichen Parameter.

## <a name="remarks"></a>Hinweise

Wenn Ja/Nein (J/N)-Eingabeaufforderungen während der Laufwerksvorbereitung angezeigt wurden, wird eine „Ja“-Antwort angenommen. Um einen Fehler anzuzeigen, der während der Laufwerksvorbereitung aufgetreten ist, überprüfen Sie das Systemereignisprotokoll im **Microsoft-Windows-BitLocker-DrivePreparationTool**-Ereignisanbieter.

## <a name="examples"></a><a name="BKMK_Examples"></a>Beispiele

Im folgenden Beispiel wird die Verwendung des **quiet** -Befehls veranschaulicht.

```
bdehdcfg -target default -quiet
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bdehdcfg](bdehdcfg.md)