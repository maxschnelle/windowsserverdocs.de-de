---
title: WDSUTIL Remove-ImageGroup
description: Referenz Artikel zu "WDSUTIL Remove-ImageGroup", mit dem eine Abbild Gruppe von einem Server entfernt wird.
ms.topic: reference
ms.assetid: 5b2c9813-5df2-4272-8449-26f3bb16f82b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c9691281a706a2929c7406bfcca2c3f3410112e0
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730514"
---
# <a name="wdsutil-remove-imagegroup"></a>WDSUTIL Remove-ImageGroup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt eine Abbild Gruppe von einem Server.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /remove-ImageGroup Group:<Image group name> [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|ImageGroup:<Image group name>|Gibt den Namen der zu entfernenden Abbild Gruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Um die Abbild Gruppe zu entfernen, geben Sie eine der folgenden Informationen ein:
```
wdsutil /remove-ImageGroumediaGroup:ImageGroup1
wdsutil /verbose /remove-ImageGroumediaGroup:My Image Group /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl "Add-ImageGroup"](wdsutil-add-imagegroup.md)
- [Befehl "WDSUTIL Get-allimagegroups"](wdsutil-get-allimagegroups.md)
- [Befehl "WDSUTIL Get-ImageGroup"](wdsutil-get-imagegroup.md)
- [Befehl "WDSUTIL Set-ImageGroup"](wdsutil-set-imagegroup.md)
