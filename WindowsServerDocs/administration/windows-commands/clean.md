---
title: clean
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: cd5eb2ec1bde4523eb6f0f919e09b9711b2654fb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434318"
---
# <a name="clean"></a>clean

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Der Diskpart-Befehls "bereinigen" entfernt alle Partition oder dem Volume, die vom Datenträger mit dem Fokus formatieren.
## <a name="syntax"></a>Syntax
```
clean [all]
```
## <a name="parameters"></a>Parameter

| Parameter |                                                        Beschreibung                                                        |
|-----------|---------------------------------------------------------------------------------------------------------------------------|
|    all    | Gibt an, dass alle Sektoren auf dem Datenträger 0 ist, wird dadurch werden vollständig alle Daten auf dem Datenträger gelöscht. |

## <a name="remarks"></a>Hinweise
- Bei Datenträgern master Boot Record (MBR) nur die MBR-Partitionierung und ausgeblendeten Sektoreninformationen überschrieben werden.
- Auf Datenträgern für GUID-Partitionstabelle (Gpt) werden die Informationen, einschließlich der Schutz-MBR-Partitionierung überschrieben. Es gibt keine ausgeblendeten Sektoreninformationen.
- Ein Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **select Disk** Befehl aus, wählen Sie einen Datenträger und verschiebt den Fokus auf sie.
  ## <a name="BKMK_examples"></a>Beispiele für
  Um die gesamte Formatierung aus den ausgewählten Datenträger zu entfernen, geben Sie Folgendes ein:
  ```
  clean
  ```

[Clear-Disk](https://technet.microsoft.com/library/hh848661.aspx)
