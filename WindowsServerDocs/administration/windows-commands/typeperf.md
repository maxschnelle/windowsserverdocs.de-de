---
title: typeperf
description: Referenz Thema für typeperf, das Leistungsdaten in das Befehlsfenster oder in eine Protokolldatei schreibt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0c7ca89a-03b3-4626-afcf-ef8565e90043
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a996abc1417fdb6aa50370a942433716d8df2cbe
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721209"
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
|\<Counter [Counter [...]] >|Gibt die zu überwachenden Leistungsindikatoren an.|

> [!NOTE]
> Counter>der vollständige Name eines Leistungs Zählers im * \\ \\computer\object (Instance) \Counter* -Format, z ** \\ \\. b. Server1\Processor\% (0) User Time**. ** \<**

## <a name="options"></a>Optionen

|                   Option                   |                                                         BESCHREIBUNG                                                          |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
|                     -?                     |                                               Zeigt die kontextbezogene Hilfe an.                                               |
| -f \<CSV&verbar;TSV&verbar;bin&verbar;SQL> |                                    Gibt das Format der Ausgabedatei an. Der Standardwert ist CSV.                                     |
|              -CF \<filename>               |              Gibt eine Datei an, die eine Liste der zu überwachenden Leistungsindikatoren mit einem Zähler pro Zeile enthält.               |
|             -Si < [[hh:] mm:] SS>             |                                  Gibt das Stichproben Intervall an. Der Standardwert ist 1 Sekunde.                                   |
|               -o \<Dateiname>               |     Gibt den Pfad für die Ausgabedatei oder die SQL-Datenbank an. Der Standardwert ist stdout (in das Befehlsfenster geschrieben).      |
|                -q [Objekt]                 | Zeigt eine Liste installierter Leistungsindikatoren (keine Instanzen) an. Zum Auflisten der Zähler für ein Objekt fügen Sie den Objektnamen ein. \*\*\*Beispiel |
|                -QX [Objekt]                |        Zeigt eine Liste installierter Leistungsindikatoren mit Instanzen an. Zum Auflisten der Zähler für ein Objekt fügen Sie den Objektnamen ein.        |
|               -SC \<-Beispiele>               |             Gibt die Anzahl der zu sammelnden Stichproben an. Der Standardwert ist das Sammeln von Daten, bis STRG + C gedrückt wird.              |
|            -Konfigurations \<Dateiname>             |                                    Gibt eine Einstellungsdatei an, die Befehlsoptionen enthält.                                     |
|            -s \<computer_name>             |                   Gibt einen Remote Computer an, der überwacht werden soll, wenn im Verbindungs Pfad kein Computer angegeben ist.                    |
|                     -y                     |                                        Antworten Sie auf Ja, um alle Fragen zu beantworten.                                        |

## <a name="examples"></a>Beispiele

- , Wenn die Werte für die Prozessorzeit des Leistungs Leistungs ** \\ \\Prozessors (_Total\% )** des lokalen Computers in das Befehlsfenster in einem standardmäßigen Stichproben Intervall von 1 Sekunde geschrieben werden, bis STRG + C gedrückt wird.  
  ```
  typeperf \Processor(_Total)\% Processor Time
  ```  
- , Um die Werte für die Liste der Leistungsindikatoren in der Datei **Counters. txt** in die durch Tabstopps getrennte Datei **Domäne2. TSV** in einem Stichproben Intervall von 5 Sekunden zu schreiben, bis 50 Stichproben erfasst wurden.  
  ```
  typeperf -cf counters.txt -si 5 -sc 50 -f TSV -o domain2.tsv
  ```  
- , Wenn installierte Leistungsindikatoren mit Instanzen für das Leistungsindikator Objekt **PhysicalDisk** abgefragt und die resultierende Liste in die Datei " **Counters. txt**" geschrieben wird.  
  ```
  typeperf -qx PhysicalDisk -o counters.txt
  ```
