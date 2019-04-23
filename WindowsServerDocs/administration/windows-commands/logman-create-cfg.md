---
title: Logman erstellen cfg
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bfc87093-3ff5-4e19-aa93-d185fb8e2239
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0412ff8c535f5e9eef23b63eddbe129aeda97de1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868091"
---
# <a name="logman-create-cfg"></a>Logman erstellen cfg

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Erstellen Sie einen Datensammler Konfiguration.  
  
## <a name="syntax"></a>Syntax  
```  
logman create cfg <[-n] <name>> [options]  
```  
## <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|/?|Zeigt, die kontextbezogene Hilfe an.|  
|-s <computer name>|Führen Sie den Befehl auf dem angegebenen Remotecomputer.|  
|-config <value>|Gibt an, die Befehlsoptionen enthält Datei mit den Einstellungen.|  
|[-n] <name>|Der Name des Zielobjekts.|  
|-f < Bin&#124;Bincirc&#124;Csv&#124;Tsv&#124;Sql >|Gibt das Protokollformat für den Datensammler.|  
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
|-[-]ni|Aktivieren (-ni) oder zu deaktivieren (-ni) Netzwerk-Schnittstelle Abfragen.|  
|Reg - < Pfad [Pfad [...]] >|Gibt an, Registrierung Werte zu sammeln.|  
|-Mgt < Abfrage [Abfrage [...]] >|Gibt die WMI-Objekte, erfassen Sie mithilfe von SQL-Abfragesprache.|  
|-Ftc < Pfad [Pfad [...]] >|Gibt den vollständigen Pfad zu die Dateien zu sammeln.|  
## <a name="remarks"></a>Hinweise  
Wobei [-] aufgelistet ist, negiert ein zusätzliches - die Option.  
## <a name="BKMK_examples"></a>Beispiele für  
Der folgende Befehl erstellt einen Konfiguration-Datensammler-wird aufgerufen, mit dem Registrierungsschlüssel %%amp;quot;HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentverion Cfg_log\\.  
```  
logman create cfg cfg_log -reg "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentverion\\"  
```  
Der folgende Befehl erstellt einen Datensammler ein Konfiguration aufgerufen Cfg_log, in dem alle WMI-Objekte aus Root\wmi MSNdis_Vendordriverversion in der Datenbank aufgezeichnet.  
```  
logman create cfg cfg_log -mgt "root\wmi:select * FROM MSNdis_Vendordriverversion"  
```  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
