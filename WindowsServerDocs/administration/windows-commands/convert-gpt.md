---
title: convert gpt
description: Windows-Befehls Thema für Convert GPT, das einen leeren Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR) in einen Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle) konvertiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b3b1b747-0a7a-4be2-8487-2c4be16ee190
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3c1ffe61245f7752ccc81d21d513fa00acd7b68b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847283"
---
# <a name="convert-gpt"></a>convert gpt

Konvertiert einen leeren Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR) in einen Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle).

Anweisungen zur Verwendung dieses Befehls finden Sie unter [Ändern eines Master Boot Record-Datenträgers in einen Datenträger mit einer GUID-Partitionstabelle](https://go.microsoft.com/fwlink/?LinkId=207049) (https://go.microsoft.com/fwlink/?LinkId=207049).

## <a name="syntax"></a>Syntax

```
convert gpt [noerr]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

> [!IMPORTANT]
> Der Datenträger muss leer sein, damit er in einen GPT-Datenträger konvertiert werden kann. Sichern Sie Ihre Daten, und löschen Sie dann alle Partitionen oder Volumes, bevor Sie den Datenträger umstellen.
> -   Die erforderliche Mindestgröße für die Datenträger Größe für die Konvertierung in GPT beträgt 128 Megabyte.
> -   Ein einfacher MBR-Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Verwenden Sie den Befehl Datenträger **auswählen** , um einen Basis Datenträger auszuwählen und den Fokus darauf zu verschieben.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um eine Basis-CD von MBR-Partitions Stil in GPT-Partitions Stil zu konvertieren:
```
convert gpt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

