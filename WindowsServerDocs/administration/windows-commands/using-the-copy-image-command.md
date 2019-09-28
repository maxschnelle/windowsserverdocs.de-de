---
title: Verwenden des Befehls "Copy-Image"
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bea41cf4-36e6-4181-afa5-00170ebd4fdc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2f269884e9c1f96151c9e1220242fad917b76831
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363558"
---
# <a name="using-the-copy-image-command"></a>Verwenden des Befehls "Copy-Image"

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert Bilder, die sich innerhalb derselben Bild Gruppe befinden. Um Bilder zwischen Bildgruppen zu kopieren, verwenden Sie den Befehl [Export-Image](using-the-export-image-command.md) , und verwenden Sie dann den Befehl [Add-Image](using-the-add-image-command.md) .
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /copy-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Install
    mediaGroup:<Image group name>]
     [/Filename:<File name>]
     /DestinationImage
         /Name:<Name>
         /Filename:<File name>
         [/Description:<Description>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien: <Image name>|Gibt den Namen des zu kopierenden Bilds an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: Installieren|Gibt den Typ des zu kopierenden Bilds an. Diese Option muss auf **Installieren**festgelegt sein.|
|\mediagroup: <Image group name>]|Gibt die Bild Gruppe an, die das zu kopierende Bild enthält. Wenn keine Abbild Gruppe angegeben wird und nur eine Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe standardmäßig verwendet. Wenn auf dem Server mehr als eine Abbildgruppe vorhanden ist, müssen Sie die Abbildgruppe angeben.|
|[/Filename:<Filename>]|Gibt den Dateinamen des zu kopierenden Bilds an. Wenn das Quell Image nicht anhand des Namens eindeutig identifiziert werden kann, müssen Sie den Dateinamen angeben.|
|/DestinationImage|Gibt die Einstellungen für das Ziel Image an, wie in der folgenden Tabelle beschrieben.<br /><br />-/Name: <Name>: legt den anzeigen amen des Bilds fest, das kopiert werden soll.<br />-/Filename: <Filename>: legt den Namen der Zielbilddatei fest, die die Bild Kopie enthalten soll.<br />-[/Description: <Description>]: Legt die Beschreibung der Bild Kopie fest.|
## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um eine Kopie des angegebenen Images zu erstellen und diese mit windowsvista. wim zu benennen:
```
wdsutil /copy-Imagmedia:"Windows Vista with Officemediatype:Install /DestinationImage /Name:"copy of Windows Vista with Office" /Filename:"WindowsVista.wim"
```
Wenn Sie eine Kopie des angegebenen Bilds erstellen möchten, wenden Sie die angegebenen Einstellungen an, und benennen Sie die Kopie windowsvista. wim. Geben Sie Folgendes ein:
```
wdsutil /verbose /Progress /copy-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /DestinationImage /Name:"copy of Windows Vista with Office" /Filename:"WindowsVista.wim" /Description:"This is a copy of the original Windows image with Office installed"
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
 mithilfe des Befehls "[Add-Image](using-the-add-image-command.md)" 
 mithilfe des Befehls "[Export-](using-the-export-image-command.md)Image" 
 mithilfe des Befehls "[Get-](using-the-get-image-command.md)Image" 
 mit dem Befehl "[Remove-](using-the-remove-image-command.md)Image" 
 mithilfe[der Replace-Image-Befehl](using-the-replace-image-command.md)1-[Unterbefehl: Set-Image](subcommand-set-image.md)
