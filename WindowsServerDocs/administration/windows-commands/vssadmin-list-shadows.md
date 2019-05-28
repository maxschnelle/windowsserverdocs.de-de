---
title: Vssadmin Liste Schatten
description: Eine Beschreibung der Liste Vssadmin führt Shadowing für Befehl.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3601986a51e8c5b362a28c686ed132eda8e4b640
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2019
ms.locfileid: "63706564"
---
# <a name="vssadmin-list-shadows"></a>Vssadmin Liste Schatten

>Gilt für: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Listet alle vorhandenen Schattenkopien eines angegebenen Volumes an. Verwendung mit diesem Befehl ohne Parameter zeigt an, wenn alle Schattenkopien des Volumes auf dem Computer in der Reihenfolge von vorgegeben **Shadow Copy festgelegt**.

## <a name="syntax"></a>Syntax

```PowerShell
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---|---|
|/for=\<ForVolumeSpec>|Gibt an, welches Volume die Schattenkopien für aufgeführt werden.|
|/shadow=\<ShadowID>|Listet die Schattenkopie durch ShadowID angegeben. Verwenden Sie zum Abrufen der Schattenkopie-ID der **Vssadmin Liste Shadows** Befehl. Wenn Sie eine Schattenkopie-ID, geben Sie das folgende Format haben, verwenden, in dem jede *X* steht für eine hexadezimale Zeichen:<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|

## <a name="additional-references"></a>Weitere Verweise

* [Befehlszeilensyntax](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)