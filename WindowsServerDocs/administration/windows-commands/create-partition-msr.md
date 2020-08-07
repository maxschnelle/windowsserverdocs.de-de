---
title: create partition msr
description: Referenz Artikel zu CREATE Partition MSR, mit dem eine Microsoft Reserved-Partition (MSR) auf einem GPT-Datenträger (GUID-Partitionstabelle) erstellt wird.
ms.topic: article
ms.assetid: 04fba033-23cb-4521-bd5d-db96131f2e73
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b697aa278849e2cd084ef7e9378b7997032a820c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879880"
---
# <a name="create-partition-msr"></a>create partition msr

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine reservierte Microsoft-Partition (MSR) auf einem GPT-Datenträger (GUID-Partitionstabelle). Auf jedem GPT-Datenträger ist eine reservierte Microsoft-Partition erforderlich. Die Größe dieser Partition hängt von der Gesamtgröße des GPT-Datenträgers ab. Der GPT-Datenträger muss mindestens 32 MB groß sein, um eine reservierte Microsoft-Partition zu erstellen.

> [!IMPORTANT]
> Gehen Sie bei der Verwendung dieses Befehls sehr vorsichtig vor. Da GPT-Datenträger ein bestimmtes Partitionslayout erfordern, kann das Erstellen von reservierten Microsoft-Partitionen dazu führen, dass der Datenträger nicht mehr lesbar ist.
>
> Ein einfacher GPT-Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Sie müssen den Befehl "Datenträger [auswählen](select-disk.md) " verwenden, um einen einfachen GPT-Datenträger auszuwählen und den Fokus darauf zu verschieben.

## <a name="syntax"></a>Syntax

```
create partition msr [size=<n>] [offset=<n>] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Größe =`<n>` | Die Größe der Partition in Megabyte (MB). Die Partition ist mindestens so lang wie die Zahl, die durch angegeben wird `<n>` . Wenn keine Größe angegeben wird, wird die Partition so lange fortgesetzt, bis in der aktuellen Region kein freier Speicherplatz mehr verfügbar ist. |
| Offset =`<n>` | Gibt den Offset in Kilobyte (KB) an, bei dem die Partition erstellt wird. Der Offset wird aufgerundet, um alle verwendeten Sektorgrößen vollständig auszufüllen. Wenn kein Offset angegeben wird, wird die Partition in den ersten Datenträger Block eingefügt, der groß genug ist, um Sie zu speichern. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

#### <a name="remarks"></a>Bemerkungen

- Auf GPT-Datenträgern, die zum Starten des Windows-Betriebssystems verwendet werden, ist die Systempartition des Extensible Firmware Interface (EFI) die erste Partition auf dem Datenträger, gefolgt von der reservierten Microsoft-Partition. GPT-Datenträger, die nur für die Datenspeicherung verwendet werden, verfügen über keine EFI-Systempartition. in diesem Fall ist die reservierte Microsoft-Partition die erste Partition.

- Von Windows werden keine reservierten Partitionen von Microsoft einbinden. Sie können keine Daten auf den Daten speichern, und Sie können Sie nicht löschen.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine reservierte Microsoft-Partition mit einer Größe von 1000 Megabyte zu erstellen:

```
create partition msr size=1000
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Create-Befehl](create.md)

- [select disk](select-disk.md)
