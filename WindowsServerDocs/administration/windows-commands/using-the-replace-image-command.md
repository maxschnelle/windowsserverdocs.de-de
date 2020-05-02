---
title: Replace-Image
description: Referenz Thema für Replace-Image, das ein vorhandenes Image durch eine neue Version dieses Images ersetzt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 68ded3df-e309-420f-9f5d-caeb609385a5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9dad35e54f064e02b863059ae6da9378403ee4f9
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720319"
---
# <a name="using-the-replace-image-command"></a>Verwenden des "Replace-Image"-Befehls

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ersetzt ein vorhandenes Bild durch eine neue Version dieses Bilds.
## <a name="syntax"></a>Syntax
für Start Abbilder:
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
für Installations Images:
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
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
Medien<Image name>|Gibt den Namen des zu ersetzenden Bilds an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: {Boot &#124; Installation}|Gibt den Typ des zu ersetzenden Bilds an.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des zu ersetzenden Bilds an. Da es möglich ist, den gleichen Image Namen für verschiedene Start Images in verschiedenen Architekturen zu haben, wird durch die Angabe der Architektur sichergestellt, dass das richtige Image ersetzt wird.|
|[/Filename:<File name>]|Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
|/replacementImage|Gibt die Einstellungen für das Ersatz Bild an. Diese Einstellungen werden mithilfe der folgenden Optionen festgelegt:<p>-mediafile: <file path> : gibt den Namen und den Speicherort (vollständiger Pfad) der neuen WIM-Datei an.<br />-[/SourceImage: <image name>]: gibt das Bild an, das verwendet werden soll, wenn die WIM-Datei mehrere Abbilder enthält. Diese Option gilt nur für das Installieren von Images.<br />-[/Name:<Image name>] legt den anzeigen amen des Bilds fest.<br />-[/Description:<Image description>]: legt die Beschreibung des Bilds fest.|
## <a name="examples"></a>Beispiele
Um ein Start Abbild zu ersetzen, geben Sie einen der folgenden Informationen ein:
```
wdsutil /replace-Imagmedia:WinPE Boot Imagemediatype:Boot /Architecture:x86 /replacementImagmediaFile:C:\MyFolder\Boot.wim
wdsutil /verbose /Progress /replace-Imagmedia:WinPE Boot Image /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim 
/replacementImagmediaFile:\\MyServer\Share\Boot.wim /Name:My WinPE Image /Description:WinPE Image with drivers
```
Um ein Installations Abbild zu ersetzen, geben Sie einen der folgenden Informationen ein:
```
wdsutil /replace-Imagmedia:Windows Vista Homemediatype:Install /replacementImagmediaFile:C:\MyFolder\Install.wim
wdsutil /verbose /Progress /replace-Imagmedia:Windows Vista Pro /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:Install.wim /replacementImagmediaFile:\\MyServer\Share \Install.wim /SourceImage:Windows Vista Ultimate /Name:Windows Vista Desktop /Description:Windows Vista Ultimate with standard business applications.
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
mithilfe des Befehls "[Add-Image](using-the-add-image-command.md)
" mithilfe des Befehls "[Copy-Image](using-the-copy-image-command.md)
" mithilfe des Befehls "[Export-Image](using-the-export-image-command.md)
" mit dem Befehl "[Get-](using-the-get-image-command.md)
Image" mithilfe des Befehls Unterbefehl "[Replace-](using-the-replace-image-command.md)
Image"[: Set-Image](subcommand-set-image.md)
