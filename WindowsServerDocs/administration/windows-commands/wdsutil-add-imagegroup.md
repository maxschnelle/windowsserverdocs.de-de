---
title: WDSUTIL Add-ImageGroup
description: Referenz Artikel für den Befehl "WDSUTIL Add-ImageGroup", mit dem einem Windows-Bereitstellungsdiensteserver eine Abbild Gruppe hinzugefügt wird.
ms.topic: reference
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3bffb562ba019bb55c783541b78c906dd4a08dc7
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524465"
---
# <a name="wdsutil-add-imagegroup"></a>WDSUTIL Add-ImageGroup

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einem Windows-Bereitstellungsdiensteserver eine Abbild Gruppe hinzu.

## <a name="syntax"></a>Syntax

```
wdsutil [Options] /add-ImageGroup imageGroup:<Imagegroupname> [/Server:<Server name>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| ImageGroup: `<Imagegroupname>` ] | Gibt den Namen des hinzu zufügenden Bilds an. |
| [/Server:`<Servername>`] | Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |

## <a name="examples"></a>Beispiele

Zum Hinzufügen einer Abbild Gruppe geben Sie Folgendes ein:

```
wdsutil /add-ImageGroup imageGroup:ImageGroup2
```

```
wdsutil /verbose /add-Imagegroup imageGroup:My Image Group /Server:MyWDSServer
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "WDSUTIL Get-allimagegroups"](wdsutil-get-allimagegroups.md)

- [Befehl "WDSUTIL Get-ImageGroup"](wdsutil-get-imagegroup.md)

- [WDSUTIL Remove-ImageGroup-Befehl](wdsutil-remove-imagegroup.md)

- [Befehl "WDSUTIL Set-ImageGroup"](wdsutil-set-imagegroup.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
