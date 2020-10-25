---
title: WDSUTIL Add-drivergrouppackage
description: Referenz Artikel für den Befehl "WDSUTIL Add-drivergrouppackage", mit dem einer Treiber Gruppe ein Treiber Paket hinzugefügt wird.
ms.topic: reference
ms.assetid: 7cd323ae-9049-448e-a460-6c7d6462d4c8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4bf7b7c6cae4551e09fa5aa7d0244e5e4f0407e4
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524545"
---
# <a name="wdsutil-add-drivergrouppackage"></a>WDSUTIL Add-drivergrouppackage

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einer Treiber Gruppe ein Treiber Paket hinzu.

## <a name="syntax"></a>Syntax

```
wdsutil /add-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /DriverGroup:`<Groupname>` | Gibt den Namen der neuen Treiber Gruppe an. |
| Servers`<Servername>` | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| /DriverPackage:`<Name>` | Gibt den Namen des Treiber Pakets an, das der Gruppe hinzugefügt werden soll. Sie müssen diese Option angeben, wenn das Treiber Paket nicht anhand des Namens eindeutig identifiziert werden kann. |
| PackageId`<ID>` | Gibt die ID für ein Paket an. Wählen Sie zum Ermitteln der Paket-ID die Treiber Gruppe aus, in der sich das Paket befindet (oder den Knoten **alle Pakete** ), klicken Sie mit der rechten Maustaste auf das Paket, und wählen Sie dann **Eigenschaften**aus. Die Paket-ID ist auf der Registerkarte **Allgemein** aufgeführt, z. b.: **{DD098D20-1850-4FC8-8E35-EA24A1BEFF5E}**. |

## <a name="examples"></a>Beispiele

Zum Hinzufügen eines Treiber Gruppen Pakets geben Sie Folgendes ein:

```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```

```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /DriverPackage:XYZ
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [WDSUTIL-Befehl "Add-drivergroupfilter"](wdsutil-add-drivergroupfilter.md)

- [WDSUTIL-Befehl "Add-drivergrouppackages"](wdsutil-add-drivergrouppackages.md)

- [WDSUTIL-Befehl "Add-drivergroup"](wdsutil-add-drivergroup.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
