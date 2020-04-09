---
title: Verwenden des Add-AllDriverPackages-Unterbefehls
description: Windows-Befehls Artikel für Add-AllDriverPackages, mit dem alle Treiber Pakete, die in einem Ordner gespeichert sind, einem Server hinzugefügt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ba6641c1-d7e9-43a9-9819-702dad5484ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc8252339fcae04517c2074c24bbfab44228b779
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832263"
---
# <a name="add-alldriverpackages"></a>Add-AllDriverPackages

Fügt einem Server alle Treiber Pakete hinzu, die in einem Ordner gespeichert sind.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Add-AllDriverPackages /FolderPath:<Folder Path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>]
```

### <a name="parameters"></a>Parameter

|          Parameter           |                                                              Beschreibung                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|  /FolderPath:\<Ordner Pfad >  |                      Gibt den vollständigen Pfad zum Ordner an, der die INF-Dateien für die Treiber Pakete enthält.                      |
|   [/Server:\<Server Name >]   | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
|     [/Architecture: {x86      |                                                                 ia64                                                                  |
| [/DriverGroup:\<Gruppen Name >] |                             Gibt den Namen der Treiber Gruppe an, der die Pakete hinzugefügt werden sollen.                             |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Zum Hinzufügen von Treiber Paketen geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /verbose /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers /Architecture:x86
```
```
WDSUTIL /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers\Printers /DriverGroup:Printer Drivers
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Add-wdsdriverpackage](https://technet.microsoft.com/library/dn283440.aspx)