---
title: New-DiscoverImage
description: Windows-Befehls Thema für New-DiscoverImage, das ein neues Ermittlungs Image aus einem vorhandenen Start Abbild erstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ede9fbbb-0bba-4309-8c21-3cc13e1dc3cd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f184d420e689faa687378e6843c48babdbf67690
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830703"
---
# <a name="new-discoverimage"></a>New-DiscoverImage

Erstellt ein neues Ermittlungs Image aus einem vorhandenen Start Abbild. Abbilder ermitteln sind Start Abbilder, die erzwingen, dass das Programm Setup. exe im Modus Windows-Bereitstellungs Dienste gestartet wird, und dann einen Windows-Bereitstellungsdiensteserver Diese Images werden normalerweise verwendet, um Images auf Computern bereitzustellen, die nicht mit PXE gestartet werden können. Weitere Informationen finden Sie unter Erstellen von Images ([https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311)).

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

|        Parameter         |                                                                                                                                                                                                                                                                                                                                                                                                                       Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:\<Server Name >] |                                                                                                                                                                                                                                                                                                                                     Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                                                                                                                                                                                                                                                     |
|   /Image:\<Bildname >   |                                                                                                                                                                                                                                                                                                                                                                                                      Gibt den Namen des Quell Start Abbilds an.                                                                                                                                                                                                                                                                                                                                                                                                       |
|    /Architecture: {x86    |                                                                                                                                                                                                                                                                                                                                                                                                                          ia64                                                                                                                                                                                                                                                                                                                                                                                                                           |
| [/Filename:\<Dateiname >] |                                                                                                                                                                                                                                                                                                                                                                         Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.                                                                                                                                                                                                                                                                                                                                                                          |
|    /DestinationImage     | Gibt die Einstellungen für das Ziel Image an. Sie können die Einstellungen mithilfe der folgenden Optionen angeben:</br>-/FilePath: < Dateipfad und-Name > den vollständigen Dateipfad für das neue Image fest.</br>-[/Name:\<Name >]: legt den anzeigen amen des Bilds fest. Wenn kein Anzeige Name angegeben ist, wird der Anzeige Name des Quell Bilds verwendet.</br>-[/Description: \<Description >]: legt die Beschreibung des Bilds fest.</br>-[/WDSServer: \<Server Name >]: gibt den Namen des Servers an, mit dem alle Clients, die vom angegebenen Abbild starten, eine Verbindung zum Herunterladen des Installations Images aufnehmen sollten. Standardmäßig ermitteln alle Clients, die dieses Abbild starten, einen gültigen Windows-Bereitstellungsdiensteserver. Wenn Sie diese Option verwenden, wird die Ermittlungs Funktionalität umgangen, und der gestartete Client wird gezwungen, den angegebenen Server zu kontaktieren.</br>-[/Overwrite: {Yes |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)