---
title: WDSUTIL Add-ImageGroup
description: Referenz Artikel zu WDSUTIL Add-ImageGroup, mit dem einem Windows-Bereitstellungsdiensteserver eine Abbild Gruppe hinzugefügt wird.
ms.topic: reference
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 97f1439a4212a770dff6f6c42837c531f08c3d25
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730431"
---
# <a name="wdsutil-add-imagegroup"></a>WDSUTIL Add-ImageGroup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einem Windows-Bereitstellungsdiensteserver eine Abbild Gruppe hinzu.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /add-ImageGroup imageGroup:<Image group name> [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|ImageGroup:<Image group name>|Gibt den Namen der hinzu zufügenden Abbild Gruppe an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn Sie keinen Servernamen angeben, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Zum Hinzufügen einer Abbild Gruppe geben Sie eine der folgenden Informationen ein:
```
wdsutil /add-ImageGroup imageGroup:ImageGroup2
wdsutil /verbose /add-Imagegroup imageGroup:My Image Group /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [Befehl "WDSUTIL Get-allimagegroups"](wdsutil-get-allimagegroups.md)
- [Befehl "WDSUTIL Get-ImageGroup"](wdsutil-get-imagegroup.md)
- [WDSUTIL Remove-ImageGroup-Befehl](wdsutil-remove-imagegroup.md)
- [Befehl "WDSUTIL Set-ImageGroup"](wdsutil-set-imagegroup.md)
