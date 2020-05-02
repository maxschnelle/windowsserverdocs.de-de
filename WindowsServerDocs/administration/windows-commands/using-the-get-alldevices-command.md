---
title: "\"Get-alldevices\""
description: Referenz Thema zu "Get-alldevices", in dem die Eigenschaften der Windows-Bereitstellungs Dienste aller vorab bereitgestellten Computer angezeigt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5824b3d2-2df1-4ed6-a289-e6c47c13fea2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 26e114be7ecf104687da237636b54b79e4114591
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720904"
---
# <a name="get-alldevices"></a>"Get-alldevices"

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt die Eigenschaften der Windows-Bereitstellungs Dienste aller vorab bereitgestellten Computer an. Ein vorab bereitgestellter Computer ist ein physischer Computer, der mit einem Computer Konto in den Active Directory-Domänen Diensten verknüpft ist.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-AllDevices [/forest:{Yes | No}] [/ReferralServer:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Forest: {yes &#124; No}]|Gibt an, ob die Windows-Bereitstellungs Dienste Computer in der Gesamtstruktur oder in der lokalen Domäne zurückgeben sollen. Die Standardeinstellung ist " **Nein**". Dies bedeutet, dass nur die Computer in der lokalen Domäne zurückgegeben werden.|
|[/ReferralServer:<Server name>]|Gibt nur die Computer zurück, die für den angegebenen Server vorab bereitgestellt werden.|
## <a name="examples"></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um alle Computer anzuzeigen:
```
wdsutil /Get-AllDevices
wdsutil /verbose /Get-AllDevices /forest:Yes /ReferralServer:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Unterbefehl: setzen Sie das Gerät](subcommand-set-device.md)
[mithilfe des Befehls](using-the-add-device-command.md)
"Add-Device"[mithilfe des Befehls "Get-Device](using-the-get-device-command.md) ".
