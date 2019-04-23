---
title: Verwenden des Add-AllDriverPackages Unterbefehls
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ba6641c1-d7e9-43a9-9819-702dad5484ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c7a9e95ebd36209d5729f81b7eae9e2660b3606
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890691"
---
# <a name="using-the-add-alldriverpackages-subcommand"></a>Verwenden des Add-AllDriverPackages Unterbefehls



Fügt alle Treiberpakete, die in einem Ordner auf einem Server gespeichert sind.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Add-AllDriverPackages /FolderPath:<Folder Path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ "FolderPath":\<Ordnerpfad >|Gibt den vollständigen Pfad zu dem Ordner, der die INF-Dateien für die Treiberpakete enthält.|
|[/ Server:\<Servername >]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.|
|[/ Architecture: {X86 | ia64 | x64}]|Gibt die Architektur für die Treiberpakete hinzufügen. Treiberpakete für andere Architekturen werden ignoriert.|
|[/ DriverGroup:\<Gruppenname >]|Gibt den Namen der Gruppe "Treiber", der die Pakete hinzugefügt werden soll.|

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie einen der folgenden Schritte aus, um Treiberpakete hinzuzufügen:
```
WDSUTIL /verbose /Add-AllDriverPackages /FolderPath:"C:\Temp\Drivers" /Architecture:x86
```
```
WDSUTIL /Add-AllDriverPackages /FolderPath:"C:\Temp\Drivers\Printers" /DriverGroup:"Printer Drivers"
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

[Add-WdsDriverPackage](https://technet.microsoft.com/library/dn283440.aspx)