---
title: Verwenden des Befehls "Add-drivergrouppackage"
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7cd323ae-9049-448e-a460-6c7d6462d4c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eb443b6e6fdc71ccd3340552a23491ef7e61e0b2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363807"
---
# <a name="using-the-add-drivergrouppackage-command"></a>Verwenden des Befehls "Add-drivergrouppackage"

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einer Treiber Gruppe ein Treiber Paket hinzu.
## <a name="syntax"></a>Syntax
```
wdsutil /add-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```
## <a name="parameters"></a>Parameter

|         Parameter         |                                                                                                                                               Beschreibung                                                                                                                                               |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /DriverGroup: <Group Name> |                                                                                                                                 Gibt den Namen der Treiber Gruppe an.                                                                                                                                 |
|   /Server: <Server name>   |                                                                                  Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                  |
|   /DriverPackage: <Name>   |                                                                      Gibt den Namen des Treiber Pakets an, das der Gruppe hinzugefügt werden soll. Sie müssen diese Option angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann.                                                                       |
|      /PackageId: <ID>      | Gibt die ID für ein Paket an. Klicken Sie zum Ermitteln der Paket-ID auf die Treiber Gruppe, in der sich das Paket befindet (oder auf den Knoten **alle Pakete** ), klicken Sie mit der rechten Maustaste auf das Paket, und klicken Sie dann auf **Eigenschaften**. Die Paket-ID ist auf der Registerkarte **Allgemein** aufgeführt, z. b.: **{DD098D20-1850-4FC8-8E35-EA24A1BEFF5E}** . |

## <a name="BKMK_examples"></a>Beispiele
Wenn Sie ein Treiber Paket hinzufügen möchten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /DriverPackage:XYZ
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Add-drivergrouppackages-Befehls](using-the-add-drivergrouppackages-command.md)
 mithilfe[des Add-DriverPackage-Befehls](using-the-add-driverpackage-command.md)
[mit dem Add-AllDriverPackages-Unterbefehl](using-the-add-alldriverpackages-subcommand.md) .
