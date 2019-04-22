---
title: Mithilfe des Export-Image-Befehls
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a9b8b467-0f2d-4754-8998-55503a262778
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: efa9b2d09c37a383a91883ee02c995eedb2f235e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823141"
---
# <a name="using-the-export-image-command"></a>Mithilfe des Export-Image-Befehls

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Exportiert ein vorhandenes Image aus dem imagespeicher zu einer anderen Windows-Abbild (WIM)-Datei an.
## <a name="syntax"></a>Syntax
für Startabbilder:
```
wdsutil [Options] /Export-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>]
     /DestinationImage
         /Filepath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No}]
```
bei Installationsabbildern:
```
wdsutil [Options] /Export-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:InstallmediaGroup:<Image group name>]
     [/Filename:<File name>]
     /DestinationImage
         /Filepath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No | append}]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien:<Image name>|Gibt den Namen des Bildes, das exportiert werden.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
mediatype:{Boot &#124; Install}|Gibt den Typ des Bilds, das exportiert werden.|
|\mediaGroup:<Image group name>]|Gibt die Image-Gruppe mit dem Image exportiert werden soll. Wenn kein Bild-Gruppenname angegeben und nur eine Abbildgruppe auf dem Server vorhanden ist, wird standardmäßig diese Abbildgruppe verwendet werden. Wenn mehr als eine Abbildgruppe auf dem Server vorhanden ist, muss die Abbildgruppe angegeben werden.|
|/Architecture:{x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Bildes, das exportiert werden. Da es möglich, dass der gleiche ImageName für Startabbilder in verschiedenen Architekturen handelt, wird sichergestellt, das den Architektur-angibt, dass das richtige Bild zurückgegeben wird.|
|[/Filename:<Filename>]|Wenn das Bild nach Namen eindeutig identifiziert werden kann, muss der Dateiname angegeben werden.|
|/DestinationImage|Gibt die Einstellungen für das Zielabbild. Sie können diese Einstellungen mithilfe der folgenden Optionen angeben:<br /><br />-Destinationimage/FilePath:<File path and name> -gibt den vollständigen Pfad für das neue Image.<br />-[/ Name:<Name>]-legt den Anzeigenamen des Images fest. Wenn kein Name angegeben ist, wird der Anzeigename des Quellbilds verwendet werden.<br />-[/ Description: <Description>]-Legt die Beschreibung des Images fest.|
|[/ Overwrite: {Yes &#124; keine &#124; append}]|Bestimmt, ob die angegebene Datei in die **/DestinationImage** Option überschrieben werden, wenn eine vorhandene Datei mit diesem Namen bereits auf dem destinationimage/FilePath vorhanden ist.<br /><br />-   **Ja** bewirkt, dass die vorhandene Datei überschrieben werden sollen.<br />-   **Keine** (die Standardoption) bewirkt, dass einen Fehler auftreten, wenn eine Datei mit dem gleichen Namen bereits vorhanden.<br />-   **Fügen Sie** bewirkt, dass das generierte Bild als ein neues Image innerhalb der vorhandenen WIM-Datei angefügt werden soll.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie einen der folgenden Schritte aus, um ein Startabbild zu exportieren:
```
wdsutil /Export-Imagmedia:"WinPE boot imagemediatype:Boot /Architecture:x86 /DestinationImage /Filepath:"C:\temp\boot.wim"
wdsutil /verbose /Progress /Export-Imagmedia:"WinPE boot image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim 
/DestinationImage /Filepath:"\\Server\Share\ExportImage.wim" /Name:"Exported WinPE image" /Description:"WinPE Image from WDS server" /Overwrite:Yes
```
Geben Sie eine der folgenden Schritte aus, um ein Installationsabbild zu exportieren:
```
wdsutil /Export-Imagmedia:"Windows Vista with Officemediatype:Install /DestinationImage /Filepath:"C:\Temp\Install.wim"
wdsutil /verbose /Progress /Export-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /DestinationImage /Filepath:\\server\share\export.wim /Name:"Exported Windows image" /Description:"Windows Vista image from WDS server" /Overwrite:append
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl-Add-Image](using-the-add-image-command.md)
[mit dem Befehl-Kopieren-Image](using-the-copy-image-command.md)
[mit dem Get-Image Befehl](using-the-get-image-command.md)
[mit dem Remove-Image-Befehl](using-the-remove-image-command.md)
[mit dem Replace-Image-Befehl](using-the-replace-image-command.md)
[Unterbefehl : Set-Image](subcommand-set-image.md)
