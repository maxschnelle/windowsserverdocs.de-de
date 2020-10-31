---
title: WDSUTIL-Export-Image
description: Referenz Artikel für den Befehl WDSUTIL Export-Image, mit dem ein vorhandenes Image aus dem Image Speicher in eine andere Windows-Abbild Datei (WIM) exportiert wird.
ms.topic: reference
ms.assetid: a9b8b467-0f2d-4754-8998-55503a262778
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8c3c390e43cc8707d8d94ade757130276b5f2753
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93071042"
---
# <a name="wdsutil-export-image"></a>WDSUTIL-Export-Image

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Exportiert ein vorhandenes Bild aus dem Image Speicher in eine andere Windows-Abbild Datei (WIM).

## <a name="syntax"></a>Syntax

Für Start Abbilder:

```
wdsutil [options] /Export-Image image:<Image name> [/Server:<Servername>]
    imagetype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<Filename>]
     /DestinationImage
         /Filepath:<Filepath and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No}]
```

Für Installations Images:

```
wdsutil [options] /Export-Image image:<Image name> [/Server:<Servername>]
    imagetype:Install imageGroup:<Image group name>]
     [/Filename:<Filename>]
     /DestinationImage
         /Filepath:<Filepath and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No | append}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| Klang`<Imagename>` | Gibt den Namen des zu exportierenden Bilds an. |
| [/Server:`<Servername>`] | Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| ImageType`{Boot|Install}` | Gibt den Typ des zu exportierenden Bilds an. |
| \imagegroup: `<Image group name>` ] | Gibt die Abbild Gruppe mit dem zu exportierenden Bild an. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe standardmäßig verwendet. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, muss die Abbild Gruppe angegeben werden. |
| Architektur`{x86|ia64|x64}` | Gibt die Architektur des zu exportierenden Bilds an. Da es möglich ist, den gleichen Image Namen für Start Images in verschiedenen Architekturen zu haben, wird durch Angeben des Architektur Werts sichergestellt, dass das richtige Image zurückgegeben wird. |
| [/Filename:`<Filename>`] | Wenn das Bild nicht anhand des Namens eindeutig identifiziert werden kann, muss der Dateiname angegeben werden. |
| /DestinationImage | Gibt die Einstellungen für das Ziel Image an. Sie können diese Einstellungen mithilfe der folgenden Optionen angeben:<ul><li>`/Filepath:<Filepath and name>` : Gibt den vollständigen Dateipfad für das neue Bild an.</li><li>`[/Name:<Name>]` : Legt den anzeigen amen des Bilds fest. Wenn kein Name angegeben ist, wird der Anzeige Name des Quell Bilds verwendet.</li><li>`[/Description: <Description>]` : Legt die Beschreibung des Bilds fest.</li></ul> |
| [/Overwrite: `{Yes|No|append}` ] | Bestimmt, ob die in der **/DestinationImage** -Option angegebene Datei überschrieben wird, wenn bereits eine vorhandene Datei mit diesem Namen vorhanden ist. Die Option **Ja** bewirkt, dass die vorhandene Datei überschrieben wird. die Option **Nein** (Standard) bewirkt, dass ein Fehler auftritt, wenn bereits eine Datei mit demselben Namen vorhanden ist. die Option **Anfügen** bewirkt, dass das generierte Bild als neues Bild in der vorhandenen WIM-Datei angefügt wird. |

## <a name="examples"></a>Beispiele

Zum Exportieren eines Start Abbilds geben Sie Folgendes ein:

```
wdsutil /Export-Image image:WinPE boot image imagetype:Boot /Architecture:x86 /DestinationImage /Filepath:C:\temp\boot.wim
```

```
wdsutil /verbose /Progress /Export-Image image:WinPE boot image /Server:MyWDSServer imagetype:Boot /Architecture:x64 /Filename:boot.wim /DestinationImage /Filepath:\\Server\Share\ExportImage.wim /Name:Exported WinPE image /Description:WinPE Image from WDS server /Overwrite:Yes
```

Zum Exportieren eines Installations Abbilds geben Sie Folgendes ein:

```
wdsutil /Export-Image image:Windows Vista with Office imagetype:Install /DestinationImage /Filepath:C:\Temp\Install.wim
```

```
wdsutil /verbose /Progress /Export-Image image:Windows Vista with Office /Server:MyWDSServer imagetype:Instal imageGroup:ImageGroup1 /Filename:install.wim /DestinationImage /Filepath:\\server\share\export.wim /Name:Exported Windows image /Description:Windows Vista image from WDS server /Overwrite:append
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [WDSUTIL-Befehl "Add-Image"](wdsutil-add-image.md)

- [Befehl "WDSUTIL Copy-Image"](wdsutil-copy-image.md)

- [Befehl "WDSUTIL Get-Image"](wdsutil-get-image.md)

- [Befehl "Remove-Image" mit WDSUTIL](wdsutil-remove-image.md)

- [Befehl "WDSUTIL Replace-Image"](wdsutil-replace-image.md)

- [Befehl "WDSUTIL Set-Image"](wdsutil-set-image.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)