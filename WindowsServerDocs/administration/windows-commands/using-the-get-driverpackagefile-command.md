---
title: Verwenden des Befehls Get-DriverPackageFile
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 21bbe17e56177da5cd2c1bf83c712d256cc794c8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363147"
---
# <a name="using-the-get-driverpackagefile-command"></a>Verwenden des Befehls Get-DriverPackageFile



Zeigt Informationen zu einem Treiber Paket an, einschließlich der darin enthaltenen Treiber und Dateien.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Get-DriverPackageFile /InfFile:<Inf File path> [/Architecture:{x86 | ia64 | x64}] [/Show:{Drivers | Files | All}]
```

## <a name="parameters"></a>Parameter

|         Parameter         |                              Beschreibung                               |
|---------------------------|------------------------------------------------------------------------|
| /InfFile: \<inf-Dateipfad > | Gibt den vollständigen Pfad und den Dateinamen der INF-Datei des Treiber Pakets an. |
|    [/Architecture: {x86    |                                  ia64                                  |
|     [/Show: {Drivers      |                                 Dateien                                  |

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen zu einer Treiberdatei anzuzeigen:
```
WDSUTIL /Get-DriverPackageFile /InfFile:"C:\temp\1394.inf" /Architecture:x86
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)