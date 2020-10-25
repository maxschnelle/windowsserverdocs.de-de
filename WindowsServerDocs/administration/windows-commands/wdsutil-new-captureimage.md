---
title: New-CaptureImage
description: Referenz Artikel für "New-CaptureImage", mit dem ein neues Erfassungs Image aus einem vorhandenen Start Abbild erstellt wird.
ms.topic: reference
ms.assetid: 2dfd08f0-be59-4715-96e6-c498305873f4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 28dfc8d64a1027eced15fb3d09a607a41535975c
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524345"
---
# <a name="new-captureimage"></a>New-CaptureImage

Erstellt ein neues Erfassungs Image aus einem vorhandenen Start Abbild. Aufzeichnungs Images sind Start Abbilder, mit denen das Erfassungs Hilfsprogramm der Windows-Bereitstellungs Dienste gestartet wird, anstatt Setup Wenn Sie einen Referenz Computer, der mit syunp vorbereitet wurde, in ein Aufzeichnungs Abbild starten, erstellt ein Assistent ein Installations Abbild des Referenz Computers und speichert es als Windows-Abbild Datei (WIM-Datei). Sie können das Image auch Medien hinzufügen (z. b. eine CD, DVD oder ein USB-Laufwerk) und dann einen Computer von diesem Medium aus starten. Nachdem Sie das Installations Abbild erstellt haben, können Sie das Abbild dem Server für die PXE-Start Bereitstellung hinzufügen. Weitere Informationen finden Sie unter Erstellen von Images ( [https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311) ).

## <a name="syntax"></a>Syntax

```
wdsutil [Options] /New-CaptureImage [/Server:<Server name>]
     /Image:<Image name>
     /Architecture:{x86 | ia64 | x64}
     [/Filename:<File name>]
     /DestinationImage
        /FilePath:<File path and name>
        [/Name:<Name>]
        [/Description:<Description>]
        [/Overwrite:{Yes | No | Append}]
        [/UnattendFilePath:<File path>]
```

### <a name="parameters"></a>Parameter

|        Parameter         |                                                                                                                                                                                                                         BESCHREIBUNG                                                                                                                                                                                                                          |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:\<Server name>] |                                                                                                                                       Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                                                        |
|   /Image:\<Image name>   |                                                                                                                                                                                                         Gibt den Namen des Quell Start Abbilds an.                                                                                                                                                                                                         |
|   /Architecture: {x86    |                                                                                                                                                                                                                             ia64                                                                                                                                                                                                                             |
| [/Filename: \<Filename> ] |                                                                                                                                                                            Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.                                                                                                                                                                            |
|    /DestinationImage     | Gibt die Einstellungen für das Ziel Image an. Sie geben die Einstellungen mithilfe der folgenden Optionen an:</br>-/FilePath: \<File path and name> legt den vollständigen Dateipfad für das neue Aufzeichnungs Abbild fest.</br>-[/Name: \<Name> ]: legt den anzeigen amen des Bilds fest. Wenn kein Anzeige Name angegeben ist, wird der Anzeige Name des Quell Bilds verwendet.</br>-[/Description: \<Description> ]: legt die Beschreibung des Bilds fest.</br>-[/Overwrite: {Yes |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Aufzeichnungs Abbild zu erstellen, und nennen Sie es winpecapture. Wim:
```
wdsutil /New-CaptureImage /Image:WinPE boot image /Architecture:x86 /DestinationImage /FilePath:C:\Temp\WinPECapture.wim
```
Geben Sie Folgendes ein, um ein Aufzeichnungs Abbild zu erstellen und die angegebenen Einstellungen anzuwenden:
```
wdsutil /Verbose /Progress /New-CaptureImage /Server:MyWDSServer /Image:WinPE boot image /Architecture:x64 /Filename:boot.wim
/DestinationImage /FilePath:\\Server\Share\WinPECapture.wim /Name:New WinPE image /Description:WinPE image with capture utility /Overwrite:No /UnattendFilePath:\\Server\Share\WDSCapture.inf
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)