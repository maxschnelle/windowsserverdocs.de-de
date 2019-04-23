---
title: Mithilfe des Befehls Get-AllDevices
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: e5f51bcc2332cced906be1eec3265541ffd2d225
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886371"
---
# <a name="using-the-get-alldevices-command"></a>Mithilfe des Befehls Get-AllDevices

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt die Eigenschaften der Windows-Bereitstellungsdienste von allen vorab bereitgestellten Computern. Kein vorab bereitgestellter Computer ist ein physischer Computer, der mit der ein Computerkonto in active Directory-Domänendiensten verknüpft wurde.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-AllDevices [/forest:{Yes | No}] [/ReferralServer:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/forest:{Yes &#124; No}]|Gibt an, ob Windows-Bereitstellungsdienste Computer in der Gesamtstruktur oder in der lokalen Domäne zurückgeben soll. Die Standardeinstellung ist **keine**, Bedeutung, die nur die Computer in der lokalen Domäne zurückgegeben werden.|
|[/ReferralServer:<Server name>]|Gibt nur die Computer, die für den angegebenen Server vorbereitet sind.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie einen der folgenden Schritte aus, um alle Computer anzuzeigen:
```
wdsutil /Get-AllDevices
wdsutil /verbose /Get-AllDevices /forest:Yes /ReferralServer:MyWDSServer
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[Unterbefehl: Set-Device-](subcommand-set-device.md)
[mit dem Befehl Hinzufügen von Geräten](using-the-add-device-command.md)
[mithilfe des Get-Geräte Befehl](using-the-get-device-command.md)
