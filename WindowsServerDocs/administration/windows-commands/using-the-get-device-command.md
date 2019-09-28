---
title: Verwenden des Befehls Get-Device
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 6451e0a55a72fc88867a3f3be0e1317d881391aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363197"
---
# <a name="using-the-get-device-command"></a>Verwenden des Befehls Get-Device

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen zu den Windows-Bereitstellungs Diensten zu einem vorab bereitgestellten Computer ab (d. h. ein physischer Computer, der zu einem Computer Konto in den Active Directory-Domänen Diensten gehört).
## <a name="syntax"></a>Syntax
```
wdsutil /Get-Device {/Device:<Device name> | /ID:<MAC or UUID>} [/Domain:<Domain>] [/forest:{Yes | No}]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/Device: <Device name>|Gibt den Namen des Computers an (samAccountName).|
|/ID: <MAC or UUID>|Gibt die Mac-Adresse oder die UUID (GUID) des Computers an, wie in den folgenden Beispielen gezeigt. Beachten Sie, dass eine gültige GUID in einem von zwei Formaten eine binäre Zeichenfolge oder eine GUID-Zeichenfolge sein muss.<br /><br />-   -**Binär Zeichenfolge**:/ID: ACEFA3E81F20694E953EB2DAA1E8B1B6<br />**MAC-Adresse**für -   : 00b056882(keine Bindestriche) oder 00-B0-56-88-2F-DC (mit Bindestrichen)<br />-   -**GUID-Zeichenfolge**:/ID: E8A3EFAC-201F-4E69-953-B2DAA1E8B1B6|
|[/Domain: <Domain>]|Gibt die Domäne an, die nach dem vorab bereitgestellten Computer durchsucht werden soll. Der Standardwert für diesen Parameter ist die lokale Domäne.|
|[/Forest: {Yes &#124; No}]|Gibt an, ob die Windows-Bereitstellungs Dienste die gesamte Gesamtstruktur oder die lokale Domäne durchsuchen sollen. Der Standardwert ist **Nein**. Dies bedeutet, dass nur die lokale Domäne durchsucht wird.|
## <a name="BKMK_examples"></a>Beispiele
Um Informationen mithilfe des Computer namens zu erhalten, geben Sie Folgendes ein:
```
wdsutil /Get-Device /Device:computer1
```
Um Informationen über die Mac-Adresse zu erhalten, geben Sie Folgendes ein:
```
wdsutil /verbose /Get-Device /ID:"00-B0-56-88-2F-DC" /Domain:MyDomain
```
Um Informationen mithilfe der GUID-Zeichenfolge zu erhalten, geben Sie Folgendes ein:
```
wdsutil /verbose /Get-Device /ID:E8A3EFAC-201F-4E69-953-B2DAA1E8B1B6 /forest:Yes
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Unterbefehl: Set-Device](subcommand-set-device.md)
[mithilfe des Add-Device-Befehls](using-the-add-device-command.md)
[mithilfe des Befehls "Get-alldevices](using-the-get-alldevices-command.md) "
