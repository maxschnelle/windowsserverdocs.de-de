---
title: Verwenden des Befehls "Add-ImageGroup"
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 5e870bd5435e1aa2b155fee880d32c0d784ac398
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363678"
---
# <a name="using-the-add-imagegroup-command"></a>Verwenden des Befehls "Add-ImageGroup"

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einem Windows-Bereitstellungsdiensteserver eine Abbild Gruppe hinzu.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /add-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
mediagroup: <Image group name>|Gibt den Namen der hinzu zufügenden Abbild Gruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn Sie keinen Servernamen angeben, wird der lokale Server verwendet.|
## <a name="BKMK_examples"></a>Beispiele
Zum Hinzufügen einer Abbild Gruppe geben Sie eine der folgenden Informationen ein:
```
wdsutil /add-ImageGroumediaGroup:ImageGroup2
wdsutil /verbose /add-ImageGroumediaGroup:"My Image Group" /Server:MyWDSServer
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Get-allimagegroups](using-the-get-allimagegroups-command.md)
 mithilfe[des Befehls Get-ImageGroup](using-the-get-imagegroup-command.md)
 mit[dem Befehl Remove-ImageGroup](using-the-remove-imagegroup-command.md)
[Unterbefehl: Set-ImageGroup](subcommand-set-imagegroup.md)
