---
title: Set-DriverGroup Unterbefehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e4ba9b1c-8c52-4fd5-969b-f7905611b364
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6e645e16a3d78dd91bad98fedbb04896025b0eaf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852701"
---
# <a name="subcommand-set-drivergroup"></a>Subcommand: set-DriverGroup

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Die Eigenschaften einer vorhandenen Treiber-Gruppe wird auf einem Server festgelegt.
## <a name="syntax"></a>Syntax
```
wdsutil /Set-DriverGroup /DriverGroup:<Group Name> [/Server:<Server Name>] [/Name:<New Group Name>] [/Enabled:{Yes | No}] [/Applicability:{Matched | All}]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/DriverGroup:<Group Name>|Gibt den Namen der Gruppe "Treiber".|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn ein Servername nicht angegeben ist, wird der lokale Server verwendet.|
|[/Name:<New Group Name>]|Gibt den neuen Namen für die Treibergruppe gewährt wird.|
|[/ Aktiviert: {Yes &#124; keine}|Aktiviert oder deaktiviert die Treibergruppe gewährt wird.|
|[/ Anwendbarkeit: {abgeglichen &#124; alle}]|Gibt an, welche Pakete installieren, wenn die Filterkriterien erfüllt ist. **Übereinstimmung** bedeutet, dass nur die Treiberpakete aus, die eine s-Clienthardware entsprechen zu installieren. **Alle** bedeutet, dass alle Pakete an Clients unabhängig von ihrer Hardware installieren.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie einen der folgenden Schritte aus, zum Festlegen der Eigenschaften für eine Treibergruppe:
```
wdsutil /Set-DriverGroup /DriverGroup:printerdrivers /Enabled:Yes
```
```
wdsutil /Set-DriverGroup /DriverGroup:printerdrivers /Name:colorprinterdrivers /Applicability:All
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[Unterbefehl: Set-DriverGroupFilter](subcommand-set-drivergroupfilter.md)
