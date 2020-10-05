---
title: New-DiscoverImage
description: Referenz Artikel zu New-DiscoverImage, mit dem ein neues Ermittlungs Image aus einem vorhandenen Start Abbild erstellt wird.
ms.topic: reference
ms.assetid: ede9fbbb-0bba-4309-8c21-3cc13e1dc3cd
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: eada7c66b79450e4364d5c65854f0b4659cbde7c
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730197"
---
# <a name="new-discoverimage"></a>New-DiscoverImage

Erstellt ein neues Ermittlungs Image aus einem vorhandenen Start Abbild. Abbilder ermitteln sind Start Abbilder, die erzwingen, dass das Setup.exe Programm im Windows-Bereitstellungsdiensteserver gestartet wird Diese Images werden normalerweise verwendet, um Images auf Computern bereitzustellen, die nicht mit PXE gestartet werden können. Weitere Informationen finden Sie unter Erstellen von Images ( [https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311) ).

## <a name="syntax"></a>Syntax

```
WDSUTIL [Options] /New-DiscoverImage [/Server:<Server name>]
     /Image:<Image name>
     /Architecture:{x86 | ia64 | x64}
     [/Filename:<File name>]
     /DestinationImage
         /FilePath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
         [/WDSServer:<Server name>]
         [/Overwrite:{Yes | No | Append}]
```

### <a name="parameters"></a>Parameter

|        Parameter         |                                                                                                                                                                                                                                                                                                                                                                                                                       BESCHREIBUNG                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:\<Server name>] |                                                                                                                                                                                                                                                                                                                                     Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                                                                                                                                                                                                                                                     |
|   /Image:\<Image name>   |                                                                                                                                                                                                                                                                                                                                                                                                      Gibt den Namen des Quell Start Abbilds an.                                                                                                                                                                                                                                                                                                                                                                                                       |
|    /Architecture: {x86    |                                                                                                                                                                                                                                                                                                                                                                                                                          ia64                                                                                                                                                                                                                                                                                                                                                                                                                           |
| [/Filename:\<File name>] |                                                                                                                                                                                                                                                                                                                                                                         Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.                                                                                                                                                                                                                                                                                                                                                                          |
|    /DestinationImage     | Gibt die Einstellungen für das Ziel Image an. Sie können die Einstellungen mithilfe der folgenden Optionen angeben:</br>-/FilePath: < Dateipfad und-Name> den vollständigen Dateipfad für das neue Image fest.</br>-[/Name: \<Name> ]: legt den anzeigen amen des Bilds fest. Wenn kein Anzeige Name angegeben ist, wird der Anzeige Name des Quell Bilds verwendet.</br>-[/Description: \<Description> ]: legt die Beschreibung des Bilds fest.</br>-[/WDSServer: \<Server name> ]: gibt den Namen des Servers an, den alle Clients, die vom angegebenen Abbild starten, kontaktieren sollten, um das Installations Abbild herunterzuladen. Standardmäßig ermitteln alle Clients, die dieses Abbild starten, einen gültigen Windows-Bereitstellungsdiensteserver. Wenn Sie diese Option verwenden, wird die Ermittlungs Funktionalität umgangen, und der gestartete Client wird gezwungen, den angegebenen Server zu kontaktieren.</br>-[/Overwrite: {Yes |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Ermittlungs Image aus dem Startimage zu erstellen, und nennen Sie es winpdiscover. Wim:
```
WDSUTIL /New-DiscoverImage /Image:WinPE boot image /Architecture:x86 /DestinationImage /FilePath:C:\Temp\WinPEDiscover.wim
```
Geben Sie Folgendes ein, um ein Ermittlungs Image aus dem Startimage zu erstellen, und nennen Sie es winpdiscover. wim mit den angegebenen Einstellungen:
```
WDSUTIL /Verbose /Progress /New-DiscoverImage /Server:MyWDSServer
/Image:WinPE boot image /Architecture:x64 /Filename:boot.wim /DestinationImage /FilePath:\\Server\Share\WinPEDiscover.wim
/Name:New WinPE image /Description:WinPE image for WDS Client discovery /Overwrite:No
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)