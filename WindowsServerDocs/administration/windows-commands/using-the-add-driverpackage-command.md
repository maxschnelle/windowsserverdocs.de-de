---
title: Add-DriverPackage
description: Referenz Artikel für Add-DriverPackage, mit dem dem Server ein Treiber Paket hinzugefügt wird.
ms.topic: article
ms.assetid: 3ac9e8d5-63ec-4ce8-86fc-85d28011050b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd7ba7897006a4db144fc8bd92317fb07a34b55f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881270"
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
|   InfFile:\<Inf File path>   |                                           Gibt den vollständigen Pfad der hinzu zufügenden INF-Datei an.                                            |
|    Servers\<Server name>    | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
|      /Architecture: {x86      |                                                                 ia64                                                                  |
| [/DriverGroup: \<Group Name> ] |                             Gibt den Namen der Treiber Gruppe an, der das Paket hinzugefügt werden soll.                              |
|   [/Name: \<Friendly Name> ]   |                                           Gibt den anzeigen Amen für das Treiber Paket an.                                            |

## <a name="examples"></a>Beispiele

Wenn Sie ein Treiber Paket hinzufügen möchten, geben Sie eine der folgenden Informationen ein:
```
WDSUTIL /verbose /Add-DriverPackage /InfFile:C:\Temp\Display.inf
```
```
WDSUTIL /Add-DriverPackage /Server:MyWDSServer /InfFile:C:\Temp\Display.inf /Architecture:x86 /DriverGroup:x86Drivers /Name:Display Driver
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

