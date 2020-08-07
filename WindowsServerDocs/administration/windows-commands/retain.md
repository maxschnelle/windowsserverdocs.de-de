---
title: retain
description: Referenz Artikel für * * * *-
ms.topic: article
ms.assetid: eeab0aef-2ba5-441a-a10d-bbef6f0d7e3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9a0205f3b67bd99ca590c7ffc6fbd04b0eefd94f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883645"
---
# <a name="retain"></a>retain



Bereitet ein vorhandenes dynamisches einfaches Volume vor, das als Start-oder System Volume verwendet werden soll.

## <a name="syntax"></a>Syntax

```
retain
```

## <a name="remarks"></a>Bemerkungen

-   Auf einem dynamischen Datenträger mit Master Boot Record (MBR) erstellt dieser Befehl einen Partitionseintrag im Master Boot Record.
-   Bei einem dynamischen GPT-Datenträger (GUID-Partitionstabelle) erstellt dieser Befehl einen Partitionseintrag in der GUID-Partitionstabelle.

## <a name="additional-references"></a>Weitere Verweise

