---
title: BIFS admin util und Version
description: Windows-Befehls Thema für **BITSAdmin util und Version**, das die Version des Bits-diensdienstanbieter anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2c2518eb7a8f15d9a592ed9a77dd67a6f8d8afac
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122474"
---
# <a name="bitsadmin-util-and-version"></a>BIFS admin util und Version

Zeigt die Version des Bits-Dienstanbieter an (z. b. 2,0).

> [!NOTE]
> Dieser Befehl wird von Bits 1,5 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /util /version [/verbose]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /verbose | Verwenden Sie diesen Schalter, um die Dateiversion für jede Bits-bezogene dll anzuzeigen und zu überprüfen, ob der BITS-Dienst gestartet werden kann.|

## <a name="examples"></a>Beispiele

Im folgenden Beispiel wird die Version des Bits-Dienstanbieter veranschaulicht.

```
C:\>bitsadmin /util /version
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)