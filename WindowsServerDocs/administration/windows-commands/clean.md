---
title: clean
description: Referenz Thema für den "Diskpart Clean"-Befehl, mit dem alle Partitionen oder volumeformatierung aus dem Datenträger mit dem Fokus entfernt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9bbe6fd3-e07e-487b-9035-910957a1d326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45a23919dc07c8c1525808859471fdcb9f9e9403
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82712875"
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

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| all | Gibt an, dass jeder und jeder Sektor auf dem Datenträger auf NULL festgelegt ist, wodurch alle Daten auf dem Datenträger vollständig gelöscht werden. |

#### <a name="remarks"></a>Bemerkungen

- Auf Master Boot Record (MBR)-Datenträgern werden nur die MBR-Partitionierungs Informationen und die Informationen zum verborgenen Sektor überschrieben.

- Für GPT-Datenträger (GUID-Partitionstabelle) werden die GPT-Partitionierungs Informationen, einschließlich des schutzmbr, überschrieben. Es sind keine ausgeblendeten Sektorinformationen vorhanden.

- Ein Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die gesamte Formatierung des ausgewählten Datenträgers zu entfernen:

```
clean
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Befehl "Clear-Disk"](https://docs.microsoft.com/powershell/module/storage/clear-disk)

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
