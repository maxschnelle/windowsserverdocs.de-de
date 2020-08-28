---
title: tracerpt
description: Referenz Artikel zu tracerpt, mit dem Ereignis Ablauf Verfolgungs Protokolle, Protokolldateien, die vom System Monitor generiert werden, und echt Zeitablauf Verfolgungs Anbieter analysiert werden.
ms.topic: reference
ms.assetid: cb9eaf86-0ef6-4197-b6c8-9cca8a1d723c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 250c938963342ca46308f601b00d44773638a4ad
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89026948"
---
# <a name="tracerpt"></a>tracerpt

Der **tracerpt** -Befehl kann zum Analysieren von Ereignis Ablauf Verfolgungs Protokollen, Protokolldateien, die vom System Monitor generiert werden, und Echtzeit-Ereignis Ablauf Verfolgungs Anbietern verwendet werden. Er generiert Dumpdateien, Berichtsdateien und Berichts Schemas.

## <a name="syntax"></a>Syntax

```
tracerpt <[-l] <value [value [...]]>|-rt <session_name [session_name [...]]>> [options]
```

## <a name="options"></a>Tastatur

|              Optionsflag               |                                                                    Beschreibung                                                                    |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
|                   -?                   |                                                         Zeigt kontextabhängige Hilfe an.                                                          |
|          -config \<filename>           |                                                 Lädt eine Einstellungsdatei, die Befehlsoptionen enthält.                                                  |
|                   -y                   |                                                  Antworten Sie auf Ja, um alle Fragen zu beantworten.                                                   |
|            -f \<XML\|HTML>             |                                                                  Berichtsformat.                                                                   |
|         -von \<CSV\|EVTX\|XML>          |                                                         Dumpformat, der Standardwert ist XML.                                                          |
|            -DF \<filename>             |                                            Erstellen Sie eine Microsoft-spezifische zählungs-/Berichterstattungs-Schema Datei.                                            |
|            -int \<filename>            |                                            Die interpretierte Ereignis Struktur wird in der angegebenen Datei gespeichert.                                            |
|                  -RTS                  |                        Berichts rohzeit Stempel im Ereignis Ablauf Verfolgungs Header. Kann nur mit-o, nicht-Report oder-Summary verwendet werden.                         |
|            -TMF \<filename>            |                                                  Geben Sie eine Definitionsdatei für die Ablauf Verfolgungs Meldung an.                                                  |
|              -TP \<value>              |                            Geben Sie den TMF-Datei Suchpfad an. Es können mehrere Pfade verwendet werden, die durch ein Semikolon (;) getrennt sind.                            |
|              -i \<value>               | Geben Sie den Pfad des Anbieter Images an. Die übereinstimmende PDB wird auf dem Symbol Server gefunden. Es können mehrere Pfade verwendet werden, getrennt durch ein Semikolon (;). |
|             -PDB \<value>              |                             Geben Sie den Pfad des Symbol Servers an. Es können mehrere Pfade verwendet werden, getrennt durch ein Semikolon (;).                             |
|                  -GMT                  |                                              Konvertieren von WPP-Nutz Last Zeitstempel in Greenwich Mean Time.                                               |
|              -rl \<value>              |                                               Definieren Sie die System Berichts Ebene zwischen 1 und 5. Der Standardwert ist 1.                                               |
|          -Summary [Dateiname]           |                                  Generieren Sie eine Zusammenfassungs Bericht-Textdatei. Wenn nicht angegeben, wird der Dateiname summary.txt.                                   |
|             -o [Dateiname]              |                                      Generiert eine Textausgabe Datei. Wenn nicht angegeben, wird der Dateiname dumpfile.xml.                                      |
|           -Bericht [Dateiname]           |                                  Generiert eine textausgabeberichtsdatei. Wenn nicht angegeben, wird der Dateiname workload.xml.                                   |
|                  -LR                   |                        Legen Sie weniger restriktiv fest. Dies verwendet die bestmöglichen Anstrengungen für Ereignisse, die nicht dem Ereignis Schema entsprechen.                         |
|           -Export [Dateiname]           |                                  Generieren Sie eine Ereignis Schema-Exportdatei. Der Dateiname, wenn nicht angegeben, ist Schema. man.                                   |
|       [-l] \<value [value […]]>        |                                                   Geben Sie die zu verarbeitende Ereignis Ablauf Verfolgungs Protokoll-Datei an.                                                    |
| -RT \<session_name [session_name […]]> |                                                Geben Sie Datenquellen für Ereignis Ablauf Verfolgungs Sitzungen in Echtzeit an.                                                |

## <a name="examples"></a>Beispiele

- In diesem Beispiel wird ein Bericht erstellt, der auf den beiden Ereignisprotokollen **logfile1. ETL** und **logfile2. ETL** basiert und die Dumpdatei **logdump.xml** im XML-Format erstellt.
  ```
  tracerpt logfile1.etl logfile2.etl -o logdump.xml -of XML
  ```
- In diesem Beispiel wird ein Bericht erstellt, der auf der Ereignisprotokoll **Datei "Logfile. ETL**" basiert, die Dumpdatei **logdmp.xml** im XML-Format erstellt, die bestmögliche Vorgehensweise zum Identifizieren der nicht im Schema verwendeten Ereignisse verwendet, eine Zusammenfassungs Bericht Datei erstellt **logdump.txt**und die Berichtsdatei ** #d2 **erzeugt.
  ```
  tracerpt logfile.etl -o logdmp.xml -of XML -lr -summary logdmp.txt -report logrpt.xml
  ```
- In diesem Beispiel werden die beiden Ereignisprotokolle **logfile1. ETL** und **logfile2. ETL** verwendet, um eine Dumpdatei und eine Berichtsdatei mit den Standard Dateinamen zu entwickeln.
  ```
  tracerpt logfile1.etl logfile2.etl -o -report
  ```
- In diesem Beispiel werden das Ereignisprotokoll **logfile. ETL** und das Leistungs Protokoll **counterfile. blg** verwendet, um die Berichtsdatei **logrpt.xml** und die Microsoft-spezifische XML-Schema Datei **schema.xml**zu entwickeln.
  ```
  tracerpt logfile.etl counterfile.blg -report logrpt.xml -df schema.xml
  ```
- In diesem Beispiel wird die NT-Kernel Protokollierung der Ereignis Ablauf Verfolgungs Sitzung in Echtzeit gelesen und die Dumpdatei **logfile.csv** im CSV-Format erstellt.
  ```
  tracerpt -rt NT Kernel Logger -o logfile.csv -of CSV
  ```
