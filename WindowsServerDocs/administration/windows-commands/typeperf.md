---
title: typeperf
description: Referenz Artikel zum typeperf-Befehl, der Leistungsdaten in das Befehlsfenster oder in eine Protokolldatei schreibt.
ms.topic: reference
ms.assetid: 0c7ca89a-03b3-4626-afcf-ef8565e90043
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6a06d422db5f681c3e1775facc4f8d0eee422244
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156358"
---
# <a name="typeperf"></a>typeperf

Mit dem Befehl **typeperf** werden Leistungsdaten in das Befehlsfenster oder in eine Protokolldatei geschrieben. Drücken Sie zum Abbrechen von **typeperf**STRG + C.

## <a name="syntax"></a>Syntax

```
typeperf <counter [counter ...]> [options]
typeperf -cf <filename> [options]
typeperf -q [object] [options]
typeperf -qx [object] [options]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<counter [counter […]]>` | Gibt die zu überwachenden Leistungsindikatoren an. Der- `<counter>` Parameter ist der vollständige Name eines Leistungs Zählers im \\ computer\object (Instance) \Counter-Format, z `\\Server1\Processor(0)\% User Time` . b..  |

#### <a name="options"></a>Optionen

| Option | BESCHREIBUNG |
|--|--|
| -f `<CSV | TSV | BIN | SQL>` | Gibt das Format der Ausgabedatei an. Der Standardwert ist CSV. |
| -CF `<filename>` | Gibt eine Datei an, die eine Liste der zu überwachenden Leistungsindikatoren mit einem Zähler pro Zeile enthält. |
| -Si `<[[hh:]mm:]ss>` | Gibt das Stichproben Intervall an. Der Standardwert ist 1 Sekunde. |
| -o `<filename>` | Gibt den Pfad für die Ausgabedatei oder die SQL-Datenbank an. Der Standardwert ist stdout (in das Befehlsfenster geschrieben). |
| -q `[object]` | Zeigt eine Liste installierter Leistungsindikatoren (keine Instanzen) an. Zum Auflisten der Zähler für ein Objekt fügen Sie den Objektnamen ein. Beispiel |
| -QX `[object]` | Zeigt eine Liste installierter Leistungsindikatoren mit Instanzen an. Zum Auflisten der Zähler für ein Objekt fügen Sie den Objektnamen ein. |
| -SC `<samples>` | Gibt die Anzahl der zu sammelnden Stichproben an. Der Standardwert ist das Sammeln von Daten, bis STRG + C gedrückt wird. |
| -config `<filename>` | Gibt eine Einstellungsdatei an, die Befehlsoptionen enthält. |
| -s `<computer_name>` | Gibt einen Remote Computer an, der überwacht werden soll, wenn im Verbindungs Pfad kein Computer angegeben ist. |
| -y | Antworten Sie auf *Ja* , um alle Fragen zu beantworten. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Werte für den Leistungs Bewert des lokalen Computers in `\Processor(_Total)\% Processor Time` das Befehlsfenster in einem standardmäßigen Stichproben Intervall von 1 Sekunde zu schreiben, bis STRG + C gedrückt ist.

```
typeperf \Processor(_Total)\% Processor Time
```

Wenn Sie die Werte für die Liste der Leistungsindikatoren in der Datei *counters.txt* in die durch Tabstopps getrennte Datei *Domäne2. TSV* in einem Stichproben Intervall von 5 Sekunden schreiben möchten, bis 50 Samplings erfasst wurden, geben Sie Folgendes ein:

```
typeperf -cf counters.txt -si 5 -sc 50 -f TSV -o domain2.tsv
```

Wenn Sie installierte Leistungsindikatoren mit Instanzen für das Leistungsindikator Objekt *PhysicalDisk* Abfragen und die resultierende Liste in die Datei *counters.txt*schreiben möchten, geben Sie Folgendes ein:

```
typeperf -qx PhysicalDisk -o counters.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
