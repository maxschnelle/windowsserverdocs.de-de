---
title: Get-DriverPackageFile
description: Referenz Artikel zu Get-DriverPackageFile, in dem Informationen zu einem Treiber Paket einschließlich der darin enthaltenen Treiber und Dateien angezeigt werden.
ms.topic: reference
ms.assetid: f01a2c67-7e9c-4aad-b625-383f5a1fca25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5d1990cd307aaf5a378eaf55ac95247fe5b92405
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029658"
---
# <a name="get-driverpackagefile"></a>Get-DriverPackageFile

Zeigt Informationen zu einem Treiber Paket an, einschließlich der darin enthaltenen Treiber und Dateien.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Get-DriverPackageFile /InfFile:<Inf File path> [/Architecture:{x86 | ia64 | x64}] [/Show:{Drivers | Files | All}]
```

### <a name="parameters"></a>Parameter

|         Parameter         |                              Beschreibung                               |
|---------------------------|------------------------------------------------------------------------|
| /InfFile:\<Inf File path> | Gibt den vollständigen Pfad und den Dateinamen der INF-Datei des Treiber Pakets an. |
|    [/Architecture: {x86    |                                  ia64                                  |
|     [/Show: {Drivers      |                                 Dateien                                  |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen zu einer Treiberdatei anzuzeigen:
```
WDSUTIL /Get-DriverPackageFile /InfFile:C:\temp\1394.inf /Architecture:x86
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)