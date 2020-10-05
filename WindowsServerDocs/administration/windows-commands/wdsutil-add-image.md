---
title: WDSUTIL-Add-Image
description: Referenz Artikel zu "WDSUTIL Add-Image", mit dem einem Windows-Bereitstellungsdiensteserver Images hinzugefügt werden.
ms.topic: reference
ms.assetid: d5b6f4da-90ba-4b0e-9423-66c8ef5172e2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ef8068f45a8a2d49715420c06859d326bf93200a
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730451"
---
# <a name="wdsutil-add-image"></a>WDSUTIL-Add-Image

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einem Windows-Bereitstellungsdiensteserver Images hinzu.

## <a name="syntax"></a>Syntax
Verwenden Sie für Start Images die folgende Syntax:
```
wdsutil /add-Image imageFile:<wim file path> [/Server:<Server name> imagetype:Boot [/Skipverify] [/Name:<Image name>] [/Description:<Image description>]
[/Filename:<New wim file name>]
```
Verwenden Sie für Installations Images die folgende Syntax:
```
wdsutil /add-Image imageFile:<wim file path>
     [/Server:<Server name>]
    imagetype:Install
     [/Skipverify]
     imageGroup:<Image group name>]
     [/SingleImage:<Single image name>]
         [/Name:<Name>]
         [/Description:<Description>]
     [/Filename:<File name>]
     [/UnattendFile:<Unattend file path>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|ImageFile: <. wim-Dateipfad>|Gibt den vollständigen Pfad und den Dateinamen der Windows-Abbild Datei (WIM-Datei) an, die die hinzu zufügenden Bilder enthält.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn Sie keinen Servernamen angeben, wird der lokale Server verwendet.|
| ImageType: {Boot&#124;Installation}|Gibt den Typ der Bilder an, die hinzugefügt werden sollen.|
|[/Skipverify]|Gibt an, dass die Integritäts Überprüfung nicht für die Quell Abbild Datei durchgeführt wird, bevor das Image hinzugefügt wird.|
|[/Name: <Name> ]|Legt den anzeigen amen des Bilds fest.|
|/Description<Description>]|Legt die Beschreibung des Bilds fest.|
|[/Filename:<Filename>]|Gibt den neuen Dateinamen für die WIM-Datei an. Auf diese Weise können Sie den Dateinamen der WIM-Datei ändern, wenn Sie das Image hinzufügen. Wenn kein Dateiname angegeben wird, wird der Dateiname des Quell Bilds verwendet. In allen Fällen wird von den Windows-Bereitstellungs Diensten überprüft, ob der Dateiname im Start Abbild Speicher des Ziel Computers eindeutig ist.|
|\imagegroup: <Image group name> ]|Gibt den Namen der Abbild Gruppe an, in der die Bilder hinzugefügt werden sollen. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, muss die Abbild Gruppe angegeben werden. Wenn Sie keine Abbildgruppe angeben und noch keine Abbildgruppe vorhanden ist, wird eine neue erstellt. Andernfalls wird die vorhandene Abbildgruppe verwendet.|
|[/SingleImage: <Single image name> ] [/Name: <Name> ] /Description<Description>]|Kopiert das angegebene einzelne Bild aus einer WIM-Datei und legt den anzeigen Amen und die Beschreibung des Bilds fest.|
|[/UnattendFile:<Unattend file path>]|Gibt den vollständigen Pfad zur unbeaufsichtigten Installationsdatei an, die den hinzugefügten Images zugeordnet werden soll. Wenn **/SingleImage** nicht angegeben ist, wird die gleiche Datei für die unbeaufsichtigte Installation allen Images in der WIM-Datei zugeordnet.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um ein Startimage hinzuzufügen:
```
wdsutil /add-Image imageFile:C:\MyFolder\Boot.wim imagetype:Boot
wdsutil /verbose /Progress /add-Image imageFile:\\MyServer\Share\Boot.wim /Server:MyWDSServer imagetype:Boot /Name:My WinPE Image
/Description:WinPE Image containing the WDS Client /Filename:WDSBoot.wim
```
Geben Sie zum Hinzufügen eines Installations Abbilds einen der folgenden Informationen ein:
```
wdsutil /add-Image imageFile:C:\MyFolder\Install.wim imagetype:Install
wdsutil /verbose /Progress /add-Image imageFile:\\MyServer\Share \Install.wim /Server:MyWDSServer imagetype:Instal imageGroup:ImageGroup1
/SingleImage:Windows Pro /Name:My WDS Image
/Description:Windows Pro image with Microsoft Office /Filename:Win Pro.wim /UnattendFile:\\server\share\unattend.xml
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [Befehl "WDSUTIL Copy-Image"](wdsutil-copy-image.md)
- [Befehl "WDSUTIL Export-Image"](wdsutil-export-image.md)
- [Befehl "WDSUTIL Get-Image"](wdsutil-get-image.md)
- [Befehl "Remove-Image" mit WDSUTIL](wdsutil-remove-image.md)
- [Befehl "WDSUTIL Replace-Image"](wdsutil-replace-image.md)
- [Befehl "WDSUTIL Set-Image"](wdsutil-set-image.md)
