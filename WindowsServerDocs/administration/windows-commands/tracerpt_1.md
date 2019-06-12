---
title: tracerpt
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb9eaf86-0ef6-4197-b6c8-9cca8a1d723c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c105fe714e30866297e4f6c3c83a670ff7966a6
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440972"
---
# <a name="tracerpt"></a>tracerpt



Die **Tracerpt** Befehl kann verwendet werden, um die Protokolle der Ereignisablaufverfolgung, Protokolldateien, die vom Systemmonitor und die Echtzeit-Ereignisablaufverfolgung-Anbieter zu analysieren. Dumpdateien, Dateien und Schemas der Bericht generiert.

Beispiele zur Verwendung für **Tracerpt**, finden Sie unter [Beispiele](#BKMK_EXAMPLES).

## <a name="syntax"></a>Syntax

```
tracerpt <[-l] <value [value [...]]>|-rt <session_name [session_name [...]]>> [options]
```

## <a name="options"></a>Optionen

|              Optionsflags               |                                                                    Beschreibung                                                                    |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
|                   -?                   |                                                         Zeigt, die kontextbezogene Hilfe an.                                                          |
|          -config \<filename>           |                                                 Laden Sie eine Datei, die Befehlsoptionen enthält.                                                  |
|                   -y                   |                                                  Beantworten Sie Ja, alle Fragen ohne Eingabeaufforderung.                                                   |
|                -f \<XML                |                                                                       HTML>                                                                       |
|               -of \<CSV                |                                                                       EVTX                                                                        |
|            -df \<Dateiname >             |                                            Erstellen Sie eine Microsoft-spezifische zählen/berichterstellung-Schemadatei.                                            |
|            Int - \<Dateiname >            |                                            Sichern Sie die Ereignisstruktur interpretierte in der angegebenen Datei.                                            |
|                  Rts-                  |                        Melden Sie unformatierte Zeitstempel in der Kopfzeile der Ereignis-Ablaufverfolgung. Kann nur mit nicht - Bericht oder -Summary -o, verwendet werden.                         |
|            -Tmf \<Dateiname >            |                                                  Geben Sie eine Definitionsdatei für die Ablaufverfolgung-Nachrichtenformat.                                                  |
|              -Tp \<Wert >              |                            Geben Sie den Pfad der TMF suchen. Mehrere Pfade können verwendet werden, getrennt durch ein Semikolon (;).                            |
|              -i \<Wert >               | Geben Sie den Pfad des Anbieters Image. Die entsprechende PDB-Datei wird in den Symbolserver befinden. Mehrere Pfade können verwendet werden, getrennt durch ein Semikolon (;). |
|             -pdb \<value>              |                             Geben Sie den Pfad des Symbolservers an. Mehrere Pfade können verwendet werden, getrennt durch ein Semikolon (;).                             |
|                  -gmt                  |                                              Konvertieren Sie WPP Nutzlast Zeitstempel Greenwich Mean Time an.                                               |
|              -Rl \<Wert >              |                                               Definieren Sie die System-Berichtsebene von 1 bis 5. Standardwert ist 1.                                               |
|          -Übersicht [Dateiname]           |                                  Generieren Sie eine Textdatei Zusammenfassungsbericht. Der Dateiname nicht angegeben ist ' Summary.txt '.                                   |
|             -o [Dateiname]              |                                      Generieren Sie eine Textdatei für die Ausgabe an. Der Dateiname nicht angegeben ist "dumpfile.xml".                                      |
|           -Berichts [Dateiname]           |                                  Generieren Sie einen Bericht textausgabedatei an. Der Dateiname nicht angegeben ist workload.xml.                                   |
|                  -lr                   |                        Geben Sie "weniger restriktiv." Dabei wird die bestmögliche Weise verwendet, für Ereignisse, die nicht das Ereignisschema übereinstimmen.                         |
|           – Exportieren Sie die [Dateiname]           |                                  Generieren Sie eine Exportdatei Ereignisschema. Der Dateiname nicht angegeben ist "Schema.man".                                   |
|       [-l]. \<Wert wie [[...]] >        |                                                   Geben Sie die Ereignisablaufverfolgung-Protokolldatei zu verarbeiten.                                                    |
| -rt \<Session_name [Session_name [...]] > |                                                Geben Sie die Datenquellen in Echtzeit Ereignisablaufverfolgungs-Sitzung.                                                |

## <a name="BKMK_EXAMPLES"></a>Beispiele für

- Dieses Beispiel erstellt einen Bericht basierend auf den zwei Ereignisprotokollen **logfile1.etl** und **logfile2.etl** und erstellt die Speicherabbilddatei **logdump.xml** im XML-Format.  
  ```
  tracerpt logfile1.etl logfile2.etl -o logdump.xml -of XML
  ```  
- Dieses Beispiel erstellt einen Bericht anhand der im Ereignisprotokoll **logfile.etl**, erstellt die Speicherabbilddatei **logdmp.xml** im XML-Format erzeugt verwendet bestmögliche Weise zur Identifizierung von Ereignissen, die nicht im Schema eine Zusammenfassungsbericht-Datei **logdump.txt**, und erzeugt die Berichtsdatei **logrpt.xml**.  
  ```
  tracerpt logfile.etl -o logdmp.xml -of XML -lr -summary logdmp.txt -report logrpt.xml
  ```  
- Dieses Beispiel verwendet die zwei Ereignisprotokolle **logfile1.etl** und **logfile2.etl** um eine Dumpdatei und die Berichtsdatei mit der Standard-Dateinamen zu erzeugen.  
  ```
  tracerpt logfile1.etl logfile2.etl -o -report
  ```  
- In diesem Beispiel verwendet das Ereignisprotokoll **logfile.etl** und das Leistungsprotokoll **counterfile.blg** zum Erzeugen der Berichtsdatei **logrpt.xml** und das Microsoft-spezifische XML-Schema Datei **"Schema.xml"** .  
  ```
  tracerpt logfile.etl counterfile.blg -report logrpt.xml -df schema.xml
  ```  
- In diesem Beispiel liest die in Echtzeit Ereignisablaufverfolgungs-Sitzung "NT Kernel Logger" und erzeugt die Dumpdatei **logfile.csv** im CSV-Format.  
  ```
  tracerpt -rt "NT Kernel Logger" -o logfile.csv -of CSV
  ```