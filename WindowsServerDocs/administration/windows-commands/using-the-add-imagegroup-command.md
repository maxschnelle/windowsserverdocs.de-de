---
title: Add-ImageGroup
description: Referenz Artikel zu "Add-ImageGroup", mit dem einem Windows-Bereitstellungsdiensteserver eine Image Gruppe hinzugefügt wird.
ms.topic: reference
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 45edd86f62493cadbfbfd6e3f1e9bc86ea5bd9fc
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622209"
---
# <a name="add-imagegroup"></a>Add-ImageGroup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einem Windows-Bereitstellungsdiensteserver eine Abbild Gruppe hinzu.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /add-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
mediagroup:<Image group name>|Gibt den Namen der hinzu zufügenden Abbild Gruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn Sie keinen Servernamen angeben, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Zum Hinzufügen einer Abbild Gruppe geben Sie eine der folgenden Informationen ein:
```
wdsutil /add-ImageGroumediaGroup:ImageGroup2
wdsutil /verbose /add-ImageGroumediaGroup:My Image Group /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-get-allimagegroups-command.md) 
 Get-allimagegroups [Verwenden des Befehls](using-the-get-imagegroup-command.md) 
 Get-ImageGroup [Verwenden des Remove-ImageGroup-Befehls](using-the-remove-imagegroup-command.md) 
 [Unterbefehl: Set-ImageGroup](subcommand-set-imagegroup.md)
