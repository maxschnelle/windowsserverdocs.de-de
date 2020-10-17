---
title: vssadmin delete shadows
description: Eine Beschreibung des Befehls "vssadmin DELETE Shadows", mit dem die Schatten Kopien eines angegebenen Volumes gelöscht werden.
ms.topic: reference
author: JasonGerend
ms.author: jgerend
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2dcd1bf8cbe946c77d0b5a100d2a29ecb36ef50f
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156223"
---
# <a name="vssadmin-delete-shadows"></a>vssadmin delete shadows

> Gilt für: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Löscht die Schatten Kopien eines angegebenen Volumes. Schatten Kopien können nur mit dem vom *Client zugänglichen* Typ gelöscht werden.

## <a name="syntax"></a>Syntax

```
vssadmin delete shadows /for=<ForVolumeSpec> [/oldest | /all | /shadow=<ShadowID>] [/quiet]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /for =`<ForVolumeSpec>` | Gibt an, welche Schattenkopie des Volumes gelöscht wird. |
| /oldest | Löscht nur die älteste Schatten Kopie. |
| /all | Löscht alle Schatten Kopien des angegebenen Volumes. |
| /Shadow =`<ShadowID>` | Löscht die Schatten Kopie, die von shadowid angegeben wird. Verwenden Sie den [Befehl "vssadmin list shadows](vssadmin-list-shadows.md)", um die Schattenkopiekennung zu erhalten. Wenn Sie eine schattenkopienkennung eingeben, verwenden Sie das folgende Format, wobei jedes *X* ein hexadezimales Zeichen darstellt:<p>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx |
| /quiet | Gibt an, dass der Befehl während der Ausführung keine Meldungen anzeigt. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die älteste Schatten Kopie von Volume C zu löschen:

```
vssadmin delete shadows /for=c: /oldest
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [vssadmin-Befehl](vssadmin.md)

- [vssadmin list shadows-Befehl](vssadmin-list-shadows.md)
