---
title: erhalten
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 3b076e12c833645833f53a06476e62bbf44f2690
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384488"
---
# <a name="retain"></a>erhalten



Bereitet ein vorhandenes dynamisches einfaches Volume vor, das als Start-oder System Volume verwendet werden soll.

## <a name="syntax"></a>Syntax

```
retain
```

## <a name="remarks"></a>Hinweise

-   Auf einem dynamischen Datenträger mit Master Boot Record (MBR) erstellt dieser Befehl einen Partitionseintrag im Master Boot Record.
-   Bei einem dynamischen GPT-Datenträger (GUID-Partitionstabelle) erstellt dieser Befehl einen Partitionseintrag in der GUID-Partitionstabelle.

#### <a name="additional-references"></a>Weitere Verweise

