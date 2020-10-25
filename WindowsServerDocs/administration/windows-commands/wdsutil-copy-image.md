---
title: WDSUTIL Copy-Image
description: Referenz Artikel für den Befehl "Copy-Image" von WDSUTIL, mit dem Bilder kopiert werden, die sich in derselben Abbild Gruppe befinden.
ms.topic: reference
ms.assetid: bea41cf4-36e6-4181-afa5-00170ebd4fdc
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 690040a5f6624e33e01969a77806afb01c815ea9
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524905"
---
# <a name="wdsutil-copy-image"></a>WDSUTIL Copy-Image

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert Bilder, die sich innerhalb derselben Bild Gruppe befinden. Um Bilder zwischen Bildgruppen zu kopieren, verwenden Sie den Befehls Befehl [WDSUTIL Export-Image](wdsutil-export-image.md) und dann den Befehl [WDSUTIL Add-Image](wdsutil-add-image.md) .

## <a name="syntax"></a>Syntax

```
wdsutil [Options] /copy-Image image:<Image name> [/Server:<Server name>] imagetype:Install imageGroup:<Image group name>] [/Filename:<File name>] /DestinationImage /Name:<Name> /Filename:<File name> [/Description:<Description>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| Klang`<Imagename>` | Gibt den Namen des zu kopierenden Bilds an. |
| [/Server:`<Servername>`] | Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| ImageType: install | Gibt den Typ des zu kopierenden Bilds an. Diese Option muss auf **Installieren**festgelegt sein. |
| \imagegroup: `<Image groupname>` ] | Gibt die Bild Gruppe an, die das zu kopierende Bild enthält. Wenn keine Abbild Gruppe angegeben wird und nur eine Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe standardmäßig verwendet. Wenn auf dem Server mehr als eine Abbildgruppe vorhanden ist, müssen Sie die Abbildgruppe angeben. |
| [/Filename:`<Filename>`] | Gibt den Dateinamen des zu kopierenden Bilds an. Wenn das Quell Image nicht anhand des Namens eindeutig identifiziert werden kann, müssen Sie den Dateinamen angeben. |
| /DestinationImage | Gibt die Einstellungen für das Ziel Image an. Gültige Werte sind:<ul><li>/Name: `<Name>` legt den anzeigen amen des Bilds fest, das kopiert werden soll.</li><li>/Filename: `<Filename>` legt den Namen der Zielbilddatei fest, die die Bild Kopie enthalten soll.</li><li>[/Description: `<Description>` ] : Legt die Beschreibung der Bild Kopie fest.</li></ul> |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Kopie des angegebenen Images zu erstellen und diese mit windowsvista. wim zu benennen:

```
wdsutil /copy-Image image:Windows Vista with Office imagetype:Install /DestinationImage /Name:copy of Windows Vista with Office / Filename:WindowsVista.wim
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

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
