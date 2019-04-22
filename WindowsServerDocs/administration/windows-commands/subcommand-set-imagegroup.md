---
title: Set-ImageGroup Unterbefehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d86946a-e261-4d41-8b0c-1ab0ba2e3430
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d0c7ba47148ba6f8295ab720dd0118759ac9346c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822981"
---
# <a name="subcommand-set-imagegroup"></a>Subcommand: set-ImageGroup

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert die Attribute einer Abbildgruppe enthalten.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Set-ImageGroumediaGroup:<Image group name> [/Server:<Server name>] [/Name:<New image group name>] [/Security:<SDDL>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
mediaGroup:<Image group name>|Gibt den Namen der Abbildgruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn nicht angegeben, wird der lokale Server verwendet werden.|
|[/Name:<New image group name>]|Gibt den neuen Namen der Abbildgruppe an.|
|[/ Security:<SDDL>]|Gibt die neue Sicherheitsbeschreibung für die Abbildgruppe in Security Descriptor Definition Language (SDDL)-Format an.|
## <a name="BKMK_examples"></a>Beispiele für
Um den Namen für eine Abbildgruppe festzulegen, geben Sie Folgendes ein:
```
wdsutil /Set-ImageGroumediaGroup:ImageGroup1 /Name:"New Image Group Name"
```
Um verschiedene Einstellungen für eine Abbildgruppe angeben möchten, geben Sie Folgendes ein:
```
wdsutil /verbose /Set-ImageGroumediaGroup:ImageGroup1 /Server:MyWDSServer /Name:"New Image Group Name" 
/Security:"O:BAG:S-1-5-21-2176941838-3499754553-4071289181-513 D:AI(A;ID;FA;;;SY)(A;OICIIOID;GA;;;SY)(A;ID;FA;;;BA)(A;OICIIOID;GA;;;BA) (A;ID;0x1200a9;;;AU)(A;OICIIOID;GXGR;;;AU)"
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Add-ImageGroup](using-the-add-imagegroup-command.md)
[mit dem Befehl Get-AllImageGroups](using-the-get-allimagegroups-command.md) 
 [ Mit dem Befehl Get-ImageGroup](using-the-get-imagegroup-command.md)
[mit dem Remove-ImageGroup-Befehl](using-the-remove-imagegroup-command.md)
