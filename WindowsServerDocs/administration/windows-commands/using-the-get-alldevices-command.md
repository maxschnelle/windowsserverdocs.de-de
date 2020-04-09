---
title: "\"Get-alldevices\""
description: Windows-Befehls Thema für "Get-alldevices", das die Eigenschaften der Windows-Bereitstellungs Dienste aller vorab bereitgestellten Computer anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5824b3d2-2df1-4ed6-a289-e6c47c13fea2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 929a74b6cccaed6e85015648538c1ca875b62208
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831413"
---
# <a name="get-alldevices"></a>"Get-alldevices"

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt die Eigenschaften der Windows-Bereitstellungs Dienste aller vorab bereitgestellten Computer an. Ein vorab bereitgestellter Computer ist ein physischer Computer, der mit einem Computer Konto in den Active Directory-Domänen Diensten verknüpft ist.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-AllDevices [/forest:{Yes | No}] [/ReferralServer:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Forest: {Yes &#124; No}]|Gibt an, ob die Windows-Bereitstellungs Dienste Computer in der Gesamtstruktur oder in der lokalen Domäne zurückgeben sollen. Die Standardeinstellung ist " **Nein**". Dies bedeutet, dass nur die Computer in der lokalen Domäne zurückgegeben werden.|
|[/ReferralServer:<Server name>]|Gibt nur die Computer zurück, die für den angegebenen Server vorab bereitgestellt werden.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um alle Computer anzuzeigen:
```
wdsutil /Get-AllDevices
wdsutil /verbose /Get-AllDevices /forest:Yes /ReferralServer:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Unterbefehl: Set-Device](subcommand-set-device.md)
[mithilfe des Befehls "Add-Device](using-the-add-device-command.md) "
[mithilfe des Befehls "Get-Device](using-the-get-device-command.md) "
