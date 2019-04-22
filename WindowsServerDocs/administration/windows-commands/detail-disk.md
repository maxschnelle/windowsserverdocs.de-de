---
title: Detail-Datenträger
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6b09cf40-8d93-452b-b449-5242e62a4102
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2c7a5063edf3cb2e190e8aec957e1b571c1f15bc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819101"
---
# <a name="detail-disk"></a>Detail-Datenträger



Zeigt die Eigenschaften des ausgewählten Datenträgers und das Volume auf der Festplatte an.

## <a name="syntax"></a>Syntax

```
detail disk
```

## <a name="remarks"></a>Hinweise

-   Ein Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **select Disk** Befehl aus, wählen Sie einen Datenträger und verschiebt den Fokus auf sie.
-   Wenn der ausgewählte Datenträger eine virtuelle Festplatte (VHD), ist **Detail Datenträger** meldet der datenträgerbustyp als virtuelle.

## <a name="BKMK_examples"></a>Beispiele für

Um die Eigenschaften des ausgewählten Datenträgers, und Informationen über die Volumes auf dem Datenträger anzuzeigen, geben Sie Folgendes ein:
```
detail disk
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

