---
title: Add-DriverPackage
description: Referenz Thema für "Add-DriverPackage", mit dem dem Server ein Treiber Paket hinzugefügt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ac9e8d5-63ec-4ce8-86fc-85d28011050b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 12d7f7078cf3dde10f834a4d4c7784ecc1d9bdf2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721093"
---
# <a name="add-driverpackage"></a>Add-DriverPackage

Fügt dem Server ein Treiber Paket hinzu.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Add-DriverPackage /InfFile:<Inf File path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>] [/Name:<Friendly Name>]
```

### <a name="parameters"></a>Parameter

|          Parameter           |                                                              BESCHREIBUNG                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|   InfFile:\<INF-Dateipfad>   |                                           Gibt den vollständigen Pfad der hinzu zufügenden INF-Datei an.                                            |
|    /Server:\<Server Name>    | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
|      /Architecture: {x86      |                                                                 ia64                                                                  |
| [/DriverGroup:\<Gruppen Name>] |                             Gibt den Namen der Treiber Gruppe an, der das Paket hinzugefügt werden soll.                              |
|   [/Name:\<Anzeige Name>]   |                                           Gibt den anzeigen Amen für das Treiber Paket an.                                            |

## <a name="examples"></a>Beispiele

Wenn Sie ein Treiber Paket hinzufügen möchten, geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /verbose /Add-DriverPackage /InfFile:C:\Temp\Display.inf
```
```
WDSUTIL /Add-DriverPackage /Server:MyWDSServer /InfFile:C:\Temp\Display.inf /Architecture:x86 /DriverGroup:x86Drivers /Name:Display Driver
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

