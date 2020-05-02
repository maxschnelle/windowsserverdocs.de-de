---
title: extract
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 20dab03e-f6e1-4eb8-b8a1-fd6f1d97ee83
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1cca89a356530e49fbf2b0610ff3ced1c5733847
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725658"
---
# <a name="extract"></a>extract



## <a name="syntax"></a>Syntax

```
EXTRACT [/Y] [/A] [/D | /E] [/L dir] cabinet [filename ...]
EXTRACT [/Y] source [newname]
EXTRACT [/Y] /C source destination
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|KEs|Die Datei enthält mindestens zwei Dateien.|
|filename|Der Name der Datei, die aus der CAB-Datei extrahiert werden soll. Platzhalter und mehrere Dateinamen (durch Leerzeichen getrennt) können verwendet werden.|
|source|Komprimierte Datei (eine CAB-Datei mit nur einer Datei).|
|newname|Neuer Dateiname für die extrahierte Datei. Wenn kein Wert angegeben wird, wird der ursprüngliche Name verwendet.|
|/A|Alle Schränke verarbeiten. Folgt der CAB-Kette, beginnend mit dem ersten beschriebenen CAB.|
|/C|Kopieren Sie die Quelldatei in das Ziel (zum Kopieren von DMF-Datenträgern).|
|/D|CAB-Verzeichnis anzeigen (mit Dateiname verwenden, um Extract zu vermeiden).|
|/E|Extrahieren (verwenden Sie anstelle von *.* zum Extrahieren aller Dateien).|
|/L dir|Speicherort für extrahierte Dateien (Standardwert ist Aktuelles Verzeichnis).|
|/Y|Keine Eingabeaufforderung, bevor eine vorhandene Datei überschrieben wird.|

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)