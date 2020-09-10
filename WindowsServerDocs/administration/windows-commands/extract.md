---
title: extract
description: Referenz Artikel für den Extract-Befehl, mit dem Dateien aus einem Quell Speicherort extrahiert werden.
ms.topic: reference
ms.assetid: 20dab03e-f6e1-4eb8-b8a1-fd6f1d97ee83
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 38d73bb18c210c27859add9a419adedfb4fecac4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627667"
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

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| KEs | Verwenden Sie, wenn Sie zwei oder mehr Dateien extrahieren möchten. |
| filename | Der Name der Datei, die aus der CAB-Datei extrahiert werden soll. Platzhalter und mehrere Dateinamen (durch Leerzeichen getrennt) können verwendet werden. |
| source | Komprimierte Datei (eine CAB-Datei mit nur einer Datei). |
| newname | Neuer Dateiname für die extrahierte Datei. Wenn kein Wert angegeben wird, wird der ursprüngliche Name verwendet. |
| /a | Alle Schränke verarbeiten. Folgt der CAB-Kette, beginnend mit dem ersten beschriebenen CAB. |
| /C | Kopieren Sie die Quelldatei in das Ziel (zum Kopieren von DMF-Datenträgern). |
| /d | CAB-Verzeichnis anzeigen (mit Dateiname verwenden, um Extract zu vermeiden). |
| /e | Extrahieren (verwenden Sie anstelle von *.* zum Extrahieren aller Dateien). |
| /l dir | Speicherort für extrahierte Dateien (Standardwert ist Aktuelles Verzeichnis). |
| /y | Vor dem Überschreiben einer vorhandenen Datei wird keine Aufforderung angezeigt. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
