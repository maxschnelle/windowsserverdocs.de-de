---
title: GPT
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d6f9029-807f-4420-a336-36669b5361bc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 585e08aac887bc80f5211148f64f94402dd10f09
ms.sourcegitcommit: dffde00fdcee2f0c3eaafae358e98e190a3957a2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2020
ms.locfileid: "76973660"
---
# <a name="gpt"></a>GPT

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Bei einfachen GPT-Datenträgern (GUID-Partitionstabelle) werden die GPT-Attribute der Partition mit dem Fokus zugewiesen.  GPT-Partitions Attribute bietet zusätzliche Informationen zur Verwendung der Partition. Einige Attribute sind spezifisch für die GUID des Partitions Typs.

> [!CAUTION]
> Das Ändern der GPT-Attribute kann dazu führen, dass ihren grundlegenden Datenvolumes keine Laufwerk Buchstaben zugewiesen werden, oder dass die Bereitstellung des Dateisystems verhindert wird. Sie sollten die GPT-Attribute nur dann ändern, wenn Sie ein ursprünglicher Gerätehersteller (OEM) oder IT-Experte sind, der mit GPT-Datenträgern vertraut ist.

## <a name="syntax"></a>Syntax

```
gpt attributes=<n>
```

## <a name="parameters"></a>Parameter

|   Parameter    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Attribute =<n> | Gibt den Wert für das Attribut an, das Sie auf die Partition mit dem Fokus anwenden möchten. Das GPT-Attribut Feld ist ein 64-Bit-Feld, das zwei Unterfelder enthält. Das höhere Feld wird nur im Kontext der Partitions-ID interpretiert, während das untere Feld allen Partitions-IDs gemeinsam ist. Akzeptierte Werte sind:<br /><br />-   **0x0000000000000001**. Gibt an, dass die Partition für den ordnungsgemäßen Betrieb des Computers erforderlich ist.<br />-   **0x8000000000000000**. Gibt an, dass die Partition standardmäßig keinen Laufwerk Buchstaben erhält, wenn der Datenträger auf einen anderen Computer verschoben wird oder wenn der Datenträger zum ersten Mal von einem Computer angezeigt wird.<br />-   **0x4000000000000000**. Blendet das Volume einer Partition aus. Das heißt, die Partition wird vom Mount Manager nicht erkannt.<br />-   **0x2000000000000000**. Gibt an, dass die Partition eine Schatten Kopie einer anderen Partition ist.<br />-   **0x1000000000000000**. Gibt an, dass die Partition schreibgeschützt ist. Dieses Attribut verhindert, dass das Volume in geschrieben wird.<br /><br />Weitere Informationen zu diesen Attributen finden Sie im Abschnitt "Attribute" unter [create_PARTITION_PARAMETERS Struktur](https://go.microsoft.com/fwlink/?LinkId=203812). |

## <a name="remarks"></a>Hinweise

- Die EFI-System Partition enthält nur die Binärdateien, die zum Starten des Betriebssystems erforderlich sind. Dies vereinfacht das Platzieren von OEM-Binärdateien oder Binärdateien, die für ein betriebssystemspezifisch sind, auf anderen Partitionen.
- Eine grundlegende GPT-Partition muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl **Partition auswählen** eine einfache GPT-Partition aus, und verschieben Sie den Fokus darauf.

## <a name="BKMK_examples"></a>Beispiele

  Wenn Sie einen GPT-Datenträger auf einen neuen Computer verschieben und verhindern möchten, dass dieser Computer der Partition mit dem Fokus automatisch einen Laufwerk Buchstaben zuweist, geben Sie Folgendes ein:
  ```
  gpt attributes=0x8000000000000000
  ```
