---
title: BIFS admin util und Version
description: Windows-Befehls Thema für BITSAdmin util und Version, das die Version des Bits-diensdienstanbieter anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 087cc1033166ab93e7496caaa7335433cafd6249
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848833"
---
# <a name="bitsadmin-util-and-version"></a>BIFS admin util und Version

Zeigt die Version des Bits-Dienstanbieter an (z. b. 2,0).

**Bikadmin 1,5 und früher**: nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Util /Version [/Verbose]
```

## <a name="remarks"></a>Hinweise

Der Schalter " **verbose** " führt Folgendes aus:
-   Zeigt die Dateiversion für jede Bits-bezogene dll an
-   Überprüft, ob der BITS-Dienst gestartet werden kann.
-   Zeigt Bits Gruppenrichtlinie Werte an (nur Windows Vista).

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Version des Bits-Dienstanbieter veranschaulicht.
```
C:\>bitsadmin /Util /Version
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)