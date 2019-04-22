---
title: Verwenden die Replace-Image-Befehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68ded3df-e309-420f-9f5d-caeb609385a5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e396ee678e22885a50c02800d77ecea1cc5ef8ba
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819651"
---
# <a name="using-the-replace-image-command"></a>Verwenden die Replace-Image-Befehl

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

ersetzt ein vorhandenes Image mit einer neuen Version des Images an.
## <a name="syntax"></a>Syntax
für Startabbilder:
```
wdsutil [Options] /replace-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Boot
     /Architecture:{x86 | ia64 | x64}
     [/Filename:<File name>]
     /replacementImage
       mediaFile:<wim file path>
         [/Name:<Image name>]
         [/Description:<Image description>]
```
bei Installationsabbildern:
```
wdsutil [Options] /replace-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Install
    mediaGroup:<Image group name>]
     [/Filename:<File name>]
     /replacementImage
       mediaFile:<wim file path>
         [/SourceImage:<Source image name>]
         [/Name:<Image name>]
         [/Description:<Image description>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien:<Image name>|Gibt den Namen des Bildes, das ersetzt werden.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
mediatype:{Boot &#124; Install}|Gibt den Typ des Bilds, das ersetzt werden.|
|/Architecture:{x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Bildes, das ersetzt werden. Da es möglich, dass der gleiche ImageName für verschiedene Startabbilder in verschiedenen Architekturen handelt, wird sichergestellt, die die Architektur angibt, dass das richtige Bild ersetzt wird.|
|[/Filename:<File name>]|Wenn das Bild kann nicht eindeutig anhand des Namens identifiziert werden, müssen Sie diese Option verwenden, um den Dateinamen angeben.|
|/replacementImage|Gibt die Einstellungen für das Image ersetzt. Diese Einstellungen mithilfe der folgenden Optionen festlegen:<br /><br />-MediaFile: <file path> -gibt den Namen und Speicherort (vollständiger Pfad), der die neue WIM-Datei.<br />-[/ SourceImage: <image name>]: Gibt das Bild an verwendet werden, wenn die WIM-Datei mehrere Abbilder enthält. Diese Option gilt nur für Images installieren.<br />-[/ Name:<Image name>] legt den Anzeigenamen des Images fest.<br />-[/ Description:<Image description>]-legt die Beschreibung des Images fest.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie einen der folgenden Schritte aus, um ein Startabbild zu ersetzen:
```
wdsutil /replace-Imagmedia:"WinPE Boot Imagemediatype:Boot /Architecture:x86 /replacementImagmediaFile:"C:\MyFolder\Boot.wim"
wdsutil /verbose /Progress /replace-Imagmedia:"WinPE Boot Image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim 
/replacementImagmediaFile:\\MyServer\Share\Boot.wim /Name:"My WinPE Image" /Description:"WinPE Image with drivers"
```
Geben Sie eine der folgenden Schritte aus, um ein Installationsabbild zu ersetzen:
```
wdsutil /replace-Imagmedia:"Windows Vista Homemediatype:Install /replacementImagmediaFile:"C:\MyFolder\Install.wim"
wdsutil /verbose /Progress /replace-Imagmedia:"Windows Vista Pro" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:Install.wim /replacementImagmediaFile:\\MyServer\Share \Install.wim /SourceImage:"Windows Vista Ultimate" /Name:"Windows Vista Desktop" /Description:"Windows Vista Ultimate with standard business applications."
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl-Add-Image](using-the-add-image-command.md)
[mit dem Befehl-Kopieren-Image](using-the-copy-image-command.md)
[mithilfe der Export-Image-Befehl](using-the-export-image-command.md)
[mit dem Get-Image-Befehl](using-the-get-image-command.md)
[mit dem Replace-Image-Befehl](using-the-replace-image-command.md) 
 [ Unterbefehl: Set-Image](subcommand-set-image.md)
