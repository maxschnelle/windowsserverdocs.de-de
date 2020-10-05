---
title: WDSUTIL Get-drivergroup
description: Referenz Artikel zu "WDSUTIL Get-drivergroup", der Informationen zu den Treiber Gruppen auf einem Server anzeigt.
ms.topic: reference
ms.assetid: 7cfe10c3-a63f-48e7-bef9-f6b474b4ddbe
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ec801255bcd71ca0fb4a38f61f33faa4ae4f5dc4
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730278"
---
# <a name="wdsutil-get-drivergroup"></a>WDSUTIL Get-drivergroup

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
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl "Get-alldrivergroups"](wdsutil-get-alldrivergroups.md)
