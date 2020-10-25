---
title: WDSUTIL-Add-Image
description: Referenz Artikel für den Befehl "WDSUTIL Add-Image", mit dem einem Windows-Bereitstellungsdiensteserver Images hinzugefügt werden.
ms.topic: reference
ms.assetid: d5b6f4da-90ba-4b0e-9423-66c8ef5172e2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e0d80c0a3aa9cfc6a5b9e05f11542dfcc8621946
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524517"
---
# <a name="wdsutil-add-image"></a>WDSUTIL-Add-Image

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einem Windows-Bereitstellungsdiensteserver Images hinzu.

## <a name="syntax"></a>Syntax

Verwenden Sie für Start Images die folgende Syntax:

```
wdsutil /add-Image imageFile:<wim file path> [/Server:<Server name> imagetype:Boot [/Skipverify] [/Name:<Image name>] [/Description:<Image description>] [/Filename:<New wim file name>]
```

Verwenden Sie für Installations Images die folgende Syntax:

```
wdsutil /add-Image imageFile:<wim filepath> [/Server:<Servername>] imagetype:Install [/Skipverify] imageGroup:<Image group name>] [/SingleImage:<Single image name>] [/Name:<Name>] [/Description:<Description>] [/Filename:<File name>] [/UnattendFile:<Unattend file path>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| ImageFile:`<.wim filepath>` | Gibt den vollständigen Pfad und den Dateinamen der Windows-Abbild Datei (WIM-Datei) an, die die hinzu zufügenden Bilder enthält. |
| [/Server:`<Servername>`] | Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| ImageType`{Boot|Install}` | Gibt den Typ der Bilder an, die hinzugefügt werden sollen. |
| [/Skipverify] | Gibt an, dass die Integritäts Überprüfung nicht für die Quell Abbild Datei durchgeführt wird, bevor das Image hinzugefügt wird. |
| [/Name: `<Name>` ] | Legt den anzeigen amen des Bilds fest. |
| [/Description: `<Description>` ] | Legt die Beschreibung des Bilds fest. |
| [/Filename:`<Filename>`] | Gibt den neuen Dateinamen für die WIM-Datei an. Auf diese Weise können Sie den Dateinamen der WIM-Datei beim Hinzufügen des Bilds ändern. Wenn Sie keinen Dateinamen angeben, wird der Dateiname des Quell Bilds verwendet. In allen Fällen wird von den Windows-Bereitstellungs Diensten überprüft, ob der Dateiname im Start Abbild Speicher des Ziel Computers eindeutig ist. |
| \imagegroup: `<Imagegroupname>` ] | Gibt den Namen der Abbild Gruppe an, in der die Bilder hinzugefügt werden sollen. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, muss die Abbild Gruppe angegeben werden. Wenn Sie die Abbild Gruppe nicht angeben und bereits eine Abbild Gruppe vorhanden ist, wird eine neue Abbild Gruppe erstellt. Andernfalls wird die vorhandene Abbild Gruppe verwendet. |
| [/SingleImage: `<Singleimagename>` ] [/Name: `<Name>` ] [/Description: `<Description>` ] | Kopiert das angegebene einzelne Bild aus einer WIM-Datei und legt den anzeigen Amen und die Beschreibung des Bilds fest. |
| [/UnattendFile:`<Unattendfilepath>`] | Gibt den vollständigen Pfad zur unbeaufsichtigten Installationsdatei an, die den hinzugefügten Images zugeordnet werden soll. Wenn **/SingleImage** nicht angegeben ist, wird die gleiche Datei für die unbeaufsichtigte Installation allen Images in der WIM-Datei zugeordnet. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Startimage hinzuzufügen:

```
wdsutil /add-Image imageFile:C:\MyFolder\Boot.wim imagetype:Boot
wdsutil /verbose /Progress /add-Image imageFile:\\MyServer\Share\Boot.wim /Server:MyWDSServer imagetype:Boot /Name:My WinPE Image /Description:WinPE Image containing the WDS Client /Filename:WDSBoot.wim
```

Geben Sie zum Hinzufügen eines Installations Abbilds einen der folgenden Informationen ein:

```
wdsutil /add-Image imageFile:C:\MyFolder\Install.wim imagetype:Install
wdsutil /verbose /Progress /add-Image imageFile:\\MyServer\Share \Install.wim /Server:MyWDSServer imagetype:Instal imageGroup:ImageGroup1
/SingleImage:Windows Pro /Name:My WDS Image /Description:Windows Pro image with Microsoft Office /Filename:Win Pro.wim /UnattendFile:\\server\share\unattend.xml
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "WDSUTIL Copy-Image"](wdsutil-copy-image.md)

- [Befehl "WDSUTIL Export-Image"](wdsutil-export-image.md)

- [Befehl "WDSUTIL Get-Image"](wdsutil-get-image.md)

- [Befehl "Remove-Image" mit WDSUTIL](wdsutil-remove-image.md)

- [Befehl "WDSUTIL Replace-Image"](wdsutil-replace-image.md)

- [Befehl "WDSUTIL Set-Image"](wdsutil-set-image.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
