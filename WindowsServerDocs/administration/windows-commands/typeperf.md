---
title: typeperf
description: Referenz Artikel für typeperf, der Leistungsdaten in das Befehlsfenster oder in eine Protokolldatei schreibt.
ms.topic: reference
ms.assetid: 0c7ca89a-03b3-4626-afcf-ef8565e90043
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b7c28b77bb374d8a7ece9163458cfd09418ca890
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626596"
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

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<counter [counter […]]>|Gibt die zu überwachenden Leistungsindikatoren an.|

> [!NOTE]
> **\<counter>** der vollständige Name eines Leistungs Zählers im * \\ \\ computer\object (Instance) \Counter* -Format, z. b. ** \\ \\ Server1\Processor (0) \% User Time**.

## <a name="options"></a>Tastatur

|                   Option                   |                                                         BESCHREIBUNG                                                          |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
|                     -?                     |                                               Zeigt die kontextbezogene Hilfe an.                                               |
| -f \<CSV&verbar;TSV&verbar;BIN&verbar;SQL> |                                    Gibt das Format der Ausgabedatei an. Der Standardwert ist CSV.                                     |
|              -CF \<filename>               |              Gibt eine Datei an, die eine Liste der zu überwachenden Leistungsindikatoren mit einem Zähler pro Zeile enthält.               |
|             -Si < [[hh:] mm:] SS>             |                                  Gibt das Stichproben Intervall an. Der Standardwert ist 1 Sekunde.                                   |
|               -o \<filename>               |     Gibt den Pfad für die Ausgabedatei oder die SQL-Datenbank an. Der Standardwert ist stdout (in das Befehlsfenster geschrieben).      |
|                -q [Objekt]                 | Zeigt eine Liste installierter Leistungsindikatoren (keine Instanzen) an. Zum Auflisten der Zähler für ein Objekt fügen Sie den Objektnamen ein. \*\*\*Beispiel |
|                -QX [Objekt]                |        Zeigt eine Liste installierter Leistungsindikatoren mit Instanzen an. Zum Auflisten der Zähler für ein Objekt fügen Sie den Objektnamen ein.        |
|               -SC \<samples>               |             Gibt die Anzahl der zu sammelnden Stichproben an. Der Standardwert ist das Sammeln von Daten, bis STRG + C gedrückt wird.              |
|            -config \<filename>             |                                    Gibt eine Einstellungsdatei an, die Befehlsoptionen enthält.                                     |
|            -s \<computer_name>             |                   Gibt einen Remote Computer an, der überwacht werden soll, wenn im Verbindungs Pfad kein Computer angegeben ist.                    |
|                     -y                     |                                        Antworten Sie auf Ja, um alle Fragen zu beantworten.                                        |

## <a name="examples"></a>Beispiele

- , Wenn die Werte für die Prozessorzeit des Leistungs Leistungs ** \\ \\ Prozessors (_Total \% )** des lokalen Computers in das Befehlsfenster in einem standardmäßigen Stichproben Intervall von 1 Sekunde geschrieben werden, bis STRG + C gedrückt wird.
  ```
  typeperf \Processor(_Total)\% Processor Time
  ```
- Um die Werte für die Liste der Leistungsindikatoren in der Datei **counters.txt** in die durch Tabstopps getrennte Datei **Domäne2. TSV** in einem Stichproben Intervall von 5 Sekunden zu schreiben, bis 50 Stichproben erfasst wurden.
  ```
  typeperf -cf counters.txt -si 5 -sc 50 -f TSV -o domain2.tsv
  ```
- , Wenn installierte Leistungsindikatoren mit Instanzen für das Leistungsindikator Objekt **PhysicalDisk** abgefragt und die resultierende Liste in die Datei **counters.txt**geschrieben wird.
  ```
  typeperf -qx PhysicalDisk -o counters.txt
  ```
