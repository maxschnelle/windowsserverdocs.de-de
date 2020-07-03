---
title: bdehdcfg quiet
description: Referenz Artikel für den Befehl bdehdcfg quiet, der bdehdcfg anweist, nicht alle Aktionen und Fehler anzuzeigen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7f75b702-890b-4ff9-805c-edf5cadd8822
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b6a62314109d1c299187d87fba23b8e59669d66
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923458"
---
# <a name="bdehdcfg-quiet"></a>bdehdcfg: Quiet

Informiert das Befehlszeilen Tool bdehdcfg, dass alle Aktionen und Fehler nicht in der Befehlszeilenschnittstelle angezeigt werden. Alle während der Laufwerks Vorbereitung angezeigten Eingabe Aufforderungen für Ja/Nein (Y/N) werden von der Antwort "yes" angenommen. Um einen Fehler anzuzeigen, der während der Laufwerksvorbereitung aufgetreten ist, überprüfen Sie das Systemereignisprotokoll im **Microsoft-Windows-BitLocker-DrivePreparationTool**-Ereignisanbieter.

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge} -quiet
```

#### <a name="parameters"></a>Parameter

Dieser Befehl weist keine zusätzlichen Parameter auf.

## <a name="examples"></a>Beispiele

So verwenden Sie den **quiet** -Befehl:

```
bdehdcfg -target default -quiet
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
