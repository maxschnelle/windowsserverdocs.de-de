---
title: Unterbefehls Satz-drivergroup
description: Referenz Artikel für den Unterbefehl set-drivergroup, der die Eigenschaften einer vorhandenen Treiber Gruppe auf einem Server festlegt.
ms.topic: reference
ms.assetid: e4ba9b1c-8c52-4fd5-969b-f7905611b364
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c4d014933ae4ebc530977325210887d4abf90817
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730125"
---
# <a name="subcommand-set-drivergroup"></a>Unterbefehl: Set-drivergroup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt die Eigenschaften einer vorhandenen Treiber Gruppe auf einem Server fest.

## <a name="syntax"></a>Syntax
```
wdsutil /Set-DriverGroup /DriverGroup:<Group Name> [/Server:<Server Name>] [/Name:<New Group Name>] [/Enabled:{Yes | No}] [/Applicability:{Matched | All}]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|/DriverGroup:<Group Name>|Gibt den Namen der Treiber Gruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|[/Name: <New Group Name> ]|Gibt den neuen Namen für die Treiber Gruppe an.|
|[/Enabled: {yes &#124; No}|Aktiviert oder deaktiviert die Treiber Gruppe.|
|[/Applicability: {abgeglichen &#124; alle}]|Gibt an, welche Pakete installiert werden sollen, wenn die Filterkriterien erfüllt sind. **Übereinstimmende** bedeutet, dass nur die Treiber Pakete installiert werden, die mit einer Client-e- **Alle** bedeutet, dass alle Pakete unabhängig von Ihrer Hardware auf Clients installiert werden.|
## <a name="examples"></a>Beispiele
Um die Eigenschaften für eine Treiber Gruppe festzulegen, geben Sie eine der folgenden Informationen ein:
```
wdsutil /Set-DriverGroup /DriverGroup:printerdrivers /Enabled:Yes
```
```
wdsutil /Set-DriverGroup /DriverGroup:printerdrivers /Name:colorprinterdrivers /Applicability:All
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Unterbefehl: Set-drivergroupfilter](subcommand-set-drivergroupfilter.md)
