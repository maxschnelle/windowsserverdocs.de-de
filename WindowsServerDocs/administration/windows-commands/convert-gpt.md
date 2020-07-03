---
title: convert gpt
description: Referenz Artikel zum Convert GPT-Befehl, der einen leeren Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR) in einen Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle) konvertiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b3b1b747-0a7a-4be2-8487-2c4be16ee190
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d8025e897a8ce7083b938e984f9a11b6c32ed312
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928957"
---
# <a name="convert-gpt"></a>convert gpt

Konvertiert einen leeren Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR) in einen Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle). Ein einfacher MBR-Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Verwenden Sie den Befehl Datenträger [auswählen](select-disk.md) , um einen Basis Datenträger auszuwählen und den Fokus darauf zu verschieben.

> [!IMPORTANT]
> Der Datenträger muss leer sein, um ihn in einen Basis Datenträger zu konvertieren. Sichern Sie Ihre Daten, und löschen Sie dann alle Partitionen oder Volumes, bevor Sie den Datenträger umstellen. Die erforderliche Mindestgröße für die Datenträger Größe für die Konvertierung in GPT beträgt 128 Megabyte.

> [!NOTE]
> Anweisungen zur Verwendung dieses Befehls finden Sie unter [Ändern eines Master Boot Record-Datenträgers in einen Datenträger mit einer GUID-Partitionstabelle](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc725671(v=ws.11)).

## <a name="syntax"></a>Syntax

```
convert gpt [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Basis-CD von MBR-Partitions Stil in GPT-Partitions Stil zu konvertieren:

```
convert gpt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Convert-Befehl](convert.md)
