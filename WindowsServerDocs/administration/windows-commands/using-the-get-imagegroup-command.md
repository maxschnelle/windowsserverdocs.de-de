---
title: Get-ImageGroup
description: Referenz Artikel zu Get-ImageGroup, der Informationen zu einer Abbild Gruppe und den darin abgerufenen Images abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0fc25aca-a529-44ee-bc8e-96bc8affb458
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 32ca965981b02bd951a0cc84160a2c5ea0643ae0
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932213"
---
# <a name="get-imagegroup"></a>Get-ImageGroup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen zu einer Abbild Gruppe und den darin enthaltenen Bildern ab.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-ImageGroumediaGroup:<Image group name> [/Server:<Server name>] [/detailed]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
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
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-add-imagegroup-command.md) 
 "Add-ImageGroup" [Verwenden des Befehls](using-the-get-allimagegroups-command.md) 
 Get-allimagegroups [Verwenden des Remove-ImageGroup-Befehls](using-the-remove-imagegroup-command.md) 
 [Unterbefehl: Set-ImageGroup](subcommand-set-imagegroup.md)
