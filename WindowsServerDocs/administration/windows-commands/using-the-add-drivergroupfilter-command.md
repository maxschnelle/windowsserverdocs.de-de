---
title: Mithilfe des Befehls Add-DriverGroupFilter
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a66c5e68-99ea-4e47-b68d-8109633ae336
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 16962bd87fabd1ee689b962547c2b1aa470283c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817381"
---
# <a name="using-the-add-drivergroupfilter-command"></a>Mithilfe des Befehls Add-DriverGroupFilter



Fügt einen Filter eine Treibergruppe auf einem Server an.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> /Policy:{Include | Exclude} /Value:<Value> [/Value:<Value> ...]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ DriverGroup:\<Gruppenname >|Gibt den Namen der Gruppe "Treiber".|
|[/ Server:\<Servername >]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.|
|/FilterType:\<FilterType>|Gibt den Typ des Filters, zu der Gruppe hinzuzufügen. Sie können mehrere Filtertypen in einem einzigen Befehl angeben. Muss jeden Filtertyp folgen **setzten** und fügen Sie mindestens eine **-Wert-**. \<FilterType > kann **BiosVendor**, **BiosVersion**, **ChassisType**, **Hersteller**, **Uuid**, **"Osversion"**, **OsEdition**, oder **"OSLanguage"**. Informationen dazu, wie Sie die Werte für allen übrigen Filtertypen erhalten, finden Sie unter [Treibergruppenfilter%](https://go.microsoft.com/fwlink/?LinkID=155158) (https://go.microsoft.com/fwlink/?LinkID=155158).|
|[/ Policy: {einschließen | Exclude}]|Wenn **setzten** nastaven NA hodnotu **Include**, Clientcomputer, die dem Filter entsprechen dürfen in dieser Gruppe die Treiber zu installieren. Wenn **setzten** nastaven NA hodnotu **ausschließen**, Clientcomputer, die dem Filter entsprechen dürfen nicht in dieser Gruppe die Treiber zu installieren.|
|[/ Value:\<Wert >]|Gibt an, den Client-Wert, der entspricht **/FilterType**. Sie können mehrere Werte für einen einzelnen Typ angeben. Finden Sie unter der folgenden Liste gültiger Werte für die **ChassisType**. Informationen dazu, wie Sie die Werte für allen übrigen Filtertypen erhalten, finden Sie unter [Treibergruppenfilter%](https://go.microsoft.com/fwlink/?LinkID=155158) (https://go.microsoft.com/fwlink/?LinkID=155158).</br>**Andere**</br>**UnknownChassis**</br>**Desktop**</br>**LowProfileDesktop**</br>**PizzaBox**</br>**MiniTower**</br>**Tower**</br>**Tragbar**</br>**Laptop**</br>**Notebook**</br>**Handheld**</br>**DockingStation**</br>**AllInOne**</br>**SubNotebook**</br>**SpaceSaving**</br>**LunchBox**</br>**MainSystemChassis**</br>**ExpansionChassis**</br>**SubChassis**</br>**BusExpansionChassis**</br>**PeripheralChassis**</br>**StorageChassis**</br>**RackMountChassis**</br>**SealedCaseComputer**</br>**MultiSystemChassis**</br>**CompactPci**</br>**AdvancedTca**|

## <a name="BKMK_examples"></a>Beispiele für

Um eine Treibergruppe einen Filter hinzuzufügen, geben Sie eine der folgenden:
```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /Value:Name2
```
```
WDSUTIL /Add-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /Value:Name1 /FilterType:ChassisType /Policy:Exclude /Value:Tower /Value:MiniTower
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

