---
title: Add-drivergrouppackage
description: Referenz Artikel zu "Add-drivergrouppackage", mit dem einer Treiber Gruppe ein Treiber Paket hinzugefügt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7cd323ae-9049-448e-a460-6c7d6462d4c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5782fe849669619bf46426ad698866c05007e426
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937210"
---
# <a name="add-drivergrouppackage"></a>Add-drivergrouppackage

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einer Treiber Gruppe ein Treiber Paket hinzu.

## <a name="syntax"></a>Syntax
```
wdsutil /add-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```
### <a name="parameters"></a>Parameter

|         Parameter         |                                                                                                                                               Beschreibung                                                                                                                                               |
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
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls "Add-drivergrouppackages](using-the-add-drivergrouppackages-command.md) 
 " [Verwenden des Befehls](using-the-add-driverpackage-command.md) 
 "Add-DriverPackage" [Verwenden des Add-AllDriverPackages-Unterbefehls](using-the-add-alldriverpackages-subcommand.md)
