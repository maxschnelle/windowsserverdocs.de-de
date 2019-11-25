---
title: relog
description: Erfahren Sie, wie Sie Leistungsindikator Informationen aus den Leistungs-coutner-Protokolldateien extrahieren.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7480f6c0-9953-4d70-9b1c-b27e09d8db13
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: daedd85f1557c191a690e7eb750559cfd268d3a0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371625"
---
# <a name="relog"></a>relog

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Extrahiert Leistungsindikatoren aus Leistungsindikator Protokollen in andere Formate, z. b. Text-TSV (für durch Tabstopps getrennte Text), Text-CSV (für durch Trennzeichen getrennte Text), Binär-bin oder SQL.   

## <a name="syntax"></a>Syntax  
```  
relog [<FileName> [<FileName> ...]] [/a] [/c <path> [<path> ...]] [/cf <FileName>] [/f  {bin|csv|tsv|SQL}] [/t <Value>] [/o {OutputFile|DSN!CounterLog}] [/b <M/D/YYYY> [[<HH>:] <MM>:] <SS>] [/e <M/D/YYYY> [[<HH>:] <MM>:] <SS>] [/config {<FileName>|i}] [/q]  
```  

### <a name="parameters"></a>Parameter  

|                                         Parameter                                          |                                                                                                                                                                  Beschreibung                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                *Dateiname* [*filename...* ]                                 |                                                                                                                      Gibt den Pfadnamen eines vorhandenen Leistungs Protokoll Protokolls an. Sie können mehrere Eingabedateien angeben.                                                                                                                      |
|                                             -a                                             |                                                                                                          Fügt die Ausgabedatei an, anstatt überschrieben zu werden. Diese Option gilt nicht für das SQL-Format, bei dem standardmäßig immer angefügt wird.                                                                                                           |
|                                   -c *Pfad* [*Pfad...* ]                                   |                                                       Gibt den zu protokolferenden Leistungsdaten Wert Pfad an. Wenn Sie mehrere Counter-Pfade angeben möchten, trennen Sie diese durch ein Leerzeichen, und schließen Sie die gegen Pfade in Anführungszeichen ein (z. b. **"** <em>Counterpath1</em> <em>Counterpath2</em> **"** ).                                                       |
|                                       -CF *Dateiname*                                       |                                            Gibt den Pfadnamen der Textdatei an, in der die Leistungsindikatoren aufgelistet werden, die in einer erneuten Protokolldatei enthalten sein sollen. Verwenden Sie diese Option, um die zählige Pfade in einer Eingabedatei aufzulisten, eine pro Zeile. Die Standardeinstellung ist, dass alle Zähler in der ursprünglichen Protokolldatei erneut protokolliert werden.                                            |
|                                  -f {bin\| CSV\|TSV\|SQL}                                  |                                       Gibt den Pfadnamen des Ausgabedatei Formats an. Das Standardformat ist **bin**. Für eine SQL-Datenbank gibt die Ausgabedatei den *DSN an. Gegen Protokoll*. Sie können den Daten Bank Speicherort angeben, indem Sie den ODBC-Manager verwenden, um den DSN (Name des Datenbanksystems) zu konfigurieren.                                        |
|                                         -t- *Wert*                                         |                                                                                                           Gibt Beispiel Intervalle in "*N*"-Datensätzen an. Schließt jeden ten-Datenpunkt in die erneut aufzuzeichnen-Datei ein. Der Standardwert ist jeder Datenpunkt.                                                                                                           |
| -o {*OutputFile* \| *"SQL: DSN! Counter_Log*}, wobei es sich bei DSN um einen im System definierten odmc-DSN handelt. |                                                   Gibt den Pfadnamen der Ausgabedatei oder der SQL-Datenbank an, in die die Leistungsindikatoren geschrieben werden. <br>Hinweis: für die 64-Bit-und 32-Bit-Versionen von Relog. exe müssen Sie einen DSN in der ODBC-Datenquelle (64 Bit bzw. 32 Bit) definieren.                                                   |
|                          -b \<*M*/*D*/*yyyy*> [[*HH*:]*mm*:]*SS*                           |                                                                          Gibt die Anfangszeit zum Kopieren des ersten Datensatzes aus der Eingabedatei an. Datum und Uhrzeit müssen das genaue Format <em>M</em> **/** <em>D</em> **/** <em>yyyyhh</em> **:** <em>mm</em> **:** <em>SS</em>aufweisen.                                                                          |
|                          -e \<*M*/*D*/*yyyy*> [[*HH*:]*mm*:]*SS*                           |                                                                           Gibt die Endzeit zum Kopieren des letzten Datensatzes aus der Eingabedatei an. Datum und Uhrzeit müssen das genaue Format <em>M</em> **/** <em>D</em> **/** <em>yyyyhh</em> **:** <em>mm</em> **:** <em>SS</em>aufweisen.                                                                            |
|                                -config {*filename* \| *i*}                                 | Gibt den Pfadnamen der Einstellungsdatei an, die Befehlszeilenparameter enthält. Verwenden Sie *-i* in der Konfigurationsdatei als Platzhalter für eine Liste von Eingabedateien, die in der Befehlszeile abgelegt werden können. In der Befehlszeile müssen Sie jedoch nicht " *i*" verwenden. Sie können auch Platzhalter verwenden, wie z. b. \*. blg, um viele Eingabe Dateinamen anzugeben. |
|                                             -q                                             |                                                                                                                          Zeigt die Leistungsindikatoren und die Zeit Bereiche der Protokolldateien an, die in der Eingabedatei angegeben sind.                                                                                                                           |
|                                             -y                                             |                                                                                                                                            Umgeht die Aufforderung, indem für alle Fragen "Ja" beantwortet wird.                                                                                                                                             |
|                                             /?                                             |                                                                                                                                                      Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                      |

## <a name="remarks"></a>Hinweise  
Kontopfad-Format:  
- Das allgemeine Format für Indikator Pfade lautet wie folgt: [\\\<Computer >] \\\<Objekt > [\<Parent >\\< > Instance # Index \\] \<>], wobei die übergeordneten, Instanz-, Index-und Indikator Komponenten des Formats entweder einen gültigen Namen oder ein Platzhalter Zeichen enthalten können. Die Computer-, übergeordneten, Instanz-und Indexkomponenten sind nicht für alle Leistungsindikatoren erforderlich.  
- Sie bestimmen die zu verwendenden Counter-Pfade basierend auf dem Wert selbst. Beispielsweise verfügt das LogicalDisk-Objekt über eine Instanz <Index>, sodass Sie den < #Index > oder einen Platzhalter angeben müssen. Daher können Sie das folgende Format verwenden: **\logicaldisk (\*/\*#\*)** \\\\*  
- Im Vergleich dazu erfordert das Process-Objekt keine Instanz \<Index >. Daher können Sie das folgende Format verwenden: **\Process (\*) \id Process**  
- Wenn im übergeordneten Namen ein Platzhalter Zeichen angegeben ist, werden alle Instanzen des angegebenen-Objekts zurückgegeben, die mit der angegebenen Instanz und den angegebenen Felder identisch sind.  
- Wenn im Instanznamen ein Platzhalter Zeichen angegeben ist, werden alle Instanzen des angegebenen Objekts und des übergeordneten Objekts zurückgegeben, wenn alle Instanznamen, die dem angegebenen Index entsprechen, mit dem Platzhalter Zeichen übereinstimmen.  
- Wenn im Indikator Namen ein Platzhalter Zeichen angegeben ist, werden alle Zähler des angegebenen Objekts zurückgegeben.  
- Zeichen folgen Übereinstimmungen für partielle Zählers (z. b. pro *) werden nicht unterstützt.  

Gegen Dateien:  
-   Indikator Dateien sind Textdateien, in denen mindestens ein Leistungsindikator im vorhandenen Protokoll aufgeführt ist. Kopieren Sie den vollständigen Namen des Leistungs Zählers aus dem Protokoll oder der **/q** -Ausgabe in \<Computer >\\\<Objekt >\\\<>\\\<>. Auflisten eines Counter-Pfads in jeder Zeile.  

Zähler werden kopiert:  
-   Bei der Ausführung kopiert **erneut aufzuzeichnen** angegebene Leistungsindikatoren aus jedem Datensatz in der Eingabedatei, wobei das Format bei Bedarf umgerechnet wird. Platzhalter Pfade sind in der Counter-Datei zulässig.  
Speichern von Teilmengen von Eingabedateien:  
-   Verwenden Sie den **/t** -Parameter, um anzugeben, dass Eingabedateien in den Ausgabedateien in Intervallen jedes <n>Th-Datensatzes eingefügt werden. Standardmäßig werden Daten von jedem Datensatz neu protokolliert.  
Verwenden von **/b** -und **/e** -Parametern mit Protokolldateien  
-   Sie können angeben, dass die Ausgabe Protokolle Datensätze von vor der Anfangszeit (d. h. **/b**) enthalten, um Daten für Indikatoren bereitzustellen, die Berechnungs Werte des formatierten Werts benötigen. Die Ausgabedatei enthält die letzten Datensätze aus Eingabedateien mit Zeitstempel, die kleiner sind als der **/e** -Parameter (Endzeit).  
Verwenden der **/config** -Option:  
-   Der Inhalt der Einstellungsdatei, die mit der Option **/config** verwendet wird, sollte das folgende Format aufweisen:  
    -   \<commandoption >\\\<Wert >, wobei \<commandoption > eine Befehlszeilenoption und \<Wert > den Wert angibt.

Weitere Informationen zum Einbinden von **erneut aufzuzeichnen** in Ihre Windows-Verwaltungsinstrumentation Skripts (WMI) finden Sie unter "Scripting WMI" auf der [Microsoft Windows Resource Kits-Website](https://go.microsoft.com/fwlink/?LinkId=4665).  

## <a name="BKMK_Examples"></a>Beispiele  
Zum erneuten durchführen vorhandener Ablauf Verfolgungs Protokolle in einem Intervall von 30, Listen Sie Leistungs-und Ausgabedateien und Formate auf:  
```  
relog c:\perflogs\daily_trace_log.blg /cf counter_file.txt /o c:\perflogs\reduced_log.csv /t 30 /f csv  
```  
Um vorhandene Ablauf Verfolgungs Protokolle in einem bestimmten Intervall von 30 zu testen, Listen Sie die Leistungs Regel Pfade und die Ausgabedatei auf:  
```  
relog c:\perflogs\daily_trace_log.blg /cf counter_file.txt /o c:\perflogs\reduced_log.blg /t 30  
```
So führen Sie eine erneute Stichprobe vorhandener Ablauf Verfolgungs Protokolle in einer Datenbank aus
```
relog "c:\perflogs\daily_trace_log.blg" -f sql -o "SQL:sql2016x64odbc!counter_log"
```

## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
