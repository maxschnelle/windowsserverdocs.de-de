---
title: typeperf
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c7ca89a-03b3-4626-afcf-ef8565e90043
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 087b201c51d5aec8e6f61c7469c59307d3ed8b4d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392297"
---
# <a name="typeperf"></a>typeperf



Mit dem Befehl **typeperf** werden Leistungsdaten in das Befehlsfenster oder in eine Protokolldatei geschrieben. Drücken Sie zum Abbrechen von **typeperf**STRG + C.

Beispiele für die Verwendung von **typeperf**finden Sie unter [Beispiele](#BKMK_EXAMPLES).

## <a name="syntax"></a>Syntax

```
typeperf <counter [counter ...]> [options]
typeperf -cf <filename> [options]
typeperf -q [object] [options]
typeperf -qx [object] [options]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Counter [...]] >|Gibt die zu überwachenden Leistungsindikatoren an.|

> [!NOTE]
> **\<Counter >** ist der vollständige Name eines Leistungs Zählers im *\\\\computer\object (Instance) \Counter* -Format, z. b. **\\\\Server1\Processor (0)\% Benutzer Zeit**.

## <a name="options"></a>Optionen

|                   Option                   |                                                         Beschreibung                                                          |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
|                     -?                     |                                               Zeigt die kontextbezogene Hilfe an.                                               |
| -f \<CSV&verbar;TSV&verbar;bin&verbar;SQL > |                                    Gibt das Format der Ausgabedatei an. Der Standardwert ist CSV.                                     |
|              -CF \<Dateiname >               |              Gibt eine Datei an, die eine Liste der zu überwachenden Leistungsindikatoren mit einem Zähler pro Zeile enthält.               |
|             -Si < [[hh:] mm:] SS >             |                                  Gibt das Stichproben Intervall an. Der Standardwert ist 1 Sekunde.                                   |
|               -o \<Dateiname >               |     Gibt den Pfad für die Ausgabedatei oder die SQL-Datenbank an. Der Standardwert ist stdout (in das Befehlsfenster geschrieben).      |
|                -q [Objekt]                 | Zeigt eine Liste installierter Leistungsindikatoren (keine Instanzen) an. Zum Auflisten der Zähler für ein Objekt fügen Sie den Objektnamen ein. \*\*\*Beispiel |
|                -QX [Objekt]                |        Zeigt eine Liste installierter Leistungsindikatoren mit Instanzen an. Zum Auflisten der Zähler für ein Objekt fügen Sie den Objektnamen ein.        |
|               -SC \<Beispiele >               |             Gibt die Anzahl der zu sammelnden Stichproben an. Der Standardwert ist das Sammeln von Daten, bis STRG + C gedrückt wird.              |
|            -config \<filename >             |                                    Gibt eine Einstellungsdatei an, die Befehlsoptionen enthält.                                     |
|            -s \<computer_name >             |                   Gibt einen Remote Computer an, der überwacht werden soll, wenn im Verbindungs Pfad kein Computer angegeben ist.                    |
|                     -y                     |                                        Antworten Sie auf Ja, um alle Fragen zu beantworten.                                        |

## <a name="BKMK_EXAMPLES"></a>Beispiele

- Im folgenden Beispiel werden die Werte für den Leistungsdaten Bereich des lokalen Computers **\\\\Prozessorzeit (_Total)\% Prozessorzeit** in das Befehlsfenster in einem standardmäßigen Stichproben Intervall von 1 Sekunde geschrieben, bis STRG + C gedrückt wird.  
  ```
  typeperf "\Processor(_Total)\% Processor Time"
  ```  
- Im folgenden Beispiel werden die Werte für die Liste der Leistungsindikatoren in der Datei **Counters. txt** in die durch Tabstopps getrennte Datei **Domäne2. TSV** in einem Stichproben Intervall von 5 Sekunden geschrieben, bis 50 Stichproben erfasst wurden.  
  ```
  typeperf -cf counters.txt -si 5 -sc 50 -f TSV -o domain2.tsv
  ```  
- Im folgenden Beispiel werden installierte Leistungsindikatoren mit Instanzen für das Leistungsindikator Objekt **PhysicalDisk** abgefragt und die resultierende Liste in die Datei " **Counters. txt**" geschrieben.  
  ```
  typeperf -qx PhysicalDisk -o counters.txt
  ```
