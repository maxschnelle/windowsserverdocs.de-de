---
title: Unterbefehl Start-MulticastTransmission
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1b2d459-1ece-49d4-997c-9d206c463b61
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c0e05a1d625e560d85f0af6ae1d76ef8116ddfd8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383826"
---
# <a name="subcommand-start-multicasttransmission"></a>Unterbefehl: Start-MulticastTransmission

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

startet eine geplantes Cast Übertragung eines Bilds.
## <a name="syntax"></a>Syntax
**Windows Server 2008**
```
wdsutil /start-MulticastTransmissiomedia:<Image name> [/Server:<Server namemediatype:InstallmediaGroup:<Image group name>] [/Filename:<File name>]
```
**Windows Server 2008 R2** für Start Abbilder:
```
wdsutil [Options] /start-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
      mediatype:Boot
        /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
für Installations Images:
```
wdsutil [Options] /start-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
      mediatype:Install
       mediaGroup:<Image Group>]
        [/Filename:<File name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien: <Image name>|Gibt den Namen des Bilds an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: {Install&#124;Boot}|Gibt den Bildtyp an. Beachten Sie, dass diese Option für die **Installation** von für Windows Server 2008 festgelegt werden muss.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Die Architektur des Start Abbilds, das mit der zu startenden Übertragung verknüpft ist. Da es möglich ist, den gleichen Image Namen für Start Images in verschiedenen Architekturen zu verwenden, sollten Sie die Architektur angeben, um sicherzustellen, dass die richtige Übertragung verwendet wird.|
|\mediagroup: <Image group name>]|Gibt die Bild Gruppe des Bilds an. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe verwendet. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, müssen Sie diese Option verwenden, um den Namen der Abbild Gruppe anzugeben.|
|[/Filename:<File name>]|Gibt den Namen der Datei an, die das Bild enthält. Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
## <a name="BKMK_examples"></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um eine Multicast Übertragung zu starten:
```
wdsutil /start-MulticastTransmissiomedia:"Vista with Office"
/Imagetype:Install
wdsutil /start-MulticastTransmission /Server:MyWDSServemedia:"Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
Geben Sie Folgendes ein, um eine Multicast Übertragung für ein Start Abbild für Windows Server 2008 R2 zu starten:
```
wdsutil /start-MulticastTransmission /Server:MyWDSServemedia:"X64 Boot Imagemediatype:Boot /Architecture:x64
/Filename:boot.wim\n\
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Get-allmulticasttransmission](using-the-get-allmulticasttransmissions-command.md)
 mithilfe[des Befehls Get-MulticastTransmission](using-the-get-multicasttransmission-command.md)
 mit dem Befehl[New-MulticastTransmission](using-the-new-multicasttransmission-command.md)
 mit[dem Befehl Remove-MulticastTransmission-Befehl](using-the-remove-multicasttransmission-command.md)
