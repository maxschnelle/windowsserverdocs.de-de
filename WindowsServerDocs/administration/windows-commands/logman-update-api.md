---
title: Logman update api
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6f322e52-0f9f-42b1-bd64-8b8f8fe086fc britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 285e4b527cf02061380ab2d9b5525e5b297a43cc
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437662"
---
# <a name="logman-update-api"></a>Logman update api

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Aktualisieren der Eigenschaften einer vorhandenen API-Ablaufverfolgung den Datensammler.  

## <a name="syntax"></a>Syntax  
```  
logman update api <[-n] <name>> [options]  
```  
## <a name="parameters"></a>Parameter  

|                    Parameter                     |                                                                               Beschreibung                                                                               |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                        /?                        |                                                                    Zeigt, die kontextbezogene Hilfe an.                                                                     |
|                -s <computer name>                |                                                          Führen Sie den Befehl auf dem angegebenen Remotecomputer.                                                          |
|                 -config <value>                  |                                                         Gibt an, die Befehlsoptionen enthält Datei mit den Einstellungen.                                                         |
|                   [-n] <name>                    |                                                                       Der Name des Zielobjekts.                                                                        |
| -f < Bin&#124;Bincirc&#124;Csv&#124;Tsv&#124;Sql > |                                                            Gibt das Protokollformat für den Datensammler.                                                             |
|             -[-] u < Benutzer [Kennwort] >              | Gibt die Ausführung als Benutzer an. Eingeben einer \* für das Kennwort eine Aufforderung zur Kennworteingabe erzeugt. Das Kennwort wird nicht angezeigt, wenn Sie es an der kennworteingabeaufforderung eingeben. |
|    -m < [Start] [Start] [[Start] [Start] [...]] >    |                                                Ändern Sie in den manuellen Start oder beenden Sie, anstatt einem geplanten Zeitpunkt von Begin- und End.                                                 |
|                -rf < [[Hh:] mm:] ss >                |                                                        Führen Sie den Datensammler für den angegebenen Zeitraum.                                                         |
|        -b < m/JJJJ hh: mm: [Uhr&#124;PM] >         |                                                              Starten Sie das Sammeln von Daten zum angegebenen Zeitpunkt.                                                               |
|        -e: < m/JJJJ hh: mm: [Uhr&#124;PM] >         |                                                               Beenden der Datensammlung von zum angegebenen Zeitpunkt.                                                                |
|                -si <[[hh:]mm:]ss>                |                                                 Gibt das Beispiel für Performance Counter-Datensammler an.                                                  |
|              -o <path&#124;dsn!log>              |                                              Gibt an, dass die Ausgabeprotokolldatei oder der DSN einzurichten und sich Name in einer SQL­Datenbank.                                               |
|                      -[-]r                       |                                                  Wiederholen Sie den Datensammler täglich um bestimmten Anfangs- und Endzeit ein.                                                  |
|                      -[-]a                       |                                                                     Fügen Sie an einer vorhandenen Protokolldatei.                                                                     |
|                      -[-]ow                      |                                                                     Überschreiben einer vorhandenen Protokolldatei an.                                                                     |
|           -[-]v <nnnnnn&#124;mmddhhmm>           |                                                   Fügen Sie Versionsinformationen für die Datei an das Ende der Name der Protokolldatei.                                                   |
|                  -[-]rc <task>                   |                                                         Führen Sie den Befehl angegebenen jedes Mal, die das Protokoll geschlossen wird.                                                          |
|                 -[-]max <value>                  |                                                 Maximale Größe der Protokolldatei in MB oder die maximale Anzahl von Datensätzen für die SQL-Protokolle.                                                  |
|              -[-]cnf <[[hh:]mm:]ss>              |     Wenn Zeit angegeben wird, erstellen Sie eine neue Datei, wenn die angegebene Zeit verstrichen ist. Wenn Zeit nicht angegeben ist, erstellen eine neue Datei ein, wenn die maximale Größe überschritten wird.     |
|                        -y                        |                                                             Beantworten Sie Ja, alle Fragen ohne Eingabeaufforderung.                                                              |
|            -Module < Pfad [Pfad [...]] >             |                                                          Gibt die Liste der Module-API-Aufrufe aus anmelden.                                                           |
|     -Inapis < Modul! api [Modul! api [...]] >      |                                                         Gibt die Liste der API-Aufrufe an die Protokollierung einschließt.                                                          |
|     -Exapis < Modul! api [Modul! api [...]] >      |                                                        Gibt die Liste der API-Aufrufe, Protokollierung ausgeschlossen werden sollen.                                                         |
|                     -[-]ano                      |                                                     Log (-Ano) API-Namen, oder melden Sie sich nicht nur (-Ano) API-Namen.                                                     |
|                  -[-]recursive                   |                                          Log (-rekursiv) oder melden Sie sich nicht (-rekursive) APIs rekursiv über die erste Ebene.                                           |
|                   -EXE-Datei <value>                   |                                                        Gibt den vollständigen Pfad zu einer ausführbaren Datei für die API-Ablaufverfolgung an.                                                        |

## <a name="remarks"></a>Hinweise  
Wobei [-] aufgelistet ist, negiert ein zusätzliches - die Option.  
## <a name="BKMK_examples"></a>Beispiele für  
Der folgende Befehl Updates die vorhandene API-Ablaufverfolgung-Leistungsindikator wird Trace_notepad für die ausführbare Datei c:\windows\notepad.exe aufgerufen, durch den API-Aufruf "Kernel32.dll" Modul "erzeugten TlsGetValue ausschließen.  
```  
logman create api trace_notepad -exe c:\windows\notepad.exe -exapis kernel32.dll!TlsGetValue  
```  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
[Logman-api erstellen](logman-create-api.md)  
