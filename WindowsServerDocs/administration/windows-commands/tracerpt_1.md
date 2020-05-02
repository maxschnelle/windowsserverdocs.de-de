---
title: tracerpt
description: Referenz Thema für tracerpt, mit dem Ereignis Ablauf Verfolgungs Protokolle, Protokolldateien, die vom System Monitor generiert werden, und echt Zeitablauf Verfolgungs Anbieter analysiert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cb9eaf86-0ef6-4197-b6c8-9cca8a1d723c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 79eac1db4d91bfcfe52cf71cbab683b7489d5287
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721313"
---
# <a name="tracerpt"></a>tracerpt

Der **tracerpt** -Befehl kann zum Analysieren von Ereignis Ablauf Verfolgungs Protokollen, Protokolldateien, die vom System Monitor generiert werden, und Echtzeit-Ereignis Ablauf Verfolgungs Anbietern verwendet werden. Er generiert Dumpdateien, Berichtsdateien und Berichts Schemas.

## <a name="syntax"></a>Syntax

```
tracerpt <[-l] <value [value [...]]>|-rt <session_name [session_name [...]]>> [options]
```

## <a name="options"></a>Tastatur

|              Optionsflag               |                                                                    BESCHREIBUNG                                                                    |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
|                   -?                   |                                                         Zeigt kontextabhängige Hilfe an.                                                          |
|          -Konfigurations \<Dateiname>           |                                                 Lädt eine Einstellungsdatei, die Befehlsoptionen enthält.                                                  |
|                   -y                   |                                                  Antworten Sie auf Ja, um alle Fragen zu beantworten.                                                   |
|            -f \<XML\|-HTML->             |                                                                  Berichtsformat.                                                                   |
|         -von \<CSV\|-evtx\|-XML->          |                                                         Dumpformat, der Standardwert ist XML.                                                          |
|            -DF \<Dateiname>             |                                            Erstellen Sie eine Microsoft-spezifische zählungs-/Berichterstattungs-Schema Datei.                                            |
|            -int \<Dateiname>            |                                            Die interpretierte Ereignis Struktur wird in der angegebenen Datei gespeichert.                                            |
|                  -RTS                  |                        Berichts rohzeit Stempel im Ereignis Ablauf Verfolgungs Header. Kann nur mit-o, nicht-Report oder-Summary verwendet werden.                         |
|            -TMF \<Dateiname>            |                                                  Geben Sie eine Definitionsdatei für die Ablauf Verfolgungs Meldung an.                                                  |
|              -TP \<-Wert>              |                            Geben Sie den TMF-Datei Suchpfad an. Es können mehrere Pfade verwendet werden, die durch ein Semikolon (;) getrennt sind.                            |
|              -i \<-Wert>               | Geben Sie den Pfad des Anbieter Images an. Die übereinstimmende PDB wird auf dem Symbol Server gefunden. Es können mehrere Pfade verwendet werden, getrennt durch ein Semikolon (;). |
|             -PDB \<-Wert>              |                             Geben Sie den Pfad des Symbol Servers an. Es können mehrere Pfade verwendet werden, getrennt durch ein Semikolon (;).                             |
|                  -GMT                  |                                              Konvertieren von WPP-Nutz Last Zeitstempel in Greenwich Mean Time.                                               |
|              -RL \<-Wert>              |                                               Definieren Sie die System Berichts Ebene zwischen 1 und 5. Der Standardwert ist 1.                                               |
|          -Summary [Dateiname]           |                                  Generieren Sie eine Zusammenfassungs Bericht-Textdatei. Der Dateiname, wenn er nicht angegeben ist                                   |
|             -o [Dateiname]              |                                      Generiert eine Textausgabe Datei. Dateiname, wenn nicht angegeben                                      |
|           -Bericht [Dateiname]           |                                  Generiert eine textausgabeberichtsdatei. Der Dateiname, wenn er nicht angegeben wird                                   |
|                  -LR                   |                        Legen Sie weniger restriktiv fest. Dies verwendet die bestmöglichen Anstrengungen für Ereignisse, die nicht dem Ereignis Schema entsprechen.                         |
|           -Export [Dateiname]           |                                  Generieren Sie eine Ereignis Schema-Exportdatei. Der Dateiname, wenn nicht angegeben, ist Schema. man.                                   |
|       [-l] \<Wert [Wert [...]] >        |                                                   Geben Sie die zu verarbeitende Ereignis Ablauf Verfolgungs Protokoll-Datei an.                                                    |
| -RT \<session_name [session_name [...]] > |                                                Geben Sie Datenquellen für Ereignis Ablauf Verfolgungs Sitzungen in Echtzeit an.                                                |

## <a name="examples"></a>Beispiele

- In diesem Beispiel wird ein Bericht erstellt, der auf den beiden Ereignisprotokollen **logfile1. ETL** und **logfile2. ETL** basiert und die Dumpdatei **logdump. XML** im XML-Format erstellt.  
  ```
  tracerpt logfile1.etl logfile2.etl -o logdump.xml -of XML
  ```  
- In diesem Beispiel wird ein Bericht erstellt, der auf der Ereignisprotokoll **Datei "Logfile. ETL**" basiert, die Dumpdatei " **logdmp. XML** " im XML-Format erstellt, die besten Verfahren zur Identifizierung von Ereignissen, die sich nicht im Schema befinden, erstellt und die **Berichtsdatei "** **logrpt. XML**" erstellt.  
  ```
  tracerpt logfile.etl -o logdmp.xml -of XML -lr -summary logdmp.txt -report logrpt.xml
  ```  
- In diesem Beispiel werden die beiden Ereignisprotokolle **logfile1. ETL** und **logfile2. ETL** verwendet, um eine Dumpdatei und eine Berichtsdatei mit den Standard Dateinamen zu entwickeln.  
  ```
  tracerpt logfile1.etl logfile2.etl -o -report
  ```  
- In diesem Beispiel werden das Ereignisprotokoll **logfile. ETL** und das Leistungs Protokoll **counterfile. blg** verwendet, um die Berichtsdatei " **logrpt. XML** " und die Microsoft-spezifische XML-Schema Datei " **Schema. XML**" zu entwickeln.  
  ```
  tracerpt logfile.etl counterfile.blg -report logrpt.xml -df schema.xml
  ```  
- In diesem Beispiel wird die NT-Kernel Protokollierung der Ereignis Ablauf Verfolgungs Sitzung von Echtzeit gelesen und die Dumpdatei **logfile. CSV** im CSV-Format erstellt.  
  ```
  tracerpt -rt NT Kernel Logger -o logfile.csv -of CSV
  ```
