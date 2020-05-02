---
title: erhalten
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7391c0b60d07cc2eb5a6230b283ac180cc028508
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722342"
---
# <a name="retain"></a>erhalten



Bereitet ein vorhandenes dynamisches einfaches Volume vor, das als Start-oder System Volume verwendet werden soll.

## <a name="syntax"></a>Syntax

```
retain
```

## <a name="remarks"></a>Bemerkungen

-   Auf einem dynamischen Datenträger mit Master Boot Record (MBR) erstellt dieser Befehl einen Partitionseintrag im Master Boot Record.
-   Bei einem dynamischen GPT-Datenträger (GUID-Partitionstabelle) erstellt dieser Befehl einen Partitionseintrag in der GUID-Partitionstabelle.

## <a name="additional-references"></a>Zusätzliche Referenzen

