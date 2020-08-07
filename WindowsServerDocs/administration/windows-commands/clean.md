---
title: clean
description: Referenz Artikel zum Clean-Befehl DiskPart, mit dem alle Partitionen oder volumeformatierung aus dem Datenträger mit dem Fokus entfernt werden.
ms.topic: article
ms.assetid: 9bbe6fd3-e07e-487b-9035-910957a1d326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9a8ab6d0b245862fbb935945b76f380b7163d2a3
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880211"
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

#### <a name="remarks"></a>Bemerkungen

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
