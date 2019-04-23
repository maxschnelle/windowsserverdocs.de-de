---
title: Verwenden Sie das Remove-Image-Befehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 2aaf7d63d858045f9dd5df399c5f3f92b038bc2e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846701"
---
# <a name="using-the-remove-image-command"></a>Verwenden Sie das Remove-Image-Befehl

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Löscht ein Abbild von einem Server an.
## <a name="syntax"></a>Syntax
für Startabbilder:
```
wdsutil [Options] /remove-Imagmedia:<Image name> [/Server:<Server name>mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<Filename>]
```
bei Installationsabbildern:
```
wdsutil [Options] /remove-Imagmedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image group name>] [/Filename:<Filename>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien:<Image name>|Gibt den Namen des Bilds.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
mediatype:{Boot &#124; Install}|Gibt den Typ des Bilds an.|
|/Architecture:{x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Bilds. Da es möglich, dass der gleiche ImageName für verschiedene Startabbilder in verschiedenen Architekturen handelt, wird sichergestellt, das den Architektur-angibt, dass das richtige Bild entfernt werden.|
|\mediaGroup:<Image group name>]|Gibt die Image-Gruppe, die das Bild enthält. Wenn kein Bild-Gruppenname angegeben und nur eine Abbildgruppe auf dem Server vorhanden ist, wird diese Abbildgruppe verwendet. Wenn mehr als eine Abbildgruppe vorhanden ist, müssen Sie diese Option verwenden, um die Abbildgruppe angeben.|
|[/Filename:<File name>]|Wenn das Bild kann nicht eindeutig anhand des Namens identifiziert werden, müssen Sie diese Option verwenden, um den Dateinamen angeben.|
## <a name="BKMK_examples"></a>Beispiele für
Um ein Startabbild zu entfernen, geben Sie Folgendes ein:
```
wdsutil /remove-Imagmedia:"WinPE Boot Imagemediatype:Boot /Architecture:x86
```
```
wdsutil /verbose /remove-Imagmedia:"WinPE Boot Image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim
```
Um ein Installationsabbild zu entfernen, geben Sie Folgendes ein:
```
wdsutil /remove-Imagmedia:"Windows Vista with Officemediatype:Install
```
```
wdsutil /verbose /remove-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl-Add-Image](using-the-add-image-command.md)
[mit dem Befehl-Kopieren-Image](using-the-copy-image-command.md)
[mithilfe der Export-Image-Befehl](using-the-export-image-command.md)
[mit dem Get-Image-Befehl](using-the-get-image-command.md)
[mit dem Replace-Image-Befehl](using-the-replace-image-command.md) 
 [ Unterbefehl: Set-Image](subcommand-set-image.md)
