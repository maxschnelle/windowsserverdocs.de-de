---
title: Mithilfe des Befehls Get-AllDriverGroups
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f245ba53-f150-41b1-8418-38dcf0410a05
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 236a2f798fb07ee6eafb9baf9314dbf46a984cdf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874001"
---
# <a name="using-the-get-alldrivergroups-command"></a>Mithilfe des Befehls Get-AllDriverGroups

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt Informationen zu den Treibergruppen auf einem Server an.
## <a name="syntax"></a>Syntax
```
wdsutil /Get-AllDriverGroups [/Server:<Server name>] [/Show:{PackageMetaData | Filters | All}]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn ein Servername nicht angegeben ist, wird der lokale Server verwendet.|
|[/Show: {PackageMetaData &#124; Filters &#124; All}]|Zeigt die Metadaten für alle Treiberpakete in der angegebenen Gruppe. **PackageMetaData** zeigt Informationen über alle Filter für die Treibergruppe gewährt wird. **Filter** zeigt die Metadaten für alle Treiberpakete und Filter für die Gruppe an.|
## <a name="BKMK_examples"></a>Beispiele für
Um Informationen über eine Treiberdatei anzuzeigen, geben Sie Folgendes ein:
```
wdsutil /Get-AllDriverGroups /Server:MyWdsServer /Show:All
```
```
wdsutil /Get-AllDriverGroups [/Show:PackageMetaData]
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Get-DriverGroup](using-the-get-drivergroup-command.md)
