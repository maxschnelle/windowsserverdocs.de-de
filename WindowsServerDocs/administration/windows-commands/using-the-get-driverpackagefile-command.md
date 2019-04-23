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
ms.openlocfilehash: ed9518fae07745502d01dc0084b7443a1332db83
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859801"
---
# <a name="using-the-get-driverpackagefile-command"></a>Mithilfe des Befehls Get-DriverPackageFile



Zeigt Informationen zu einem Treiberpaket, einschließlich der Treiber und die darin enthaltenen Dateien.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Get-DriverPackageFile /InfFile:<Inf File path> [/Architecture:{x86 | ia64 | x64}] [/Show:{Drivers | Files | All}]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ INF:\<Pfad der Inf-Datei >|Gibt den vollständigen Pfad und Dateiname den Namen des Pakets INF-Treiberdatei an.|
|[/ Architecture: {X86 | ia64 | x64}]|Gibt die Architektur des Treiberpakets.|
|[/Show: {Drivers | Dateien | All}]|Gibt an, die Paketinformationen angezeigt. Wenn **/anzeigen** nicht angegeben ist, wird standardmäßig nur den Treiber Paketmetadaten zurückgegeben werden. **Treiber** zeigt die Liste der Treiber in das Paket. **Dateien** zeigt die Liste der Dateien im Paket. **Alle** zeigt Dateien und Treiber.|

## <a name="BKMK_examples"></a>Beispiele für

Um Informationen über eine Treiberdatei anzuzeigen, geben Sie Folgendes ein:
```
WDSUTIL /Get-DriverPackageFile /InfFile:"C:\temp\1394.inf" /Architecture:x86
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)