---
title: Get-ImageGroup
description: Referenz Thema zu Get-ImageGroup, das Informationen zu einer Abbild Gruppe und den darin abgerufenen Images abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0fc25aca-a529-44ee-bc8e-96bc8affb458
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 30a87085cb935f95a209ffdd78ecf2b9fb45dc15
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719903"
---
# <a name="get-imagegroup"></a>Get-ImageGroup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen zu einer Abbild Gruppe und den darin enthaltenen Bildern ab.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-ImageGroumediaGroup:<Image group name> [/Server:<Server name>] [/detailed]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
mediagroup:<Image group name>|Gibt den Namen der Abbildgruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Detailed|Gibt die Bild Metadaten für jedes Bild zurück. Wenn dieser Parameter nicht verwendet wird, besteht das Standardverhalten darin, nur den Bildnamen, die Beschreibung und den Dateinamen zurückzugeben.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu einer Abbild Gruppe anzuzeigen:
```
wdsutil /Get-ImageGroumediaGroup:ImageGroup1
```
Geben Sie Folgendes ein, um Informationen einschließlich Metadaten anzuzeigen:
```
wdsutil /verbose /Get-ImageGroumediaGroup:ImageGroup1 /Server:MyWDSServer /detailed
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
mithilfe des Befehls "[Add-ImageGroup](using-the-add-imagegroup-command.md)
" mithilfe des Befehls "[Get-allimagegroups](using-the-get-allimagegroups-command.md)
" mit dem Befehl "[Remove-ImageGroup Command](using-the-remove-imagegroup-command.md)
[unter Command: Set-ImageGroup](subcommand-set-imagegroup.md) "
