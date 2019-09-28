---
title: Verwenden des Befehls Get-drivergroup
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7cfe10c3-a63f-48e7-bef9-f6b474b4ddbe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7fd8e4dd22e32722bbfe0dcdcfc79168ab7e3b72
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363178"
---
# <a name="using-the-get-drivergroup-command"></a>Verwenden des Befehls Get-drivergroup

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu den Treiber Gruppen auf einem Server an.
## <a name="syntax"></a>Syntax
```
wdsutil /Get-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/DriverGroup: <Group Name>|Gibt den Namen der Treiber Gruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln.  Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|[/Show: {packagemetadata &#124; Filters &#124; all}]|Zeigt die Metadaten für alle Treiber Pakete in der angegebenen Gruppe an. **Packagemetadata** zeigt Informationen zu allen Filtern für die Treiber Gruppe an. **Filter** zeigt die Metadaten für alle Treiber Pakete und Filter für die Gruppe an.|
## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu einer Treiberdatei anzuzeigen:
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Show:PackageMetaData
```
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Server:MyWdsServer /Show:Filters
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Get-alldrivergroups](using-the-get-alldrivergroups-command.md)
