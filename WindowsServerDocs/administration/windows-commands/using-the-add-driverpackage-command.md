---
title: Add-DriverPackage
description: Windows-Befehls Thema für "Add-DriverPackage", mit dem dem Server ein Treiber Paket hinzugefügt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ac9e8d5-63ec-4ce8-86fc-85d28011050b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2ccdfcddd2f605eccd9cd32fed7b8c6921297fc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832013"
---
# <a name="add-driverpackage"></a>Add-DriverPackage

Fügt dem Server ein Treiber Paket hinzu.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Add-DriverPackage /InfFile:<Inf File path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>] [/Name:<Friendly Name>]
```

### <a name="parameters"></a>Parameter

|          Parameter           |                                                              Beschreibung                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|   InfFile:\<INF-Dateipfad >   |                                           Gibt den vollständigen Pfad der hinzu zufügenden INF-Datei an.                                            |
|    /Server:\<Server Name >    | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
|      /Architecture: {x86      |                                                                 ia64                                                                  |
| [/DriverGroup:\<Gruppen Name >] |                             Gibt den Namen der Treiber Gruppe an, der das Paket hinzugefügt werden soll.                              |
|   [/Name:\<Anzeige Name >]   |                                           Gibt den anzeigen Amen für das Treiber Paket an.                                            |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Wenn Sie ein Treiber Paket hinzufügen möchten, geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /verbose /Add-DriverPackage /InfFile:C:\Temp\Display.inf
```
```
WDSUTIL /Add-DriverPackage /Server:MyWDSServer /InfFile:C:\Temp\Display.inf /Architecture:x86 /DriverGroup:x86Drivers /Name:Display Driver
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

