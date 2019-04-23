---
title: Start-MulticastTransmission Unterbefehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d7e3e59a0907caf2769d5df00aeaf00589ab450d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842681"
---
# <a name="subcommand-start-multicasttransmission"></a>Unterbefehl: Start-MulticastTransmission

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Startet eine Scheduledcast-Übertragung eines Bilds an.
## <a name="syntax"></a>Syntax
**Windows Server 2008**
```
wdsutil /start-MulticastTransmissiomedia:<Image name> [/Server:<Server namemediatype:InstallmediaGroup:<Image group name>] [/Filename:<File name>]
```
**Windows Server 2008 R2** für Startabbilder:
```
wdsutil [Options] /start-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
      mediatype:Boot
        /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
bei Installationsabbildern:
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
Medien:<Image name>|Gibt den Namen des Bilds.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
mediatype:{Install&#124;Boot}|Gibt den Bildtyp an. Beachten Sie, die diese Option muss, um festgelegt werden **installieren** für Windows Server 2008.|
|/Architecture:{x86 &#124; ia64 &#124; x64}|Die Architektur des Startabbilds, das die Übertragung gestartet zugeordnet ist. Da es möglich, dass der gleiche ImageName für Startabbilder in verschiedenen Architekturen ist, sollten Sie angeben, die Architektur, um sicherzustellen, dass die richtigen Übertragung verwendet wird.|
|\mediaGroup:<Image group name>]|Gibt die Abbildgruppe des Bilds an. Wenn kein Bild-Gruppenname angegeben und nur eine Abbildgruppe auf dem Server vorhanden ist, wird diese Abbildgruppe verwendet. Wenn mehr als eine Abbildgruppe auf dem Server vorhanden ist, müssen Sie diese Option verwenden, den Namen des Abbilds an.|
|[/Filename:<File name>]|Gibt den Namen der Datei, die das Bild enthält. Wenn das Bild kann nicht eindeutig anhand des Namens identifiziert werden, müssen Sie diese Option verwenden, um den Dateinamen angeben.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie einen der folgenden Schritte aus, um eine Multicastübertragung zu starten:
```
wdsutil /start-MulticastTransmissiomedia:"Vista with Office"
/Imagetype:Install
wdsutil /start-MulticastTransmission /Server:MyWDSServemedia:"Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
Zum Starten einer Abbildung Multicastübertragung für Windows Server 2008 R2, Typ:
```
wdsutil /start-MulticastTransmission /Server:MyWDSServemedia:"X64 Boot Imagemediatype:Boot /Architecture:x64
/Filename:boot.wim\n\
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Get-AllMulticastTransmissions](using-the-get-allmulticasttransmissions-command.md)
[mit dem Befehl Get-MulticastTransmission](using-the-get-multicasttransmission-command.md) 
 [Mit dem Befehl new-MulticastTransmission](using-the-new-multicasttransmission-command.md)
[mit dem Remove-MulticastTransmission-Befehl](using-the-remove-multicasttransmission-command.md)
