---
title: WDSUTIL Add-AllDriverPackages
description: Referenz Artikel für den Befehl WDSUTIL Add-AllDriverPackages, mit dem alle Treiber Pakete, die in einem Ordner gespeichert sind, einem Server hinzugefügt werden.
ms.topic: reference
ms.assetid: ba6641c1-d7e9-43a9-9819-702dad5484ed
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 07d958fb382f040db34f486a28fed4b924ce45d8
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524655"
---
# <a name="wdsutil-add-alldriverpackages"></a>WDSUTIL Add-AllDriverPackages

Fügt einem Server alle Treiber Pakete hinzu, die in einem Ordner gespeichert sind.

## <a name="syntax"></a>Syntax

```
wdsutil /Add-AllDriverPackages /FolderPath:<folderpath> [/Server:<servername>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<groupname>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| FolderPath`<folderpath>` | Gibt den vollständigen Pfad zum Ordner an, der die INF-Dateien für die Treiber Pakete enthält. |
| [/Server:`<servername>`] | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| [/Architecture: `{x86|ia64|x64}` ] | Gibt den Architektur Typen für das Treiber Paket an. |
| [/DriverGroup: `<groupname>` ] | Gibt den Namen der Treiber Gruppe an, der die Pakete hinzugefügt werden sollen. |

## <a name="examples"></a>Beispiele

Zum Hinzufügen von Treiber Paketen geben Sie Folgendes ein:

```
wdsutil /verbose /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers /Architecture:x86
```

```
wdsutil /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers\Printers /DriverGroup:Printer Drivers
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)

- [Add-wdsdriverpackage](/powershell/module/wds/add-wdsdriverpackage)
