---
title: vssadmin list shadows
description: Eine Beschreibung des Befehls "vssadmin List Shadows", der alle vorhandenen Schatten Kopien eines angegebenen Volumes auflistet.
ms.topic: reference
author: JasonGerend
ms.author: jgerend
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: cb7ddaa09e2da350c1c5422c6224aabd8831f763
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156209"
---
# <a name="vssadmin-list-shadows"></a>vssadmin list shadows

> Gilt für: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Listet alle vorhandenen Schatten Kopien eines angegebenen Volumes auf. Wenn Sie diesen Befehl ohne Parameter verwenden, werden alle Volumeschattenkopien auf dem Computer in der durch den **Schattenkopiesatz**vorgeschriebenen Reihenfolge angezeigt.

## <a name="syntax"></a>Syntax

```
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /for =`<ForVolumeSpec>` | Gibt an, für welches Volume die Schatten Kopien aufgeführt werden. |
| /Shadow =`<ShadowID>` | Listet die von shadowid angegebene Schatten Kopie auf. Verwenden Sie den [Befehl "vssadmin list shadows](vssadmin-list-shadows.md)", um die Schattenkopiekennung zu erhalten. Wenn Sie eine schattenkopienkennung eingeben, verwenden Sie das folgende Format, wobei jedes *X* ein hexadezimales Zeichen darstellt:<p>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [vssadmin-Befehl](vssadmin.md)

- [vssadmin list shadows-Befehl](vssadmin-list-shadows.md)
