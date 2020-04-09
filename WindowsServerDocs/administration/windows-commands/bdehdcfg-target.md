---
title: bdehdcfg-Ziel
description: Windows-Befehls Thema für das **bdehdcfg-Ziel**, das eine Partition für die Verwendung als Systemlaufwerk durch BitLocker und Windows-Wiederherstellung vorbereitet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f761d25d-8349-4ac7-ac46-6bb340a4348f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d0f3e90fbb8725360cf8db335e79721e2328ab3a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851013"
---
# <a name="bdehdcfg-target"></a>bdehdcfg: Ziel

Bereitet eine Partition für die Verwendung als Systemlaufwerk durch BitLocker und Windows-Wiederherstellung vor. Standardmäßig wird diese Partition ohne einen Laufwerkbuchstaben erstellt.

Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge}
```

#### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| default | Gibt an, dass das Befehlszeilentool dem gleichen Prozess wie der BitLocker-Setup-Assistent folgt. |
| unallocated | Erstellt die Systempartition aus dem verfügbaren Speicher auf dem Datenträger. |
| `<DriveLetter>` verkleinern | Reduziert das angegebene Laufwerk um die Speicherplatzmenge, die notwendig ist, um eine aktive Systempartition zu erstellen. Um diesen Befehl zu verwenden, muss das angegebene Laufwerk über mindestens 5 Prozent freien Speicherplatz verfügen. |
| `<DriveLetter>` Merge | Verwendet das angegebene Laufwerk als aktive Systempartition. Das Betriebssystemlaufwerk kann kein Ziel für eine Zusammenführung sein. |

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Im folgenden Beispiel wird die Verwendung des **Ziel** Befehls zum Festlegen eines vorhandenen Laufwerks (P) als Systemlaufwerk dargestellt.

```
bdehdcfg -target P: merge
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bdehdcfg](bdehdcfg.md)