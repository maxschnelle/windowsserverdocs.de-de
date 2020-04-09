---
title: Aktiv
description: Das Thema Windows-Befehle für **Active**, das auf Basis Datenträgern die Partition mit dem Fokus als aktiv markiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f25da2e-87fc-4392-a7ee-f38d09b7873c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 42f2e0d367344355e8f9a570f37cfbdc5dfc4590
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851373"
---
# <a name="active"></a>Aktiv

Auf Basis Datenträgern wird die Partition mit dem Fokus als aktiv markiert.

> [!CAUTION]
> DiskPart überprüft nur, ob die Partition die Betriebssystem-Startdateien enthalten kann. DiskPart überprüft den Inhalt der Partition nicht. Wenn Sie versehentlich eine Partition als aktiv markieren und die Betriebssystem-Startdateien nicht enthalten, wird der Computer möglicherweise nicht gestartet.

## <a name="syntax"></a>Syntax

```
active
```- 

## Remarks

-   This informs the basic input/output system (BIOS) or Extensible Firmware Interface (EFI) that the partition or volume is a valid system partition or system volume.

-   Only partitions can be marked as active.

-   A partition must be selected for this operation to succeed. Use the **select partition** command to select a partition and shift the focus to it.

## <a name=BKMK_examples></a>Examples

To mark the partition with focus as the active partition, type:

```
Aktiv
```
## Additional References

- [Command-Line Syntax Key](command-line-syntax-key.md)