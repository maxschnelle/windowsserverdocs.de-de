---
title: Verwenden des Befehls "Export-Image"
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 838d84cb5f604eea710c364ed0d4a14efdc16fec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363392"
---
# <a name="using-the-export-image-command"></a>Verwenden des Befehls "Export-Image"

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Exportiert ein vorhandenes Bild aus dem Image Speicher in eine andere Windows-Abbild Datei (WIM).
## <a name="syntax"></a>Syntax
für Start Abbilder:
```
wdsutil [Options] /Export-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>]
     /DestinationImage
         /Filepath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No}]
```
für Installations Images:
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
Medien: <Image name>|Gibt den Namen des zu exportierenden Bilds an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: {Boot &#124; install}|Gibt den Typ des zu exportierenden Bilds an.|
|\mediagroup: <Image group name>]|Gibt die Abbild Gruppe mit dem zu exportierenden Bild an. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe standardmäßig verwendet. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, muss die Abbild Gruppe angegeben werden.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des zu exportierenden Bilds an. Da es möglich ist, den gleichen Image Namen für Start Images in verschiedenen Architekturen zu haben, wird durch Angeben des Architektur Werts sichergestellt, dass das richtige Image zurückgegeben wird.|
|[/Filename:<Filename>]|Wenn das Bild nicht anhand des Namens eindeutig identifiziert werden kann, muss der Dateiname angegeben werden.|
|/DestinationImage|Gibt die Einstellungen für das Ziel Image an. Sie können diese Einstellungen mithilfe der folgenden Optionen angeben:<br /><br />-/FilePath: <File path and name>-gibt den vollständigen Dateipfad für das neue Abbild an.<br />-[/Name: <Name>]: legt den anzeigen amen des Bilds fest. Wenn kein Name angegeben ist, wird der Anzeige Name des Quell Bilds verwendet.<br />-[/Description: <Description>]: Legt die Beschreibung des Bilds fest.|
|[/Overwrite: {Yes &#124; No &#124; Append}]|Bestimmt, ob die in der **/DestinationImage** -Option angegebene Datei überschrieben wird, wenn bereits eine vorhandene Datei mit diesem Namen vorhanden ist.<br /><br />-   **Ja** bewirkt, dass die vorhandene Datei überschrieben wird.<br />-   **Nein** (die Standardoption) bewirkt, dass ein Fehler auftritt, wenn bereits eine Datei mit demselben Namen vorhanden ist.<br />-   **Anfügen** bewirkt, dass das generierte Bild als neues Bild in der vorhandenen WIM-Datei angefügt wird.|
## <a name="BKMK_examples"></a>Beispiele
Geben Sie zum Exportieren eines Start Abbilds einen der folgenden Informationen ein:
```
wdsutil /Export-Imagmedia:"WinPE boot imagemediatype:Boot /Architecture:x86 /DestinationImage /Filepath:"C:\temp\boot.wim"
wdsutil /verbose /Progress /Export-Imagmedia:"WinPE boot image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim 
/DestinationImage /Filepath:"\\Server\Share\ExportImage.wim" /Name:"Exported WinPE image" /Description:"WinPE Image from WDS server" /Overwrite:Yes
```
Geben Sie zum Exportieren eines Installations Abbilds einen der folgenden Informationen ein:
```
wdsutil /Export-Imagmedia:"Windows Vista with Officemediatype:Install /DestinationImage /Filepath:"C:\Temp\Install.wim"
wdsutil /verbose /Progress /Export-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /DestinationImage /Filepath:\\server\share\export.wim /Name:"Exported Windows image" /Description:"Windows Vista image from WDS server" /Overwrite:append
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
 mithilfe des Befehls "[Add-Image](using-the-add-image-command.md)" 
 mithilfe des Befehls "[Copy-](using-the-copy-image-command.md)Image" 
 mithilfe des Befehls "[Get-](using-the-get-image-command.md)Image" 
 mit dem Befehl "[Remove-](using-the-remove-image-command.md)Image" @no__t[-9 Replace-Image-Befehl](using-the-replace-image-command.md)1-[Unterbefehl: Set-Image](subcommand-set-image.md)
