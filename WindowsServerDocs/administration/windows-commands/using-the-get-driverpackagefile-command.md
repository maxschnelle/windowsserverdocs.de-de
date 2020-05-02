---
title: Get-DriverPackageFile
description: Referenz Thema zu Get-DriverPackageFile, in dem Informationen zu einem Treiber Paket einschließlich der darin enthaltenen Treiber und Dateien angezeigt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f01a2c67-7e9c-4aad-b625-383f5a1fca25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 71fc38e31471a1deb9d6be29b04d3cd911be1bd6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719930"
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
| /InfFile:\<INF-Dateipfad> | Gibt den vollständigen Pfad und den Dateinamen der INF-Datei des Treiber Pakets an. |
|    [/Architecture: {x86    |                                  ia64                                  |
|     [/Show: {Drivers      |                                 Dateien                                  |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen zu einer Treiberdatei anzuzeigen:
```
WDSUTIL /Get-DriverPackageFile /InfFile:C:\temp\1394.inf /Architecture:x86
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)