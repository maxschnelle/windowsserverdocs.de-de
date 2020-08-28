---
title: bdehdcfg quiet
description: Referenz Artikel für den Befehl bdehdcfg quiet, der bdehdcfg anweist, nicht alle Aktionen und Fehler anzuzeigen.
ms.topic: reference
ms.assetid: 7f75b702-890b-4ff9-805c-edf5cadd8822
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 842788b4413cda828d208e8e7fbbeed28d7a72be
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031528"
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
