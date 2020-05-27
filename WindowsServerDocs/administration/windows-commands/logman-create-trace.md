---
title: logman Create Trace
description: Referenz Thema für den Befehl logman Create Trace, der einen Ereignis Ablauf Verfolgungs Datensammler erstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1b4dfecd-6f56-4c51-b622-c2054b4aabd7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 08a9b0a74c6da894eeadef8aef86f25761d6616e
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820450"
---
# <a name="logman-create-trace"></a>logman Create Trace

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellen Sie einen Ereignis Ablauf Verfolgungs Datensammler.

## <a name="syntax"></a>Syntax

```
logman create trace <[-n] <name>> [options]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| -s`<computer name>` | Führt den Befehl auf dem angegebenen Remote Computer aus. |
| -config`<value>` | Gibt die Einstellungsdatei an, die Befehlsoptionen enthält. |
| -ETS | Sendet Befehle direkt an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen. |
| [-n]`<name>` | Name des Zielobjekts |
| -f`<bin|bincirc>` | Gibt das Protokoll Format für den Datensammler an. |
| -[-] u`<user [password]>` | Gibt den Benutzer an, der als ausgeführt werden soll. Wenn Sie `*` für das Kennwort eingeben, wird eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, während Sie es an der Eingabeaufforderung eingeben. |
| -m`<[start] [stop] [[start] [stop] [...]]>` | Änderungen an manuellem starten oder beenden anstelle einer geplanten Anfangs-oder Endzeit. |
| -RF`<[[hh:]mm:]ss>` | Führt den Datensammler für den angegebenen Zeitraum aus. |
| -b`<M/d/yyyy h:mm:ss[AM|PM]>` | Beginnt mit dem Sammeln von Daten zum angegebenen Zeitpunkt. |
| -e `<M/d/yyyy h:mm:ss[AM|PM]>` | Beendet die Datensammlung zum angegebenen Zeitpunkt. |
| -o`<path|dsn!log>` | Gibt die Ausgabeprotokoll Datei oder den DSN-und Protokoll Satz Namen in einer SQL-Datenbank an. |
| -[-] r | Wiederholt den Datensammler täglich zu den angegebenen Anfangs-und Endzeiten. |
| -[-] a | Fügt eine vorhandene Protokolldatei an. |
| -[-] OW | Überschreibt eine vorhandene Protokolldatei. |
| -[-] v`<nnnnnn|mmddhhmm>` | Fügt Datei Versionsinformationen an das Ende des Protokoll Dateinamens an. |
| -[-] RC`<task>` | Führt den Befehl aus, der bei jedem Schließen des Protokolls angegeben wird. |
| -[-] max.`<value>` | Maximale Protokolldatei Größe in MB oder maximale Anzahl von Datensätzen für SQL-Protokolle. |
| -[-] cnf`<[[hh:]mm:]ss>` | Wenn Time angegeben ist, wird eine neue Datei erstellt, wenn die angegebene Zeit abgelaufen ist. Wenn Time nicht angegeben wird, wird eine neue Datei erstellt, wenn die maximale Größe überschritten wird. |
| -y | Antworten auf Ja für alle Fragen ohne Aufforderung. |
| -CT`<perf|system|cycle>` | Gibt den Sitzungstyp der Ereignis Ablauf Verfolgung an. |
| -LN`<logger_name>` | Gibt den Namen der Protokollierung für Ereignis Ablauf Verfolgungs Sitzungen an. |
| -FT`<[[hh:]mm:]ss>` | Gibt den Timer für die Ereignis Ablauf Verfolgungs Sitzung an. |
| -[-] p`<provider [flags [level]]>` | Gibt einen einzelnen Ereignis Ablauf Verfolgungs Anbieter an, der aktiviert werden soll. |
| -PF`<filename>` | Gibt eine Datei an, die mehrere Ereignis Ablauf Verfolgungs Anbieter zum Aktivieren auflistet. Bei der Datei muss es sich um eine Textdatei handeln, die einen Anbieter pro Zeile enthält. |
| -[-] RT | Führt die Ereignis Ablauf Verfolgungs Sitzung im Echtzeitmodus aus. |
| -[-] UL | Führt die Ereignis Ablauf Verfolgungs Sitzung im Benutzer aus. |
| -SB`<value>` | Gibt die Puffergröße der Ereignis Ablauf Verfolgungs Sitzung in KB an. |
| -NB`<min max>` | Gibt die Anzahl der Sitzungs Puffer für die Ereignis Ablauf Verfolgung an. |
| -Modus`<globalsequence|localsequence|pagedmemory>` | Gibt den Protokollierungs Modus der Ereignis Ablauf Verfolgungs Sitzung an, einschließlich:<ul><li>**Globalsequence** : gibt an, dass die Ereignisüberwachung jedem empfangenen Ereignis eine Sequenznummer hinzufügt, unabhängig davon, welche Ablauf Verfolgungs Sitzung das Ereignis empfangen hat.</li><li>**Localsequence** : gibt an, dass der Ereignis Überwachungs Sequenznummern für Ereignisse hinzufügt, die bei einer bestimmten Ablauf Verfolgungs Sitzung empfangen werden. Wenn diese Option verwendet wird, können doppelte Sequenznummern über alle Sitzungen hinweg vorhanden sein, in jeder Ablauf Verfolgungs Sitzung jedoch eindeutig sein.</li><li>**Pgedmemory** : gibt an, dass die Ereignisüberwachung einen ausgelagerten Speicher anstelle des nicht ausgelagerten Standard Speicherpools für interne Puffer Belegungen verwendet.</li></ul> |
| /? | Zeigt die kontextbezogene Hilfe an. |

#### <a name="remarks"></a>Hinweise

- Wenn [-] aufgeführt ist, wird durch das Hinzufügen eines zusätzlichen Bindestrichs (-) die Option negiert.

### <a name="examples"></a>Beispiele

Zum Erstellen eines Ereignis-Ablauf Verfolgungs Daten Sammlers mit dem Namen trace_log mit einer Größe von weniger als 16 und nicht mehr als 256 Puffern, bei denen jeder Puffer 64 KB groß ist und die Ergebnisse in "c:\logfile" lautet, geben Sie Folgendes ein:

```
logman create trace trace_log -nb 16 256 -bs 64 -o c:\logfile
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman](logman.md)
