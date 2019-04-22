---
title: Mithilfe des Befehls Add-DriverGroup
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a92fe8f-03f9-462a-b99e-f23275259807
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 322a9a671f90bf56f6357289f7727c142a0145cc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825091"
---
# <a name="using-the-add-drivergroup-command"></a>Mithilfe des Befehls Add-DriverGroup

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Fügt eine Treibergruppe auf dem Server.
Beispiele, wie Sie diesen Befehl verwenden können, finden Sie unter [Beispiele](#BKMK_examples).
## <a name="syntax"></a>Syntax
```
wdsutil /add-DriverGroup /DriverGroup:<Group Name>\n\
[/Server:<Server name>] [/Enabled:{Yes | No}] [/Applicability:{Matched | All}] [/Filtertype:<Filter type> /Policy:{Include | Exclude} /Value:<Value> [/Value:<Value> ...]]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/DriverGroup:<Group Name>|Gibt den Namen der neuen Gruppe "Treiber".|
|/ Server:<Server name>|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.|
|/ Aktiviert: {Yes &#124; keine}|Aktiviert oder deaktiviert das Paket.|
|/ Anwendbarkeit: {abgeglichen &#124; alle}|Gibt an, welche Pakete installieren, wenn die Filterkriterien erfüllt sind. **Übereinstimmung** bedeutet, dass nur die Treiberpakete aus, die eine s-Clienthardware entsprechen zu installieren. **Alle** bedeutet, dass alle Pakete an Clients unabhängig von ihrer Hardware zu installieren.|
|/Filtertype:<Filtertype>|Gibt den Typ des Filters, der zur Gruppe hinzuzufügen. Sie können mehrere Filtertypen in einem einzigen Befehl angeben. Jeder Filtertyp muss folgen **setzten** und mindestens eine **-Wert-**. <Filtertype> Dabei kann es sich um eine der folgenden sein:<br /><br />**BiosVendor**<br /><br />**Biosversion**<br /><br />**Chassistype**<br /><br />**Hersteller**<br /><br />**Uuid**<br /><br />**Osversion**<br /><br />**Osedition**<br /><br />**OsLanguage**<br /><br />Informationen zum Abrufen von Werten für allen übrigen Filtertypen finden Sie unter [Treibergruppenfilter%](https://go.microsoft.com/fwlink/?LinkID=155158) (https://go.microsoft.com/fwlink/?LinkID=155158).|
|[/Policy:{Include &#124; Exclude}]|Gibt die Richtlinie für den Filter festgelegt werden soll. Wenn **setzten** nastaven NA hodnotu **Include**, Clientcomputer, die dem Filter entsprechen dürfen in dieser Gruppe die Treiber zu installieren. Wenn **setzten** nastaven NA hodnotu **ausschließen**, und klicken Sie dann Clientcomputer, die dem Filter entsprechen nicht, zum Installieren von Treibern in dieser Gruppe zulässig sind.|
|[Wert:<Value>]|Gibt an, den Client-Wert, der entspricht **/Filtertype**. Sie können mehrere Werte für einen einzelnen Typ angeben. Finden Sie in der folgenden Liste gültiger Werte für bestimmte Arten von Filtern. Die folgenden Attribute sind für **Chassistype**. Informationen dazu, wie Sie die Werte für allen übrigen Filtertypen erhalten, finden Sie unter [Treibergruppenfilter%](https://go.microsoft.com/fwlink/?LinkID=155158) (https://go.microsoft.com/fwlink/?LinkID=155158).<br /><br />**Andere**<br /><br />**UnknownChassis**<br /><br />**Desktop**<br /><br />**LowProfileDesktop**<br /><br />**PizzaBox**<br /><br />**MiniTower**<br /><br />**Tower**<br /><br />**Tragbar**<br /><br />**Laptop**<br /><br />**Notebook**<br /><br />**Handheld**<br /><br />**DockingStation**<br /><br />**AllInOne**<br /><br />**SubNotebook**<br /><br />**SpaceSaving**<br /><br />**LunchBox**<br /><br />**MainSystemChassis**<br /><br />**ExpansionChassis**<br /><br />**SubChassis**<br /><br />**BusExpansionChassis**<br /><br />**PeripheralChassis**<br /><br />**StoraeChassis**<br /><br />**RackmountChassis**<br /><br />**SealedCasecomputer**<br /><br />**MultiSystemChassis**<br /><br />**compactPci**<br /><br />**AdvancedTca**|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie einen der folgenden Schritte aus, zum Hinzufügen einer Treibergruppe:
```
wdsutil /add-DriverGroup /DriverGroup:printerdrivers /Enabled:Yes
```
```
wdsutil /add-DriverGroup /DriverGroup:printerdrivers /Applicability:All /Filtertype:Manufacturer /Policy:Include /Value:Name1 /Filtertype:Chassistype /Policy:Exclude /Value:Tower /Value:MiniTower
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Add-DriverGroupPackage](using-the-add-drivergrouppackage-command.md)
[mithilfe des Befehls Add-DriverGroupPackages](using-the-add-drivergrouppackages-command.md) 
 [ Mithilfe des Befehls Add-DriverGroupFilter](using-the-add-drivergroupfilter-command.md)
