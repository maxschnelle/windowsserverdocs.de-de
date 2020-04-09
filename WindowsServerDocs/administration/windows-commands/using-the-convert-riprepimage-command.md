---
title: Convert-RiprepImage
description: Windows-Befehls Thema für Convert-RiprepImage, das ein vorhandenes Image für die Remoteinstallations Vorbereitung (RIPrep) in ein Windows-Abbild Format (WIM) konvertiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 88c2b96f-5947-4b64-9dcf-1946b3c013cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 01e33580a6d2da55df15fabde70697c22f894f7c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831813"
---
# <a name="convert-riprepimage"></a>Convert-RiprepImage

Konvertiert ein vorhandenes RIPrep-Image (Remote Installation Preparation) in ein Windows-Abbild Format (WIM).

## <a name="syntax"></a>Syntax

```
WDSUTIL [Options] /Convert-RIPrepImage /FilePath:<File path and name>
     /DestinationImage
         /FilePath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
         [/InPlace]
         [/Overwrite:{Yes | No | Append}]
```

### <a name="parameters"></a>Parameter

|            Parameter            |                                                                                                                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                                                                                                                |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /FilePath:\<Dateipfad und-Name > |                                                                                                                                                                                                       Gibt den vollständigen Pfad und den Dateinamen der SIF-Datei an, die dem RIPrep-Image entspricht. Diese Datei wird in der Regel als Riprep. sif bezeichnet und befindet sich im Unterordner \Templates des Ordners, der das RIPrep-Image enthält.                                                                                                                                                                                                       |
|        /DestinationImage        | Gibt die Einstellungen für das Ziel Image mit den folgenden Optionen an.</br>-/FilePath:\<Dateipfad und-Name > legt den vollständigen Dateipfad für die neue Datei fest. Beispiel: **c:\temp\convert.wim**</br>-[/Name:\<Name >]: legt den anzeigen amen des Bilds fest. Wenn kein Anzeige Name angegeben ist, wird der Anzeige Name des Quell Bilds verwendet.</br>-[/Description: \<Description >]: legt die Beschreibung des Bilds fest.</br>-[/Inplace]: gibt an, dass die Konvertierung im ursprünglichen RIPrep-Image stattfinden soll, und nicht in einer Kopie des ursprünglichen Bilds. Dies ist das Standardverhalten.</br>-[/Overwrite: {Yes |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um das angegebene Riprep. sif-Image in Riprep. wim zu konvertieren:
```
WDSUTIL /Convert-RiPrepImage /FilePath:R:\RemoteInstall\Setup\English
\Images\Win2k3.SP1\i386\Templates\riprep.sif /DestinationImage
/FilePath:C:\Temp\RIPREP.wim
```
Wenn Sie das angegebene Riprep. sif-Image mit dem angegebenen Namen und der Beschreibung in Riprep. WIM konvertieren und es mit der neuen Datei überschreiben möchten, wenn bereits eine Datei vorhanden ist, geben Sie Folgendes ein:
```
WDSUTIL /Verbose /Progress /Convert-RiPrepImage /FilePath:\\Server
\RemInst\Setup\English\Images\WinXP.SP2\i386\Templates\riprep.sif
/DestinationImage /FilePath:\\Server\Share\RIPREP.wim
/Name:WindowsXP image /Description:Converted RIPREP image of WindowsXP
/Overwrite:Append
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)