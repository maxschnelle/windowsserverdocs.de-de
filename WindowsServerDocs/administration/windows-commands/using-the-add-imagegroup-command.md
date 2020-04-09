---
title: Add-ImageGroup
description: Windows-Befehlszeilen Thema für Add-ImageGroup, das einem Windows-Bereitstellungsdiensteserver eine Abbild Gruppe hinzufügt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f12ed27ca1a809ec34dbefbc4ff7288ff194a83e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831893"
---
# <a name="add-imagegroup"></a>Add-ImageGroup

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einem Windows-Bereitstellungsdiensteserver eine Abbild Gruppe hinzu.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /add-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
mediagroup:<Image group name>|Gibt den Namen der hinzu zufügenden Abbild Gruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn Sie keinen Servernamen angeben, wird der lokale Server verwendet.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Zum Hinzufügen einer Abbild Gruppe geben Sie eine der folgenden Informationen ein:
```
wdsutil /add-ImageGroumediaGroup:ImageGroup2
wdsutil /verbose /add-ImageGroumediaGroup:My Image Group /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Get-allimagegroups](using-the-get-allimagegroups-command.md)
[mithilfe des Befehls Get-ImageGroup](using-the-get-imagegroup-command.md)
[mithilfe des Befehls Remove-ImageGroup](using-the-remove-imagegroup-command.md)
[Unterbefehl: Set-ImageGroup](subcommand-set-imagegroup.md)
