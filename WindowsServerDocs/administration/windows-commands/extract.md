---
title: extract
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 967f08e271019cc33970419179c9ddbf902b1882
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377258"
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
|KEs|Die Datei enthält mindestens zwei Dateien.|
|Dateiname|Der Name der Datei, die aus der CAB-Datei extrahiert werden soll. Platzhalter und mehrere Dateinamen (durch Leerzeichen getrennt) können verwendet werden.|
|Quelle|Komprimierte Datei (eine CAB-Datei mit nur einer Datei).|
|newname|Neuer Dateiname für die extrahierte Datei. Wenn kein Wert angegeben wird, wird der ursprüngliche Name verwendet.|
|/A|Alle Schränke verarbeiten. Folgt der CAB-Kette, beginnend mit dem ersten beschriebenen CAB.|
|/C|Kopieren Sie die Quelldatei in das Ziel (zum Kopieren von DMF-Datenträgern).|
|/D|CAB-Verzeichnis anzeigen (mit Dateiname verwenden, um Extract zu vermeiden).|
|/E|Extrahieren (verwenden Sie anstelle von *.* zum Extrahieren aller Dateien).|
|/L dir|Speicherort für extrahierte Dateien (Standardwert ist Aktuelles Verzeichnis).|
|/Y|Keine Eingabeaufforderung, bevor eine vorhandene Datei überschrieben wird.|

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)