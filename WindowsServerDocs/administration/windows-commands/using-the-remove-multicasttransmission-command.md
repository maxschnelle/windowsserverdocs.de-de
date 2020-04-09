---
title: Remove-MulticastTransmission
description: Windows-Befehls Thema für Remove-MulticastTransmission, das die Multicast Übertragung für ein Bild deaktiviert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9a7f5c31-bfbf-425d-9129-a6f9173fe83d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 36bb666b841c4c0c33f12c5ca766e619afc176ef
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830333"
---
# <a name="using-the-remove-multicasttransmission-command"></a>Verwenden des Remove-MulticastTransmission-Befehls

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Deaktiviert die Multicast Übertragung für ein Bild. Wenn Sie **/Force**nicht angeben, wird die Abbild Übertragung durch vorhandene Clients beendet, der Beitritt neuer Clients ist jedoch nicht gestattet.

## <a name="syntax"></a>Syntax
**Windows Server 2008**
```
wdsutil /remove-MulticastTransmissiomedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image Group>] [/Filename:<File name>] [/force]
```
**Windows Server 2008 R2** für Start Abbilder:
```
wdsutil [Options] /remove-MulticastTransmissiomedia:<Image name>
\x20    [/Server:<Server name>]
\x20  mediatype:Boot
\x20    /Architecture:{x86 | ia64 | x64}
\x20    [/Filename:<File name>]
```
für Installations Images:
```
wdsutil [Options] /remove-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
      mediatype:Install
       mediaGroup:<Image Group
        [/Filename:<File name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien:<Image name>|Gibt den Namen des Images an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: {Install&#124;Boot}|Gibt den Bildtyp an. Beachten Sie, dass diese Option für die **Installation** von für Windows Server 2008 festgelegt werden muss.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Start Abbilds an, das mit der zu startenden Übertragung verknüpft ist. Da es möglich ist, den gleichen Image Namen für Start Images in verschiedenen Architekturen zu verwenden, sollten Sie die Architektur angeben, um sicherzustellen, dass die richtige Übertragung verwendet wird.|
|\mediagroup:<Image group name>]|Gibt die Bild Gruppe an, die das Bild enthält. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe verwendet. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, müssen Sie diese Option verwenden, um den Namen der Abbild Gruppe anzugeben.|
|[/Filename:<File name>]|Gibt den Dateinamen an. Wenn das Quell Image nicht anhand des Namens eindeutig identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
|/Force|entfernt die Übertragung und beendet alle Clients. Wenn Sie keinen Wert für die Option **/Force** angeben, können vorhandene Clients die Abbild Übertragung beenden, aber neue Clients können nicht beitreten.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Geben Sie Folgendes ein, um einen Namespace zu beenden (aktuelle Clients schließen die Übertragung ab, aber neue Clients können nicht beitreten). Geben Sie Folgendes ein:
```
wdsutil /remove-MulticastTransmissiomedia:Vista with Office
/Imagetype:Install
```
```
wdsutil /remove-MulticastTransmissiomedia:x64 Boot Image
/Imagetype:Boot /Architecture:x64
```
Wenn Sie die Beendigung aller Clients erzwingen möchten, geben Sie Folgendes ein:
```
wdsutil /remove-MulticastTransmission /Server:MyWDSServer
/Image:Vista with Officemediatype:InstalmediaGroup:ImageGroup1
/Filename:install.wim /force
```
## <a name="additional-references"></a>Weitere Verweise
- Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Get-allmulticasttransmission](using-the-get-allmulticasttransmissions-command.md)
[mithilfe des Befehls Get-MulticastTransmission](using-the-get-multicasttransmission-command.md)
[mithilfe des Befehls New-MulticastTransmission](using-the-new-multicasttransmission-command.md)
[Unterbefehl: Start-MulticastTransmission](subcommand-start-multicasttransmission.md)
