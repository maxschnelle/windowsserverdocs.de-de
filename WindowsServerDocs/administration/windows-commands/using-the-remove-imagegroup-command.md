---
title: Remove-ImageGroup
description: Windows-Befehls Thema für Remove-ImageGroup, das eine Abbild Gruppe von einem Server entfernt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5b2c9813-5df2-4272-8449-26f3bb16f82b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d8406959037a958ea6d61b8e8145317635955e6d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830353"
---
# <a name="using-the-remove-imagegroup-command"></a>Verwenden des Remove-ImageGroup-Befehls

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt eine Abbild Gruppe von einem Server.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /remove-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
mediagroup:<Image group name>|Gibt den Namen der zu entfernenden Abbild Gruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Um die Abbild Gruppe zu entfernen, geben Sie eine der folgenden Informationen ein:
```
wdsutil /remove-ImageGroumediaGroup:ImageGroup1
wdsutil /verbose /remove-ImageGroumediaGroup:My Image Group /Server:MyWDSServer 
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
[Verwenden des Befehls "Add-ImageGroup"](using-the-add-imagegroup-command.md)  
[Verwenden des Befehls Get-allimagegroups](using-the-get-allimagegroups-command.md)  
[Verwenden des Befehls Get-ImageGroup](using-the-get-imagegroup-command.md)  
[Unterbefehl: Set-ImageGroup](subcommand-set-imagegroup.md)  
