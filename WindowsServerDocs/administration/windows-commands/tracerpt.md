---
title: tracerpt
description: Referenz Artikel für den tracerpt-Befehl, mit dem Ereignis Ablauf Verfolgungs Protokolle, Protokolldateien, die vom System Monitor generiert werden, und Echtzeit-Ereignis Ablauf Verfolgungs Anbieter analysiert werden.
ms.topic: reference
ms.assetid: cb9eaf86-0ef6-4197-b6c8-9cca8a1d723c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1e468dab3c99219560047668f9f1bd001e8e451e
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156712"
---
# <a name="tracerpt"></a>tracerpt

Der **tracerpt** -Befehl analysiert Ereignis Ablauf Verfolgungs Protokolle, Protokolldateien, die vom System Monitor generiert werden, und echt Zeitablauf Verfolgungs Anbieter. Außerdem werden Dumpdateien, Berichtsdateien und Berichts Schemas generiert.

## <a name="syntax"></a>Syntax

```
tracerpt <[-l] <value [value [...]]>|-rt <session_name [session_name [...]]>> [options]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -config `<filename>` | Gibt an, welche Einstellungsdatei geladen werden soll, die die Befehlsoptionen enthält. |
| -y | Gibt an, dass für alle Fragen ohne Aufforderung auf **Ja** geantwortet werden soll. |
| -f `<XML | HTML>` | Gibt das Format der Berichtsdatei an. |
| -von `<CSV | EVTX | XML>` | Gibt das Format der Dumpdatei an. Der Standardwert ist **XML*. |
| -DF `<filename>` | Gibt an, dass eine Microsoft-spezifische zählungs-/Berichterstattungs Schema Datei erstellt werden soll |
| -int `<filename>` | Gibt an, dass die interpretierte Ereignis Struktur in der angegebenen Datei gespeichert wird. |
| -RTS | Gibt an, dass der Berichts rohzeit Stempel im Ereignis Ablauf Verfolgungs Header hinzugefügt wird. Kann nur mit **-o**verwendet werden. Die Verwendung von **-Report** oder **-Summary**wird nicht unterstützt. |
| -TMF `<filename>` | Gibt die zu verwendende Format Definitionsdatei für die Ablauf Verfolgungs Meldung an. |
| -TP `<value>` | Gibt den TMF-Datei Suchpfad an. Es können mehrere Pfade verwendet werden, die durch ein Semikolon (;) getrennt sind. |
| -i `<value>` | Gibt den Pfad des Anbieter Images an. Die übereinstimmende PDB wird auf dem Symbol Server gefunden. Es können mehrere Pfade verwendet werden, getrennt durch ein Semikolon (;). |
| -PDB `<value>` | Gibt den Pfad des Symbol Servers an. Es können mehrere Pfade verwendet werden, getrennt durch ein Semikolon (;). |
| -GMT | Gibt an, dass WPP-Nutz Last Zeitstempel in Greenwich Mean Time konvertiert werden sollen. |
| -rl `<value>` | Gibt die System Berichts Ebene zwischen 1 und 5 an. Der Standardwert ist *1*. |
| -Summary [Dateiname] | Gibt an, dass eine Zusammenfassungs Berichts Textdatei erstellt werden soll. Wenn nicht angegeben, wird der Dateiname *summary.txt*. |
| -o [Dateiname] | Gibt an, dass eine Textausgabe Datei erstellt werden soll. Wenn nicht angegeben, wird der Dateiname *dumpfile.xml*. |
| -Bericht [Dateiname] | Gibt an, dass eine Textausgabe Berichtsdatei erstellt werden soll. Wenn nicht angegeben, wird der Dateiname *workload.xml*. |
| -LR | Gibt an, dass weniger restriktiv ist. Dies verwendet die bestmöglichen Anstrengungen für Ereignisse, die nicht dem Ereignis Schema entsprechen. |
| -Export [Dateiname] | Gibt an, dass eine Ereignis Schema-Exportdatei erstellt werden soll. Wenn nicht angegeben, ist der Dateiname " *Schema. man*". |
| [-l] `<value [value […]]>` | Gibt die zu verarbeitende Ereignis Ablauf Verfolgungs Protokoll-Datei an. |
| -RT `<session_name [session_name […]]>` | Gibt die Datenquellen der Ereignis Ablauf Verfolgungs Sitzung in Echtzeit an. |
| -? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen Bericht zu erstellen, der auf den beiden Ereignisprotokollen *logfile1. ETL* und *logfile2. ETL*basiert, und um die Dumpdatei *logdump.xml* im *XML* -Format zu erstellen:

```
tracerpt logfile1.etl logfile2.etl -o logdump.xml -of XML
```

Wenn Sie einen Bericht erstellen möchten, der auf der Ereignisprotokoll *Datei "Logfile. ETL*" basiert, um die Dumpdatei *logdmp.xml* im XML-Format zu erstellen, verwenden Sie zum Ermitteln der am Schema nicht im Schema verwendeten Ereignisse und zum Erstellen einer Zusammenfassungs Berichtsdatei *logdump.txt* und einer Berichts * #d2 *Datei Folgendes:

```
tracerpt logfile.etl -o logdmp.xml -of XML -lr -summary logdmp.txt -report logrpt.xml
```

Geben Sie Folgendes ein, um die zwei Ereignisprotokolle *logfile1. ETL* und *logfile2. ETL* zum Entwickeln einer Dumpdatei und zum Melden der Datei mit den Standard Dateinamen zu verwenden:

```
tracerpt logfile1.etl logfile2.etl -o -report
```

Geben Sie Folgendes ein, um das Ereignisprotokoll " *logfile. ETL* " und das Leistungs Protokoll " *counterfile. blg* " zu verwenden, um die Berichtsdatei *logrpt.xml* und die Microsoft-spezifische XML-Schema Datei *schema.xml*zu entwickeln:

```
tracerpt logfile.etl counterfile.blg -report logrpt.xml -df schema.xml
```

Geben Sie Folgendes ein, um die NT-Kernel Protokollierung der Ereignis Ablauf Verfolgungs Sitzung zu lesen und die Dumpdatei *logfile.csv* im *CSV* -Format zu erhalten:

```
tracerpt -rt NT Kernel Logger -o logfile.csv -of CSV
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
