---
title: Unterbefehls Satz-drivergroup
description: Windows-Befehls Thema für den Unterbefehl "Set-drivergroup", mit dem die Eigenschaften einer vorhandenen Treiber Gruppe auf einem Server festgelegt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e4ba9b1c-8c52-4fd5-969b-f7905611b364
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c49381dc65f3b2ffc9a04e4fb2699818515a931f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834033"
---
# <a name="subcommand-set-drivergroup"></a>Unterbefehl: Set-drivergroup

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt die Eigenschaften einer vorhandenen Treiber Gruppe auf einem Server fest.

## <a name="syntax"></a>Syntax
```
wdsutil /Set-DriverGroup /DriverGroup:<Group Name> [/Server:<Server Name>] [/Name:<New Group Name>] [/Enabled:{Yes | No}] [/Applicability:{Matched | All}]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/DriverGroup:<Group Name>|Gibt den Namen der Treiber Gruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|[/Name:<New Group Name>]|Gibt den neuen Namen für die Treiber Gruppe an.|
|[/Enabled: {Yes &#124; No}|Aktiviert oder deaktiviert die Treiber Gruppe.|
|[/Applicability: {Matching &#124; all}]|Gibt an, welche Pakete installiert werden sollen, wenn die Filterkriterien erfüllt sind. **Übereinstimmende** bedeutet, dass nur die Treiber Pakete installiert werden, die mit einer Client-e- **Alle** bedeutet, dass alle Pakete unabhängig von Ihrer Hardware auf Clients installiert werden.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Um die Eigenschaften für eine Treiber Gruppe festzulegen, geben Sie eine der folgenden Informationen ein:
```
wdsutil /Set-DriverGroup /DriverGroup:printerdrivers /Enabled:Yes
```
```
wdsutil /Set-DriverGroup /DriverGroup:printerdrivers /Name:colorprinterdrivers /Applicability:All
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Unterbefehl: Set-drivergroupfilter](subcommand-set-drivergroupfilter.md)
