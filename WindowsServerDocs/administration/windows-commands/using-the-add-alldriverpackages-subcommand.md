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
ms.openlocfilehash: 3f934d8c65da939fb60c564b375699f411b7c9ac
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440835"
---
# <a name="using-the-add-alldriverpackages-subcommand"></a>Verwenden des Add-AllDriverPackages Unterbefehls



Fügt alle Treiberpakete, die in einem Ordner auf einem Server gespeichert sind.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Add-AllDriverPackages /FolderPath:<Folder Path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>]
```

## <a name="parameters"></a>Parameter

|          Parameter           |                                                              Beschreibung                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|  / "FolderPath":\<Ordnerpfad >  |                      Gibt den vollständigen Pfad zu dem Ordner, der die INF-Dateien für die Treiberpakete enthält.                      |
|   [/ Server:\<Servername >]   | Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet. |
|     [/ Architecture: {X86      |                                                                 ia64                                                                  |
| [/ DriverGroup:\<Gruppenname >] |                             Gibt den Namen der Gruppe "Treiber", der die Pakete hinzugefügt werden soll.                             |

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie einen der folgenden Schritte aus, um Treiberpakete hinzuzufügen:
```
WDSUTIL /verbose /Add-AllDriverPackages /FolderPath:"C:\Temp\Drivers" /Architecture:x86
```
```
WDSUTIL /Add-AllDriverPackages /FolderPath:"C:\Temp\Drivers\Printers" /DriverGroup:"Printer Drivers"
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Add-WdsDriverPackage](https://technet.microsoft.com/library/dn283440.aspx)