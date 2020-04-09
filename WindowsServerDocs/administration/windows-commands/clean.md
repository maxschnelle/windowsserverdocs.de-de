---
title: clean
description: Windows-Befehle-Thema für den Befehl "Diskpart Clean", mit dem alle Partitionen bzw. volumeformatierung aus dem Datenträger mit dem Fokus entfernt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9bbe6fd3-e07e-487b-9035-910957a1d326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d573a0480c24a2a622618197dea7dccaeddac271
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847753"
---
# <a name="clean"></a>clean

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der "Diskpart Clean"-Befehl entfernt alle Partitionen bzw. volumeformatierung von der Festplatte mit dem Fokus.

## <a name="syntax"></a>Syntax
```
clean [all]
```
### <a name="parameters"></a>Parameter

| Parameter |                                                        Beschreibung                                                        |
|-----------|---------------------------------------------------------------------------------------------------------------------------|
|    all    | Gibt an, dass jeder und jeder Sektor auf dem Datenträger auf NULL festgelegt ist, wodurch alle Daten auf dem Datenträger vollständig gelöscht werden. |

## <a name="remarks"></a>Hinweise
- Auf Master Boot Record (MBR)-Datenträgern werden nur die MBR-Partitionierungs Informationen und die Informationen zu verborgenen Sektoren überschrieben.
- Für GPT-Datenträger (GUID-Partitionstabelle) werden die GPT-Partitionierungs Informationen, einschließlich des schutzmbr, überschrieben. Es sind keine ausgeblendeten Sektorinformationen vorhanden.
- Ein Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
  Geben Sie Folgendes ein, um die gesamte Formatierung des ausgewählten Datenträgers zu entfernen:
  ```
  clean
  ```

## <a name="additional-references"></a>Weitere Verweise
[Clear-Disk](https://technet.microsoft.com/library/hh848661.aspx)
