---
title: retain
description: Referenz Artikel für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 958ee0de7bd69c9391407ec6f4a832e1262746a2
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933072"
---
# <a name="retain"></a>retain



Bereitet ein vorhandenes dynamisches einfaches Volume vor, das als Start-oder System Volume verwendet werden soll.

## <a name="syntax"></a>Syntax

```
retain
```

## <a name="remarks"></a>Hinweise

-   Auf einem dynamischen Datenträger mit Master Boot Record (MBR) erstellt dieser Befehl einen Partitionseintrag im Master Boot Record.
-   Bei einem dynamischen GPT-Datenträger (GUID-Partitionstabelle) erstellt dieser Befehl einen Partitionseintrag in der GUID-Partitionstabelle.

## <a name="additional-references"></a>Weitere Verweise

