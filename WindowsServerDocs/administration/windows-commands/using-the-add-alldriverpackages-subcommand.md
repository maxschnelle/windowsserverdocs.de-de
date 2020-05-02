---
title: Verwenden des Add-AllDriverPackages-Unterbefehls
description: Referenz Thema für Add-AllDriverPackages, mit dem alle Treiber Pakete, die in einem Ordner gespeichert sind, einem Server hinzugefügt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ba6641c1-d7e9-43a9-9819-702dad5484ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 31daa8fc3e3304dba5079672ea4619fd085dd74f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721156"
---
# <a name="add-alldriverpackages"></a>Add-AllDriverPackages

Fügt einem Server alle Treiber Pakete hinzu, die in einem Ordner gespeichert sind.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Add-AllDriverPackages /FolderPath:<Folder Path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>]
```

### <a name="parameters"></a>Parameter

|          Parameter           |                                                              BESCHREIBUNG                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|  /FolderPath:\<Ordner Pfad>  |                      Gibt den vollständigen Pfad zum Ordner an, der die INF-Dateien für die Treiber Pakete enthält.                      |
|   [/Server:\<Server Name>]   | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
|     [/Architecture: {x86      |                                                                 ia64                                                                  |
| [/DriverGroup:\<Gruppen Name>] |                             Gibt den Namen der Treiber Gruppe an, der die Pakete hinzugefügt werden sollen.                             |

## <a name="examples"></a>Beispiele

Zum Hinzufügen von Treiber Paketen geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /verbose /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers /Architecture:x86
```
```
WDSUTIL /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers\Printers /DriverGroup:Printer Drivers
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Add-wdsdriverpackage](https://technet.microsoft.com/library/dn283440.aspx)