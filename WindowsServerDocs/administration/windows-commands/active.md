---
title: aktiv
description: Im Referenz Artikel für den aktiven Befehl, der auf Basis Datenträgern Festplatten, wird die Partition mit dem Fokus als aktiv markiert.
ms.topic: reference
ms.assetid: 1f25da2e-87fc-4392-a7ee-f38d09b7873c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6baad8bd60307eeddf7b777f059ab5ba3846e1d4
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029477"
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
