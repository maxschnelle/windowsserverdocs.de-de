---
title: active
description: Windows-Befehls Thema für **Active** -on-Basis Datenträger markiert die Partition mit dem Fokus als aktiv.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: c926bf9b7a583cf7eaa23166e09e6f0a1599e625
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382849"
---
# <a name="active"></a>active



Auf Basis Datenträgern wird die Partition mit dem Fokus als aktiv markiert.

> [!CAUTION]
> DiskPart überprüft nur, ob die Partition die Betriebssystem-Startdateien enthalten kann. DiskPart überprüft den Inhalt der Partition nicht. Wenn Sie versehentlich eine Partition als aktiv markieren und die Betriebssystem-Startdateien nicht enthalten, wird der Computer möglicherweise nicht gestartet.

## <a name="syntax"></a>Syntax

```
active
```

## <a name="remarks"></a>Hinweise

-   Dadurch wird dem grundlegenden Eingabe-/Ausgabesystem (BIOS) oder der Extensible Firmware Interface (EFI) mitgeteilt, dass die Partition oder das Volume eine gültige Systempartition oder ein System Volume ist.
-   Nur Partitionen können als aktiv gekennzeichnet werden.
-   Eine Partition muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl **Partition auswählen** eine Partition aus, und verschieben Sie den Fokus auf die Partition.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die Partition mit dem Fokus als aktive Partition zu markieren:
```
active
```

#### <a name="additional-references"></a>Weitere Verweise

