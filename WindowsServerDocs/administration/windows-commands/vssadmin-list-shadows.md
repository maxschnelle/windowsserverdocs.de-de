---
title: Schatten der vssadmin-Liste
description: Eine Beschreibung des Befehls "vssadmin List Shadows".
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 38eda178b6c9e34fec1d63ed6c59f01023b859c4
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436673"
---
# <a name="vssadmin-list-shadows"></a>Schatten der vssadmin-Liste

> Gilt für: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Listet alle vorhandenen Schatten Kopien eines angegebenen Volumes auf. Wenn Sie diesen Befehl ohne Parameter verwenden, werden alle Volumeschattenkopien auf dem Computer in der durch den **Schattenkopiesatz**vorgeschriebenen Reihenfolge angezeigt.

## <a name="syntax"></a>Syntax

```PowerShell
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---|---|
|/for = \< forvolumespec>|Gibt an, für welches Volume die Schatten Kopien aufgeführt werden.|
|/Shadow = \< shadowid>|Listet die von shadowid angegebene Schatten Kopie auf. Verwenden Sie den Befehl " **vssadmin list shadows** ", um die Schattenkopiekennung zu erhalten. Wenn Sie eine schattenkopienkennung eingeben, verwenden Sie das folgende Format, wobei jedes *X* ein hexadezimales Zeichen darstellt:<br><br>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx|

## <a name="additional-references"></a>Zusätzliche Referenzen

* [Befehlszeilen-Syntax Schlüssel](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)