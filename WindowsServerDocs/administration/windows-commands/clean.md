---
title: clean
description: Referenz Artikel zum Clean-Befehl DiskPart, mit dem alle Partitionen oder volumeformatierung aus dem Datenträger mit dem Fokus entfernt werden.
ms.topic: reference
ms.assetid: 9bbe6fd3-e07e-487b-9035-910957a1d326
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 82026520c456c76823993d34a4fb09bcd4b79808
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89629655"
---
# <a name="clean"></a>clean

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt alle Partitionen oder volumeformatierung von der Festplatte mit dem Fokus.

>[!NOTE]
> Eine PowerShell-Version dieses Befehls finden Sie unter [Clear-Disk-Befehl](/powershell/module/storage/clear-disk).

## <a name="syntax"></a>Syntax

```
clean [all]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| alle | Gibt an, dass jeder und jeder Sektor auf dem Datenträger auf NULL festgelegt ist, wodurch alle Daten auf dem Datenträger vollständig gelöscht werden. |

#### <a name="remarks"></a>Hinweise

- Auf Master Boot Record (MBR)-Datenträgern werden nur die MBR-Partitionierungs Informationen und die Informationen zum verborgenen Sektor überschrieben.

- Für GPT-Datenträger (GUID-Partitionstabelle) werden die GPT-Partitionierungs Informationen, einschließlich des schutzmbr, überschrieben. Es sind keine ausgeblendeten Sektorinformationen vorhanden.

- Ein Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die gesamte Formatierung des ausgewählten Datenträgers zu entfernen:

```
clean
```

## <a name="additional-references"></a>Weitere Verweise

- [Befehl "Clear-Disk"](/powershell/module/storage/clear-disk)

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
