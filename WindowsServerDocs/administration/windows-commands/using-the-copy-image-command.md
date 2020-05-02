---
title: Kopieren/Abbild
description: Referenz Thema für Copy-Image, mit dem Bilder kopiert werden, die sich in derselben Abbild Gruppe befinden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bea41cf4-36e6-4181-afa5-00170ebd4fdc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b3ffd590682ec36f78d3cbd53fd67fe3b5981e4c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720999"
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
|\mediagroup:<Image group name>]|Gibt die Bild Gruppe an, die das zu kopierende Bild enthält. Wenn keine Abbild Gruppe angegeben wird und nur eine Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe standardmäßig verwendet. Wenn auf dem Server mehr als eine Abbildgruppe vorhanden ist, müssen Sie die Abbildgruppe angeben.|
|[/Filename:<Filename>]|Gibt den Dateinamen des zu kopierenden Bilds an. Wenn das Quell Image nicht anhand des Namens eindeutig identifiziert werden kann, müssen Sie den Dateinamen angeben.|
|/DestinationImage|Gibt die Einstellungen für das Ziel Image an, wie in der folgenden Tabelle beschrieben.<p>-/Name:<Name> legt den anzeigen amen des Bilds fest, das kopiert werden soll.<br />-/Filename:<Filename> legt den Namen der Zielbilddatei fest, die die Bild Kopie enthalten soll.<br />-[/Description: <Description>]: Legt die Beschreibung der Bild Kopie fest.|
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
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
mithilfe des Befehls "[Add-Image](using-the-add-image-command.md)
" mithilfe des Befehls "[Export-Image](using-the-export-image-command.md)
" mithilfe des Befehls "[Get-Image](using-the-get-image-command.md)
" mit dem Befehl "[Remove](using-the-remove-image-command.md)
-Image" mithilfe des Befehls Unterbefehl "[Replace-](using-the-replace-image-command.md)
Image"[: Set-Image](subcommand-set-image.md)
