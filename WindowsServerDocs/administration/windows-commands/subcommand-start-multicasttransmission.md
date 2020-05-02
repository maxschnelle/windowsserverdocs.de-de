---
title: Unterbefehl Start-MulticastTransmission
description: Referenz Thema für den Unterbefehl "Start-MulticastTransmission", bei dem eine Übertragung eines Bilds mit einem geplanten Cast gestartet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a1b2d459-1ece-49d4-997c-9d206c463b61
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5f3ea615da5aa48e805b3b5e3d0df0a02198a304
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721667"
---
# <a name="subcommand-start-multicasttransmission"></a>Unterbefehl: Start-MulticastTransmission

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Startet eine geplantes Cast Übertragung eines Bilds.

## <a name="syntax"></a>Syntax
**Windows Server 2008**
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
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
Medien<Image name>|Gibt den Namen des Images an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: {Install&#124;Boot}|Gibt den Bildtyp an. Beachten Sie, dass diese Option für die **Installation** von für Windows Server 2008 festgelegt werden muss.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Die Architektur des Start Abbilds, das mit der zu startenden Übertragung verknüpft ist. Da es möglich ist, den gleichen Image Namen für Start Images in verschiedenen Architekturen zu verwenden, sollten Sie die Architektur angeben, um sicherzustellen, dass die richtige Übertragung verwendet wird.|
|\mediagroup:<Image group name>]|Gibt die Bild Gruppe des Bilds an. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe verwendet. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, müssen Sie diese Option verwenden, um den Namen der Abbild Gruppe anzugeben.|
|[/Filename:<File name>]|Gibt den Namen der Datei an, die das Bild enthält. Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
## <a name="examples"></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um eine Multicast Übertragung zu starten:
```
wdsutil /start-MulticastTransmissiomedia:Vista with Office
/Imagetype:Install
wdsutil /start-MulticastTransmission /Server:MyWDSServemedia:Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
Geben Sie Folgendes ein, um eine Multicast Übertragung für ein Start Abbild für Windows Server 2008 R2 zu starten:
```
wdsutil /start-MulticastTransmission /Server:MyWDSServemedia:X64 Boot Imagemediatype:Boot /Architecture:x64
/Filename:boot.wim\n\
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Get-allmulticasttransmission](using-the-get-allmulticasttransmissions-command.md)
mithilfe des Befehls[Get-MulticastTransmission](using-the-get-multicasttransmission-command.md)
mit dem Befehl "[New-MulticastTransmission](using-the-new-multicasttransmission-command.md)
" mit dem Befehl "[Remove-MulticastTransmission](using-the-remove-multicasttransmission-command.md) "
