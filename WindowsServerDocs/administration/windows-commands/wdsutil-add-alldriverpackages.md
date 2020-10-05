---
title: WDSUTIL Add-AllDriverPackages
description: Referenz Artikel zu WDSUTIL Add-AllDriverPackages, mit dem alle Treiber Pakete, die in einem Ordner gespeichert sind, einem Server hinzugefügt werden.
ms.topic: reference
ms.assetid: ba6641c1-d7e9-43a9-9819-702dad5484ed
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d3ec9b3d61c481eacd192ff74e149dbb56134b17
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730480"
---
# <a name="wdsutil-add-alldriverpackages"></a>WDSUTIL Add-AllDriverPackages

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [wsdutil Add-wdsdriverpackage](/previous-versions/windows/powershell-scripting/dn283440(v=wps.630))
