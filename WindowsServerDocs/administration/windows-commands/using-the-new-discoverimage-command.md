---
title: Verwenden des Befehls "New-DiscoverImage"
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ede9fbbb-0bba-4309-8c21-3cc13e1dc3cd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b17777eb4d8541ce5669ee6becbd51e2b9da236
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362987"
---
# <a name="using-the-new-discoverimage-command"></a>Verwenden des Befehls "New-DiscoverImage"



Erstellt ein neues Ermittlungs Image aus einem vorhandenen Start Abbild. Abbilder ermitteln sind Start Abbilder, die erzwingen, dass das Programm Setup. exe im Modus Windows-Bereitstellungs Dienste gestartet wird, und dann einen Windows-Bereitstellungsdiensteserver Diese Images werden normalerweise verwendet, um Images auf Computern bereitzustellen, die nicht mit PXE gestartet werden können. Weitere Informationen finden Sie unter Erstellen von Bildern ([https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311)).

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

## <a name="parameters"></a>Parameter

|        Parameter         |                                                                                                                                                                                                                                                                                                                                                                                                                       Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server: \<Server Name >] |                                                                                                                                                                                                                                                                                                                                     Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                                                                                                                                                                                                                                                     |
|   /Image: \<bildname >   |                                                                                                                                                                                                                                                                                                                                                                                                      Gibt den Namen des Quell Start Abbilds an.                                                                                                                                                                                                                                                                                                                                                                                                       |
|    /Architecture: {x86    |                                                                                                                                                                                                                                                                                                                                                                                                                          ia64                                                                                                                                                                                                                                                                                                                                                                                                                           |
| [/Filename: \<dateiname >] |                                                                                                                                                                                                                                                                                                                                                                         Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.                                                                                                                                                                                                                                                                                                                                                                          |
|    /DestinationImage     | Gibt die Einstellungen für das Ziel Image an. Sie können die Einstellungen mithilfe der folgenden Optionen angeben:</br>-/FilePath: < Dateipfad und-Name > den vollständigen Dateipfad für das neue Image fest.</br>-[/Name: \<name >]: legt den anzeigen amen des Bilds fest. Wenn kein Anzeige Name angegeben ist, wird der Anzeige Name des Quell Bilds verwendet.</br>-[/Description: \<description >]: legt die Beschreibung des Bilds fest.</br>-[/WDSServer: \<Server Name >]: gibt den Namen des Servers an, den alle Clients, die vom angegebenen Abbild starten, kontaktieren sollten, um das Installations Abbild herunterzuladen. Standardmäßig ermitteln alle Clients, die dieses Abbild starten, einen gültigen Windows-Bereitstellungsdiensteserver. Wenn Sie diese Option verwenden, wird die Ermittlungs Funktionalität umgangen, und der gestartete Client wird gezwungen, den angegebenen Server zu kontaktieren.</br>-[/Overwrite: {Yes |

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um ein Ermittlungs Image aus dem Startimage zu erstellen, und nennen Sie es winpdiscover. Wim:
```
WDSUTIL /New-DiscoverImage /Image:"WinPE boot image" /Architecture:x86 /DestinationImage /FilePath:"C:\Temp\WinPEDiscover.wim"
```
Geben Sie Folgendes ein, um ein Ermittlungs Image aus dem Startimage zu erstellen, und nennen Sie es winpdiscover. wim mit den angegebenen Einstellungen:
```
WDSUTIL /Verbose /Progress /New-DiscoverImage /Server:MyWDSServer
/Image:"WinPE boot image" /Architecture:x64 /Filename:boot.wim /DestinationImage /FilePath:"\\Server\Share\WinPEDiscover.wim" 
/Name:"New WinPE image" /Description:"WinPE image for WDS Client discovery" /Overwrite:No
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)