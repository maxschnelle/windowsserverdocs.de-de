---
title: Unterbefehls Satz-ImageGroup
description: Referenz Thema für den untergeordneten Befehlssatz-ImageGroup, der die Attribute einer Abbild Gruppe ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4d86946a-e261-4d41-8b0c-1ab0ba2e3430
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 429a8fee5b0236d264eb421f110219a1bc037368
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721699"
---
# <a name="subcommand-set-imagegroup"></a>Unterbefehl: Set-ImageGroup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert die Attribute einer Abbild Gruppe.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Set-ImageGroumediaGroup:<Image group name> [/Server:<Server name>] [/Name:<New image group name>] [/Security:<SDDL>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
mediagroup:<Image group name>|Gibt den Namen der Abbildgruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn nicht angegeben, wird der lokale Server verwendet.|
|[/Name:<New image group name>]|Gibt den neuen Namen der Abbild Gruppe an.|
|[/Security:<SDDL>]|Gibt die neue Sicherheits Beschreibung der Abbild Gruppe im SDDL-Format (Security Deskriptor Definition Language) an.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um den Namen für eine Abbild Gruppe festzulegen:
```
wdsutil /Set-ImageGroumediaGroup:ImageGroup1 /Name:New Image Group Name
```
Geben Sie Folgendes ein, um verschiedene Einstellungen für eine Abbild Gruppe anzugeben:
```
wdsutil /verbose /Set-ImageGroumediaGroup:ImageGroup1 /Server:MyWDSServer /Name:New Image Group Name 
/Security:O:BAG:S-1-5-21-2176941838-3499754553-4071289181-513 D:AI(A;ID;FA;;;SY)(A;OICIIOID;GA;;;SY)(A;ID;FA;;;BA)(A;OICIIOID;GA;;;BA) (A;ID;0x1200a9;;;AU)(A;OICIIOID;GXGR;;;AU)
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls "Add-ImageGroup](using-the-add-imagegroup-command.md)
" mithilfe des Befehls "[Get-allimagegroups](using-the-get-allimagegroups-command.md)
" mithilfe des Befehls "[Get-ImageGroup](using-the-get-imagegroup-command.md)
" mit dem Befehl "[Remove-ImageGroup](using-the-remove-imagegroup-command.md) "
