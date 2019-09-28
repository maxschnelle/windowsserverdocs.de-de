---
title: Verwenden des Befehls Get-Image
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ecaa999-72ad-4191-adb5-a418de42a001
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 73b25fd70c1512f99b5097b2317c3f0403f3526c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363107"
---
# <a name="using-the-get-image-command"></a>Verwenden des Befehls Get-Image

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen zu einem Bild ab.
## <a name="syntax"></a>Syntax
für Start Abbilder:
```
wdsutil [Options] /Get-Imagmedia:<Image name> [/Server:<Server name>mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>]
```
für Installations Images:
```
wdsutil [Options] /Get-Imagmedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image group name>] [/Filename:<File name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien: <Image name>|Gibt den Namen des Bilds an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: {Boot &#124; install}|Gibt den Typ des Bilds an.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Bilds an. Da es möglich ist, den gleichen Image Namen für Start Images in verschiedenen Architekturen zu haben, wird durch Angeben des Architektur Werts sichergestellt, dass das richtige Bild zurückgegeben wird.|
|[/Filename:<File name>]|Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
|\mediagroup: <Image group name>]|Gibt die Bild Gruppe an, die das Bild enthält. Wenn keine Abbild Gruppe angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Gruppe verwendet. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, müssen Sie diesen Parameter verwenden, um die Abbild Gruppe anzugeben.|
## <a name="BKMK_examples"></a>Beispiele
Zum Abrufen von Informationen zu einem Start Abbild geben Sie eine der folgenden Informationen ein:
```
wdsutil /Get-Imagmedia:"WinPE boot imagemediatype:Boot /Architecture:x86
wdsutil /verbose /Get-Imagmedia:"WinPE boot image" /Server:MyWDSServemediatype:Boot /Architecture:x86 /Filename:boot.wim
```
Zum Abrufen von Informationen zu einem Installations Abbild geben Sie eine der folgenden Informationen ein:
```
wdsutil /Get-Imagmedia:"Windows Vista with Officemediatype:Install
wdsutil /verbose /Get-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
 mithilfe des Befehls "[Add-Image](using-the-add-image-command.md)" 
 mithilfe des Befehls "[Copy-Image](using-the-copy-image-command.md)" 
 mithilfe des Befehls "[Export-](using-the-export-image-command.md)Image" 
 mit dem Befehl "[Remove-](using-the-remove-image-command.md)Image" @no__t[-9 Replace-Image-Befehl](using-the-replace-image-command.md)1-[Unterbefehl: Set-Image](subcommand-set-image.md)
