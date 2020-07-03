---
title: Get-DriverPackageFile
description: Referenz Artikel zu Get-DriverPackageFile, in dem Informationen zu einem Treiber Paket einschließlich der darin enthaltenen Treiber und Dateien angezeigt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f01a2c67-7e9c-4aad-b625-383f5a1fca25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1daa93cb8976229c4c847390416f9332769c5ff5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932238"
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
|     [/Show: {Drivers      |                                 Files                                  |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen zu einer Treiberdatei anzuzeigen:
```
WDSUTIL /Get-DriverPackageFile /InfFile:C:\temp\1394.inf /Architecture:x86
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)