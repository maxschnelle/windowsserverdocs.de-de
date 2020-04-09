---
title: Get-Device
description: Windows-Befehls Thema für Get-Device, das Informationen zu den Windows-Bereitstellungs Diensten von einem vorab bereitgestellten Computer (d. h. ein physischer Computer, der zu einem Computer Konto in den Active Directory-Domänen Diensten gehört hat) abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1da79286-7e1d-45f2-aea2-d446e16a6911
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b9554ed6236d02be0be3502f42552bafbbfe1cb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831113"
---
# <a name="get-device"></a>Get-Device

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen zu den Windows-Bereitstellungs Diensten zu einem vorab bereitgestellten Computer ab (d. h. ein physischer Computer, der zu einem Computer Konto in den Active Directory-Domänen Diensten gehört).

## <a name="syntax"></a>Syntax
```
wdsutil /Get-Device {/Device:<Device name> | /ID:<MAC or UUID>} [/Domain:<Domain>] [/forest:{Yes | No}]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/Device:<Device name>|Gibt den Namen des Computers an (samAccountName).|
|/ID:<MAC or UUID>|Gibt die Mac-Adresse oder die UUID (GUID) des Computers an, wie in den folgenden Beispielen gezeigt. Beachten Sie, dass eine gültige GUID in einem von zwei Formaten eine binäre Zeichenfolge oder eine GUID-Zeichenfolge sein muss.<p>-   **binäre Zeichenfolge**:/ID: ACEFA3E81F20694E953EB2DAA1E8B1B6<br />-   **MAC-Adresse**: 00b056882(keine Bindestriche) oder 00-B0-56-88-2F-DC (mit Bindestrichen)<br />-   **GUID-Zeichenfolge**:/ID: E8A3EFAC-201F-4E69-953-B2DAA1E8B1B6|
|[/Domain:<Domain>]|Gibt die Domäne an, die nach dem vorab bereitgestellten Computer durchsucht werden soll. Der Standardwert für diesen Parameter ist die lokale Domäne.|
|[/Forest: {Yes &#124; No}]|Gibt an, ob die Windows-Bereitstellungs Dienste die gesamte Gesamtstruktur oder die lokale Domäne durchsuchen sollen. Der Standardwert ist **Nein**. Dies bedeutet, dass nur die lokale Domäne durchsucht wird.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Um Informationen mithilfe des Computer namens zu erhalten, geben Sie Folgendes ein:
```
wdsutil /Get-Device /Device:computer1
```
Um Informationen über die Mac-Adresse zu erhalten, geben Sie Folgendes ein:
```
wdsutil /verbose /Get-Device /ID:00-B0-56-88-2F-DC /Domain:MyDomain
```
Um Informationen mithilfe der GUID-Zeichenfolge zu erhalten, geben Sie Folgendes ein:
```
wdsutil /verbose /Get-Device /ID:E8A3EFAC-201F-4E69-953-B2DAA1E8B1B6 /forest:Yes
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Unterbefehl: legen](subcommand-set-device.md) Sie
[mithilfe des Befehls "Add-Device](using-the-add-device-command.md) "
[mithilfe des Befehls "Get-alldevices](using-the-get-alldevices-command.md) " fest.
