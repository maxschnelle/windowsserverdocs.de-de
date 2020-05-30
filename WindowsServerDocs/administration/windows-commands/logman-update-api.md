---
title: logman Update-API
description: Referenz Thema für den Befehl logman Update API, mit dem die Eigenschaften eines vorhandenen API-Überwachungsdaten Sammlers aktualisiert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6f322e52-0f9f-42b1-bd64-8b8f8fe086fc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0087edc7cd96bf2bf7611d9a3975d97384c02949
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222780"
---
# <a name="logman-update-api"></a>logman Update-API

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktualisiert die Eigenschaften eines vorhandenen API-Ablauf Verfolgungs Daten Sammlers.

## <a name="syntax"></a>Syntax

```
logman update api <[-n] <name>> [options]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| -s`<computer name>` | Führt den Befehl auf dem angegebenen Remote Computer aus. |
| -config`<value>` | Gibt die Einstellungsdatei an, die Befehlsoptionen enthält. |
| [-n]`<name>` | Name des Zielobjekts |
| -f`<bin|bincirc>` | Gibt das Protokoll Format für den Datensammler an. |
| -[-] u`<user [password]>` | Gibt den Benutzer an, der als ausgeführt werden soll. Wenn Sie einen als Kennwort eingeben, wird `*` eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, während Sie es an der Eingabeaufforderung eingeben. |
| -m`<[start] [stop] [[start] [stop] [...]]>` | Wurde zum manuellen Starten oder beenden gewechselt, anstelle einer geplanten Begin-oder End-Zeit. |
| -RF`<[[hh:]mm:]ss>` | Führt den Datensammler für den angegebenen Zeitraum aus. |
| -b`<M/d/yyyy h:mm:ss[AM|PM]>` | Beginnt mit dem Sammeln von Daten zum angegebenen Zeitpunkt. |
| -e `<M/d/yyyy h:mm:ss[AM|PM]>` | Beenden Sie die Datensammlung zum angegebenen Zeitpunkt. |
| -Si`<[[hh:]mm:]ss>` | Gibt das Stichproben Intervall für Leistungsdaten Sammler an. |
| -o`<path|dsn!log>` | Gibt die Ausgabeprotokoll Datei oder den DSN-und Protokoll Satz Namen in einer SQL-Datenbank an. |
| -[-] r | Wiederholen Sie den Datensammler täglich zu den angegebenen Anfangs-und Endzeiten. |
| -[-] a | Fügen Sie eine vorhandene Protokolldatei an. |
| -[-] OW | Hiermit wird eine vorhandene Protokolldatei überschrieben. |
| -[-] v`<nnnnnn|mmddhhmm>` | Fügt Datei Versionsinformationen an das Ende des Protokoll Dateinamens an. |
| -[-] RC`<task>` | Führen Sie den Befehl aus, der bei jedem Schließen des Protokolls angegeben wird. |
| -[-] max.`<value>` | Maximale Protokolldatei Größe in MB oder maximale Anzahl von Datensätzen für SQL-Protokolle. |
| -[-] cnf`<[[hh:]mm:]ss>` | Wenn Time angegeben ist, wird eine neue Datei erstellt, wenn die angegebene Zeit abgelaufen ist. Wenn Time nicht angegeben wird, wird eine neue Datei erstellt, wenn die maximale Größe überschritten wird. |
| -y | Antworten Sie auf Ja, um alle Fragen zu beantworten. |
| -Mods`<path [path [...]]>` | Gibt die Liste der Module an, von denen API-Aufrufe protokolliert werden. |
| -inapis` <module!api [module!api [...]]>` | Gibt die Liste der bei der Protokollierung einzuschließenden API-Aufrufe an. |
| -exapis`<module!api [module!api [...]]>` | Gibt die Liste der von der Protokollierung auszuschließenden API-Aufrufe an. |
| -[-] Ano | Verwenden Sie nur die API-Namen (-ANO), oder Protokollieren Sie keine (-ANO) API-Namen. |
| -[-] rekursiv | Protokolliert (-rekursiv) oder protokolliert (rekursiv) APIs nicht rekursiv über die erste Ebene hinaus. |
| -exe`<value>` | Gibt den vollständigen Pfad einer ausführbaren Datei für die API-Ablauf Verfolgung an |
| /? | Zeigt die kontextbezogene Hilfe an. |

#### <a name="remarks"></a>Hinweise

- Wenn [-] aufgeführt ist, wird durch das Hinzufügen eines zusätzlichen Bindestrichs (-) die Option negiert.

### <a name="examples"></a>Beispiele

Zum Aktualisieren eines vorhandenen API-Ablaufverfolgungs-Leistungs Zählers namens " *trace_notepad*" für die ausführbare Datei "c:\windows\notepad.exe", indem Sie den API-Aufruf "TlsGetValue", der vom Modul Kernel32

```
logman update api trace_notepad -exe c:\windows\notepad.exe -exapis kernel32.dll!TlsGetValue
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman Create API-Befehl](logman-create-api.md)

- [logman-Befehl](logman.md)
