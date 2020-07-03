---
title: clean
description: Referenz Artikel zum Clean-Befehl DiskPart, mit dem alle Partitionen oder volumeformatierung aus dem Datenträger mit dem Fokus entfernt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9bbe6fd3-e07e-487b-9035-910957a1d326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7a30e1f765959ed60efa662301f95defc21d6587
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929908"
---
# <a name="clean"></a>clean

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt alle Partitionen oder volumeformatierung von der Festplatte mit dem Fokus.

>[!NOTE]
> Eine PowerShell-Version dieses Befehls finden Sie unter [Clear-Disk-Befehl](https://docs.microsoft.com/powershell/module/storage/clear-disk).

## <a name="syntax"></a>Syntax

```
clean [all]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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

- [Befehl "Clear-Disk"](https://docs.microsoft.com/powershell/module/storage/clear-disk)

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
