---
title: Mithilfe des Get-Geräte-Befehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1da79286-7e1d-45f2-aea2-d446e16a6911
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 117720c5102da5713c1b0bb5e59cbcc099f3aa8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871031"
---
# <a name="using-the-get-device-command"></a>Mithilfe des Get-Geräte-Befehl

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ruft die Windows-Bereitstellungsdienste-Informationen zu einem vorab bereitgestellten Computer (d. h. ein physischer Computer, die auf ein Computerkonto in active Directory-Domänendienste eingebunden wurde, hat.
## <a name="syntax"></a>Syntax
```
wdsutil /Get-Device {/Device:<Device name> | /ID:<MAC or UUID>} [/Domain:<Domain>] [/forest:{Yes | No}]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/ Gerät:<Device name>|Gibt den Namen des Computers ("sAMAccountName").|
|/ID:<MAC or UUID>|Gibt entweder die MAC-Adresse oder den UUID (GUID) des Computers an, wie in den folgenden Beispielen gezeigt. Beachten Sie, dass in einem der zwei Formate Binärzeichenfolge oder einem GUID-Zeichenfolge eine gültige GUID sein muss<br /><br />-   **Binäre Zeichenfolge**: /ID:ACEFA3E81F20694E953EB2DAA1E8B1B6<br />-   **MAC-Adresse**: 00B056882FDC (ohne Bindestriche) oder 00-B0-56-88-2F-DC (mit Bindestrichen)<br />-   **GUID string**: /ID:E8A3EFAC-201F-4E69-953-B2DAA1E8B1B6|
|[/ Domain:<Domain>]|Gibt die Domäne, für den vorab bereitgestellten Computer gesucht werden soll. Der Standardwert für diesen Parameter ist die lokale Domäne.|
|[/forest:{Yes &#124; No}]|Gibt an, ob Windows-Bereitstellungsdienste der Gesamtstruktur oder die lokale Domäne durchsuchen soll. Der Standardwert ist **keine**, was bedeutet, dass nur die lokale Domäne durchsucht werden.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie Folgendes ein, um Informationen mit den Namen des Computers zu erhalten:
```
wdsutil /Get-Device /Device:computer1
```
Geben Sie Folgendes ein, um Informationen über die MAC-Adresse zu erhalten:
```
wdsutil /verbose /Get-Device /ID:"00-B0-56-88-2F-DC" /Domain:MyDomain
```
Geben Sie Folgendes ein, um die GUID-Zeichenfolge mit Informationen zu erhalten:
```
wdsutil /verbose /Get-Device /ID:E8A3EFAC-201F-4E69-953-B2DAA1E8B1B6 /forest:Yes
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[Unterbefehl: Set-Device-](subcommand-set-device.md)
[mit dem Befehl Hinzufügen von Geräten](using-the-add-device-command.md)
[mithilfe der Get-AllDevices-Befehl](using-the-get-alldevices-command.md)
