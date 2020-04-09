---
title: Remove-Image
description: Windows-Befehls Thema für Remove-Image, mit dem ein Bild von einem Server gelöscht wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce5e2384-2264-4b22-92af-74eec8c10ae0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 760c61c3109255000fe1177a456243a5c91c883f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830363"
---
# <a name="remove-image"></a>Remove-Image

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht ein Abbild von einem Server.

## <a name="syntax"></a>Syntax
für Start Abbilder:
```
wdsutil [Options] /remove-Imagmedia:<Image name> [/Server:<Server name>mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<Filename>]
```
für Installations Images:
```
wdsutil [Options] /remove-Imagmedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image group name>] [/Filename:<Filename>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien:<Image name>|Gibt den Namen des Images an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: {Boot &#124; install}|Gibt den Typ des Bilds an.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Bilds an. Da es möglich ist, den gleichen Image Namen für verschiedene Start Abbilder in verschiedenen Architekturen zu haben, wird durch Angeben des Architektur Werts sichergestellt, dass das richtige Image entfernt wird.|
|\mediagroup:<Image group name>]|Gibt die Bild Gruppe an, die das Bild enthält. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe verwendet. Wenn mehr als eine Abbild Gruppe vorhanden ist, müssen Sie diese Option verwenden, um die Abbild Gruppe anzugeben.|
|[/Filename:<File name>]|Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Zum Entfernen eines Start Abbilds geben Sie Folgendes ein:
```
wdsutil /remove-Imagmedia:WinPE Boot Imagemediatype:Boot /Architecture:x86
```
```
wdsutil /verbose /remove-Imagmedia:WinPE Boot Image /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim
```
Zum Entfernen eines Installations Abbilds geben Sie Folgendes ein:
```
wdsutil /remove-Imagmedia:Windows Vista with Officemediatype:Install
```
```
wdsutil /verbose /remove-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
## <a name="additional-references"></a>Weitere Verweise
- Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls "Add-Image](using-the-add-image-command.md) "
[mithilfe des Befehls "Copy-Image](using-the-copy-image-command.md) "
[mithilfe des Befehls "Export-Image](using-the-export-image-command.md) "
mithilfe des Befehls " [Get-Image](using-the-get-image-command.md) "
mithilfe des Befehls " [Replace-](using-the-replace-image-command.md) Image"
[Unterbefehl: Set-Image](subcommand-set-image.md)
