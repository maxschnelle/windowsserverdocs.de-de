---
title: Mithilfe des Befehls Get-DriverGroup
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 7f82969e03b3474cf39afd2ae5c3ef2f9d4f8b5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847151"
---
# <a name="using-the-get-drivergroup-command"></a>Mithilfe des Befehls Get-DriverGroup

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt Informationen zu den Treibergruppen auf einem Server an.
## <a name="syntax"></a>Syntax
```
wdsutil /Get-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/DriverGroup:<Group Name>|Gibt den Namen der Gruppe "Treiber".|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein.  Wenn ein Servername nicht angegeben ist, wird der lokale Server verwendet.|
|[/Show: {PackageMetaData &#124; Filters &#124; All}]|Zeigt die Metadaten für alle Treiberpakete in der angegebenen Gruppe. **PackageMetaData** zeigt Informationen über alle Filter für die Treibergruppe gewährt wird. **Filter** zeigt die Metadaten für alle Treiberpakete und Filter für die Gruppe an.|
## <a name="BKMK_examples"></a>Beispiele für
Um Informationen über eine Treiberdatei anzuzeigen, geben Sie Folgendes ein:
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Show:PackageMetaData
```
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Server:MyWdsServer /Show:Filters
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Get-AllDriverGroups](using-the-get-alldrivergroups-command.md)
