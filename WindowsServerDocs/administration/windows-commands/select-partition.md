---
title: select partition
description: Referenz Artikel für * * * *-
ms.topic: reference
ms.assetid: 25f70083-b8f7-4a8e-9b34-4b3ffbe06670
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ebed1eda02fa2f97516ccd81d89fcabfe21b430c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635487"
---
# <a name="select-partition"></a>select partition

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

wählt die angegebene Partition aus und verschiebt den Fokus darauf. Dieser Befehl kann auch verwendet werden, um die Partition anzuzeigen, die derzeit den Fokus auf dem ausgewählten Datenträger hat.



## <a name="syntax"></a>Syntax

```
select partition=<n>
```

### <a name="parameters"></a>Parameter

|   Parameter    |                                                                                    BESCHREIBUNG                                                                                    |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| spaltet\=<n> | Die Nummer der Partition, die den Fokus erhalten soll. Sie können die Zahlen für alle Partitionen auf dem aktuell ausgewählten Datenträger anzeigen, indem Sie den Befehl **Partition auflisten** in DiskPart verwenden. |

## <a name="remarks"></a>Hinweise

-   Bevor Sie eine Partition auswählen können, müssen Sie zunächst mithilfe des Befehls **Select Disk** (Datenträger auswählen) einen Datenträger auswählen.

-   Wenn keine Partitionsnummer angegeben ist, zeigt dieser Befehl die Partition an, die derzeit den Fokus auf dem ausgewählten Datenträger hat.

-   Wenn ein Volume mit einer entsprechenden Partition ausgewählt ist, wird die Partition automatisch ausgewählt.

-   Wenn eine Partition mit einem entsprechenden Volume ausgewählt wird, wird das Volume automatisch ausgewählt.

## <a name="examples"></a>Beispiele
Wenn Sie den Fokus auf Partition 3 verschieben möchten, geben Sie Folgendes ein:

```
select partitition=3
```

Geben Sie Folgendes ein, um die Partition anzuzeigen, die derzeit den Fokus auf dem ausgewählten Datenträger hat:

```
select partition
```

## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)




