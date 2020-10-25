---
title: Convert-RiprepImage
description: Referenz Artikel für den Befehl Convert-RiprepImage, mit dem ein vorhandenes RIPrep-Image (Remoteinstallations Vorbereitung) in ein Windows-Abbild Format (WIM) konvertiert wird.
ms.topic: reference
ms.assetid: 88c2b96f-5947-4b64-9dcf-1946b3c013cf
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4062aa747bd02956a498c16c9e8aa15e96d8170d
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524925"
---
# <a name="convert-riprepimage"></a>Convert-RiprepImage

Konvertiert ein vorhandenes RIPrep-Image (Remote Installation Preparation) in ein Windows-Abbild Format (WIM).

## <a name="syntax"></a>Syntax

```
wdsutil [Options] /Convert-RIPrepImage /FilePath:<Filepath and name> /DestinationImage /FilePath:<Filepath and name> [/Name:<Name>] [/Description:<Description>] [/InPlace] [/Overwrite:{Yes | No | Append}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| FilePath`<Filepath and name>` | Gibt den vollständigen Datei Pfad und den Namen der SIF-Datei an, die dem RIPrep-Image entspricht. Diese Datei wird in der Regel als Riprep. sif bezeichnet und befindet sich im Unterordner **\Templates** des Ordners, der das RIPrep-Image enthält. |
| /DestinationImage | Gibt die Einstellungen für das Ziel Image an.  Verwendet die folgenden Optionen:<ul><li>`/FilePath:<Filepath and name>` : Legt den vollständigen Dateipfad für die neue Datei fest. Beispiel: **c:\temp\convert.wim**</li><li>[ `/Name:<Name>` ]: Legt den anzeigen amen des Bilds fest. Wenn kein Anzeige Name angegeben ist, wird der Anzeige Name des Quell Bilds verwendet.</li><li>[ `/Description:<Description>` ]: Legt die Beschreibung des Bilds fest.</li><li>[/Inplace]: gibt an, dass die Konvertierung im ursprünglichen RIPrep-Image und nicht in einer Kopie des ursprünglichen Bilds stattfinden soll. Dies ist das Standardverhalten.</li><li>[ `/Overwrite:{Yes | No | Append}` : Legt fest, ob dieses Bild vorhandene Dateien überschreiben oder anfügen soll.</li></ul> |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das angegebene Riprep. sif-Image in Riprep. wim zu konvertieren:

```
wdsutil /Convert-RiPrepImage /FilePath:R:\RemoteInstall\Setup\English \Images\Win2k3.SP1\i386\Templates\riprep.sif /DestinationImage /FilePath:C:\Temp\RIPREP.wim
```

Wenn Sie das angegebene Riprep. sif-Image mit dem angegebenen Namen und der Beschreibung in Riprep. WIM konvertieren und es mit der neuen Datei überschreiben möchten, wenn bereits eine Datei vorhanden ist, geben Sie Folgendes ein:

```
wdsutil /Verbose /Progress /Convert-RiPrepImage /FilePath:\\Server \RemInst\Setup\English\Images\WinXP.SP2\i386\Templates\riprep.sif /DestinationImage /FilePath:\\Server\Share\RIPREP.wim /Name:WindowsXP image /Description:Converted RIPREP image of WindowsXP /Overwrite:Append
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
