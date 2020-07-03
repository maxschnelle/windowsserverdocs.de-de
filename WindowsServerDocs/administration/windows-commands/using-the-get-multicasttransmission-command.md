---
title: Get-MulticastTransmission
description: Referenz Artikel zu Get-MulticastTransmission, der Informationen über die Multicast Übertragung für ein angegebenes Abbild anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b733737b-1e81-43d4-a058-d6985a613bef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a764aa0a975fe29daed54e50b7ab0284a12a399f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932198"
---
# <a name="get-multicasttransmission"></a>Get-MulticastTransmission

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen über die Multicast Übertragung für ein angegebenes Abbild an.

## <a name="syntax"></a>Syntax
**Windows Server 2008**
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image group name>]
[/Filename:<File name>] [/Show:Clients]
```
**Windows Server 2008 R2** für Start Abbild Übertragungen:
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name>
    [/Server:<Server name>]
    [/details:Clients]
  mediatype:Boot
    /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
für Installations Abbild Übertragungen:
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name>
         [/Server:<Server name>]
         [/details:Clients]
       mediatype:Install
    mediaGroup:<Image Group>]
     [/Filename:<File name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien<Image name>|Zeigt die Multicast Übertragung an, die diesem Bild zugeordnet ist.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: Installieren|Gibt den Bildtyp an. Beachten Sie, dass diese Option auf **Installieren**festgelegt werden muss.|
|\mediagroup: <Image group name> ]|Gibt die Bild Gruppe an, die das Bild enthält. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe verwendet. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, müssen Sie diese Option verwenden, um eine Abbild Gruppe anzugeben.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Start Abbilds an, das mit der Übertragung verknüpft ist. Da es möglich ist, den gleichen Image Namen für Start Images in verschiedenen Architekturen zu verwenden, sollten Sie die Architektur angeben, um sicherzustellen, dass das richtige Image verwendet wird.|
|[/Filename:<File name>]|Gibt die Datei an, die das Bild enthält. Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
|[/Show: Clients]<p>oder<p>[/Details: Clients]|Hiermit werden Informationen zu Client Computern angezeigt, die mit der Multicast Übertragung verbunden sind.|
## <a name="examples"></a>Beispiele
**Windows Server 2008** Um Informationen zur Übertragung für ein Image mit dem Namen Vista und Office anzuzeigen, geben Sie eine der folgenden Informationen ein:
```
wdsutil /Get-MulticastTransmissiomedia:Vista with Officemediatype:Install
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim /Show:Clients
```
**Windows Server 2008 R2** Um Informationen zur Übertragung für ein Image mit dem Namen Vista und Office anzuzeigen, geben Sie eine der folgenden Informationen ein:
```
wdsutil /Get-MulticastTransmissiomedia:Vista with Office
 /Imagetype:Install
```
```
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim /details:Clients
```
```
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:X64 Boot Imagemediatype:Boot /Architecture:x64 /Filename:boot.wim /details:Clients
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-get-allmulticasttransmissions-command.md) 
 Get-allmulticasttransmissions [Verwenden des New-MulticastTransmission-Befehls](using-the-new-multicasttransmission-command.md) 
 [Verwenden des Remove-MulticastTransmission-Befehls](using-the-remove-multicasttransmission-command.md) 
 [Unterbefehl: Start-MulticastTransmission](subcommand-start-multicasttransmission.md)
