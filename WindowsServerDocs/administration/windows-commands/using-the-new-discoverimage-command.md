---
title: New-DiscoverImage
description: Referenz Thema für "New-DiscoverImage", mit dem ein neues Ermittlungs Image aus einem vorhandenen Start Abbild erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ede9fbbb-0bba-4309-8c21-3cc13e1dc3cd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45202f2bde3ca045a27e604743c25659df2436f9
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725797"
---
# <a name="new-discoverimage"></a>New-DiscoverImage

Erstellt ein neues Ermittlungs Image aus einem vorhandenen Start Abbild. Abbilder ermitteln sind Start Abbilder, die erzwingen, dass das Programm Setup. exe im Modus Windows-Bereitstellungs Dienste gestartet wird, und dann einen Windows-Bereitstellungsdiensteserver Diese Images werden normalerweise verwendet, um Images auf Computern bereitzustellen, die nicht mit PXE gestartet werden können. Weitere Informationen finden Sie unter Erstellen von Images[https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311)().

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
| [/Server:\<Server Name>] |                                                                                                                                                                                                                                                                                                                                     Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                                                                                                                                                                                                                                                     |
|   /Image:\<Bildname>   |                                                                                                                                                                                                                                                                                                                                                                                                      Gibt den Namen des Quell Start Abbilds an.                                                                                                                                                                                                                                                                                                                                                                                                       |
|    /Architecture: {x86    |                                                                                                                                                                                                                                                                                                                                                                                                                          ia64                                                                                                                                                                                                                                                                                                                                                                                                                           |
| [/Filename:\<Dateiname>] |                                                                                                                                                                                                                                                                                                                                                                         Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.                                                                                                                                                                                                                                                                                                                                                                          |
|    /DestinationImage     | Gibt die Einstellungen für das Ziel Image an. Sie können die Einstellungen mithilfe der folgenden Optionen angeben:</br>-/FilePath: < Dateipfad und-Name> den vollständigen Dateipfad für das neue Image fest.</br>-[/Name:\<Name>]: legt den anzeigen amen des Bilds fest. Wenn kein Anzeige Name angegeben ist, wird der Anzeige Name des Quell Bilds verwendet.</br>-[/Description: \<Description>]: legt die Beschreibung des Bilds fest.</br>-[/WDSServer: \<Server Name>]: gibt den Namen des Servers an, mit dem alle Clients, die vom angegebenen Abbild starten, eine Verbindung zum Herunterladen des Installations Images aufnehmen sollten. Standardmäßig ermitteln alle Clients, die dieses Abbild starten, einen gültigen Windows-Bereitstellungsdiensteserver. Wenn Sie diese Option verwenden, wird die Ermittlungs Funktionalität umgangen, und der gestartete Client wird gezwungen, den angegebenen Server zu kontaktieren.</br>-[/Overwrite: {Yes |

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