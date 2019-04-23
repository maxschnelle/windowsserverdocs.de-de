---
title: extract
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 20dab03e-f6e1-4eb8-b8a1-fd6f1d97ee83
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9113c34b61b98fb738bc0aff03193ab73b1abbd7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882311"
---
# <a name="extract"></a>extract



## <a name="syntax"></a>Syntax

```
EXTRACT [/Y] [/A] [/D | /E] [/L dir] cabinet [filename ...]
EXTRACT [/Y] source [newname]
EXTRACT [/Y] /C source destination
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|CAB-|Datei enthält zwei oder mehr Dateien.|
|Dateiname|Der Name der Datei, die aus der CAB-Datei zu extrahieren. Platzhalter und mehrere Dateinamen (getrennt durch Leerzeichen) können verwendet werden.|
|Quelle|Komprimierte Datei (CAB-Datei mit nur einer Datei).|
|Neuer Name|Neuen Dateinamen für die extrahierte Datei ein. Wenn nicht angegeben, wird der ursprüngliche Name verwendet.|
|/A|ALLE CAB-Dateien zu verarbeiten. Resultiert aus CAB-Kette genannten ersten CAB-Datei ab.|
|/C|Kopieren Sie Quelldatei, in Ziel (in der DMF-Datenträger zu kopieren).|
|/D|Zeigen Sie die CAB-Verzeichnis (verwenden Sie mit dem Dateinamen, extrahieren zu vermeiden).|
|/E|Extrahieren (verwenden Sie anstelle von *.* Um alle Dateien zu extrahieren).|
|/ L dir|Speicherort, um die extrahierten Dateien ablegen (der Standardwert ist aktuelles Verzeichnis).|
|/ Y|Vor dem Überschreiben einer vorhandenen Datei keine Aufforderung.|

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)