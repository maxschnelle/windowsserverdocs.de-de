---
title: Remove-ImageGroup
description: Referenz Artikel zu Remove-ImageGroup, mit dem eine Abbild Gruppe von einem Server entfernt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5b2c9813-5df2-4272-8449-26f3bb16f82b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3d11a24152250786e600332c5eea0a6ffebc4848
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933328"
---
# <a name="using-the-remove-imagegroup-command"></a>Verwenden des Remove-ImageGroup-Befehls

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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
## <a name="examples"></a>Beispiele
Um die Abbild Gruppe zu entfernen, geben Sie eine der folgenden Informationen ein:
```
wdsutil /remove-ImageGroumediaGroup:ImageGroup1
wdsutil /verbose /remove-ImageGroumediaGroup:My Image Group /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-add-imagegroup-command.md) 
 "Add-ImageGroup" [Verwenden des Befehls](using-the-get-allimagegroups-command.md) 
 Get-allimagegroups [Verwenden des Befehls](using-the-get-imagegroup-command.md) 
 Get-ImageGroup [Unterbefehl: Set-ImageGroup](subcommand-set-imagegroup.md)
