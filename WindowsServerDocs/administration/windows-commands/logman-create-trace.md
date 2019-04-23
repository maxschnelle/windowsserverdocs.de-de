---
title: Logman Ablaufverfolgung erstellen.
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b4dfecd-6f56-4c51-b622-c2054b4aabd7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 065c5bfc9278d4e7deef453ee8bd3e20296d3a56
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832281"
---
# <a name="logman-create-trace"></a>Logman Ablaufverfolgung erstellen.

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Erstellen Sie eine ereignisdatensammlung für die Ablaufverfolgung ein.  
  
## <a name="syntax"></a>Syntax  
```  
logman create trace <[-n] <name>> [options]  
```  
## <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|/?|Zeigt, die kontextbezogene Hilfe an.|  
|-s <computer name>|Führen Sie den Befehl auf dem angegebenen Remotecomputer.|  
|-config <value>|Gibt an, die Befehlsoptionen enthält Datei mit den Einstellungen.|  
|-ets|Senden von Befehlen an Ereignisablaufverfolgungssitzungen direkt ohne Speichern oder zu planen.|  
|[-n] <name>|Der Name des Zielobjekts.|  
|-f < Bin&#124;Bincirc&#124;Csv&#124;Tsv&#124;Sql >|Gibt das Protokollformat für den Datensammler.|  
|-[-] u < Benutzer [Kennwort] >|Gibt die Ausführung als Benutzer an. Eingeben einer * für das Kennwort eine Aufforderung zur Kennworteingabe erzeugt. Das Kennwort wird nicht angezeigt, wenn Sie es an der kennworteingabeaufforderung eingeben.|  
|-m < [Start] [Start] [[Start] [Start] [...]] >|Ändern Sie in den manuellen Start oder beenden Sie, anstatt einem geplanten Zeitpunkt von Begin- und End.|  
|-rf < [[Hh:] mm:] ss >|Führen Sie den Datensammler für den angegebenen Zeitraum.|  
|-b < m/JJJJ hh: mm: [Uhr&#124;PM] >|Starten Sie das Sammeln von Daten zum angegebenen Zeitpunkt.|  
|-e: < m/JJJJ hh: mm: [Uhr&#124;PM] >|Beenden der Datensammlung von zum angegebenen Zeitpunkt.|  
|-o <path&#124;dsn!log>|Gibt an, dass die Ausgabeprotokolldatei oder der DSN einzurichten und sich Name in einer SQL­Datenbank.|  
|-[-]r|Wiederholen Sie den Datensammler täglich um bestimmten Anfangs- und Endzeit ein.|  
|-[-]a|Fügen Sie an einer vorhandenen Protokolldatei.|  
|-[-]ow|Überschreiben einer vorhandenen Protokolldatei an.|  
|-[-]v <nnnnnn&#124;mmddhhmm>|Fügen Sie Versionsinformationen für die Datei an das Ende der Name der Protokolldatei.|  
|-[-]rc <task>|Führen Sie den Befehl angegebenen jedes Mal, die das Protokoll geschlossen wird.|  
|-[-]max <value>|Maximale Größe der Protokolldatei in MB oder die maximale Anzahl von Datensätzen für die SQL-Protokolle.|  
|-[-]cnf <[[hh:]mm:]ss>|Wenn Zeit angegeben wird, erstellen Sie eine neue Datei, wenn die angegebene Zeit verstrichen ist. Wenn Zeit nicht angegeben ist, erstellen eine neue Datei ein, wenn die maximale Größe überschritten wird.|  
|-y|Beantworten Sie Ja, alle Fragen ohne Eingabeaufforderung.|  
|-ct <perf&#124;system&#124;cycle>|Gibt den Typ der Uhr Ereignisablaufverfolgungs-Sitzung an.|  
|-ln < Logger_name >|Gibt den Protokollierungsnamen für Trace-Ereignissitzungen.|  
|-ft < [[Hh:] mm:] ss >|Gibt den Leerungszeitgeber Ereignisablaufverfolgungs-Sitzung an.|  
|-[-] p < Anbieter [Flags [Level]] >|Gibt einen einzelnen Anbieter für Ereignisablaufverfolgung zu aktivieren.|  
|-pf <filename>|Gibt eine Datei mit dem Auflisten von Ablaufverfolgungsanbietern zu aktivieren. Die Datei sollte eine Textdatei mit einem Anbieter pro Zeile.|  
|-[-]rt|Die Ereignisablaufverfolgungs-Sitzung im Real-Time-Modus ausführen.|  
|-[-] Ul|Die Ereignisablaufverfolgungs-Sitzung im Benutzermodus ausgeführt.|  
|-bs <value>|Gibt die Puffergröße Ereignisablaufverfolgungs-Sitzung in kb.|  
|-nb <min max>|Gibt die Anzahl der Puffer von Ereignisablaufverfolgungs-Sitzung an.|  
|-mode <globalsequence&#124;localsequence&#124;pagedmemory>|Gibt an, die Ereignis-Ablaufverfolgung Sitzungsmodus Protokollierung.<br /><br />**Globalsequence** gibt an, dass die Ereignis-Ablaufverfolgung Datenträgers eine Sequenznummer zu jedem Ereignis er empfängt, die unabhängig von der Ablaufverfolgung Sitzung das Ereignis empfangen.<br /><br />**Localsequence** gibt an, dass die Ereignis-Ablaufverfolgung Sequenznummern für Ereignisse, die auf eine bestimmte ereignisablaufverfolgungs-Sitzung empfangen hinzufügen. Wenn die **Localsequence** Option verwendet wird, doppelte Sequenznummern können sind in allen Sitzungen vorhanden, jedoch werden in jeder ereignisablaufverfolgungs-Sitzung eindeutig sein.<br /><br />**Pagedmemory** gibt an, dass die Ereignis-Ablaufverfolgung für die internen pufferzuordnungen ausgelagerter Speicher anstelle von den Standardpool für nicht ausgelagerte Arbeitsspeicher verwenden.|  
## <a name="remarks"></a>Hinweise  
Wobei [-] aufgelistet ist, negiert ein zusätzliches - die Option.  
## <a name="BKMK_examples"></a>Beispiele für  
Im folgende Beispiel erstellt ein Trace-ereignisdatensammlung auf, die Trace_log verwenden keine Puffer weniger als 16 und nicht mehr als 256, für jeden Puffer 64kb Groß aufgerufen und gibt die Ergebnisse an den Speicherort c:\logfile.  
```  
logman create trace trace_log -nb 16 256 -bs 64 -o c:\logfile  
```  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
