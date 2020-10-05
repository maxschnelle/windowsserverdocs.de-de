---
title: WDSUTIL Set-ImageGroup
description: Referenz Artikel für den Unterbefehl Set-ImageGroup, der die Attribute einer Abbild Gruppe ändert.
ms.topic: reference
ms.assetid: 4d86946a-e261-4d41-8b0c-1ab0ba2e3430
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6f3b2b3790ecc126f8be48ade61d305d44011f68
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730562"
---
# <a name="wdsutil-set-imagegroup"></a>WDSUTIL Set-ImageGroup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert die Attribute einer Abbild Gruppe.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /set-imagegroup:<Image group name> [/Server:<Server name>] [/Name:<New image group name>] [/Security:<SDDL>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|/set-imagegroup:<Image group name>|Gibt den Namen der Abbildgruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn nicht angegeben, wird der lokale Server verwendet.|
|[/Name: <New image group name> ]|Gibt den neuen Namen der Abbild Gruppe an.|
|[/Security: <SDDL> ]|Gibt die neue Sicherheits Beschreibung der Abbild Gruppe im SDDL-Format (Security Deskriptor Definition Language) an.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um den Namen für eine Abbild Gruppe festzulegen:
```
wdsutil /Set-ImageGroup:ImageGroup1 /Name:New Image Group Name
```
Geben Sie Folgendes ein, um verschiedene Einstellungen für eine Abbild Gruppe anzugeben:
```
wdsutil /verbose /Set-ImageGroupGroup:ImageGroup1 /Server:MyWDSServer /Name:New Image Group Name
/Security:O:BAG:S-1-5-21-2176941838-3499754553-4071289181-513 D:AI(A;ID;FA;;;SY)(A;OICIIOID;GA;;;SY)(A;ID;FA;;;BA)(A;OICIIOID;GA;;;BA) (A;ID;0x1200a9;;;AU)(A;OICIIOID;GXGR;;;AU)
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl "Add-ImageGroup"](wdsutil-add-imagegroup.md)
- [Befehl "WDSUTIL Get-allimagegroups"](wdsutil-get-allimagegroups.md)
- [Befehl "WDSUTIL Get-ImageGroup"](wdsutil-get-imagegroup.md)
- [WDSUTIL Remove-ImageGroup-Befehl](wdsutil-remove-imagegroup.md)
