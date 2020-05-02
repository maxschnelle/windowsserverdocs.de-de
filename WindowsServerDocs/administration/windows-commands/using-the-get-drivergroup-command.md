---
title: Get-drivergroup
description: Referenz Thema zu Get-drivergroup, das Informationen zu den Treiber Gruppen auf einem Server anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7cfe10c3-a63f-48e7-bef9-f6b474b4ddbe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4804b699959b4fba2551e84379db97243f093ce7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719953"
---
# <a name="get-drivergroup"></a>Get-drivergroup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu den Treiber Gruppen auf einem Server an.

## <a name="syntax"></a>Syntax
```
wdsutil /Get-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|/DriverGroup:<Group Name>|Gibt den Namen der Treiber Gruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln.  Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|[/Show: {packagemetadata &#124; Filter &#124; all}]|Zeigt die Metadaten für alle Treiber Pakete in der angegebenen Gruppe an. **Packagemetadata** zeigt Informationen zu allen Filtern für die Treiber Gruppe an. **Filter** zeigt die Metadaten für alle Treiber Pakete und Filter für die Gruppe an.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu einer Treiberdatei anzuzeigen:
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Show:PackageMetaData
```
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Server:MyWdsServer /Show:Filters
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mit dem Befehl "Get-alldrivergroups](using-the-get-alldrivergroups-command.md) "
