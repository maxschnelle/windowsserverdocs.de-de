---
title: Get-ImageGroup
description: Windows-Befehls Thema für Get-ImageGroup, das Informationen zu einer Abbild Gruppe und den darin abgerufenen Images abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0fc25aca-a529-44ee-bc8e-96bc8affb458
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0066e5d52c1d10b1f78ea627ee7a476bfd98f19d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830953"
---
# <a name="get-imagegroup"></a>Get-ImageGroup

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu einer Abbild Gruppe anzuzeigen:
```
wdsutil /Get-ImageGroumediaGroup:ImageGroup1
```
Geben Sie Folgendes ein, um Informationen einschließlich Metadaten anzuzeigen:
```
wdsutil /verbose /Get-ImageGroumediaGroup:ImageGroup1 /Server:MyWDSServer /detailed
```
## <a name="additional-references"></a>Weitere Verweise
- Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls "Add-ImageGroup](using-the-add-imagegroup-command.md) "
[mithilfe des Befehls "Get-allimagegroups](using-the-get-allimagegroups-command.md) "
[mit dem Befehl Remove-ImageGroup](using-the-remove-imagegroup-command.md)
[Unterbefehl: Set-ImageGroup](subcommand-set-imagegroup.md)
