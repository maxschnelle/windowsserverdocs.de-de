---
title: Verwenden Sie das Get-Image-Befehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b78f4ed9352c21bf6de19136a625a4f4fe7ac5f5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877441"
---
# <a name="using-the-get-image-command"></a>Verwenden Sie das Get-Image-Befehl

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ruft Informationen zu einem Bild ab.
## <a name="syntax"></a>Syntax
für Startabbilder:
```
wdsutil [Options] /Get-Imagmedia:<Image name> [/Server:<Server name>mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>]
```
bei Installationsabbildern:
```
wdsutil [Options] /Get-Imagmedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image group name>] [/Filename:<File name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien:<Image name>|Gibt den Namen des Bilds.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
mediatype:{Boot &#124; Install}|Gibt den Typ des Bilds an.|
|/Architecture:{x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Bilds. Da es möglich, dass der gleiche ImageName für Startabbilder in verschiedenen Architekturen handelt, wird sichergestellt, das den Architektur-angibt, dass das richtige Bild zurückgegeben wird.|
|[/Filename:<File name>]|Wenn das Bild kann nicht eindeutig anhand des Namens identifiziert werden, müssen Sie diese Option verwenden, um den Dateinamen angeben.|
|\mediaGroup:<Image group name>]|Gibt die Image-Gruppe, die das Bild enthält. Wenn keine Abbildgruppe angegeben und nur eine Abbildgruppe auf dem Server vorhanden ist, wird dieser Gruppe verwendet werden. Wenn mehr als eine Abbildgruppe auf dem Server vorhanden ist, müssen Sie diesen Parameter verwenden, um die Abbildgruppe angeben.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie zum Abrufen von Informationen zu einem Startabbild, eine der folgenden aus:
```
wdsutil /Get-Imagmedia:"WinPE boot imagemediatype:Boot /Architecture:x86
wdsutil /verbose /Get-Imagmedia:"WinPE boot image" /Server:MyWDSServemediatype:Boot /Architecture:x86 /Filename:boot.wim
```
Geben Sie zum Abrufen von Informationen über ein Installationsabbild, eine der folgenden aus:
```
wdsutil /Get-Imagmedia:"Windows Vista with Officemediatype:Install
wdsutil /verbose /Get-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl-Add-Image](using-the-add-image-command.md)
[mit dem Befehl-Kopieren-Image](using-the-copy-image-command.md)
[mithilfe der Export-Image-Befehl](using-the-export-image-command.md)
[mit dem Remove-Image-Befehl](using-the-remove-image-command.md)
[mit dem Replace-Image-Befehl](using-the-replace-image-command.md) 
 [Unterbefehl: Set-Image](subcommand-set-image.md)
