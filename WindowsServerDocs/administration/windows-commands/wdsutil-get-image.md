---
title: WDSUTIL Get-Image
description: Referenz Artikel für WDSUTIL Get-Image, das Informationen zu einem Image abruft.
ms.topic: reference
ms.assetid: 0ecaa999-72ad-4191-adb5-a418de42a001
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0f6cfcf3783ef49f2dd57941ae9a2ae4feb3742e
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730251"
---
# <a name="wdsutil-get-image"></a>WDSUTIL Get-Image

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen zu einem Bild ab.

## <a name="syntax"></a>Syntax
für Start Abbilder:
```
wdsutil [Options] /Get-Image image:<Image name> [/Server:<Server name> imagetype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>]
```
für Installations Images:
```
wdsutil [Options] /Get-image image:<Image name> [/Server:<Server name> imagetype:Install imagegroup:<Image group name>] [/Filename:<File name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
| Klang<Image name>|Gibt den Namen des Images an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
| ImageType: {Boot &#124; Installation}|Gibt den Typ des Bilds an.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Bilds an. Da es möglich ist, den gleichen Image Namen für Start Images in verschiedenen Architekturen zu haben, wird durch Angeben des Architektur Werts sichergestellt, dass das richtige Bild zurückgegeben wird.|
|[/Filename:<File name>]|Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
|\imagegroup: <Image group name> ]|Gibt die Bild Gruppe an, die das Bild enthält. Wenn keine Abbild Gruppe angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Gruppe verwendet. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, müssen Sie diesen Parameter verwenden, um die Abbild Gruppe anzugeben.|
## <a name="examples"></a>Beispiele
Zum Abrufen von Informationen zu einem Start Abbild geben Sie eine der folgenden Informationen ein:
```
wdsutil /Get-Image image:WinPE boot imagetype:Boot /Architecture:x86
wdsutil /verbose /Get-Image image:WinPE boot image /Server:MyWDSServer imagetype:Boot /Architecture:x86 /Filename:boot.wim
```
Zum Abrufen von Informationen zu einem Installations Abbild geben Sie eine der folgenden Informationen ein:
```
wdsutil /Get-Image:Windows Vista with Office imagetype:Install
wdsutil /verbose /Get-Image:Windows Vista with Office /Server:MyWDSServer imagetype:Install imagegroup:ImageGroup1 /Filename:install.wim
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl "Add-Image"](wdsutil-add-image.md)
- [Befehl "WDSUTIL Copy-Image"](wdsutil-copy-image.md)
- [Befehl "WDSUTIL Export-Image"](wdsutil-export-image.md)
- [Befehl "Remove-Image" mit WDSUTIL](wdsutil-remove-image.md)
- [Befehl "WDSUTIL Replace-Image"](wdsutil-replace-image.md)
- [Befehl "WDSUTIL Set-Image"](wdsutil-set-image.md)
