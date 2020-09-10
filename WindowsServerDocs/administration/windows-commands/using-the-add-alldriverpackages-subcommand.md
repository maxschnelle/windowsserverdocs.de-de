---
title: Verwenden des Add-AllDriverPackages-Unterbefehls
description: Referenz Artikel für Add-AllDriverPackages, mit dem alle Treiber Pakete, die in einem Ordner gespeichert sind, einem Server hinzugefügt werden.
ms.topic: reference
ms.assetid: ba6641c1-d7e9-43a9-9819-702dad5484ed
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 71b081f8d0617aaa91e75e73705d53ab20661076
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626548"
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
|  FolderPath\<Folder Path>  |                      Gibt den vollständigen Pfad zum Ordner an, der die INF-Dateien für die Treiber Pakete enthält.                      |
|   [/Server:\<Server name>]   | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
|     [/Architecture: {x86      |                                                                 ia64                                                                  |
| [/DriverGroup: \<Group Name> ] |                             Gibt den Namen der Treiber Gruppe an, der die Pakete hinzugefügt werden sollen.                             |

## <a name="examples"></a>Beispiele

Zum Hinzufügen von Treiber Paketen geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /verbose /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers /Architecture:x86
```
```
WDSUTIL /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers\Printers /DriverGroup:Printer Drivers
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Add-wdsdriverpackage](/previous-versions/windows/powershell-scripting/dn283440(v=wps.630))
