---
title: Mithilfe des neuen DiscoverImage-Befehls
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 4a017e3090ec05bbcd7984e630cdb3670a35bd27
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440423"
---
# <a name="using-the-new-discoverimage-command"></a>Mithilfe des neuen DiscoverImage-Befehls



erstellt ein neues Discover-Image aus einem vorhandenen Startabbild an. Ermitteln Sie, dass Abbilder Startabbilder werden, die erzwingen, das Programm "Setup.exe dass" im Windows-bereitstellungsdienstemodus zu starten, und klicken Sie dann zu einen Windows-Bereitstellungsdiensteserver ermitteln. Diese Images werden in der Regel verwendet, zum Bereitstellen von Images auf Computern, die nicht in PXE gestartet werden kann. Weitere Informationen finden Sie unter Erstellen von Images ([https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311)).

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
| [/ Server:\<Servername >] |                                                                                                                                                                                                                                                                                                                                     Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.                                                                                                                                                                                                                                                                                                                                     |
|   / Image:\<Image-Name >   |                                                                                                                                                                                                                                                                                                                                                                                                      Gibt den Namen des Startabbilds Quelle.                                                                                                                                                                                                                                                                                                                                                                                                       |
|    / Architecture: {X86    |                                                                                                                                                                                                                                                                                                                                                                                                                          ia64                                                                                                                                                                                                                                                                                                                                                                                                                           |
| [/ Filename:\<Dateiname >] |                                                                                                                                                                                                                                                                                                                                                                         Wenn das Bild kann nicht eindeutig anhand des Namens identifiziert werden, müssen Sie diese Option verwenden, um den Dateinamen angeben.                                                                                                                                                                                                                                                                                                                                                                          |
|    /DestinationImage     | Gibt die Einstellungen für das Zielabbild. Sie können die Einstellungen, die mithilfe der folgenden Optionen angeben:</br>-Destinationimage/FilePath: < Datei Pfad und Name > - Sets vollständigen Dateipfad für das neue Image.</br>-[/ Name:\<Name >]-legt den Anzeigenamen des Images fest. Wenn kein Anzeigename angegeben wird, wird der Anzeigename des Quellbilds verwendet werden.</br>-[/ Description: \<Beschreibung >]-legt die Beschreibung des Images fest.</br>-[/ WDSServer: \<Servername >]: Gibt den Namen des Servers, die alle Clients, die aus dem angegebenen Bild starten kontaktieren sollte, um das Installationsabbild herunterzuladen. Standardmäßig werden alle Clients, die diesem Abbild starten einen gültigen Windows-Bereitstellungsdienste-Server feststellen. Mit dieser Option umgangen, das die ermittlungsfunktionalität und zwingt den Client gestarteten, mit dem angegebenen Server herzustellen.</br>-[/ Overwrite: {Yes |

## <a name="BKMK_examples"></a>Beispiele für

Zum Erstellen von ein Suchabbild der Out-of Startabbild, und nennen Sie sie WinPEDiscover.wim, geben Sie Folgendes ein:
```
WDSUTIL /New-DiscoverImage /Image:"WinPE boot image" /Architecture:x86 /DestinationImage /FilePath:"C:\Temp\WinPEDiscover.wim"
```
Erstellen ein Suchabbild der Out-of Startabbild, und nennen Sie sie WinPEDiscover.wim mit den angegebenen Einstellungen, geben Sie Folgendes ein:
```
WDSUTIL /Verbose /Progress /New-DiscoverImage /Server:MyWDSServer
/Image:"WinPE boot image" /Architecture:x64 /Filename:boot.wim /DestinationImage /FilePath:"\\Server\Share\WinPEDiscover.wim" 
/Name:"New WinPE image" /Description:"WinPE image for WDS Client discovery" /Overwrite:No
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)