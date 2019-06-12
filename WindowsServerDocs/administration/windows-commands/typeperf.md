---
title: typeperf
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: cfcbac82b88c0c8d8bcc706ebfd807f96e359de7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440786"
---
# <a name="typeperf"></a>typeperf



Die **Typeperf** Befehl schreibt Leistungsdaten in die Befehlszeile oder in eine Protokolldatei. So beenden Sie **Typeperf**, drücken Sie STRG + C.

Beispiele zur Verwendung für **Typeperf**, finden Sie unter [Beispiele](#BKMK_EXAMPLES).

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
|\<Leistungsindikator [Leistungsindikator [...]] >|Gibt die zu überwachenden Leistungsindikatoren an.|

> [!NOTE]
> **\<Leistungsindikator >** ist der vollständige Name des Leistungsindikators im  *\\ \\Computer\Object (Instanz) \Counter* format, z. B.  **\\ \\Server1\ Prozessor(0)\% Benutzerzeit**.

## <a name="options"></a>Optionen

|                   Option                   |                                                         Beschreibung                                                          |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
|                     -?                     |                                               Zeigt, die kontextbezogene Hilfe an.                                               |
| -f \<CSV&verbar;TSV&verbar;BIN&verbar;SQL> |                                    Gibt das Format der Ausgabedatei an. Der Standardwert ist CSV.                                     |
|              -Cf \<Dateiname >               |              Gibt eine Datei mit einer Liste von Leistungsindikatoren zur Überwachung, mit einem Indikator pro Zeile.               |
|             -si <[[hh:]mm:]ss>             |                                  Gibt an, die für das Samplingintervall. Der Standardwert ist 1 Sekunde.                                   |
|               -o \<Dateiname >               |     Gibt den Pfad für die Ausgabedatei oder die SQL-Datenbank. Der Standardwert ist "stdout" (in das Befehlsfenster geschrieben).      |
|                -q [object]                 | Eine Liste der installierten Leistungsindikatoren (keine Instanzen) angezeigt. Zum Auflisten von Leistungsindikatoren für ein Objekt auch den Objektnamen ein. \*\*\*BEISPIEL |
|                -Qx [Objekt]                |        Eine Liste der installierten Leistungsindikatoren mit Instanzen angezeigt. Zum Auflisten von Leistungsindikatoren für ein Objekt auch den Objektnamen ein.        |
|               -sc \<Beispiele >               |             Gibt die Anzahl der Samplings sammeln. Der Standardwert ist zum Sammeln von Daten, bis Sie STRG + C, gedrückt wird.              |
|            -config \<filename>             |                                    Gibt eine Datei, die Befehlsoptionen enthält.                                     |
|            -s \<Computername >             |                   Gibt an, einem Remotecomputer zu überwachen, wenn kein Computer in der Counter-Pfad angegeben wird.                    |
|                     -y                     |                                        Beantworten Sie Ja, alle Fragen ohne Eingabeaufforderung.                                        |

## <a name="BKMK_EXAMPLES"></a>Beispiele für

- Im folgende Beispiel schreibt die Werte für Leistungsindikator des lokalen Computers  **\\ \\Prozessor(_Total)\% Prozessorzeit** im Befehlsfenster in einem Beispiel-Standardintervall von 1 Sekunde bis STRG + C, gedrückt wird.  
  ```
  typeperf "\Processor(_Total)\% Processor Time"
  ```  
- Das folgende Beispiel schreibt die Werte für die Liste der Leistungsindikatoren in der Datei **counters.txt** in die Datei mit Tabstopptrennzeichen **Domäne2.tsv** in einem Beispiel Intervall von 5 Sekunden bis 50 Proben gesammelt wurden.  
  ```
  typeperf -cf counters.txt -si 5 -sc 50 -f TSV -o domain2.tsv
  ```  
- Das folgende Beispiel fragt installiert Leistungsindikatoren mit Instanzen, für das Leistungsindikatorobjekt **PhysicalDisk** und schreibt die resultierende Liste in die Datei **counters.txt**.  
  ```
  typeperf -qx PhysicalDisk -o counters.txt
  ```
