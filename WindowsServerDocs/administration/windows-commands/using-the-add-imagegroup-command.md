---
title: Mithilfe des Befehls Add-ImageGroup
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 71050bfecdac4933bfe36f40ce09dae626735664
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829901"
---
# <a name="using-the-add-imagegroup-command"></a>Mithilfe des Befehls Add-ImageGroup

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Fügt eine Abbildgruppe auf einem Windows-Bereitstellungsdiensteserver hinzu.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /add-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
mediaGroup:<Image group name>|Gibt den Namen der Abbildgruppe hinzugefügt werden.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn Sie keinen Servernamen angeben, wird der lokale Server verwendet.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie eine der folgenden Schritte aus, zum Hinzufügen einer Abbildgruppe enthalten:
```
wdsutil /add-ImageGroumediaGroup:ImageGroup2
wdsutil /verbose /add-ImageGroumediaGroup:"My Image Group" /Server:MyWDSServer
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Get-AllImageGroups](using-the-get-allimagegroups-command.md)
[mit dem Befehl Get-ImageGroup](using-the-get-imagegroup-command.md) 
 [ Indem Sie den Befehl Remove-ImageGroup](using-the-remove-imagegroup-command.md)
[Unterbefehl: Set-ImageGroup](subcommand-set-imagegroup.md)
