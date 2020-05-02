---
title: "\"Get-alldrivergroups\""
description: Referenz Thema zu Get-alldrivergroups, das Informationen zu allen Treiber Gruppen auf einem Server anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f245ba53-f150-41b1-8418-38dcf0410a05
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c4ac3e0c7b05c96383714c3a702cffd6aa8df18a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720888"
---
# <a name="get-alldrivergroups"></a>"Get-alldrivergroups"

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu allen Treiber Gruppen auf einem Server an.

## <a name="syntax"></a>Syntax
```
wdsutil /Get-AllDriverGroups [/Server:<Server name>] [/Show:{PackageMetaData | Filters | All}]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|[/Show: {packagemetadata &#124; Filter &#124; all}]|Zeigt die Metadaten für alle Treiber Pakete in der angegebenen Gruppe an. **Packagemetadata** zeigt Informationen zu allen Filtern für die Treiber Gruppe an. **Filter** zeigt die Metadaten für alle Treiber Pakete und Filter für die Gruppe an.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu einer Treiberdatei anzuzeigen:
```
wdsutil /Get-AllDriverGroups /Server:MyWdsServer /Show:All
```
```
wdsutil /Get-AllDriverGroups [/Show:PackageMetaData]
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mit dem Get-drivergroup-Befehl](using-the-get-drivergroup-command.md)
