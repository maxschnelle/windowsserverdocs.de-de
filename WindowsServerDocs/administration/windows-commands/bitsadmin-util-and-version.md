---
title: bitsadmin util and version
description: Referenz Thema für den Befehl BITSAdmin util und Version, der die Version des Bits-diensdienstanweises anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 20c3db6e6fcd5ef3d00287f36c9f9624ab5224dd
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707591"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "BIFS admin util"](bitsadmin-util.md)

- [Bider admin-Befehl](bitsadmin.md)
