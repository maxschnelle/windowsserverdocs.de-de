---
title: Vssadmin löschen Schatten
description: Eine Beschreibung des Befehls Schatten Vssadmin löschen.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 71119174c7fc5929eb4e1982183ba0aed7eb1735
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082160"
---
# <a name="vssadmin-delete-shadows"></a>Vssadmin löschen Schatten

>Betrifft: 10 Windows, Windows 8.1, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008

Löscht eine angegebene Volume Schattenkopien.

## <a name="syntax"></a>Syntax

```PowerShell
vssadmin delete shadows /for=<ForVolumeSpec> [/oldest | /all | /shadow=<ShadowID>] [/quiet]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---|---|
|/ for = \ < FürVolumespec >|Gibt an, welche Volumeschattenkopie gelöscht werden.|
|/ ältesten|Löscht nur die älteste Schattenkopie.|
|/ all|Löscht alle Schattenkopien für das angegebene Volume.|
|/ shadow = \ < ShadowID >|Löscht die Schattenkopie durch ShadowID angegeben. Um die Shadow Copy-ID erhalten möchten, verwenden Sie den Befehl **Vssadmin Liste Schatten** . Wenn Sie eine Shadow Copy-ID eingeben, verwenden Sie das folgende Format, wobei jedes *X* ein hexadezimale Zeichen darstellt:<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|
|/ quiet|Gibt an, dass der Befehl Nachrichten während der Ausführung nicht angezeigt wird.|

## <a name="remarks"></a>Hinweise

Sie können nur mit dem Client zugänglichen Typ Schattenkopien löschen.

## <a name="examples"></a>Beispiele

Geben Sie diesen Befehl, um die älteste Schattenkopie des Datenträgers C zu löschen:

```PowerShell
vssadmin delete shadows /for=c: /oldest
```

## <a name="additional-references"></a>Weitere Informationsquellen

* [Befehlszeilensyntax Schlüssel](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)
* [Vssadmin Liste Schatten](vssadmin-list-shadows.md)