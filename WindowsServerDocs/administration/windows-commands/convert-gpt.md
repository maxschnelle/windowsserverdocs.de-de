---
title: convert gpt
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3b1b747-0a7a-4be2-8487-2c4be16ee190
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9a6392cbcff618c642b9d0f168fe555e8be9e759
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379090"
---
# <a name="convert-gpt"></a>convert gpt



Konvertiert einen leeren Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR) in einen Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle).

Anweisungen zur Verwendung dieses Befehls finden Sie unter [Ändern eines Master Boot Record-Datenträgers in einen Datenträger mit einer GUID-Partitionstabelle](https://go.microsoft.com/fwlink/?LinkId=207049) (https://go.microsoft.com/fwlink/?LinkId=207049).

## <a name="syntax"></a>Syntax

```
convert gpt [noerr]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

> [!IMPORTANT]
> Der Datenträger muss leer sein, damit er in einen GPT-Datenträger konvertiert werden kann. Sichern Sie Ihre Daten, und löschen Sie dann alle Partitionen oder Volumes, bevor Sie den Datenträger umstellen.
> -   Die erforderliche Mindestgröße für die Datenträger Größe für die Konvertierung in GPT beträgt 128 Megabyte.
> -   Ein einfacher MBR-Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Verwenden Sie den Befehl Datenträger **auswählen** , um einen Basis Datenträger auszuwählen und den Fokus darauf zu verschieben.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Basis-CD von MBR-Partitions Stil in GPT-Partitions Stil zu konvertieren:
```
convert gpt
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

