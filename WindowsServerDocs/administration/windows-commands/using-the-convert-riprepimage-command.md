---
title: Mithilfe des Convert-RiprepImage-Befehls
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: cf5fffdedbc25ad97e9e96a84d3ff1bbdaf87b2a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835051"
---
# <a name="using-the-convert-riprepimage-command"></a>Mithilfe des Convert-RiprepImage-Befehls



Ein vorhandenes zur Vorbereitung der Remoteinstallation (RIPrep)-Image konvertiert in Windows-Abbild (WIM)-Format.

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

|Parameter|Beschreibung|
|---------|-----------|
|/ %FilePath:\<Dateipfad und >|Gibt den vollständigen Pfad und Namen der .sif-Datei, die das RIPrep-Abbild entspricht. Diese Datei wird in der Regel Riprep.sif aufgerufen und befindet sich im \Templates Unterordner des Ordners, der die RIPrep-Abbild enthält.|
|/DestinationImage|Gibt die Einstellungen für das Zielabbild mithilfe der folgenden Optionen.</br>-Destinationimage/FilePath:\<Dateipfad und >: Legt den vollständigen Pfad für die neue Datei. Zum Beispiel: **C:\Temp\convert.wim**</br>-[/ Name:\<Name >]-legt den Anzeigenamen des Images fest. Wenn kein Anzeigename angegeben wird, wird der Anzeigename des Quellbilds verwendet werden.</br>-[/ Description: \<Beschreibung >]-legt die Beschreibung des Images fest.</br>-[/InPlace]: Gibt an, dass die Konvertierung ausgeführt werden soll, auf das ursprüngliche RIPrep-Abbild und nicht auf eine Kopie des ursprünglichen Bilds, die das Standardverhalten ist.</br>-[/ Overwrite: {Yes | Nein | Append}] – bestimmt, ob die angegebene Datei in die **/DestinationImage** Option überschrieben werden sollen, wenn eine vorhandene Datei mit diesem Namen bereits am destinationimage/FilePath vorhanden ist. **Ja** überschreibt die vorhandene Datei. **Keine** (Standard) führt dazu, dass einen Fehler auftreten, wenn eine andere Datei mit dem gleichen Namen ist bereits vorhanden. **Fügen Sie** das generierte Bild als ein neues Image innerhalb der vorhandenen WIM-Datei angefügt.|

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie Folgendes ein, um das angegebene RIPrep.sif Bild in RIPREP.wim zu konvertieren:
```
WDSUTIL /Convert-RiPrepImage /FilePath:"R:\RemoteInstall\Setup\English
\Images\Win2k3.SP1\i386\Templates\riprep.sif" /DestinationImage
/FilePath:"C:\Temp\RIPREP.wim"
```
Um das angegebene RIPrep.sif Bild in RIPREP.wim konvertieren, mit dem angegebenen Namen und Beschreibung, und mit der neuen Datei zu überschreiben, wenn eine Datei bereits vorhanden ist, geben Sie Folgendes ein:
```
WDSUTIL /Verbose /Progress /Convert-RiPrepImage /FilePath:"\\Server
\RemInst\Setup\English\Images\WinXP.SP2\i386\Templates\riprep.sif"
/DestinationImage /FilePath:"\\Server\Share\RIPREP.wim"
/Name:"WindowsXP image" /Description:"Converted RIPREP image of WindowsXP"
/Overwrite:Append
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)