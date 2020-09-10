---
title: Kopieren/Abbild
description: Referenz Artikel für Copy-Image, mit dem Bilder kopiert werden, die sich in derselben Abbild Gruppe befinden.
ms.topic: reference
ms.assetid: bea41cf4-36e6-4181-afa5-00170ebd4fdc
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 15b838dff8c3b7a1ceb372416eaef5617a00f7ba
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622150"
---
# <a name="copy-image"></a>Kopieren/Abbild

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert Bilder, die sich innerhalb derselben Bild Gruppe befinden. Um Bilder zwischen Bildgruppen zu kopieren, verwenden Sie den Befehl [Export-Image](using-the-export-image-command.md) , und verwenden Sie dann den Befehl [Add-Image](using-the-add-image-command.md) .

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
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
Medien<Image name>|Gibt den Namen des zu kopierenden Bilds an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: Installieren|Gibt den Typ des zu kopierenden Bilds an. Diese Option muss auf **Installieren**festgelegt sein.|
|\mediagroup: <Image group name> ]|Gibt die Bild Gruppe an, die das zu kopierende Bild enthält. Wenn keine Abbild Gruppe angegeben wird und nur eine Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe standardmäßig verwendet. Wenn auf dem Server mehr als eine Abbildgruppe vorhanden ist, müssen Sie die Abbildgruppe angeben.|
|[/Filename:<Filename>]|Gibt den Dateinamen des zu kopierenden Bilds an. Wenn das Quell Image nicht anhand des Namens eindeutig identifiziert werden kann, müssen Sie den Dateinamen angeben.|
|/DestinationImage|Gibt die Einstellungen für das Ziel Image an, wie in der folgenden Tabelle beschrieben.<p>-/Name: <Name> legt den anzeigen amen des Bilds fest, das kopiert werden soll.<br />-/Filename: <Filename> legt den Namen der Zielbilddatei fest, die die Bild Kopie enthalten soll.<br />-[/Description: <Description>]: Legt die Beschreibung der Bild Kopie fest.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um eine Kopie des angegebenen Images zu erstellen und diese mit windowsvista. wim zu benennen:
```
wdsutil /copy-Imagmedia:Windows Vista with Officemediatype:Install /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim
```
Wenn Sie eine Kopie des angegebenen Bilds erstellen möchten, wenden Sie die angegebenen Einstellungen an, und benennen Sie die Kopie windowsvista. wim. Geben Sie Folgendes ein:
```
wdsutil /verbose /Progress /copy-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1
/Filename:install.wim /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim /Description:This is a copy of the original Windows image with Office installed
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-add-image-command.md) 
 "Add-Image" [Verwenden des Befehls](using-the-export-image-command.md) 
 "Export-Image" [Verwenden des Befehls](using-the-get-image-command.md) 
 Get-Image [Verwenden des Remove-Image-Befehls](using-the-remove-image-command.md) 
 [Verwenden des "Replace-Image"-Befehls](using-the-replace-image-command.md) 
 [Unterbefehl: Set-Image](subcommand-set-image.md)
