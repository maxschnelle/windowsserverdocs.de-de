---
title: Verwenden des Befehls Get-alldevices
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5824b3d2-2df1-4ed6-a289-e6c47c13fea2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b7d2ce709c7e3fbaf7ab4f0e49be14c98ba1cd9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401980"
---
# <a name="using-the-get-alldevices-command"></a>Verwenden des Befehls Get-alldevices

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt die Eigenschaften der Windows-Bereitstellungs Dienste aller vorab bereitgestellten Computer an. Ein vorab bereitgestellter Computer ist ein physischer Computer, der mit einem Computer Konto in den Active Directory-Domänen Diensten verknüpft ist.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-AllDevices [/forest:{Yes | No}] [/ReferralServer:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Forest: {Yes &#124; No}]|Gibt an, ob die Windows-Bereitstellungs Dienste Computer in der Gesamtstruktur oder in der lokalen Domäne zurückgeben sollen. Die Standardeinstellung ist " **Nein**". Dies bedeutet, dass nur die Computer in der lokalen Domäne zurückgegeben werden.|
|[/ReferralServer: <Server name>]|Gibt nur die Computer zurück, die für den angegebenen Server vorab bereitgestellt werden.|
## <a name="BKMK_examples"></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um alle Computer anzuzeigen:
```
wdsutil /Get-AllDevices
wdsutil /verbose /Get-AllDevices /forest:Yes /ReferralServer:MyWDSServer
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Unterbefehl: Set-Device](subcommand-set-device.md)
[mithilfe des Befehls "Add-Device](using-the-add-device-command.md)" 
[mit dem Befehl "Get-Device](using-the-get-device-command.md) "
