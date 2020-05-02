---
title: logman Update-API
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6f322e52-0f9f-42b1-bd64-8b8f8fe086fc britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 42ee594bfb4578cebec062a5c2a81d11dae81349
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724317"
---
# <a name="logman-update-api"></a>logman Update-API

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktualisieren Sie die Eigenschaften eines vorhandenen API-Ablauf Verfolgungs Daten Sammlers.  

## <a name="syntax"></a>Syntax  
```  
logman update api <[-n] <name>> [options]  
```  
### <a name="parameters"></a>Parameter  

|                    Parameter                     |                                                                               BESCHREIBUNG                                                                               |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                        /?                        |                                                                    Zeigt die kontextbezogene Hilfe an.                                                                     |
|                -s<computer name>                |                                                          Führen Sie den Befehl auf dem angegebenen Remote Computer aus.                                                          |
|                 -config <value>                  |                                                         Gibt die Einstellungsdatei an, die Befehlsoptionen enthält.                                                         |
|                   [-n]<name>                    |                                                                       Name des Zielobjekts                                                                        |
| -f <bin&#124;bincirc&#124;CSV&#124;TSV&#124;SQL> |                                                            Gibt das Protokoll Format für den Datensammler an.                                                             |
|             -[-] u <Benutzer [Kennwort] >              | Gibt den Benutzer an, der als ausgeführt werden soll. Wenn Sie \* einen als Kennwort eingeben, wird eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, wenn Sie es an der Eingabeaufforderung eingeben. |
|    -m < [Start] [Ende] [[Start] [Ende] [...]] >    |                                                Wechseln Sie zu "manueller Start" oder "beenden" anstelle eines geplanten Anfangs-oder Endzeit Zeitraums.                                                 |
|                -RF < [[hh:] mm:] SS>                |                                                        Führt den Datensammler für den angegebenen Zeitraum aus.                                                         |
|        -b <M/d/yyyy h:mm: SS [am&#124;pm] >         |                                                              Beginnt mit dem Sammeln von Daten zum angegebenen Zeitpunkt.                                                               |
|        -e <M/d/yyyy h:mm: SS [am&#124;pm] >         |                                                               Beenden Sie die Datensammlung zum angegebenen Zeitpunkt.                                                                |
|                -Si < [[hh:] mm:] SS>                |                                                 Gibt das Stichproben Intervall für Leistungsdaten Sammler an.                                                  |
|              -o <Pfad&#124;DSN! Log>              |                                              Gibt die Ausgabeprotokoll Datei oder den DSN-und Protokoll Satz Namen in einer SQL-Datenbank an.                                               |
|                      -[-] r                       |                                                  Wiederholen Sie den Datensammler täglich zu den angegebenen Anfangs-und Endzeiten.                                                  |
|                      -[-] a                       |                                                                     Fügen Sie an eine vorhandene Protokolldatei an.                                                                     |
|                      -[-] OW                      |                                                                     Hiermit wird eine vorhandene Protokolldatei überschrieben.                                                                     |
|           -[-] v <nnnnnn&#124;mmddhhmm>           |                                                   Fügen Sie Datei Versionsinformationen an das Ende des Protokoll Dateinamens an.                                                   |
|                  -[-] RC<task>                   |                                                         Führen Sie den Befehl aus, der bei jedem Schließen des Protokolls angegeben wird.                                                          |
|                 -[-] max. <value>                  |                                                 Maximale Protokolldatei Größe in MB oder maximale Anzahl von Datensätzen für SQL-Protokolle.                                                  |
|              -[-] cnf-< [[hh:] mm:] SS>              |     Wenn Time angegeben ist, wird eine neue Datei erstellt, wenn die angegebene Zeit abgelaufen ist. Wenn Time nicht angegeben ist, erstellen Sie eine neue Datei, wenn die maximale Größe überschritten wird.     |
|                        -y                        |                                                             Antworten Sie auf Ja, um alle Fragen zu beantworten.                                                              |
|            -Mods <Pfad [Pfad [...]] >             |                                                          Gibt die Liste der Module an, von denen API-Aufrufe protokolliert werden.                                                           |
|     -inapis <Modul! API [Module! API [...]] >      |                                                         Gibt die Liste der bei der Protokollierung einzuschließenden API-Aufrufe an.                                                          |
|     -exapis <Modul! API [Module! API [...]] >      |                                                        Gibt die Liste der von der Protokollierung auszuschließenden API-Aufrufe an.                                                         |
|                     -[-] Ano                      |                                                     Verwenden Sie nur die API-Namen (-ANO), oder Protokollieren Sie keine (-ANO) API-Namen.                                                     |
|                  -[-] rekursiv                   |                                          Protokolliert (-rekursiv) oder protokolliert (rekursiv) APIs nicht rekursiv über die erste Ebene hinaus.                                           |
|                   -exe <value>                   |                                                        Gibt den vollständigen Pfad einer ausführbaren Datei für die API-Ablauf Verfolgung an                                                        |

## <a name="remarks"></a>Bemerkungen  
Wenn [-] aufgeführt ist, wird die-Option durch ein extra negiert.  
## <a name="examples"></a>Beispiele  
Der folgende Befehl aktualisiert den vorhandenen API-Ablaufverfolgungs-Leistungs beausdruck "trace_notepad" für die ausführbare Datei "c:\windows\notepad.exe", indem er den API-Aufruf "TlsGetValue" ausschließt, der vom Modul Kernel32  
```  
logman create api trace_notepad -exe c:\windows\notepad.exe -exapis kernel32.dll!TlsGetValue  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
[logman Create-API](logman-create-api.md)  
