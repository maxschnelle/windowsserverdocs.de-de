---
title: Bdehdcfg-Ziel
description: Windows-Befehle Thema Bdehdcfg Ziel - bereitet eine Partition für die Verwendung als Systemlaufwerk von BitLocker und Windows Recovery vor.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f761d25d-8349-4ac7-ac46-6bb340a4348f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8d180974f480b4c40532dab529ad49dcc33540d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881531"
---
# <a name="bdehdcfg-target"></a>Bdehdcfg: Ziel



Bereitet eine Partition für die Verwendung als Systemlaufwerk von BitLocker und Windows-Wiederherstellung. Standardmäßig wird diese Partition ohne einen Laufwerkbuchstaben erstellt. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge}
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|default|Gibt an, dass das Befehlszeilentool dem gleichen Prozess wie der BitLocker-Setup-Assistent folgt.|
|unallocated|Erstellt die Systempartition aus dem verfügbaren Speicher auf dem Datenträger.|
|\<DriveLetter > Verkleinern|Reduziert das angegebene Laufwerk um die Speicherplatzmenge, die notwendig ist, um eine aktive Systempartition zu erstellen. Um diesen Befehl zu verwenden, muss das angegebene Laufwerk über mindestens 5 Prozent freien Speicherplatz verfügen.|
|\<DriveLetter > Merge|Verwendet das angegebene Laufwerk als aktive Systempartition. Das Betriebssystemlaufwerk kann kein Ziel für eine Zusammenführung sein.|

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel zeigt, mit der **Ziel** Befehl aus, um ein vorhandenes Laufwerk (P) als dem Systemlaufwerk festzulegen.
```
bdehdcfg -target P: merge
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)