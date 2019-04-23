---
title: Bitsadmin Util und version
description: Windows-Befehle Thema **Bitsadmin Util und Version** -zeigt die Version der BITS-Dienst.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e768ec5ae43fc17c480b9deede698cca01c6291
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882871"
---
# <a name="bitsadmin-util-and-version"></a>Bitsadmin Util und version

Zeigt die Version der BITS-Dienst (z. B. "2.0").

**BITSAdmin 1.5 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Util /Version [/Verbose]
```

## <a name="remarks"></a>Hinweise

Die **ausführlich** Schalter führt die folgenden:
-   Zeigt die Dateiversion für die einzelnen BITS verknüpfte DLLs
-   Überprüft, ob der BITS-Dienst gestartet werden kann
-   Zeigt die BITS-Gruppenrichtlinien-Werte (nur Windows Vista)

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel die Version der BITS-Dienst.
```
C:\>bitsadmin /Util /Version
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)