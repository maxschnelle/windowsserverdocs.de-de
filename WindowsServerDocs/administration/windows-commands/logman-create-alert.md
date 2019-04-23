---
title: Logman Warnung erstellen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 93e6fc2b-5bf5-413b-84b4-be8b9dd3a57d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1bb131d4cff6dc40909a05c39e0819307ca472dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873821"
---
# <a name="logman-create-alert"></a>Logman Warnung erstellen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Erstellen Sie eine Warnungssammlung.  
  
## <a name="syntax"></a>Syntax  
```  
logman create alert <[-n] <name>> [options]  
```  
## <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|/?|Zeigt, die kontextbezogene Hilfe an.|  
|-s <computer name>|Führen Sie den Befehl auf dem angegebenen Remotecomputer.|  
|-config <value>|Gibt an, die Befehlsoptionen enthält Datei mit den Einstellungen.|  
|[-n] <name>|Der Name des Zielobjekts.|  
|-[-] u < Benutzer [Kennwort] >|Gibt die Ausführung als Benutzer an. Eingeben einer * für das Kennwort eine Aufforderung zur Kennworteingabe erzeugt. Das Kennwort wird nicht angezeigt, wenn Sie es an der kennworteingabeaufforderung eingeben.|  
|-m < [Start] [Start] [[Start] [Start] [...]] >|Ändern Sie in den manuellen Start oder beenden Sie, anstatt einem geplanten Zeitpunkt von Begin- und End.|  
|-rf < [[Hh:] mm:] ss >|Führen Sie den Datensammler für den angegebenen Zeitraum.|  
|-b < m/JJJJ hh: mm: [Uhr&#124;PM] >|Starten Sie das Sammeln von Daten zum angegebenen Zeitpunkt.|  
|-e: < m/JJJJ hh: mm: [Uhr&#124;PM] >|Beenden der Datensammlung von zum angegebenen Zeitpunkt.|  
|-si <[[hh:]mm:]ss>|Gibt das Beispiel für Performance Counter-Datensammler an.|  
|-o <path&#124;dsn!log>|Gibt an, dass die Ausgabeprotokolldatei oder der DSN einzurichten und sich Name in einer SQL­Datenbank.|  
|-[-]r|Wiederholen Sie den Datensammler täglich um bestimmten Anfangs- und Endzeit ein.|  
|-[-]a|Fügen Sie an einer vorhandenen Protokolldatei.|  
|-[-]ow|Überschreiben einer vorhandenen Protokolldatei an.|  
|-[-]v <nnnnnn&#124;mmddhhmm>|Fügen Sie Versionsinformationen für die Datei an das Ende der Name der Protokolldatei.|  
|-[-]rc <task>|Führen Sie den Befehl angegebenen jedes Mal, die das Protokoll geschlossen wird.|  
|-[-]max <value>|Maximale Größe der Protokolldatei in MB oder die maximale Anzahl von Datensätzen für die SQL-Protokolle.|  
|-[-]cnf <[[hh:]mm:]ss>|Wenn Zeit angegeben wird, erstellen Sie eine neue Datei, wenn die angegebene Zeit verstrichen ist. Wenn Zeit nicht angegeben ist, erstellen eine neue Datei ein, wenn die maximale Größe überschritten wird.|  
|-y|Beantworten Sie Ja, alle Fragen ohne Eingabeaufforderung.|  
|-cf <filename>|Gibt die Auflistung der zu erfassenden Leistungsindikatoren an. Die Datei sollte ein Name des Leistungsindikators pro Zeile enthalten.|  
|-[-]el|Aktiviert oder deaktiviert die berichterstellung Ereignisprotokoll.|  
|-ten < Schwellenwert [Schwellenwert [...]] >|Geben Sie Leistungsindikatoren und die Schwellenwerte für Warnung.|  
|-[-]rdcs <name>|Gibt an, den Sammlungssatz zu starten, wenn eine Warnung ausgelöst wird.|  
|-[-]tn <task>|Gibt an, die Aufgabe ausgeführt wird, wenn eine Warnung ausgelöst wird.|  
|-[-]targ <argument>|Gibt die Argumente der Aufgabe, die mit der Aufgabe, die mit -tn angegeben verwendet werden.|  
## <a name="remarks"></a>Hinweise  
Wobei [-] aufgelistet ist, negiert ein zusätzliches - die Option.  
## <a name="BKMK_examples"></a>Beispiele für  
Der folgende Befehl erstellt eine Warnung wird aufgerufen, New_alert, die ausgelöst wird, wenn der Performance Counter % Prozessorzeit in der Gruppe "Prozessor(_Total)-Leistungsindikator" den Wert dieses Indikators 50 überschreitet.  
```  
logman create alert new_alert -th "\Processor(_Total)\% Processor time>50"  
```  
> [!NOTE]  
> Der definierten Schwellenwert basiert auf den Wert, der von den Zähler, gesammelt werden, damit in diesem Beispiel der Wert 50, 50 % der Prozessorzeit entspricht.  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
