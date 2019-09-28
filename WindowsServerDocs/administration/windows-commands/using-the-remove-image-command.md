---
title: Verwenden des Remove-Image-Befehls
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce5e2384-2264-4b22-92af-74eec8c10ae0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c0876649a4de55604707f03ca98cf0ceed2920b9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362826"
---
# <a name="using-the-remove-image-command"></a>Verwenden des Remove-Image-Befehls

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien: <Image name>|Gibt den Namen des Bilds an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: {Boot &#124; install}|Gibt den Typ des Bilds an.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Bilds an. Da es möglich ist, den gleichen Image Namen für verschiedene Start Abbilder in verschiedenen Architekturen zu haben, wird durch Angeben des Architektur Werts sichergestellt, dass das richtige Image entfernt wird.|
|\mediagroup: <Image group name>]|Gibt die Bild Gruppe an, die das Bild enthält. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe verwendet. Wenn mehr als eine Abbild Gruppe vorhanden ist, müssen Sie diese Option verwenden, um die Abbild Gruppe anzugeben.|
|[/Filename:<File name>]|Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
## <a name="BKMK_examples"></a>Beispiele
Zum Entfernen eines Start Abbilds geben Sie Folgendes ein:
```
wdsutil /remove-Imagmedia:"WinPE Boot Imagemediatype:Boot /Architecture:x86
```
```
wdsutil /verbose /remove-Imagmedia:"WinPE Boot Image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim
```
Zum Entfernen eines Installations Abbilds geben Sie Folgendes ein:
```
wdsutil /remove-Imagmedia:"Windows Vista with Officemediatype:Install
```
```
wdsutil /verbose /remove-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
 mithilfe des Befehls "[Add-Image](using-the-add-image-command.md)" 
 mithilfe des Befehls "[Copy-Image](using-the-copy-image-command.md)" 
 mithilfe des Befehls "[Export-](using-the-export-image-command.md)Image" 
 mithilfe des Befehls "[Get-](using-the-get-image-command.md)Image" 
 mithilfe[der Replace-Image-Befehl](using-the-replace-image-command.md)1-[Unterbefehl: Set-Image](subcommand-set-image.md)
