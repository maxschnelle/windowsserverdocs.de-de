---
title: Get-Device
description: Referenz Artikel zu Get-Device, der Informationen zu den Windows-Bereitstellungs Diensten zu einem vorab bereitgestellten Computer abruft (d. h. ein physischer Computer, der mit einem Computer Konto in den Active Directory-Domänen Diensten angeordnet ist.
ms.topic: reference
ms.assetid: 1da79286-7e1d-45f2-aea2-d446e16a6911
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4fdbdfa843376b328cac0fe06e68a5a215ddd915
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622590"
---
# <a name="get-device"></a>Get-Device

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen zu den Windows-Bereitstellungs Diensten zu einem vorab bereitgestellten Computer ab (d. h. ein physischer Computer, der zu einem Computer Konto in den Active Directory-Domänen Diensten gehört).

## <a name="syntax"></a>Syntax
```
wdsutil /Get-Device {/Device:<Device name> | /ID:<MAC or UUID>} [/Domain:<Domain>] [/forest:{Yes | No}]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|Schutz<Device name>|Gibt den Namen des Computers an (samAccountName).|
|Name<MAC or UUID>|Gibt die Mac-Adresse oder die UUID (GUID) des Computers an, wie in den folgenden Beispielen gezeigt. Beachten Sie, dass eine gültige GUID in einem von zwei Formaten eine binäre Zeichenfolge oder eine GUID-Zeichenfolge sein muss.<p>-   **Binäre Zeichenfolge**:/ID: ACEFA3E81F20694E953EB2DAA1E8B1B6<br />-   **MAC-Adresse**: 00b056882(keine Bindestriche) oder 00-B0-56-88-2F-DC (mit Bindestrichen)<br />-   **GUID-Zeichenfolge**:/ID: E8A3EFAC-201F-4E69-953-B2DAA1E8B1B6|
|[/Domain: <Domain> ]|Gibt die Domäne an, die nach dem vorab bereitgestellten Computer durchsucht werden soll. Der Standardwert für diesen Parameter ist die lokale Domäne.|
|[/Forest: {yes &#124; No}]|Gibt an, ob die Windows-Bereitstellungs Dienste die gesamte Gesamtstruktur oder die lokale Domäne durchsuchen sollen. Der Standardwert ist **Nein**. Dies bedeutet, dass nur die lokale Domäne durchsucht wird.|
## <a name="examples"></a>Beispiele
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
 [Unterbefehl: Set-Device](subcommand-set-device.md) 
 [Verwenden des Befehls](using-the-add-device-command.md) 
 "Add-Device" [Verwenden des Befehls Get-alldevices](using-the-get-alldevices-command.md)
