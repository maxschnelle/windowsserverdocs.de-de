---
title: WDSUTIL Add-drivergrouppackage
description: Referenz Artikel zu WDSUTIL Add-drivergrouppackage, mit dem einer Treiber Gruppe ein Treiber Paket hinzugefügt wird.
ms.topic: reference
ms.assetid: 7cd323ae-9049-448e-a460-6c7d6462d4c8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9389bbf7421e8c41c32760b8a20d85c4e4b675ea
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730455"
---
# <a name="wdsutil-add-drivergrouppackage"></a>WDSUTIL Add-drivergrouppackage

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
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl "Add-drivergrouppackages"](wdsutil-add-drivergrouppackages.md)
- [WDSUTIL-Befehl "Add-DriverPackage"](wdsutil-add-driverpackage.md)
- [WDSUTIL-Befehl "Add-AllDriverPackages"](wdsutil-add-alldriverpackages.md)
