---
title: Verwenden des Befehls Convert-RiprepImage
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88c2b96f-5947-4b64-9dcf-1946b3c013cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b0b5e75a4148359db5088e7ff60d29b8d157309d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363651"
---
# <a name="using-the-convert-riprepimage-command"></a>Verwenden des Befehls Convert-RiprepImage



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

## <a name="parameters"></a>Parameter

|            Parameter            |                                                                                                                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                                                                                                                |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /FilePath: \<dateipfad und-Name > |                                                                                                                                                                                                       Gibt den vollständigen Pfad und den Dateinamen der SIF-Datei an, die dem RIPrep-Image entspricht. Diese Datei wird in der Regel als Riprep. sif bezeichnet und befindet sich im Unterordner \Templates des Ordners, der das RIPrep-Image enthält.                                                                                                                                                                                                       |
|        /DestinationImage        | Gibt die Einstellungen für das Ziel Image mit den folgenden Optionen an.</br>-/FilePath: \<dateipfad und-Name >: legt den vollständigen Dateipfad für die neue Datei fest. Zum Beispiel: **C:\temp\convert.wim**</br>-[/Name: \<name >]: legt den anzeigen amen des Bilds fest. Wenn kein Anzeige Name angegeben ist, wird der Anzeige Name des Quell Bilds verwendet.</br>-[/Description: \<description >]: legt die Beschreibung des Bilds fest.</br>-[/Inplace]: gibt an, dass die Konvertierung im ursprünglichen RIPrep-Image stattfinden soll, und nicht in einer Kopie des ursprünglichen Bilds. Dies ist das Standardverhalten.</br>-[/Overwrite: {Yes |

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um das angegebene Riprep. sif-Image in Riprep. wim zu konvertieren:
```
WDSUTIL /Convert-RiPrepImage /FilePath:"R:\RemoteInstall\Setup\English
\Images\Win2k3.SP1\i386\Templates\riprep.sif" /DestinationImage
/FilePath:"C:\Temp\RIPREP.wim"
```
Wenn Sie das angegebene Riprep. sif-Image mit dem angegebenen Namen und der Beschreibung in Riprep. WIM konvertieren und es mit der neuen Datei überschreiben möchten, wenn bereits eine Datei vorhanden ist, geben Sie Folgendes ein:
```
WDSUTIL /Verbose /Progress /Convert-RiPrepImage /FilePath:"\\Server
\RemInst\Setup\English\Images\WinXP.SP2\i386\Templates\riprep.sif"
/DestinationImage /FilePath:"\\Server\Share\RIPREP.wim"
/Name:"WindowsXP image" /Description:"Converted RIPREP image of WindowsXP"
/Overwrite:Append
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)