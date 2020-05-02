---
title: Add-ImageGroup
description: Referenz Thema für Add-ImageGroup, mit dem einem Windows-Bereitstellungsdiensteserver eine Abbild Gruppe hinzugefügt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b08042ac6b33c0ccfe0b66bb0fec70805d55d75f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721055"
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
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
mithilfe[des Befehls Get-allimagegroups](using-the-get-allimagegroups-command.md)
mithilfe[des Befehls Get-ImageGroup](using-the-get-imagegroup-command.md)
mithilfe des Befehls Unterbefehl[Remove-ImageGroup](using-the-remove-imagegroup-command.md)
[: Set-ImageGroup](subcommand-set-imagegroup.md)
