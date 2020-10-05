---
title: WDSUTIL Copy-Image
description: Referenz Artikel zu "WDSUTIL Copy-Image", mit dem Bilder kopiert werden, die sich in derselben Abbild Gruppe befinden.
ms.topic: reference
ms.assetid: bea41cf4-36e6-4181-afa5-00170ebd4fdc
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a04848d0b673697809af08b91ca91856d6491773
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730398"
---
# <a name="wdsutil-copy-image"></a>WDSUTIL Copy-Image

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert Bilder, die sich innerhalb derselben Bild Gruppe befinden. Um Bilder zwischen Bildgruppen zu kopieren, verwenden Sie den Befehls Befehl [wdsutilexport-Image](wdsutil-export-image.md) und dann den Befehl [wdsutiladd-Image](wdsutil-add-image.md) .

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /copy-Image image:<Image name> [/Server:<Server name>]
    imagetype:Install
     imageGroup:<Image group name>]
     [/Filename:<File name>]
     /DestinationImage
         /Name:<Name>
         /Filename:<File name>
         [/Description:<Description>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
| Klang<Image name>|Gibt den Namen des zu kopierenden Bilds an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
| ImageType: install|Gibt den Typ des zu kopierenden Bilds an. Diese Option muss auf **Installieren**festgelegt sein.|
|\imagegroup: <Image group name> ]|Gibt die Bild Gruppe an, die das zu kopierende Bild enthält. Wenn keine Abbild Gruppe angegeben wird und nur eine Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe standardmäßig verwendet. Wenn auf dem Server mehr als eine Abbildgruppe vorhanden ist, müssen Sie die Abbildgruppe angeben.|
|[/Filename:<Filename>]|Gibt den Dateinamen des zu kopierenden Bilds an. Wenn das Quell Image nicht anhand des Namens eindeutig identifiziert werden kann, müssen Sie den Dateinamen angeben.|
|/DestinationImage|Gibt die Einstellungen für das Ziel Image an, wie in der folgenden Tabelle beschrieben.<p>-/Name: <Name> legt den anzeigen amen des Bilds fest, das kopiert werden soll.<br />-/Filename: <Filename> legt den Namen der Zielbilddatei fest, die die Bild Kopie enthalten soll.<br />-[/Description: <Description>]: Legt die Beschreibung der Bild Kopie fest.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um eine Kopie des angegebenen Images zu erstellen und diese mit windowsvista. wim zu benennen:
```
wdsutil /copy-Image image:Windows Vista with Office imagetype:Install /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim
```
Wenn Sie eine Kopie des angegebenen Bilds erstellen möchten, wenden Sie die angegebenen Einstellungen an, und benennen Sie die Kopie windowsvista. wim. Geben Sie Folgendes ein:
```
wdsutil /verbose /Progress /copy-Image image:Windows Vista with Office /Server:MyWDSServe imagetype:Install imageGroup:ImageGroup1
/Filename:install.wim /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim /Description:This is a copy of the original Windows image with Office installed
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl "Add-Image"](wdsutil-add-image.md)
- [Befehl "WDSUTIL Export-Image"](wdsutil-export-image.md)
- [Befehl "WDSUTIL Get-Image"](wdsutil-get-image.md)
- [Befehl "Remove-Image" mit WDSUTIL](wdsutil-remove-image.md)
- [Befehl "WDSUTIL Replace-Image"](wdsutil-replace-image.md)
- [Befehl "WDSUTIL Set-Image"](wdsutil-set-image.md)
