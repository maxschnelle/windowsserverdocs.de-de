---
title: Verwenden den Befehl Remove-MulticastTransmission
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a7f5c31-bfbf-425d-9129-a6f9173fe83d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc3ba385644ef9da9b5d592142091ff087cd7545
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839681"
---
# <a name="using-the-remove-multicasttransmission-command"></a>Verwenden den Befehl Remove-MulticastTransmission

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Deaktiviert die multicast-Übertragung für ein Bild. Es sei denn, Sie geben **/force**, vorhandene Clients führen die Übertragung des Images neue Clients sind jedoch nicht zulässig, beizutreten.
## <a name="syntax"></a>Syntax
**Windows Server 2008**
```
wdsutil /remove-MulticastTransmissiomedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image Group>] [/Filename:<File name>] [/force]
```
**Windows Server 2008 R2** für Startabbilder:
```
wdsutil [Options] /remove-MulticastTransmissiomedia:<Image name>
\x20    [/Server:<Server name>]
\x20  mediatype:Boot
\x20    /Architecture:{x86 | ia64 | x64}
\x20    [/Filename:<File name>]
```
bei Installationsabbildern:
```
wdsutil [Options] /remove-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
      mediatype:Install
       mediaGroup:<Image Group
        [/Filename:<File name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien:<Image name>|Gibt den Namen des Bilds.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollständig qualifizierten Domänennamen (FQDN) sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.|
mediatype:{Install&#124;Boot}|Gibt den Bildtyp an. Beachten Sie, die diese Option muss, um festgelegt werden **installieren** für Windows Server 2008.|
|/Architecture:{x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Startabbilds, das die Übertragung gestartet zugeordnet ist. Da es möglich, dass der gleiche ImageName für Startabbilder in verschiedenen Architekturen handelt, sollten Sie angeben, die Architektur, um sicherzustellen, dass die richtigen Übertragung verwendet wird.|
|\mediaGroup:<Image group name>]|Gibt die Image-Gruppe, die das Bild enthält. Wenn kein Bild-Gruppenname angegeben und nur eine Abbildgruppe auf dem Server vorhanden ist, wird diese Abbildgruppe verwendet. Wenn mehr als eine Abbildgruppe auf dem Server vorhanden ist, müssen Sie diese Option verwenden, den Namen des Abbilds an.|
|[/Filename:<File name>]|Gibt den Dateinamen an. Wenn das Quellbild eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen angeben.|
|[/force]|die Übertragung entfernt, und alle Clients beendet. Es sei denn, Sie geben Sie einen Wert für die **/force** Option vorhandene Clients kann die Übertragung des Images ausführen, aber neue Clients sind nicht beitreten.|
## <a name="BKMK_examples"></a>Beispiele für
So beenden Sie einen Namespace (aktuellen Clients werden die Übertragung abgeschlossen, aber neue Clients werden nicht in der Lage, verknüpfen), Typ:
```
wdsutil /remove-MulticastTransmissiomedia:"Vista with Office"
/Imagetype:Install
```
```
wdsutil /remove-MulticastTransmissiomedia:"x64 Boot Image"
/Imagetype:Boot /Architecture:x64
```
Um die Beendigung aller Clients zu erzwingen, geben Sie Folgendes ein:
```
wdsutil /remove-MulticastTransmission /Server:MyWDSServer
/Image:"Vista with Officemediatype:InstalmediaGroup:ImageGroup1
/Filename:install.wim /force
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Get-AllMulticastTransmissions](using-the-get-allmulticasttransmissions-command.md)
[mit dem Befehl Get-MulticastTransmission](using-the-get-multicasttransmission-command.md) 
 [Mit dem Befehl new-MulticastTransmission](using-the-new-multicasttransmission-command.md)
[Unterbefehl: Start-MulticastTransmission](subcommand-start-multicasttransmission.md)
