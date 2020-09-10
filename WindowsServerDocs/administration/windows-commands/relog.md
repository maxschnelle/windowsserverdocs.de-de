---
title: relog
description: Referenz Artikel für den Befehl erneut aufzuzeichnen, mit dem Leistungsdaten aus den Leistungsdaten-Protokolldateien extrahiert werden.
ms.topic: reference
ms.assetid: 7480f6c0-9953-4d70-9b1c-b27e09d8db13
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: 9ced8c1c4f0eb2cabaf65c98f5a9c4ecb0135c11
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640291"
---
# <a name="relog"></a>relog

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Extrahiert Leistungsindikatoren aus Leistungsindikator Protokollen in andere Formate, z. b. Text-TSV (für durch Tabstopps getrennte Text), Text-CSV (für durch Trennzeichen getrennte Text), Binär-bin oder SQL.

>[!NOTE]
>Weitere Informationen zur Integration von **erneut aufzuzeichnen** in Ihre Windows-Verwaltungsinstrumentation Skripts (WMI) finden Sie im [Scripting-Blog](https://devblogs.microsoft.com/scripting/).

## <a name="syntax"></a>Syntax

```
relog [<filename> [<filename> ...]] [/a] [/c <path> [<path> ...]] [/cf <filename>] [/f  {bin|csv|tsv|SQL}] [/t <value>] [/o {outputfile|DSN!CounterLog}] [/b <M/D/YYYY> [[<HH>:] <MM>:] <SS>] [/e <M/D/YYYY> [[<HH>:] <MM>:] <SS>] [/config {<filename>|i}] [/q]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `filename [filename ...]` | Gibt den Pfadnamen eines vorhandenen Leistungs Protokoll Protokolls an. Sie können mehrere Eingabedateien angeben. |
| -a | Fügt die Ausgabedatei an, anstatt überschrieben zu werden. Diese Option gilt nicht für das SQL-Format, bei dem standardmäßig immer angefügt wird. |
| -c `path [path ...]` | Gibt den zu protokolferenden Leistungsdaten Wert Pfad an. Wenn Sie mehrere Counter-Pfade angeben möchten, trennen Sie diese durch ein Leerzeichen, und schließen Sie die Zählers in Anführungszeichen (z `"path1 path2"` . b.) ein. |
| -CF Dateiname | Gibt den Pfadnamen der Textdatei an, in der die Leistungsindikatoren aufgelistet werden, die in einer erneuten Protokolldatei enthalten sein sollen. Verwenden Sie diese Option, um die zählige Pfade in einer Eingabedatei aufzulisten, eine pro Zeile. Die Standardeinstellung ist, dass alle Zähler in der ursprünglichen Protokolldatei erneut protokolliert werden. |
| -f `{bin | csv | tsv | SQL}` | Gibt den Pfadnamen des Ausgabedatei Formats an. Das Standardformat ist **bin**. Für eine SQL-Datenbank wird in der Ausgabedatei angegeben `DSN!CounterLog` . Sie können den Daten Bank Speicherort angeben, indem Sie den ODBC-Manager verwenden, um den DSN (Name des Datenbanksystems) zu konfigurieren. |
| -t-Wert | Gibt Beispiel Intervalle in *n* Datensätzen an. Schließt jeden ten-Datenpunkt in die erneut aufzuzeichnen-Datei ein. Der Standardwert ist jeder Datenpunkt. |
| -o `{Outputfile | SQL:DSN!Counter_Log}` | Gibt den Pfadnamen der Ausgabedatei oder der SQL-Datenbank an, in die die Leistungsindikatoren geschrieben werden. <P>**Hinweis:** Für die 64-Bit-und 32-Bit-Versionen von relog.exe müssen Sie einen DSN in der ODBC-Datenquelle (64-Bit bzw. 32-Bit) auf dem System definieren. Verwenden Sie den ODBC-Treiber "SQL Server", um einen DSN zu definieren. |
| -b `<M/D/YYYY> [[<HH>:]<MM>:]<SS>]` | Gibt die Anfangszeit zum Kopieren des ersten Datensatzes aus der Eingabedatei an. Datum und Uhrzeit müssen das genaue Format M/D/yyyyhh: mm: SS aufweisen. |
| -e `<M/D/YYYY> [[<HH>:]<MM>:]<SS>]` | Gibt die Endzeit an, zu der der letzte Datensatz aus der Eingabedatei kopiert werden soll. Datum und Uhrzeit müssen das genaue Format M/D/yyyyhh: mm: SS aufweisen. |
| -config `{filename | i}` | Gibt den Pfadnamen der Einstellungsdatei an, die Befehlszeilenparameter enthält. Wenn Sie eine Konfigurationsdatei verwenden, können Sie **-i** als Platzhalter für eine Liste von Eingabedateien verwenden, die in der Befehlszeile abgelegt werden können. Verwenden Sie **-i**nicht, wenn Sie die Befehlszeile verwenden. Sie können auch Platzhalter verwenden, z `*.blg` . b., um mehrere Eingabe Dateinamen gleichzeitig anzugeben. |
| -q | Zeigt die Leistungsindikatoren und die Zeit Bereiche der Protokolldateien an, die in der Eingabedatei angegeben sind. |
| -y | Umgeht die Aufforderung, indem für alle Fragen "Ja" beantwortet wird. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Das allgemeine Format für Indikator Pfade lautet wie folgt: `[\<computer>] \<object>[<parent>\<instance#index>] \<counter>]` wo die übergeordneten, Instanzen-, Index-und Indikator Komponenten des Formats entweder einen gültigen Namen oder ein Platzhalter Zeichen enthalten können. Die Computer-, übergeordneten, Instanz-und Indexkomponenten sind für alle Leistungsindikatoren nicht erforderlich.

- Sie bestimmen die zu verwendenden Counter-Pfade basierend auf dem Wert selbst. Das **LogicalDisk** -Objekt verfügt z. b. über eine-Instanz `<index>` , sodass Sie oder einen Platzhalter angeben müssen `<#index>` . Daher können Sie das folgende Format verwenden: `\LogicalDisk(*/*#*)\\*` .

- Im Vergleich dazu ist für das **Process** -Objekt keine-Instanz erforderlich `<index>` . Daher können Sie das folgende Format verwenden: `\Process(*)\ID Process` .

- Wenn im über **geordneten** Namen ein Platzhalter Zeichen angegeben ist, werden alle Instanzen des angegebenen-Objekts zurückgegeben, die mit der angegebenen Instanz und den angegebenen Felder identisch sind.

- Wenn im **Instanznamen** ein Platzhalter Zeichen angegeben ist, werden alle Instanzen des angegebenen Objekts und des übergeordneten Objekts zurückgegeben, wenn alle Instanznamen, die dem angegebenen Index entsprechen, mit dem Platzhalter Zeichen übereinstimmen.

- Wenn im **Indikator Namen ein** Platzhalter Zeichen angegeben ist, werden alle Zähler des angegebenen Objekts zurückgegeben.

- Zeichen folgen Übereinstimmungen für partielle Zeichen folgen (z.b. pro *) werden nicht unterstützt.

- Indikator Dateien sind Textdateien, in denen mindestens ein Leistungsindikator im vorhandenen Protokoll aufgeführt ist. Kopieren Sie den vollständigen Namen des Leistungs Zählers aus dem Protokoll oder der **/q** -Ausgabe im `<computer>\<object>\<instance>\<counter>` Format. Auflisten eines Counter-Pfads in jeder Zeile.

- Bei der Durchführung kopiert der Befehl " **erneut aufzuzeichnen** " angegebene Leistungsindikatoren aus jedem Datensatz in der Eingabedatei und umwandelt das Format bei Bedarf. Platzhalter Pfade sind in der Counter-Datei zulässig.

- Verwenden Sie den **/t** -Parameter, um anzugeben, dass Eingabedateien in den Ausgabedateien in den Intervallen jedes `nth` Datensatzes eingefügt werden. Standardmäßig werden Daten von jedem Datensatz neu protokolliert.

- Sie können angeben, dass die Ausgabe Protokolle Datensätze von vor der Anfangszeit (d. h. **/b**) enthalten, um Daten für Indikatoren bereitzustellen, die Berechnungs Werte des formatierten Werts benötigen. Die Ausgabedatei enthält die letzten Datensätze aus Eingabedateien mit Zeitstempel, die kleiner sind als der **/e** -Parameter (Endzeit).

- Der Inhalt der Einstellungsdatei, die mit der **/config** -Option verwendet wird, sollte das folgende Format aufweisen: `<commandoption>\<value>` , wobei `<commandoption>` eine Befehlszeilenoption ist und `<value>` ihren Wert angibt.

##<a name="q-examples"></a>F #-Beispiele

Geben Sie Folgendes ein, um vorhandene Ablauf Verfolgungs Protokolle in einem bestimmten Intervall von 30 zu testen, um die Liste der Leistungs Zähl Pfade, Ausgabedateien und Formate aufzulisten:

```
relog c:\perflogs\daily_trace_log.blg /cf counter_file.txt /o c:\perflogs\reduced_log.csv /t 30 /f csv
```

Geben Sie Folgendes ein, um vorhandene Ablauf Verfolgungs Protokolle in einem bestimmten Intervall von 30, Listen-und Ausgabedateien neu zu überführen:

```
relog c:\perflogs\daily_trace_log.blg /cf counter_file.txt /o c:\perflogs\reduced_log.blg /t 30
```

Geben Sie Folgendes ein, um vorhandene Ablauf Verfolgungs Protokolle in eine Datenbank zu überführen:

```
relog "c:\perflogs\daily_trace_log.blg" -f sql -o "SQL:sql2016x64odbc!counter_log"
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
