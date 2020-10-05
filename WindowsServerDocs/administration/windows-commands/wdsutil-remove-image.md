---
title: WDSUTIL Remove-Image
description: Referenz Artikel zu "WDSUTIL Remove-Image", mit dem ein Image von einem Server gelöscht wird.
ms.topic: reference
ms.assetid: ce5e2384-2264-4b22-92af-74eec8c10ae0
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f1d955f54f345b6d2832eabe2334dd77f32633e7
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730511"
---
# <a name="wdsutil-remove-image"></a>WDSUTIL Remove-Image

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht ein Abbild von einem Server.

## <a name="syntax"></a>Syntax
für Start Abbilder:
```
wdsutil [Options] /remove-Image:<Image name> [/Server:<Server name> type:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<Filename>]
```
für Installations Images:
```
wdsutil [Options] /remove-image:<Image name> [/Server:<Server name> type:Install ImageGroup:<Image group name>] [/Filename:<Filename>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
| /Remove-Image<Image name>|Gibt den Namen des Images an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: {Boot &#124; Installation}|Gibt den Typ des Bilds an.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Bilds an. Da es möglich ist, den gleichen Image Namen für verschiedene Start Abbilder in verschiedenen Architekturen zu haben, wird durch Angeben des Architektur Werts sichergestellt, dass das richtige Image entfernt wird.|
|\Imagegroup: <Image group name> ]|Gibt die Bild Gruppe an, die das Bild enthält. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe verwendet. Wenn mehr als eine Abbild Gruppe vorhanden ist, müssen Sie diese Option verwenden, um die Abbild Gruppe anzugeben.|
|[/Filename:<File name>]|Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
## <a name="examples"></a>Beispiele
Zum Entfernen eines Start Abbilds geben Sie Folgendes ein:
```
wdsutil /remove-Imagmedia:WinPE Boot Imagemediatype:Boot /Architecture:x86
```
```
wdsutil /verbose /remove-Image:WinPE Boot Image /Server:MyWDSServer type:Boot /Architecture:x64 /Filename:boot.wim
```
Zum Entfernen eines Installations Abbilds geben Sie Folgendes ein:
```
wdsutil /remove-Image:Windows Vista with Officemediatype:Install
```
```
wdsutil /verbose /remove-Image:Windows Vista with Office /Server:MyWDSServemediatype:Instal ImageGroup:ImageGroup1 /Filename:install.wim
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl "Add-Image"](wdsutil-add-image.md)
- [Befehl "WDSUTIL Copy-Image"](wdsutil-copy-image.md)
- [Befehl "WDSUTIL Export-Image"](wdsutil-export-image.md)
- [Befehl "WDSUTIL Get-Image"](wdsutil-get-image.md)
- [Befehl "WDSUTIL Replace-Image"](wdsutil-replace-image.md)
- [Befehl "WDSUTIL Set-Image"](wdsutil-set-image.md)
