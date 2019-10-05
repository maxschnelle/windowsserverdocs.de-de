---
title: Verwenden des Remove-ImageGroup-Befehls
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b2c9813-5df2-4272-8449-26f3bb16f82b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 30e4c2c7c5cf2668d62e96d8d2a54dc33e3d2a55
ms.sourcegitcommit: 9855d6b59b1f8722f39ae74ad373ce1530da0ccf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/04/2019
ms.locfileid: "71960954"
---
# <a name="using-the-remove-imagegroup-command"></a>Verwenden des Remove-ImageGroup-Befehls

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

entfernt eine Abbild Gruppe von einem Server.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /remove-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
mediagroup: <Image group name>|Gibt den Namen der zu entfernenden Abbild Gruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="BKMK_examples"></a>Beispiele
Um die Abbild Gruppe zu entfernen, geben Sie eine der folgenden Informationen ein:
```
wdsutil /remove-ImageGroumediaGroup:ImageGroup1
wdsutil /verbose /remove-ImageGroumediaGroup:"My Image Group" /Server:MyWDSServer 
```
#### <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
[Verwenden des Befehls "Add-ImageGroup"](using-the-add-imagegroup-command.md)  
[Verwenden des Befehls Get-allimagegroups](using-the-get-allimagegroups-command.md)  
[Verwenden des Befehls Get-ImageGroup](using-the-get-imagegroup-command.md)  
[Unterbefehl: Set-ImageGroup](subcommand-set-imagegroup.md)  
