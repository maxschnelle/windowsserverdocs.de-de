---
title: gpt
description: Referenz Artikel für den GPT-Befehl, der die GPT-Attribute der Partition mit dem Fokus zuweist.
ms.topic: article
ms.assetid: 1d6f9029-807f-4420-a336-36669b5361bc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 561bc4a11580a45452ac71cffddee1c58e48cf86
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888550"
---
# <a name="gpt"></a>gpt

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Bei einfachen GPT-Datenträgern (GUID-Partitionstabelle) weist dieser Befehl die GPT-Attribute der Partition mit dem Fokus zu. GPT-Partitions Attribute bietet zusätzliche Informationen zur Verwendung der Partition. Einige Attribute sind spezifisch für die GUID des Partitions Typs.

Sie müssen eine einfache GPT-Partition auswählen, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem [Befehl Partition auswählen](select-partition.md) eine einfache GPT-Partition aus, und verschieben Sie den Fokus darauf.

> [!CAUTION]
> Das Ändern der GPT-Attribute kann dazu führen, dass ihren grundlegenden Datenvolumes keine Laufwerk Buchstaben zugewiesen werden, oder dass die Bereitstellung des Dateisystems verhindert wird. Es wird dringend empfohlen, die GPT-Attribute nicht zu ändern, es sei denn, Sie sind ein ursprünglicher Gerätehersteller (OEM) oder IT-Experte, der mit GPT-Datenträgern vertraut ist.

## <a name="syntax"></a>Syntax

```
gpt attributes=<n>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Attribute =`<n>` | Gibt den Wert für das Attribut an, das Sie auf die Partition mit dem Fokus anwenden möchten. Das GPT-Attribut Feld ist ein 64-Bit-Feld, das zwei Unterfelder enthält. Das höhere Feld wird nur im Kontext der Partitions-ID interpretiert, während das untere Feld allen Partitions-IDs gemeinsam ist. Akzeptierte Werte sind:<ul><li>**0x0000000000000001** : gibt an, dass die Partition für die ordnungsgemäße Funktion des Computers erforderlich ist.</li><li>**0x8000000000000000** : gibt an, dass die Partition standardmäßig keinen Laufwerk Buchstaben erhält, wenn der Datenträger auf einen anderen Computer verschoben wird oder wenn der Datenträger zum ersten Mal von einem Computer angezeigt wird.</li><li>**0x4000000000000000** : Blendet das Volume einer Partition aus, sodass es vom Mount Manager nicht erkannt wird.</li><li>**0x2000000000000000** : gibt an, dass die Partition eine Schatten Kopie einer anderen Partition ist.</li><li>**0x1000000000000000** : gibt an, dass die Partition schreibgeschützt ist. Dieses Attribut verhindert, dass das Volume in geschrieben wird.</li></ul><p>Weitere Informationen zu diesen Attributen finden Sie im Abschnitt "Attribute" unter [create_PARTITION_PARAMETERS Struktur](/windows/win32/api/vds/ns-vds-create_partition_parameters). |

#### <a name="remarks"></a>Bemerkungen

- Die EFI-System Partition enthält nur die Binärdateien, die zum Starten des Betriebssystems erforderlich sind. Dies vereinfacht das Platzieren von OEM-Binärdateien oder Binärdateien, die für ein betriebssystemspezifisch sind, auf anderen Partitionen.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um zu verhindern, dass der Computer der Partition mit dem Fokus automatisch einen Laufwerk Buchstaben zuweist.

```
gpt attributes=0x8000000000000000
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Partitions Befehl auswählen](select-partition.md)

- [create_PARTITION_PARAMETERS Struktur](/windows/win32/api/vds/ns-vds-create_partition_parameters)
