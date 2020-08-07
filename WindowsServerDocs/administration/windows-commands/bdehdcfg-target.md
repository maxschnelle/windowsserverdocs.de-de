---
title: bdehdcfg target
description: Referenz Artikel für den bdehdcfg-Ziel Befehl, mit dem eine Partition für die Verwendung als Systemlaufwerk durch BitLocker und Windows-Wiederherstellung vorbereitet wird.
ms.topic: article
ms.assetid: f761d25d-8349-4ac7-ac46-6bb340a4348f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a4da764bf25a661c53c27b15cbbee8e4d4ec2981
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895039"
---
# <a name="bdehdcfg-target"></a>bdehdcfg: Ziel

Bereitet eine Partition für die Verwendung als Systemlaufwerk durch BitLocker und Windows-Wiederherstellung vor. Standardmäßig wird diese Partition ohne einen Laufwerkbuchstaben erstellt.

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge}
```

#### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| default | Gibt an, dass das Befehlszeilentool dem gleichen Prozess wie der BitLocker-Setup-Assistent folgt. |
| unallocated | Erstellt die Systempartition aus dem verfügbaren Speicher auf dem Datenträger. |
| `<drive_letter>`Verkleinern | Reduziert das angegebene Laufwerk um die Speicherplatzmenge, die notwendig ist, um eine aktive Systempartition zu erstellen. Um diesen Befehl zu verwenden, muss das angegebene Laufwerk über mindestens 5 Prozent freien Speicherplatz verfügen. |
| `<drive_letter>`Merge | Verwendet das angegebene Laufwerk als aktive Systempartition. Das Betriebssystemlaufwerk kann kein Ziel für eine Zusammenführung sein. |

## <a name="examples"></a>Beispiele

So legen Sie ein vorhandenes Laufwerk (P) als Systemlaufwerk fest:

```
bdehdcfg -target P: merge
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
