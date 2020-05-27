---
title: logman Create cfg
description: Referenz Thema für den Befehl logman Create cfg, mit dem ein Konfigurationsdaten Sammler erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bfc87093-3ff5-4e19-aa93-d185fb8e2239
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38d6b02351e515230a0041369217ba248ada4793
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820460"
---
# <a name="logman-create-cfg"></a>logman Create cfg

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt einen Konfigurationsdaten Sammler.

## <a name="syntax"></a>Syntax

```
logman create cfg <[-n] <name>> [options]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| -s`<computer name>` | Führt den Befehl auf dem angegebenen Remote Computer aus. |
| -config`<value>` | Gibt die Einstellungsdatei an, die Befehlsoptionen enthält. |
| [-n]`<name>` | Name des Zielobjekts |
| -[-] u`<user [password]>` | Gibt den Benutzer an, der als ausgeführt werden soll. Wenn Sie einen als Kennwort eingeben, wird \* eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, während Sie es an der Eingabeaufforderung eingeben. |
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
| -[-] NI | Aktiviert die Netzwerkschnittstellen Abfrage (-NI) oder deaktiviert (-NI). |
| -reg`<path [path [...]]>` | Gibt die zu sammelnden Registrierungs Werte an. |
| -mgt`<query [query [...]]>` | Gibt WMI-Objekte an, die mithilfe der SQL-Abfragesprache erfasst werden sollen. |
| -FTC`<path [path [...]]>` | Gibt den vollständigen Pfad zu den Dateien an, die gesammelt werden sollen. |
| /? | Zeigt die kontextbezogene Hilfe an. |

#### <a name="remarks"></a>Hinweise

- Wenn [-] aufgeführt ist, wird durch das Hinzufügen eines zusätzlichen Bindestrichs (-) die Option negiert.

### <a name="examples"></a>Beispiele

Um einen Konfigurationsdaten Sammler namens cfg_log zu erstellen, geben Sie mit dem Registrierungsschlüssel Folgendes ein `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentverion\` :

```
logman create cfg cfg_log -reg HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentverion\\
```

Um einen Konfigurationsdaten Sammler namens cfg_log zu erstellen, der alle WMI-Objekte aus `root\wmi` der Daten Bank Spalte aufzeichnet, geben Sie Folgendes ein `MSNdis_Vendordriverversion` :

```
logman create cfg cfg_log -mgt root\wmi:select * FROM MSNdis_Vendordriverversion
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman](logman.md)
