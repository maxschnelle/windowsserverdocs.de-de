---
title: WDSUTIL-Export-Image
description: Referenz Artikel zu "WDSUTIL Export-Image", mit dem ein vorhandenes Image aus dem Image Speicher in eine andere Windows-Abbild Datei (WIM-Datei) exportiert wird.
ms.topic: reference
ms.assetid: a9b8b467-0f2d-4754-8998-55503a262778
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: cf4fd75d0e88a492b77ce6cd108d54c057503aec
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730338"
---
# <a name="wdsutil-export-image"></a>WDSUTIL-Export-Image

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Exportiert ein vorhandenes Bild aus dem Image Speicher in eine andere Windows-Abbild Datei (WIM).

## <a name="syntax"></a>Syntax
für Start Abbilder:
```
wdsutil [Options] /Export-Image image:<Image name> [/Server:<Server name>]
    imagetype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>]
     /DestinationImage
         /Filepath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No}]
```
für Installations Images:
```
wdsutil [Options] /Export-Image image:<Image name> [/Server:<Server name>]
    imagetype:Install imageGroup:<Image group name>]
     [/Filename:<File name>]
     /DestinationImage
         /Filepath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No | append}]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
| Klang<Image name>|Gibt den Namen des zu exportierenden Bilds an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
| ImageType: {Boot &#124; Installation}|Gibt den Typ des zu exportierenden Bilds an.|
|\imagegroup: <Image group name> ]|Gibt die Abbild Gruppe mit dem zu exportierenden Bild an. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe standardmäßig verwendet. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, muss die Abbild Gruppe angegeben werden.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des zu exportierenden Bilds an. Da es möglich ist, den gleichen Image Namen für Start Images in verschiedenen Architekturen zu haben, wird durch Angeben des Architektur Werts sichergestellt, dass das richtige Image zurückgegeben wird.|
|[/Filename:<Filename>]|Wenn das Bild nicht anhand des Namens eindeutig identifiziert werden kann, muss der Dateiname angegeben werden.|
|/DestinationImage|Gibt die Einstellungen für das Ziel Image an. Sie können diese Einstellungen mithilfe der folgenden Optionen angeben:<p>-/FilePath:: <File path and name> gibt den vollständigen Dateipfad für das neue Abbild an.<br />-[/Name: <Name> ]: legt den anzeigen amen des Bilds fest. Wenn kein Name angegeben ist, wird der Anzeige Name des Quell Bilds verwendet.<br />-[/Description: <Description>]: Legt die Beschreibung des Bilds fest.|
|[/Overwrite: {yes &#124; No &#124; Append}]|Bestimmt, ob die in der **/DestinationImage** -Option angegebene Datei überschrieben wird, wenn bereits eine vorhandene Datei mit diesem Namen vorhanden ist.<p>-   **Ja** bewirkt, dass die vorhandene Datei überschrieben wird.<br />-   **Nein** (die Standardoption) bewirkt, dass ein Fehler auftritt, wenn bereits eine Datei mit demselben Namen vorhanden ist.<br />-   **Anfügen** bewirkt, dass das generierte Bild als neues Bild in der vorhandenen WIM-Datei angefügt wird.|
## <a name="examples"></a>Beispiele
Geben Sie zum Exportieren eines Start Abbilds einen der folgenden Informationen ein:
```
wdsutil /Export-Image image:WinPE boot image imagetype:Boot /Architecture:x86 /DestinationImage /Filepath:C:\temp\boot.wim
wdsutil /verbose /Progress /Export-Image image:WinPE boot image /Server:MyWDSServer imagetype:Boot /Architecture:x64 /Filename:boot.wim
/DestinationImage /Filepath:\\Server\Share\ExportImage.wim /Name:Exported WinPE image /Description:WinPE Image from WDS server /Overwrite:Yes
```
Geben Sie zum Exportieren eines Installations Abbilds einen der folgenden Informationen ein:
```
wdsutil /Export-Image image:Windows Vista with Office imagetype:Install /DestinationImage /Filepath:C:\Temp\Install.wim
wdsutil /verbose /Progress /Export-Image image:Windows Vista with Office /Server:MyWDSServer imagetype:Instal imageGroup:ImageGroup1
/Filename:install.wim /DestinationImage /Filepath:\\server\share\export.wim /Name:Exported Windows image /Description:Windows Vista image from WDS server /Overwrite:append
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl "Add-Image"](wdsutil-add-image.md)
- [Befehl "WDSUTIL Copy-Image"](wdsutil-copy-image.md)
- [Befehl "WDSUTIL Get-Image"](wdsutil-get-image.md)
- [Befehl "Remove-Image" mit WDSUTIL](wdsutil-remove-image.md)
- [Befehl "WDSUTIL Replace-Image"](wdsutil-replace-image.md)
- [Befehl "WDSUTIL Set-Image"](wdsutil-set-image.md)
