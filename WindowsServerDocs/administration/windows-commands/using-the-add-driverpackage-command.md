---
title: Verwenden des Befehls "Add-DriverPackage"
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ac9e8d5-63ec-4ce8-86fc-85d28011050b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f5370d301f5fec15f4812b3d65588297d179455d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363750"
---
# <a name="using-the-add-driverpackage-command"></a>Verwenden des Befehls "Add-DriverPackage"



Fügt dem Server ein Treiber Paket hinzu.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Add-DriverPackage /InfFile:<Inf File path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>] [/Name:<Friendly Name>]
```

## <a name="parameters"></a>Parameter

|          Parameter           |                                                              Beschreibung                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|   InfFile: \<inf-Dateipfad >   |                                           Gibt den vollständigen Pfad der hinzu zufügenden INF-Datei an.                                            |
|    /Server: \<Server Name >    | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
|      /Architecture: {x86      |                                                                 ia64                                                                  |
| [/DriverGroup: \<gruppenname >] |                             Gibt den Namen der Treiber Gruppe an, der das Paket hinzugefügt werden soll.                              |
|   [/Name: \<anzeige Name >]   |                                           Gibt den anzeigen Amen für das Treiber Paket an.                                            |

## <a name="BKMK_examples"></a>Beispiele

Wenn Sie ein Treiber Paket hinzufügen möchten, geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /verbose /Add-DriverPackage /InfFile:"C:\Temp\Display.inf"
```
```
WDSUTIL /Add-DriverPackage /Server:MyWDSServer /InfFile:"C:\Temp\Display.inf" /Architecture:x86 /DriverGroup:x86Drivers /Name:"Display Driver"
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

