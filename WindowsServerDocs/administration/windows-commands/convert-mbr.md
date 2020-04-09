---
title: MBR konvertieren
description: Windows-Befehls Artikel zum Konvertieren von MBR, der einen leeren Basis Datenträger mit dem Partitions Stil der GUID-Partitionstabelle (GPT) in einen Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR) konvertiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a635a4c0-af73-4330-b021-51d483424537
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eeaf79a380fb5f1074d2bbef004537804caa0d8d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847203"
---
# <a name="convert-mbr"></a>MBR konvertieren

Konvertiert einen leeren Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle) in einen Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR).

> [!IMPORTANT]
> Der Datenträger muss leer sein, damit er in einen MBR-Datenträger konvertiert werden kann. Sichern Sie Ihre Daten, und löschen Sie dann alle Partitionen oder Volumes, bevor Sie den Datenträger umstellen.

Anweisungen zur Verwendung dieses Befehls finden Sie unter [Ändern eines Datenträgers der GUID-Partitionstabelle in einen Master Boot Record-Daten](https://go.microsoft.com/fwlink/?LinkId=207050) Träger (https://go.microsoft.com/fwlink/?LinkId=207050).

## <a name="syntax"></a>Syntax

```
convert mbr [noerr]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

-   Ein Basis Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Verwenden Sie den Befehl Datenträger **auswählen** , um einen Basis Datenträger auszuwählen und den Fokus darauf zu verschieben.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Zum Konvertieren eines Basis Datenträgers aus dem GPT-Partitions Stil in den MBR-Partitions Stil geben Sie >:
```
convert mbr
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

