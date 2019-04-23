---
title: Set-DriverGroupFilter Unterbefehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 829ab1f0-4514-421e-9cc0-767b238da69c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 339beda0d6e92c7632cb16566c8db7be5f1079af
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835061"
---
# <a name="subcommand-set-drivergroupfilter"></a>Subcommand: set-DriverGroupFilter



Hinzugefügt oder entfernt eine vorhandene Gruppe Treiberfilter aus einer Treibergruppe.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> [/Policy:{Include | Exclude}] [/AddValue:<Value> [/AddValue:<Value> ...]] [/RemoveValue:<Value> [/RemoveValue:<Value> ...]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ DriverGroup:\<Gruppenname >|Gibt den Namen der Gruppe "Treiber".|
|[/ Server:\<Servername >]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn ein Servername nicht angegeben ist, wird der lokale Server verwendet.|
|/FilterType:\<FilterType>|Gibt den Typ der Gruppe Treiberfilter hinzufügen oder entfernen. Sie können mehrere Filter in einem einzigen Befehl angeben. Für jede **/FilterType**, können Sie hinzufügen oder entfernen Sie mehrere Werte **/RemoveValue** und **/AddValue**. \<FilterType > kann eine der folgenden:</br>**BiosVendor**</br>**BiosVersion**</br>**ChassisType**</br>**Hersteller**</br>**Uuid**</br>**OsVersion**</br>**OsEdition**</br>**OsLanguage**|
|[/ Policy: {einschließen | Exclude}]|Gibt an, die neue Richtlinie für den Filter festgelegt werden soll. Wenn **setzten** nastaven NA hodnotu **Include**, Clientcomputer, die dem Filter entsprechen dürfen in dieser Gruppe die Treiber zu installieren. Wenn **setzten** nastaven NA hodnotu **ausschließen**, und klicken Sie dann den Clientcomputern, die den Filter entsprechen nicht, zum Installieren von Treibern in dieser Gruppe zulässig sind.|
|[/ AddValue:\<Wert >]|Gibt den neuen Client-Wert, um den Filter hinzuzufügen. Sie können mehrere Werte für ein einzelner Filter angeben. Finden Sie in der folgenden Liste die gültigen Attributwerte für **ChassisType**. Informationen dazu, wie Sie die Werte für allen übrigen Filtertypen erhalten, finden Sie unter [Treibergruppenfilter%](https://go.microsoft.com/fwlink/?LinkID=155158) (https://go.microsoft.com/fwlink/?LinkID=155158).</br>**Andere**</br>**UnknownChassis**</br>**Desktop**</br>**LowProfileDesktop**</br>**PizzaBox**</br>**MiniTower**</br>**Tower**</br>**Tragbar**</br>**Laptop**</br>**Notebook**</br>**Handheld**</br>**DockingStation**</br>**AllInOne**</br>**SubNotebook**</br>**SpaceSaving**</br>**LunchBox**</br>**MainSystemChassis**</br>**ExpansionChassis**</br>**SubChassis**</br>**BusExpansionChassis**</br>**PeripheralChassis**</br>**StorageChassis**</br>**RackMountChassis**</br>**SealedCaseComputer**</br>**MultiSystemChassis**</br>**CompactPci**</br>**AdvancedTca**|
|[/ RemoveValue:\<Wert >]|Gibt an, der vorhandenen clientwert, entfernen Sie aus dem Filter wie angegeben mit **/AddValue**.|

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie einen der folgenden Schritte aus, um einen Filter zu entfernen:
```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /AddValue:Name1 /RemoveValue:Name2
```
```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /RemoveValue:Name1 /FilterType:ChassisType /Policy:Exclude /AddValue:Tower /AddValue:MiniTower
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)