---
title: Mithilfe des Befehls Get-ImageGroup
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0fc25aca-a529-44ee-bc8e-96bc8affb458
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9dcb76155dc1044730673ed46a53cad57441a246
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862601"
---
# <a name="using-the-get-imagegroup-command"></a>Mithilfe des Befehls Get-ImageGroup

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ruft Informationen zu einer Abbildgruppe enthalten und die Abbilder ab.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-ImageGroumediaGroup:<Image group name> [/Server:<Server name>] [/detailed]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
mediaGroup:<Image group name>|Gibt den Namen der Abbildgruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
|[/detailed]|Die imagemetadaten für jedes Image zurück. Ist dieser Parameter nicht verwenden, ist das Standardverhalten, um nur die Image-Name, Beschreibung und Dateinamen zurückzugeben.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie zum Anzeigen von Informationen zu einer Abbildgruppe enthalten:
```
wdsutil /Get-ImageGroumediaGroup:ImageGroup1
```
Zum Anzeigen von Informationen, einschließlich Metadaten, geben Sie Folgendes ein:
```
wdsutil /verbose /Get-ImageGroumediaGroup:ImageGroup1 /Server:MyWDSServer /detailed
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Add-ImageGroup](using-the-add-imagegroup-command.md)
[mit dem Befehl Get-AllImageGroups](using-the-get-allimagegroups-command.md) 
 [ Indem Sie den Befehl Remove-ImageGroup](using-the-remove-imagegroup-command.md)
[Unterbefehl: Set-ImageGroup](subcommand-set-imagegroup.md)
