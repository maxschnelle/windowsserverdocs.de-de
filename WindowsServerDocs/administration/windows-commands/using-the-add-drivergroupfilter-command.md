---
title: Add-drivergroupfilter
description: Referenz Thema für "Add-drivergroupfilter", mit dem einer Treiber Gruppe auf einem Server ein Filter hinzugefügt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a66c5e68-99ea-4e47-b68d-8109633ae336
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45ed82940e89f4ab760fda4eed640cd62056daf8
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721116"
---
# <a name="add-drivergroupfilter"></a>Add-drivergroupfilter

Fügt einer Treiber Gruppe auf einem Server einen Filter hinzu.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> /Policy:{Include | Exclude} /Value:<Value> [/Value:<Value> ...]
```

### <a name="parameters"></a>Parameter

|         Parameter          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                            BESCHREIBUNG                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /DriverGroup:\<Gruppen Name> |                                                                                                                                                                                                                                                                                                                                                                                                                                                              Gibt den Namen der Treiber Gruppe an.                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|  [/Server:\<Server Name>]  |                                                                                                                                                                                                                                                                                                                                                                                                               Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                                                                                                                                                                                                                                                                                                                               |
| /FilterType:\<FilterType>  |                                                                                                                                                                                                   Gibt den Typ des Filters an, der der Gruppe hinzugefügt werden soll. Sie können mehrere Filtertypen in einem einzelnen Befehl angeben. Auf jeden Filtertyp muss **/Policy** folgen und mindestens ein **/value**enthalten sein. \<Die> "FilterType" kann " **OsLanguage** **biosvendor**", " **Biosversion**", " **chassistype**", " **Hersteller**", " **UUID**", " **OSVersion**", " **Oort dition**" Weitere Informationen zum Abrufen der Werte für alle anderen Filtertypen finden Sie unter [Treiber Gruppen Filter](https://go.microsoft.com/fwlink/?LinkID=155158) (<https://go.microsoft.com/fwlink/?LinkID=155158>).                                                                                                                                                                                                    |
|     [/Policy: {include      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                             Ausschließen}]                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|     [/Value:\<Wert>]      | Gibt den Client Wert an, der **/FilterType**entspricht. Sie können mehrere Werte für einen einzelnen Typ angeben. In der folgenden Liste finden Sie gültige Werte für **chassistype**. Weitere Informationen zum Abrufen der Werte für alle anderen Filtertypen finden Sie unter [Treiber Gruppen Filter](https://go.microsoft.com/fwlink/?LinkID=155158) (<https://go.microsoft.com/fwlink/?LinkID=155158>).</br>**Andere**</br>**Unknownchassis**</br>**Desktop**</br>**Lowprofiledesktop**</br>**Pizzabox**</br>**Minitower**</br>**Kühl**</br>**Tabel**</br>**Laptop**</br>**Notebook**</br>**Gehaltenen**</br>**Dockingstation**</br>**ALLinONE**</br>**Unter Notebook**</br>**Spacesaving**</br>**Lunchbox**</br>**Mainsystemchassis**</br>**Expansions Chassis**</br>**Subchassis**</br>**Busexpansionchassis**</br>**Peripherie Chassis**</br>**Storagechassis**</br>**Rackmountchassis**</br>**Versiegencasecomputer**</br>**Multisystemchassis**</br>**CompactPCI**</br>**AdvancedTCA** |

## <a name="examples"></a>Beispiele

Wenn Sie einer Treiber Gruppe einen Filter hinzufügen möchten, geben Sie einen der folgenden Informationen ein:
```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /Value:Name2
```
```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /FilterType:ChassisType /Policy:Exclude /Value:Tower /Value:MiniTower
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

