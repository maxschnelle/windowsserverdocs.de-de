---
title: BIFS admin util und Version
description: Windows-Befehls Thema für **BITSAdmin util und Version** -zeigt die Version des Bits-diensdienstanbieter an.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 495ef17bbf6f39f20f6729b64de4b4bec0f9a3c2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380200"
---
# <a name="bitsadmin-util-and-version"></a>BIFS admin util und Version

Zeigt die Version des Bits-Dienstanbieter an (z. b. 2,0).

**Bikadmin 1,5 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Util /Version [/Verbose]
```

## <a name="remarks"></a>Hinweise

Der Schalter " **verbose** " führt Folgendes aus:
-   Zeigt die Dateiversion für jede Bits-bezogene dll an
-   Überprüft, ob der BITS-Dienst gestartet werden kann.
-   Zeigt Bits Gruppenrichtlinie Werte an (nur Windows Vista).

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Version des Bits-Dienstanbieter veranschaulicht.
```
C:\>bitsadmin /Util /Version
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)