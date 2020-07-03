---
title: logman update counter
description: Referenz Artikel für den Befehl logman update Counter, mit dem die Eigenschaften eines vorhandenen Counter-Daten Sammlers aktualisiert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 607df6d5-876c-428d-a0b3-f59cb244e2ce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4bfeb3bf8e0bc88bdefcee308d5c77121477b095
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928588"
---
# <a name="logman-update-counter"></a>logman update counter

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktualisiert die Eigenschaften eines vorhandenen Counter-Daten Sammlers.

## <a name="syntax"></a>Syntax

```
logman update counter <[-n] <name>> [options]
```

### <a name="parameters"></a>Parameter


| Parameter | Beschreibung |
| --------- | ----------- |
| -s`<computer name>` | Führen Sie den Befehl auf dem angegebenen Remote Computer aus. |
| -config`<value>` | Gibt die Einstellungsdatei an, die Befehlsoptionen enthält. |
| [-n]`<name>` | Name des Zielobjekts |
| -f`<bin|bincirc>` | Gibt das Protokoll Format für den Datensammler an. |
| -[-] u`<user [password]>` | Gibt den Benutzer an, der als ausgeführt werden soll. Wenn Sie `*` für das Kennwort eingeben, wird eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, während Sie es an der Eingabeaufforderung eingeben. |
| -m`<[start] [stop] [[start] [stop] [...]]>` | Änderungen an manuellem starten oder beenden anstelle einer geplanten Anfangs-oder Endzeit. |
| -RF`<[[hh:]mm:]ss>` | Führt den Datensammler für den angegebenen Zeitraum aus. |
| -b`<M/d/yyyy h:mm:ss[AM|PM]>` | Beginnt mit dem Sammeln von Daten zum angegebenen Zeitpunkt. |
| -e `<M/d/yyyy h:mm:ss[AM|PM]>` | Beendet die Datensammlung zum angegebenen Zeitpunkt. |
| -Si`<[[hh:]mm:]ss>` | Gibt das Stichproben Intervall für Leistungsdaten Sammler an. |
| -o`<path|dsn!log>` | Gibt die Ausgabeprotokoll Datei oder den DSN-und Protokoll Satz Namen in einer SQL-Datenbank an. |
| -[-] r | Wiederholt den Datensammler täglich zu den angegebenen Anfangs-und Endzeiten. |
| -[-] a | Fügt eine vorhandene Protokolldatei an. |
| -[-] OW | Überschreibt eine vorhandene Protokolldatei. |
| -[-] v`<nnnnnn|mmddhhmm>` | Fügt Datei Versionsinformationen an das Ende des Protokoll Dateinamens an. |
| -[-] RC`<task>` | Führt den Befehl aus, der bei jedem Schließen des Protokolls angegeben wird. |
| -[-] max.`<value>` | Maximale Protokolldatei Größe in MB oder maximale Anzahl von Datensätzen für SQL-Protokolle. |
| -[-] cnf`<[[hh:]mm:]ss>` | Wenn Time angegeben ist, wird eine neue Datei erstellt, wenn die angegebene Zeit abgelaufen ist. Wenn Time nicht angegeben ist, erstellen Sie eine neue Datei, wenn die maximale Größe überschritten wird. |
| -y | Antworten auf Ja für alle Fragen ohne Aufforderung. |
| -CF`<filename>` | Gibt die zu sammelnden Leistungsindikatoren zum Auflisten von Dateien an. Die Datei sollte einen Leistungs Leistungs beendenamen pro Zeile enthalten. |
| -c`<path [path [ ]]>` | Gibt die zu sammelnden Leistungs Zählers an. |
| -SC`<value>` | Gibt die maximale Anzahl von Stichproben an, die mit einem Leistungsdaten Sammler erfasst werden sollen. |
| /? | Zeigt die kontextbezogene Hilfe an. |

#### <a name="remarks"></a>Hinweise

- Wenn [-] aufgeführt ist, wird durch das Hinzufügen eines zusätzlichen Bindestrichs (-) die Option negiert.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen Counter mit dem Namen *perf_log* zu erstellen, indem Sie den Wert "Prozessorzeit (%)" aus der Kategorie Prozessor (_Total)

```
logman create counter perf_log -c \Processor(_Total)\% Processor time
```

Zum Aktualisieren eines vorhandenen Zählers mit dem Namen *perf_log*, zum Ändern des Stichproben Intervalls in 10, zum Protokoll Format in CSV und zum Hinzufügen der Versionsverwaltung zum Namen der Protokolldatei im Format mmddhhmm geben Sie Folgendes ein:

```
logman update counter perf_log -si 10 -f csv -v mmddhhmm
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman Create Counter-Befehl](logman-create-counter.md)

- [logman-Befehl](logman.md)
