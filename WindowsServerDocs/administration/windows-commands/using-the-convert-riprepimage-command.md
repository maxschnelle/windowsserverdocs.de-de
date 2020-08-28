---
title: Convert-RiprepImage
description: Referenz Artikel zu Convert-RiprepImage, mit dem ein vorhandenes RIPrep-Image (Remote Installation Vorbereitungs Image) in das Windows-Abbild Format (WIM) konvertiert wird.
ms.topic: reference
ms.assetid: 88c2b96f-5947-4b64-9dcf-1946b3c013cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e9d9ec388a2f4cdd59bcf8c9b59abf8b6c5e3383
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038238"
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
| FilePath\<File path and name> |                                                                                                                                                                                                       Gibt den vollständigen Pfad und den Dateinamen der SIF-Datei an, die dem RIPrep-Image entspricht. Diese Datei wird in der Regel als Riprep. sif bezeichnet und befindet sich im Unterordner \Templates des Ordners, der das RIPrep-Image enthält.                                                                                                                                                                                                       |
|        /DestinationImage        | Gibt die Einstellungen für das Ziel Image mit den folgenden Optionen an.</br>-/FilePath: \<File path and name> legt den vollständigen Dateipfad für die neue Datei fest. Beispiel: **c:\temp\convert.wim**</br>-[/Name: \<Name> ]: legt den anzeigen amen des Bilds fest. Wenn kein Anzeige Name angegeben ist, wird der Anzeige Name des Quell Bilds verwendet.</br>-[/Description: \<Description> ]: legt die Beschreibung des Bilds fest.</br>-[/Inplace]: gibt an, dass die Konvertierung im ursprünglichen RIPrep-Image stattfinden soll, und nicht in einer Kopie des ursprünglichen Bilds. Dies ist das Standardverhalten.</br>-[/Overwrite: {Yes |

## <a name="examples"></a>Beispiele

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