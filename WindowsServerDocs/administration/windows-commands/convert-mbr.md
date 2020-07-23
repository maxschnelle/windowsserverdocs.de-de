---
title: convert mbr
description: Referenz Artikel zum Convert MBR-Befehl, der einen leeren Basis Datenträger mit dem Partitions Stil der GUID-Partitionstabelle (GPT) in einen Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR) konvertiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a635a4c0-af73-4330-b021-51d483424537
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 784521c99e3fc0cf8d372f95424af785636a0687
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958512"
---
# <a name="convert-mbr"></a>convert mbr

Konvertiert einen leeren Basis Datenträger mit dem GPT-Partitions Stil (GUID-Partitionstabelle) in einen Basis Datenträger mit dem Partitions Stil Master Boot Record (MBR). Ein Basis Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Verwenden Sie den Befehl Datenträger [auswählen](select-disk.md) , um einen Basis Datenträger auszuwählen und den Fokus darauf zu verschieben.

> [!IMPORTANT]
> Der Datenträger muss leer sein, um ihn in einen Basis Datenträger zu konvertieren. Sichern Sie Ihre Daten, und löschen Sie dann alle Partitionen oder Volumes, bevor Sie den Datenträger umstellen.

> [!NOTE]
> Anweisungen zur Verwendung dieses Befehls finden Sie unter [Ändern eines Datenträgers der GUID-Partitionstabelle in einen Master Boot Record-Daten](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc725797(v=ws.11))Träger.

## <a name="syntax"></a>Syntax

```
convert mbr [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Zum Konvertieren eines Basis Datenträgers aus dem GPT-Partitions Stil in den MBR-Partitions Stil geben Sie>:

```
convert mbr
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Convert-Befehl](convert.md)
