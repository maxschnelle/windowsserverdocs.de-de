---
title: extract
description: Referenz Thema für den Extract-Befehl, mit dem Dateien aus einem Quell Speicherort extrahiert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 20dab03e-f6e1-4eb8-b8a1-fd6f1d97ee83
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dbadcc555fc9bb0b02e568b1126a317a9d59d336
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437185"
---
# <a name="extract"></a>extract

Extrahiert Dateien aus einer CAB-Datei oder einer Quelle.

## <a name="syntax"></a>Syntax

```
extract [/y] [/a] [/d | /e] [/l dir] cabinet [filename ...]
extract [/y] source [newname]
extract [/y] /c source destination
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| KEs | Verwenden Sie, wenn Sie zwei oder mehr Dateien extrahieren möchten. |
| filename | Der Name der Datei, die aus der CAB-Datei extrahiert werden soll. Platzhalter und mehrere Dateinamen (durch Leerzeichen getrennt) können verwendet werden. |
| Quelle | Komprimierte Datei (eine CAB-Datei mit nur einer Datei). |
| newname | Neuer Dateiname für die extrahierte Datei. Wenn kein Wert angegeben wird, wird der ursprüngliche Name verwendet. |
| /a | Alle Schränke verarbeiten. Folgt der CAB-Kette, beginnend mit dem ersten beschriebenen CAB. |
| /C | Kopieren Sie die Quelldatei in das Ziel (zum Kopieren von DMF-Datenträgern). |
| /d | CAB-Verzeichnis anzeigen (mit Dateiname verwenden, um Extract zu vermeiden). |
| /e | Extrahieren (verwenden Sie anstelle von *.* zum Extrahieren aller Dateien). |
| /l dir | Speicherort für extrahierte Dateien (Standardwert ist Aktuelles Verzeichnis). |
| /y | Vor dem Überschreiben einer vorhandenen Datei wird keine Aufforderung angezeigt. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
