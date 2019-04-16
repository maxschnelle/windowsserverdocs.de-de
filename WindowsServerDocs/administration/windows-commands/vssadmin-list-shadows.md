---
title: Vssadmin Liste Schatten
description: Eine Beschreibung der Liste Vssadmin Schatten Befehl.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 07da36da1473563c3236a4fafc3ceae06259981a
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082251"
---
# <a name="vssadmin-list-shadows"></a>Vssadmin Liste Schatten

>Betrifft: 10 Windows, Windows 8.1, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008

Listet alle vorhandenen Schattenkopien eines angegebenen Volumes. Wenn Sie diesen Befehl ohne Parameter verwenden, werden alle Volumeschattenkopien auf dem Computer in der Reihenfolge von **Shadow Copy festlegen**vorgegeben angezeigt.

## <a name="syntax"></a>Syntax

```PowerShell
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---|---|
|/ for = \ < FürVolumespec >|Gibt an, welche Volume die Schattenkopien für aufgeführt werden.|
|/ shadow = \ < ShadowID >|Listet die Schattenkopie durch ShadowID angegeben. Um die Shadow Copy-ID erhalten möchten, verwenden Sie den Befehl **Vssadmin Liste Schatten** . Wenn Sie eine Shadow Copy-ID eingeben, verwenden Sie das folgende Format, wobei jedes *X* ein hexadezimale Zeichen darstellt:<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|

## <a name="additional-references"></a>Weitere Informationsquellen

* [Befehlszeilensyntax Schlüssel](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)