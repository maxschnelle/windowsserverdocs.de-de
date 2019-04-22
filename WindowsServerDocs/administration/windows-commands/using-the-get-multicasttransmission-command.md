---
title: Mithilfe des Befehls Get-MulticastTransmission
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b733737b-1e81-43d4-a058-d6985a613bef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fdbb9283285bcf56cd83c18ea076e3d36a51b966
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823231"
---
# <a name="using-the-get-multicasttransmission-command"></a>Mithilfe des Befehls Get-MulticastTransmission

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt Informationen über die Multicastübertragung für ein angegebenes Bild.
## <a name="syntax"></a>Syntax
**Windows Server 2008**
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image group name>] 
[/Filename:<File name>] [/Show:Clients]
```
**Windows Server 2008 R2** für Übertragungen von Boot Image:
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name>
    [/Server:<Server name>]
    [/details:Clients]
  mediatype:Boot
    /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
Bei Image-Übertragungen installieren:
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name>
         [/Server:<Server name>]
         [/details:Clients]
       mediatype:Install
    mediaGroup:<Image Group>]
     [/Filename:<File name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien:<Image name>|Zeigt die Multicastübertragung, die mit diesem Image zugeordnet ist.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollständig qualifizierten Domänennamen (FQDN) sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.|
mediatype:Install|Gibt den Bildtyp an. Beachten Sie, die diese Option muss, um festgelegt werden **installieren**.|
|\mediaGroup:<Image group name>]|Gibt die Image-Gruppe, die das Bild enthält. Wenn kein Bild-Gruppenname angegeben und nur eine Abbildgruppe auf dem Server vorhanden ist, wird diese Abbildgruppe verwendet. Wenn mehr als eine Abbildgruppe auf dem Server vorhanden ist, müssen Sie diese Option verwenden, eine Abbildgruppe angeben.|
|/Architecture:{x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Startabbilds, das die Übertragung zugeordnet ist. Da es möglich, dass der gleiche ImageName für Startabbilder in verschiedenen Architekturen handelt, sollten Sie angeben, die Architektur, um sicherzustellen, dass das richtige Image verwendet wird.|
|[/Filename:<File name>]|Gibt die Datei, die das Bild enthält. Wenn das Bild kann nicht eindeutig anhand des Namens identifiziert werden, müssen Sie diese Option verwenden, um den Dateinamen angeben.|
|[/Show:Clients]<br /><br />oder<br /><br />[/details:Clients]|Zeigt Informationen zu Clientcomputern, die die Multicastübertragung verbunden sind.|
## <a name="BKMK_examples"></a>Beispiele für
**Windows Server 2008** zum Anzeigen von Informationen über die Übertragung für ein Bild mit dem Namen Vista mit Office geben Sie einen der folgenden:
```
wdsutil /Get-MulticastTransmissiomedia:"Vista with Officemediatype:Install
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:"Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim /Show:Clients
```
**Windows Server 2008 R2** zum Anzeigen von Informationen über die Übertragung für ein Bild mit dem Namen Vista mit Office geben Sie einen der folgenden:
```
wdsutil /Get-MulticastTransmissiomedia:"Vista with Office"
 /Imagetype:Install
```
```
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:"Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim /details:Clients
```
```
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:"X64 Boot Imagemediatype:Boot /Architecture:x64 /Filename:boot.wim /details:Clients
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Get-AllMulticastTransmissions](using-the-get-allmulticasttransmissions-command.md)
[mit dem Befehl new-MulticastTransmission](using-the-new-multicasttransmission-command.md) 
 [Mit dem Befehl Remove-MulticastTransmission](using-the-remove-multicasttransmission-command.md)
[Unterbefehl: Start-MulticastTransmission](subcommand-start-multicasttransmission.md)
