---
title: Unterbefehls Satz-drivergroupfilter
description: Referenz Thema für den Unterbefehl set-drivergroupfilter, mit dem ein vorhandener Treiber Gruppen Filter aus einer Treiber Gruppe hinzugefügt oder daraus entfernt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 829ab1f0-4514-421e-9cc0-767b238da69c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8a8d3567785b54a722b1787c519de7eb0b7a229
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721735"
---
# <a name="subcommand-set-drivergroupfilter"></a>Unterbefehl: Set-drivergroupfilter

Hiermit wird ein vorhandener Treiber Gruppen Filter aus einer Treiber Gruppe hinzugefügt oder daraus entfernt.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> [/Policy:{Include | Exclude}] [/AddValue:<Value> [/AddValue:<Value> ...]] [/RemoveValue:<Value> [/RemoveValue:<Value> ...]]
```

### <a name="parameters"></a>Parameter

|         Parameter          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                               BESCHREIBUNG                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /DriverGroup:\<Gruppen Name> |                                                                                                                                                                                                                                                                                                                                                                                                                                                                 Gibt den Namen der Treiber Gruppe an.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|  [/Server:\<Server Name>]  |                                                                                                                                                                                                                                                                                                                                                                                                                Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| /FilterType:\<FilterType>  |                                                                                                                                                                                                                                                                       Gibt den Typ des Treiber Gruppen Filters an, der hinzugefügt oder entfernt werden soll. Sie können mehrere Filter in einem einzelnen Befehl angeben. Für jede **/FilterType**können Sie mehrere Werte mithilfe von **/RemoveValue** und **/AddValue**hinzufügen oder entfernen. \<Ein Filter Type-> kann eines der folgenden sein:</br>**Biosvendor**</br>**Biosversion**</br>**ChassisType**</br>**Hersteller**</br>**UUID**</br>**OsVersion**</br>**Odition**</br>**OSLanguage**                                                                                                                                                                                                                                                                        |
|     [/Policy: {include      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                Ausschließen}]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|    [/AddValue:\<Wert>]    | Gibt den neuen Client Wert an, der dem Filter hinzugefügt werden soll. Sie können mehrere Werte für einen einzelnen Filtertyp angeben. In der folgenden Liste finden Sie gültige Attributwerte für **chassistype**. Weitere Informationen zum Abrufen der Werte für alle anderen Filtertypen finden Sie unter [Treiber Gruppen Filter](https://go.microsoft.com/fwlink/?LinkID=155158) (<https://go.microsoft.com/fwlink/?LinkID=155158>).</br>**Andere**</br>**Unknownchassis**</br>**Desktop**</br>**Lowprofiledesktop**</br>**Pizzabox**</br>**Minitower**</br>**Kühl**</br>**Tabel**</br>**Laptop**</br>**Notebook**</br>**Gehaltenen**</br>**Dockingstation**</br>**ALLinONE**</br>**Unter Notebook**</br>**Spacesaving**</br>**Lunchbox**</br>**Mainsystemchassis**</br>**Expansions Chassis**</br>**Subchassis**</br>**Busexpansionchassis**</br>**Peripherie Chassis**</br>**Storagechassis**</br>**Rackmountchassis**</br>**Versiegencasecomputer**</br>**Multisystemchassis**</br>**CompactPCI**</br>**AdvancedTCA** |
|  [/RemoveValue:\<Wert>]   |                                                                                                                                                                                                                                                                                                                                                                                                                                     Gibt den vorhandenen Client Wert an, der aus dem Filter entfernt werden soll, wie in **/AddValue**angegeben.                                                                                                                                                                                                                                                                                                                                                                                                                                      |

## <a name="examples"></a>Beispiele

Um einen Filter zu entfernen, geben Sie einen der folgenden Informationen ein:
```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /AddValue:Name1 /RemoveValue:Name2
```
```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /RemoveValue:Name1 /FilterType:ChassisType /Policy:Exclude /AddValue:Tower /AddValue:MiniTower
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)