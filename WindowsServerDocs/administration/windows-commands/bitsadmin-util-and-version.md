---
title: bitsadmin util and version
description: Referenz Artikel für den Befehl BITSAdmin util und Version, der die Version des Bits-diensdienstanweises anzeigt.
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c3490fe4e3eaa217b81287d8a2ed38a6fdb98279
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880792"
---
# <a name="bitsadmin-util-and-version"></a>bitsadmin util and version

Zeigt die Version des Bits-Dienstanbieter an (z. b. 2,0).

> [!NOTE]
> Dieser Befehl wird von Bits 1,5 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /util /version [/verbose]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /verbose | Verwenden Sie diesen Schalter, um die Dateiversion für jede Bits-bezogene dll anzuzeigen und zu überprüfen, ob der BITS-Dienst gestartet werden kann.|

## <a name="examples"></a>Beispiele

, Um die Version des Bits-Dienes anzuzeigen.

```
bitsadmin /util /version
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "BIFS admin util"](bitsadmin-util.md)

- [Bider admin-Befehl](bitsadmin.md)
