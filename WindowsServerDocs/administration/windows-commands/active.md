---
title: aktiv
description: Im Referenz Artikel für den aktiven Befehl, der auf Basis Datenträgern Festplatten, wird die Partition mit dem Fokus als aktiv markiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f25da2e-87fc-4392-a7ee-f38d09b7873c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a5df2f67c087be31190c512be0f6b20d8a1d72cb
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924140"
---
# <a name="active"></a>aktiv

Auf Basis Datenträgern wird die Partition mit dem Fokus als aktiv markiert. Nur Partitionen können als aktiv gekennzeichnet werden. Eine Partition muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl **Partition auswählen** eine Partition aus, und verschieben Sie den Fokus auf die Partition.

> [!CAUTION]
> DiskPart informiert das grundlegende Eingabe-/Ausgabesystem (BIOS) oder Extensible Firmware Interface (EFI) nur darüber, dass es sich bei der Partition oder dem Volume um eine gültige Systempartition oder ein System Volume handelt, und kann die Betriebssystem-Startdateien enthalten. DiskPart überprüft den Inhalt der Partition nicht. Wenn Sie versehentlich eine Partition als aktiv markieren und die Betriebssystem-Startdateien nicht enthalten, wird der Computer möglicherweise nicht gestartet.

## <a name="syntax"></a>Syntax

```
active
```

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Partition mit dem Fokus als aktive Partition zu markieren:

```
active
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Partitions Befehl auswählen](select-partition.md)
