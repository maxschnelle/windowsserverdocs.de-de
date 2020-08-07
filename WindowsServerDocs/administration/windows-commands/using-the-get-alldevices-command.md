---
title: "\"Get-alldevices\""
description: Referenz Artikel zu "Get-alldevices", in dem die Eigenschaften der Windows-Bereitstellungs Dienste aller vorab bereitgestellten Computer angezeigt werden.
ms.topic: article
ms.assetid: 5824b3d2-2df1-4ed6-a289-e6c47c13fea2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1e527be333570838ecb675d78742bbf55918eff3
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896972"
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
|[/ReferralServer: <Server name> ]|Gibt nur die Computer zurück, die für den angegebenen Server vorab bereitgestellt werden.|
## <a name="examples"></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um alle Computer anzuzeigen:
```
wdsutil /Get-AllDevices
wdsutil /verbose /Get-AllDevices /forest:Yes /ReferralServer:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Unterbefehl: Set-Device](subcommand-set-device.md) 
 [Verwenden des Befehls](using-the-add-device-command.md) 
 "Add-Device" [Verwenden des Befehls Get-Device](using-the-get-device-command.md)
