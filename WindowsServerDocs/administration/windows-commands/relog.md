---
title: relog
description: Erfahren Sie, wie aus den Protokolldateien der Leistung Coutner Leistungsindikatorinformationen zu extrahieren.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6804c25af04907edc8180b6a37be7efcc470f259
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869361"
---
# <a name="relog"></a>relog

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Extrahiert Leistungsindikatoren von Leistungsindikatorprotokolle in andere Formate, z. B. Text-TSV (durch Tabstopps getrennten Text), Text-CSV (durch Trennzeichen getrennter Text), Binary-BIN- oder SQL.   

## <a name="syntax"></a>Syntax  
```  
relog [<FileName> [<FileName> ...]] [/a] [/c <path> [<path> ...]] [/cf <FileName>] [/f  {bin|csv|tsv|SQL}] [/t <Value>] [/o {OutputFile|DSN!CounterLog}] [/b <M/D/YYYY> [[<HH>:] <MM>:] <SS>] [/e <M/D/YYYY> [[<HH>:] <MM>:] <SS>] [/config {<FileName>|i}] [/q]  
```  

### <a name="parameters"></a>Parameter  

|Parameter|Beschreibung|
|--|--|
|*FileName* [*Dateiname...* ]|Gibt den Pfadnamen des vorhandenen Leistungsindikator an. Sie können mehrere Eingabedateien angeben.|
|-a |Fügt der Ausgabedatei anstatt zu überschreiben. Diese Option gilt nicht für SQL-Format, wobei der Standardwert immer ist, angefügt werden soll.  |
|-C *Pfad* [*Pfad...* ]|Gibt den Leistungsindikatorpfad, melden Sie sich an. Um mehrere Pfade angeben, trennen Sie diese durch ein Leerzeichen, und schließen Sie die Pfade in Anführungszeichen ein (z. B. **"*** Indikatorpfad1* * Indikatorpfad2 ***"**)|  
|-Cf *Dateiname*|Gibt den Pfadnamen der Textdatei, die die Leistungsindikatoren in einer Datei erneut aufzuzeichnen einzuschließenden aufgeführt sind. Verwenden Sie diese Option, um die Liste der Indikatorpfade in einer Eingabedatei, die jeweils eine pro Zeile ein. Standardeinstellung ist, dass alle Leistungsindikatoren in der ursprünglichen Protokolldatei neu protokolliert werden.|  
|-f {Bin\| Csv\|Tsv\|SQL}|Gibt den Pfadnamen der das Format der Ausgabedatei an. Das Standardformat **Bin**. Für eine SQL-Datenbank, gibt die Ausgabedatei der *DSN! Leistungsindikatorenprotokoll*. Sie können den Speicherort der Datenbank angeben, mit dem ODBC-Manager zum Konfigurieren des DSN (Datenbankname System).  |
|-t *Wert*|Gibt an, Beispiel-Intervalle in "*N*" Datensätze. Schließt jeden n-ten Datenpunkt in der Datei erneut aufzuzeichnen. Standardmäßig ist jeder Datenpunkt.|  
|-o {*OutputFile* \| *"SQL:DSN! Datenbankformaten*}, in dem DSN ist ein ODMC DSN definiert.|Gibt den Pfadnamen der Datei oder SQL-Datenbank, in dem die Leistungsindikatoren geschrieben werden. <br>Hinweis: Für die 64-Bit und 32-Bit-Versionen der Relog.exe, müssen Sie einen DSN in der ODBC-Datenquelle definieren (64-Bit und 32-Bit-bzw.)|
|-b \<*M*/*D*/*YYYY*> [[*HH*:]*MM*:]*SS*|Gibt an, die Startzeit für das Kopieren der ersten Datensatz aus der Eingabedatei. Datum und die Uhrzeit muss exakt in diesem Format *M***/*** D***/*** JJJJHH ***:*** MM ***:*** SS*.|  
|-e: \< *M*/*D*/*JJJJ*> [[*HH*:]*MM*:]*SS* |Gibt die Endzeit für das Kopieren des letzten Eintrags aus der Eingabedatei an. Datum und die Uhrzeit muss exakt in diesem Format *M***/*** D***/*** JJJJHH ***:*** MM ***:*** SS*.|  
|-config {*FileName* \| *i*}|Gibt den Pfadnamen der Datei, die Befehlszeilenparameter enthält. Verwendung *-i* in der Konfigurationsdatei als Platzhalter für eine Liste der Eingabedateien, die in der Befehlszeile angegeben werden sollen. In der Befehlszeile, aber Sie nicht müssen verwenden *ich*. Sie können auch Platzhalter wie z. B. *.blg verwenden, viele Eingabedateinamen angeben.|  
|-q|Zeigt an, die Leistungsindikatoren und Zeitbereiche der Protokolldateien in der Eingabedatei angegeben.|  
|-y|Umgehungen aufgefordert wird, indem Sie "Ja" auf alle Fragen beantworten.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise  
-Indikatorpfadformat:  
-   Das allgemeine Format für die Indikatorpfade lautet wie folgt: [\\\<Computer >] \\ \<Objekt > [\<übergeordneten >\\< Instanz-#Index >] \\ \< Leistungsindikator >], in denen die übergeordnete Instanz, Index und Leistungsindikator-Komponenten, der das Format können enthalten entweder einen gültigen Namen oder ein Platzhalterzeichen. Der Computer, übergeordneten, Instanz und Index-Komponenten sind nicht für alle Leistungsindikatoren erforderlich.  
-   Sie bestimmen die Indikatorpfade verwenden, basierend auf der Zähler selbst. Das LogicalDisk-Objekt hat beispielsweise eine Instanz <Index>, daher müssen Sie die < #index > oder einen Platzhalter angeben. Aus diesem Grund können Sie das folgende Format: **\LogicalDisk (\*/\*#\*)\\\***  
-   Im Gegensatz dazu das Prozessobjekt nicht erfordert eine Instanz \<Index >. Aus diesem Grund können Sie das folgende Format: **\Process (\*) \ID Prozess**  
-   Wenn ein Platzhalterzeichen in den Namen der übergeordneten angegeben ist, werden alle Instanzen des angegebenen Objekts, die die angegebene Instanz und der Leistungsindikator-Felder entsprechen zurückgegeben.  
-   Wenn ein Platzhalterzeichen im Instanznamen angegeben wird, werden alle Instanzen der dem angegebenen Objekt und das übergeordnete Objekt zurückgegeben, wenn es sich bei alle Instanznamen, die dem angegebenen Index entspricht das Platzhalterzeichen übereinstimmen.  
-   Wenn ein Platzhalterzeichen in den Namen des Leistungsindikators angegeben ist, werden alle Indikatoren des angegebenen Objekts zurückgegeben.  
-   Zeichenfolgenübereinstimmungen teilweise Leistungsindikator-Pfad (z. B. Pro *) werden nicht unterstützt.  

Leistungsindikatordateien:  
-   Zähler sind Textdateien, in denen eine oder mehrere der Leistungsindikatoren in das bestehende Protokoll aufgeführt. Kopieren Sie den vollständigen Leistungsindikatornamen aus dem Protokoll oder die **/q /** Ausgabe im \<Computer >\\\<Objekt >\\\<Instanz >\\ \< Leistungsindikator > Format. Listet eine Leistungsindikatorpfad in jeder Zeile.  

Kopieren die Leistungsindikatoren:  
-   Bei der Ausführung **erneut aufzuzeichnen** kopiert angegebene Leistungsindikatoren aus jeder Datensatz in der Eingabedatei, konvertieren das Format, bei Bedarf. Platzhalter-Pfade dürfen in der Counter-Datei.  
Eingabedatei-Teilmengen gespeichert:  
-   Verwenden der **/t /** Ausgabedateien, Parameter, um anzugeben, dass die Eingabedateien eingefügt werden, in Intervallen von jedem <n>th-Datensatz. Standardmäßig werden Daten aus jedem Datensatz neu protokolliert.  
Mithilfe von **/b** und **/e** Parameter mit Protokolldateien  
-   Sie können angeben, dass die Ausgabeprotokolle Datensätze aus vor der Startzeit enthalten (d. h. **/b**) Daten für Leistungsindikatoren angeben, der der Berechnungswerte des formatierten Werts erfordern. Die Ausgabedatei hat die letzten Einträge aus Eingabedateien mit Zeitstempeln kleiner als der **/e** (das heißt, Zeitpunkt der Beendigung) Parameter.  
Mithilfe der **/config /** Option:  
-   Den Inhalt der Datei mit der Verwendung der **/config /** Option sollte das folgende Format aufweisen:  
    -   \<CommandOption >\\\<Wert >, wobei \<CommandOption > ist eine Befehlszeilenoption und \<Wert > Gibt an, dessen Wert.

Weitere Informationen zum Einbinden von **erneut aufzuzeichnen** in Ihre Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) Skripts finden Sie unter "WMI-Skripterstellung" unter der [Microsoft Windows Resource Kits-Website](https://go.microsoft.com/fwlink/?LinkId=4665).  

## <a name="BKMK_Examples"></a>Beispiele für  
Neue Datenstichproben vorhandene Ablaufverfolgungsprotokolle in festen Intervallen von 30, Indikatorpfade auflisten, Ausgabedateien und Formate:  
```  
relog c:\perflogs\daily_trace_log.blg /cf counter_file.txt /o c:\perflogs\reduced_log.csv /t 30 /f csv  
```  
Listen Sie vorhandene Ablaufverfolgungsprotokolle in festen Intervallen von 30 neue Datenstichproben, Indikatorpfade und Ausgabedatei:  
```  
relog c:\perflogs\daily_trace_log.blg /cf counter_file.txt /o c:\perflogs\reduced_log.blg /t 30  
```
Vorhandene Ablaufverfolgungsprotokolle in einem verwenden der Datenbank erneut einlesen:
```
relog "c:\perflogs\daily_trace_log.blg" -f sql -o "SQL:sql2016x64odbc!counter_log"
```

## <a name="additional-references"></a>Weitere Verweise  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
  
<!---
-   The following is a list of the possible formats:  
    -   \<computer>\\\<Object>(\<Parent>/\<Instance#Index>)\<Counter>  
    -   \<computer>\<Object>(<Parent>/<Instance>)\\<Counter>  
    -   \\\\<computer>\\<Object>(<Instance#Index>)\\<Counter>  
    -   \\\\<computer>\\<Object>(<Instance>)\\<Counter>  
    -   \\\\<computer>\\<Object>\\<Counter>  
    -   \\<Object>(<Parent>/<Instance#Index>)\\<Counter>  
    -   \\<Object>(<Parent>/<Instance>)<Counter>  
    -   \\<Object>(<Instance#Index>)\\<Counter>  
    -   \\<Object>(<Instance>)\\<Counter>  
    -   \\<Object>\\<Counter>  
--->