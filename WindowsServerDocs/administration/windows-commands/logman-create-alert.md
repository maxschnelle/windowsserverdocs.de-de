---
title: Warnung zu logman Create
description: Referenz Thema für den Befehl logman Create Alert, mit dem ein Warnungs Datensammler erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 93e6fc2b-5bf5-413b-84b4-be8b9dd3a57d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 10d19f6c86d09c698a6871ae0f0e530c5189c0ca
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222830"
---
# <a name="logman-create-alert"></a>Warnung zu logman Create

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt einen Warnungs Datensammler.

## <a name="syntax"></a>Syntax

```
logman create alert <[-n] <name>> [options]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| -s`<computer name>` | Führen Sie den Befehl auf dem angegebenen Remote Computer aus. |
| -config`<value>` | Gibt die Einstellungsdatei an, die Befehlsoptionen enthält. |
| [-n]`<name>` | Name des Zielobjekts |
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
| -[-] cnf`<[[hh:]mm:]ss>` | Wenn Time angegeben ist, wird eine neue Datei erstellt, wenn die angegebene Zeit abgelaufen ist. Wenn Time nicht angegeben wird, wird eine neue Datei erstellt, wenn die maximale Größe überschritten wird. |
| -y | Antworten auf Ja für alle Fragen ohne Aufforderung. |
| -CF`<filename>` | Gibt die zu sammelnden Leistungsindikatoren zum Auflisten von Dateien an. Die Datei sollte einen Leistungs Leistungs beendenamen pro Zeile enthalten. |
| -[-] El | Aktiviert oder deaktiviert die Ereignisprotokoll Berichterstattung. |
| -Th`<threshold [threshold [...]]>` | Geben Sie Zähler und deren Schwellenwerte für eine Warnung an. |
| -[-] RDCS`<name>` | Gibt den Datensammler Satz an, der gestartet werden soll, wenn eine Warnung ausgelöst wird. |
| -[-] TN`<task>` | Gibt die Aufgabe an, die ausgeführt wird, wenn eine Warnung ausgelöst wird. |
| -[-] Targ`<argument>` | Gibt die Task Argumente an, die für die mit-TN angegebene Aufgabe verwendet werden sollen. |
| /? | Zeigt die kontextbezogene Hilfe an. |

#### <a name="remarks"></a>Hinweise

- Wenn [-] aufgeführt ist, wird durch das Hinzufügen eines zusätzlichen Bindestrichs (-) die Option negiert.

### <a name="examples"></a>Beispiele

Um eine neue Warnung namens *new_alert*zu erstellen, die ausgelöst wird, wenn der Leistungswert "% Processor Time" in der Leistungs Schwellenwert Gruppe "Prozessor" (_Total) den Wert von 50 überschreitet, geben Sie Folgendes ein:

```
logman create alert new_alert -th \Processor(_Total)\% Processor time>50
```

> [!NOTE]
> Der definierte Schwellenwert basiert auf dem Wert, der vom Leistungs Schwellenwert erfasst wird. in diesem Beispiel entspricht der Wert 50 der Prozessorzeit von 50%.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman update Alert-Befehl](logman-update-alert.md)

- [logman-Befehl](logman.md)
