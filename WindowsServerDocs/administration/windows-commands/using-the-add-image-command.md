---
title: Mithilfe des Add-Image-Befehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5b6f4da-90ba-4b0e-9423-66c8ef5172e2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0433e0775bd2088170ae17fcfe432cdaee0bf99d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817461"
---
# <a name="using-the-add-image-command"></a>Mithilfe des Add-Image-Befehl

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Fügt die Bilder auf einem Windows-Bereitstellungsdiensteserver hinzu. Beispiele, wie Sie diesen Befehl verwenden können, finden Sie unter [Beispiele](#BKMK_examples).
## <a name="syntax"></a>Syntax
Verwenden Sie für Startabbilder die folgende Syntax:
```
wdsutil /add-ImagmediaFile:<wim file path> [/Server:<Server name>mediatype:Boot [/Skipverify] [/Name:<Image name>] [/Description:<Image description>] 
[/Filename:<New wim file name>]
```
Verwenden Sie bei Installationsabbildern die folgende Syntax:
```
wdsutil /add-ImagmediaFile:<wim file path>
     [/Server:<Server name>]
   mediatype:Install
     [/Skipverify]
    mediaGroup:<Image group name>]
     [/SingleImage:<Single image name>]
         [/Name:<Name>]
         [/Description:<Description>]
     [/Filename:<File name>]
     [/UnattendFile:<Unattend file path>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Mediendatei: < Pfad der WIM-Datei >|Gibt den vollständigen Pfad und Namen der Windows-Abbild (WIM)-Datei mit den Bildern hinzugefügt werden.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn Sie keinen Servernamen angeben, wird der lokale Server verwendet.|
mediatype:{Boot&#124;Install}|Gibt den Typ von Bildern hinzugefügt werden.|
|[/Skipverify]|Gibt an, dass die integritätsprüfung nicht für die Quelldatei des Abbilds ausgeführt wird, bevor das Bild hinzugefügt wird.|
|[/Name:<Name>]|Legt den Anzeigenamen des Images fest.|
|[/ Description:<Description>]|Legt die Beschreibung des Images fest.|
|[/Filename:<Filename>]|Gibt den neuen Dateinamen für die WIM-Datei an. Dadurch können Sie den Dateinamen der WIM-Datei ändern, wenn Sie das Abbild hinzufügen. Wenn kein Dateiname angegeben wird, wird der Dateiname des Quellabbilds verwendet werden. In allen Fällen überprüft Windows Deployment Services, um zu bestimmen, ob der Dateiname eindeutig, in den imagespeicher "Start" des Zielcomputers ist.|
|\mediaGroup:<Image group name>]|Gibt den Namen der Abbildgruppe in der die Bilder sind, hinzugefügt werden. Wenn mehr als eine Abbildgruppe auf dem Server vorhanden ist, muss die Abbildgruppe angegeben werden. Wenn Sie keine Abbildgruppe angeben und noch keine Abbildgruppe vorhanden ist, wird eine neue erstellt. Andernfalls wird die vorhandene Abbildgruppe verwendet.|
|[/ SingleImage:<Single image name>] [/ Name:<Name>] [/ Description:<Description>]|Kopiert das angegebene einzelne Bild aus einer WIM-Datei, und legt das Bild der Anzeigename und Beschreibung.|
|[/UnattendFile:<Unattend file path>]|Gibt den vollständigen Pfad zur Datei für die unbeaufsichtigte Installation mit den Bildern zugeordnet werden soll, die hinzugefügt werden. Wenn **/SingleImage** nicht angegeben ist, wird dieselbe Datei für die unbeaufsichtigte Installation werden alle Bilder in der WIM-Datei zugeordnet.|
## <a name="BKMK_examples"></a>Beispiele für
Um ein Startabbild hinzuzufügen, geben Sie Folgendes ein:
```
wdsutil /add-ImagmediaFile:"C:\MyFolder\Boot.wimmediatype:Boot
wdsutil /verbose /Progress /add-ImagmediaFile:\\MyServer\Share\Boot.wim /Server:MyWDSServemediatype:Boot /Name:"My WinPE Image" 
/Description:"WinPE Image containing the WDS Client" /Filename:WDSBoot.wim
```
Um ein Installationsabbild hinzufügen möchten, geben Sie eine der folgenden:
```
wdsutil /add-ImagmediaFile:"C:\MyFolder\Install.wimmediatype:Install
wdsutil /verbose /Progress /add-ImagmediaFile:\\MyServer\Share \Install.wim /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/SingleImage:"Windows Pro" /Name:"My WDS Image"
/Description:"Windows Pro image with Microsoft Office" /Filename:"Win Pro.wim" /UnattendFile:"\\server\share\unattend.xml"
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl-Kopieren-Image](using-the-copy-image-command.md)
[mithilfe des Export-Image-Befehls](using-the-export-image-command.md)
[mithilfe der Get-Image-Befehl](using-the-get-image-command.md)
[mit dem Remove-Image-Befehl](using-the-remove-image-command.md)
[mit dem Replace-Image-Befehl](using-the-replace-image-command.md) 
 [ Unterbefehl: Set-Image](subcommand-set-image.md)
