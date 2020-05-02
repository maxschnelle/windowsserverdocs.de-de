---
title: Add-drivergrouppackage
description: Referenz Thema zu "Add-drivergrouppackage", mit dem einer Treiber Gruppe ein Treiber Paket hinzugefügt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7cd323ae-9049-448e-a460-6c7d6462d4c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4baf4f16740e65c432cc09ca24270ab479346ac2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721110"
---
# <a name="add-drivergrouppackage"></a>Add-drivergrouppackage

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einer Treiber Gruppe ein Treiber Paket hinzu.

## <a name="syntax"></a>Syntax
```
wdsutil /add-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```
### <a name="parameters"></a>Parameter

|         Parameter         |                                                                                                                                               BESCHREIBUNG                                                                                                                                               |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /DriverGroup:<Group Name> |                                                                                                                                 Gibt den Namen der Treiber Gruppe an.                                                                                                                                 |
|   Servers<Server name>   |                                                                                  Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                  |
|   /DriverPackage:<Name>   |                                                                      Gibt den Namen des Treiber Pakets an, das der Gruppe hinzugefügt werden soll. Sie müssen diese Option angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann.                                                                       |
|      PackageId<ID>      | Gibt die ID für ein Paket an. Klicken Sie zum Ermitteln der Paket-ID auf die Treiber Gruppe, in der sich das Paket befindet (oder auf den Knoten **alle Pakete** ), klicken Sie mit der rechten Maustaste auf das Paket, und klicken Sie dann auf **Eigenschaften**. Die Paket-ID ist auf der Registerkarte **Allgemein** aufgeführt, z. b.: **{DD098D20-1850-4FC8-8E35-EA24A1BEFF5E}**. |

## <a name="examples"></a>Beispiele
Wenn Sie ein Treiber Paket hinzufügen möchten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /DriverPackage:XYZ
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
mithilfe des Befehls "Add[-drivergrouppackages](using-the-add-drivergrouppackages-command.md)
" mithilfe des Befehls "Add[-DriverPackage](using-the-add-driverpackage-command.md)
"[mit dem Add-AllDriverPackages-Unterbefehl](using-the-add-alldriverpackages-subcommand.md)
