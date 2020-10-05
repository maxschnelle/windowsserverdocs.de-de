---
title: WDSUTIL Get-ImageGroup
description: Referenz Artikel zu "WDSUTIL Get-ImageGroup", mit dem Informationen zu einer Abbild Gruppe und den darin abgerufenen Images abgerufen werden.
ms.topic: reference
ms.assetid: 0fc25aca-a529-44ee-bc8e-96bc8affb458
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d40fef643ebbb8fd48f36fc048ddefc0b4b3229f
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730257"
---
# <a name="wdsutil-get-imagegroup"></a>WDSUTIL Get-ImageGroup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen zu einer Abbild Gruppe und den darin enthaltenen Bildern ab.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-ImageGroup ImageGroup:<Image group name> [/Server:<Server name>] [/detailed]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|/ImageGroup:<Image group name>|Gibt den Namen der Abbildgruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Detailed|Gibt die Bild Metadaten für jedes Bild zurück. Wenn dieser Parameter nicht verwendet wird, besteht das Standardverhalten darin, nur den Bildnamen, die Beschreibung und den Dateinamen zurückzugeben.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu einer Abbild Gruppe anzuzeigen:
```
wdsutil /Get-ImageGroup ImageGroup:ImageGroup1
```
Geben Sie Folgendes ein, um Informationen einschließlich Metadaten anzuzeigen:
```
wdsutil /verbose /Get-ImageGroup ImageGroup:ImageGroup1 /Server:MyWDSServer /detailed
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl "Add-ImageGroup"](wdsutil-add-imagegroup.md)
- [Befehl "WDSUTIL Get-allimagegroups"](wdsutil-get-allimagegroups.md)
- [WDSUTIL Remove-ImageGroup-Befehl](wdsutil-remove-imagegroup.md)
- [Befehl "WDSUTIL Set-ImageGroup"](wdsutil-set-imagegroup.md)
