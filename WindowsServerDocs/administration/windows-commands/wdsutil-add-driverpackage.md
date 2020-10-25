---
title: Add-DriverPackage
description: Referenz Artikel für den Befehl "Add-DriverPackage", mit dem dem Server ein Treiber Paket hinzugefügt wird.
ms.topic: reference
ms.assetid: 3ac9e8d5-63ec-4ce8-86fc-85d28011050b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c85279cc160ca12b52f4cf7225d0ac41700973bc
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524524"
---
# <a name="add-driverpackage"></a>Add-DriverPackage

Fügt dem Server ein Treiber Paket hinzu.

## <a name="syntax"></a>Syntax

```
wdsutil /Add-DriverPackage /InfFile:<Inf File path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>] [/Name:<Friendly Name>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /InfFile:`<InfFilepath>` | Gibt den vollständigen Pfad der hinzu zufügenden INF-Datei an. |
| [/Server:`<Servername>`] | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| [/Architecture: `{x86 | ia64 | x64}` ] | Gibt den Architektur Typen für das Treiber Paket an. |
| [/DriverGroup: `<groupname>` ] | Gibt den Namen der Treiber Gruppe an, der die Pakete hinzugefügt werden sollen. |
| [/Name: `<friendlyname>` ] | Gibt den anzeigen Amen für das Treiber Paket an. |

## <a name="examples"></a>Beispiele

Wenn Sie ein Treiber Paket hinzufügen möchten, geben Sie Folgendes ein:

```
wdsutil /verbose /Add-DriverPackage /InfFile:C:\Temp\Display.inf
```

```
wdsutil /Add-DriverPackage /Server:MyWDSServer /InfFile:C:\Temp\Display.inf /Architecture:x86 /DriverGroup:x86Drivers /Name:Display Driver
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [WDSUTIL-Befehl "Add-drivergrouppackage"](wdsutil-add-drivergrouppackage.md)

- [WDSUTIL-Befehl "Add-AllDriverPackages"](wdsutil-add-alldriverpackages.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
