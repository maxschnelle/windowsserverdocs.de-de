---
title: Beibehalten
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b437e9f0c8d671e4378311d450aa0ac7639219f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852171"
---
# <a name="retain"></a>Beibehalten



Bereitet eine vorhandene dynamische Volumes als ein Start verwendet werden soll oder Systemvolume vor.

## <a name="syntax"></a>Syntax

```
retain
```

## <a name="remarks"></a>Hinweise

-   Auf einem master Boot Record (MBR) dynamischen Datenträger erstellt dieser Befehl einen Partitionseintrag in der master Boot Record.
-   Auf einem Datenträger GUID-Partitionstabelle (GPT) dynamische erstellt dieser Befehl einen Partitionseintrag in der GUID-Partitionstabelle.

#### <a name="additional-references"></a>Weitere Verweise

