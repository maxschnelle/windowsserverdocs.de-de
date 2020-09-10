---
title: aktiv
description: Im Referenz Artikel für den aktiven Befehl, der auf Basis Datenträgern Festplatten, wird die Partition mit dem Fokus als aktiv markiert.
ms.topic: reference
ms.assetid: 1f25da2e-87fc-4392-a7ee-f38d09b7873c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8c8a90b2341bd74cf37c1431987d0d47403e1de6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633598"
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
