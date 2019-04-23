---
title: active
description: Windows-Befehle Thema **active** – auf Basisfestplatten, die Partition mit Fokus als aktiv markiert.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f25da2e-87fc-4392-a7ee-f38d09b7873c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3a039e0200fb84d446739ac7017556b6c302f4af
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868761"
---
# <a name="active"></a>active



Auf Basisdatenträgern markiert die Partition mit Fokus als aktiv.

> [!CAUTION]
> DiskPart überprüft nur, dass die Partition enthalten die Dateien des Betriebssystems starten kann. DiskPart überprüft nicht den Inhalt der Partition. Wenn Sie versehentlich eine Partition als aktiv markieren, und es keine der Dateien des Betriebssystems starten enthält, kann der Computer nicht gestartet werden.

## <a name="syntax"></a>Syntax

```
active
```

## <a name="remarks"></a>Hinweise

-   Dadurch informiert, dass die Partition oder dem Volume einen gültigen Systempartition oder Systemvolume ist die grundlegende e/a-BIOS (System) oder die Extensible Firmware Interface (EFI).
-   Nur Partitionen können als aktiv gekennzeichnet werden.
-   Eine Partition muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **wählen Partition** Befehl aus, um eine Partition auswählen, und verschiebt den Fokus auf sie.

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie Folgendes ein, um die Partition mit dem Fokus als aktive Partition zu markieren:
```
active
```

#### <a name="additional-references"></a>Weitere Verweise

