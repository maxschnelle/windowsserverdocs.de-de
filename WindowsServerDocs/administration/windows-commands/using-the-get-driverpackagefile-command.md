---
title: Mithilfe des Befehls Get-DriverPackageFile
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f01a2c67-7e9c-4aad-b625-383f5a1fca25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 264bdb6d51622e6323be00b44014b86cd9662e61
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440499"
---
# <a name="using-the-get-driverpackagefile-command"></a>Mithilfe des Befehls Get-DriverPackageFile



Zeigt Informationen zu einem Treiberpaket, einschließlich der Treiber und die darin enthaltenen Dateien.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Get-DriverPackageFile /InfFile:<Inf File path> [/Architecture:{x86 | ia64 | x64}] [/Show:{Drivers | Files | All}]
```

## <a name="parameters"></a>Parameter

|         Parameter         |                              Beschreibung                               |
|---------------------------|------------------------------------------------------------------------|
| / INF:\<Pfad der Inf-Datei > | Gibt den vollständigen Pfad und Dateiname den Namen des Pakets INF-Treiberdatei an. |
|    [/ Architecture: {X86    |                                  ia64                                  |
|     [/Show: {Drivers      |                                 Dateien                                  |

## <a name="BKMK_examples"></a>Beispiele für

Um Informationen über eine Treiberdatei anzuzeigen, geben Sie Folgendes ein:
```
WDSUTIL /Get-DriverPackageFile /InfFile:"C:\temp\1394.inf" /Architecture:x86
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)