---
title: "\"Get-alldrivergroups\""
description: Windows-Befehls Thema für Get-alldrivergroups, das Informationen zu allen Treiber Gruppen auf einem Server anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f245ba53-f150-41b1-8418-38dcf0410a05
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6112c38ec8e89effe5cdecaa99c6b75becd2e90d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831363"
---
# <a name="get-alldrivergroups"></a>"Get-alldrivergroups"

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu allen Treiber Gruppen auf einem Server an.

## <a name="syntax"></a>Syntax
```
wdsutil /Get-AllDriverGroups [/Server:<Server name>] [/Show:{PackageMetaData | Filters | All}]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|[/Show: {packagemetadata &#124; Filters &#124; all}]|Zeigt die Metadaten für alle Treiber Pakete in der angegebenen Gruppe an. **Packagemetadata** zeigt Informationen zu allen Filtern für die Treiber Gruppe an. **Filter** zeigt die Metadaten für alle Treiber Pakete und Filter für die Gruppe an.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu einer Treiberdatei anzuzeigen:
```
wdsutil /Get-AllDriverGroups /Server:MyWdsServer /Show:All
```
```
wdsutil /Get-AllDriverGroups [/Show:PackageMetaData]
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls "Get-drivergroup](using-the-get-drivergroup-command.md) "
