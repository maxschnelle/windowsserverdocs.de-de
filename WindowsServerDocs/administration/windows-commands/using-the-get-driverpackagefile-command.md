---
title: Get-DriverPackageFile
description: Referenz Artikel zu Get-DriverPackageFile, in dem Informationen zu einem Treiber Paket einschließlich der darin enthaltenen Treiber und Dateien angezeigt werden.
ms.topic: reference
ms.assetid: f01a2c67-7e9c-4aad-b625-383f5a1fca25
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9ab52e1040651398d4789ea51ef9b6dc40dc6d54
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624620"
---
# <a name="get-driverpackagefile"></a>Get-DriverPackageFile

Zeigt Informationen zu einem Treiber Paket an, einschließlich der darin enthaltenen Treiber und Dateien.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Get-DriverPackageFile /InfFile:<Inf File path> [/Architecture:{x86 | ia64 | x64}] [/Show:{Drivers | Files | All}]
```

### <a name="parameters"></a>Parameter

|         Parameter         |                              BESCHREIBUNG                               |
|---------------------------|------------------------------------------------------------------------|
| /InfFile:\<Inf File path> | Gibt den vollständigen Pfad und den Dateinamen der INF-Datei des Treiber Pakets an. |
|    [/Architecture: {x86    |                                  ia64                                  |
|     [/Show: {Drivers      |                                 Files                                  |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen zu einer Treiberdatei anzuzeigen:
```
WDSUTIL /Get-DriverPackageFile /InfFile:C:\temp\1394.inf /Architecture:x86
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)