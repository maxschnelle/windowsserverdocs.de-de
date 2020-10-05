---
title: WDSUTIL Replace-Image
description: Referenz Artikel zu "WDSUTIL Replace-Image", mit dem ein vorhandenes Image durch eine neue Version dieses Images ersetzt wird.
ms.topic: reference
ms.assetid: 68ded3df-e309-420f-9f5d-caeb609385a5
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b03bf133fa84f1a37578889ef8f3b3fefd5a8d16
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730122"
---
# <a name="wdsutil-replace-image"></a>WDSUTIL Replace-Image

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
|/replacementImage|Gibt die Einstellungen für das Ersatz Bild an. Diese Einstellungen werden mithilfe der folgenden Optionen festgelegt:<p>-mediafile:: <file path> gibt den Namen und den Speicherort (vollständiger Pfad) der neuen WIM-Datei an.<br />-[/SourceImage: <image name> ]: gibt das Bild an, das verwendet werden soll, wenn die WIM-Datei mehrere Abbilder enthält. Diese Option gilt nur für das Installieren von Images.<br />-[/Name: <Image name> ] legt den anzeigen amen des Bilds fest.<br />-[/Description: <Image description> ]: legt die Beschreibung des Bilds fest.|
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
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl "Add-Image"](wdsutil-add-image.md)
- [Befehl "WDSUTIL Copy-Image"](wdsutil-copy-image.md)
- [Befehl "WDSUTIL Export-Image"](wdsutil-export-image.md)
- [Befehl "WDSUTIL Get-Image"](wdsutil-get-image.md)
- [Befehl "WDSUTIL Replace-Image"](wdsutil-replace-image.md)
- [Befehl "WDSUTIL Set-Image"](wdsutil-set-image.md)
