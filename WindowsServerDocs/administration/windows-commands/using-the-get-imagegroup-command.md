---
title: Verwenden des Befehls Get-ImageGroup
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: d6531a3b69840a0a4910b2effdd3e349b76edf2c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363118"
---
# <a name="using-the-get-imagegroup-command"></a>Verwenden des Befehls Get-ImageGroup

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen zu einer Abbild Gruppe und den darin enthaltenen Bildern ab.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-ImageGroumediaGroup:<Image group name> [/Server:<Server name>] [/detailed]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
mediagroup: <Image group name>|Gibt den Namen der Abbildgruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Detailed|Gibt die Bild Metadaten für jedes Bild zurück. Wenn dieser Parameter nicht verwendet wird, besteht das Standardverhalten darin, nur den Bildnamen, die Beschreibung und den Dateinamen zurückzugeben.|
## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu einer Abbild Gruppe anzuzeigen:
```
wdsutil /Get-ImageGroumediaGroup:ImageGroup1
```
Geben Sie Folgendes ein, um Informationen einschließlich Metadaten anzuzeigen:
```
wdsutil /verbose /Get-ImageGroumediaGroup:ImageGroup1 /Server:MyWDSServer /detailed
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls "Add-ImageGroup](using-the-add-imagegroup-command.md)" 
 mithilfe des Befehls "[Get-allimagegroups](using-the-get-allimagegroups-command.md)" 
 mit[dem Befehl Remove-ImageGroup](using-the-remove-imagegroup-command.md)
[Unterbefehl: Set-ImageGroup](subcommand-set-imagegroup.md)
