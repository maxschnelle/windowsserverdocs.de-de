---
title: clean
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9bbe6fd3-e07e-487b-9035-910957a1d326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f871ad1d13e06bf0cbb886ba64a52e7a55a9a797
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379322"
---
# <a name="clean"></a>clean

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der "Diskpart Clean"-Befehl entfernt alle Partitionen bzw. volumeformatierung von der Festplatte mit dem Fokus.
## <a name="syntax"></a>Syntax
```
clean [all]
```
## <a name="parameters"></a>Parameter

| Parameter |                                                        Beschreibung                                                        |
|-----------|---------------------------------------------------------------------------------------------------------------------------|
|    all    | Gibt an, dass jeder und jeder Sektor auf dem Datenträger auf NULL festgelegt ist, wodurch alle Daten auf dem Datenträger vollständig gelöscht werden. |

## <a name="remarks"></a>Hinweise
- Auf Master Boot Record (MBR)-Datenträgern werden nur die MBR-Partitionierungs Informationen und die Informationen zu verborgenen Sektoren überschrieben.
- Für GPT-Datenträger (GUID-Partitionstabelle) werden die GPT-Partitionierungs Informationen, einschließlich des schutzmbr, überschrieben. Es sind keine ausgeblendeten Sektorinformationen vorhanden.
- Ein Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.
  ## <a name="BKMK_examples"></a>Beispiele
  Geben Sie Folgendes ein, um die gesamte Formatierung des ausgewählten Datenträgers zu entfernen:
  ```
  clean
  ```

[Clear-Disk](https://technet.microsoft.com/library/hh848661.aspx)
