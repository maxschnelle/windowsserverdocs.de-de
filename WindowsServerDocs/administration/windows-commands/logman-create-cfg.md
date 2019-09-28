---
title: logman Create cfg
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 9a9dffb308c9c5b73777aa2a2b4dd6e0204699ec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374590"
---
# <a name="logman-create-cfg"></a>logman Create cfg

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellen Sie einen Konfigurationsdaten Sammler.  

## <a name="syntax"></a>Syntax  
```  
logman create cfg <[-n] <name>> [options]  
```  
## <a name="parameters"></a>Parameter  

|                    Parameter                     |                                                                               Beschreibung                                                                               |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                        /?                        |                                                                    Zeigt die kontextbezogene Hilfe an.                                                                     |
|                -s <computer name>                |                                                          Führen Sie den Befehl auf dem angegebenen Remote Computer aus.                                                          |
|                 -config <value>                  |                                                         Gibt die Einstellungsdatei an, die Befehlsoptionen enthält.                                                         |
|                   [-n] <name>                    |                                                                       Der Name des Zielobjekts.                                                                        |
| -f < bin&#124;bincirc&#124;CSV&#124;TSV&#124;SQL > |                                                            Gibt das Protokoll Format für den Datensammler an.                                                             |
|             -[-] u < Benutzer [Kennwort] >              | Gibt den Benutzer an, der als ausgeführt werden soll. Wenn Sie einen \* für das Kennwort eingeben, wird eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, wenn Sie es an der Eingabeaufforderung eingeben. |
|    -m < [Start] [Ende] [[Start] [Ende] [...]] >    |                                                Wechseln Sie zu "manueller Start" oder "beenden" anstelle eines geplanten Anfangs-oder Endzeit Zeitraums.                                                 |
|                -RF < [[hh:] mm:] SS >                |                                                        Führt den Datensammler für den angegebenen Zeitraum aus.                                                         |
|        -b < M/d/yyyy h:mm: SS [am&#124;pm] >         |                                                              Beginnt mit dem Sammeln von Daten zum angegebenen Zeitpunkt.                                                               |
|        -e < M/d/yyyy h:mm: SS [am&#124;pm] >         |                                                               Beenden Sie die Datensammlung zum angegebenen Zeitpunkt.                                                                |
|                -Si < [[hh:] mm:] SS >                |                                                 Gibt das Stichproben Intervall für Leistungsdaten Sammler an.                                                  |
|              -o < Pfad&#124;DSN! Log >              |                                              Gibt die Ausgabeprotokoll Datei oder den DSN-und Protokoll Satz Namen in einer SQL-Datenbank an.                                               |
|                      -[-] r                       |                                                  Wiederholen Sie den Datensammler täglich zu den angegebenen Anfangs-und Endzeiten.                                                  |
|                      -[-] a                       |                                                                     Fügen Sie an eine vorhandene Protokolldatei an.                                                                     |
|                      -[-] OW                      |                                                                     Hiermit wird eine vorhandene Protokolldatei überschrieben.                                                                     |
|           -[-] v < nnnnnn&#124;mmddhhmm >           |                                                   Fügen Sie Datei Versionsinformationen an das Ende des Protokoll Dateinamens an.                                                   |
|                  -[-] RC <task>                   |                                                         Führen Sie den Befehl aus, der bei jedem Schließen des Protokolls angegeben wird.                                                          |
|                 -[-] max. <value>                  |                                                 Maximale Protokolldatei Größe in MB oder maximale Anzahl von Datensätzen für SQL-Protokolle.                                                  |
|              -[-] cnf-< [[hh:] mm:] SS >              |     Wenn Time angegeben ist, wird eine neue Datei erstellt, wenn die angegebene Zeit abgelaufen ist. Wenn Time nicht angegeben ist, erstellen Sie eine neue Datei, wenn die maximale Größe überschritten wird.     |
|                        -y                        |                                                             Antworten Sie auf Ja, um alle Fragen zu beantworten.                                                              |
|                      -[-] NI                      |                                                         Aktivieren Sie (-NI), oder deaktivieren Sie die Netzwerkschnittstellen Abfrage (-NI).                                                          |
|             -reg < Pfad [Pfad [...]] >             |                                                                 Gibt die zu sammelnden Registrierungs Werte an.                                                                 |
|            -mgt < Abfrage [Abfrage [...]] >            |                                                      Gibt WMI-Objekte an, die mithilfe der SQL-Abfragesprache erfasst werden sollen.                                                       |
|             -FTC < Pfad [Pfad [...]] >             |                                                           Gibt den vollständigen Pfad zu den Dateien an, die gesammelt werden sollen.                                                            |

## <a name="remarks"></a>Hinweise  
Wenn [-] aufgeführt ist, wird die-Option durch ein extra negiert.  
## <a name="BKMK_examples"></a>Beispiele  
Der folgende Befehl erstellt einen Konfigurationsdaten Sammler namens cfg_log mit dem Registrierungsschlüssel HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows nt\currentverion @ no__t-0.  
```  
logman create cfg cfg_log -reg "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentverion\\"  
```  
Der folgende Befehl erstellt einen Konfigurationsdaten Sammler namens cfg_log, der alle WMI-Objekte aus root\wmi in der Daten Bank Spalte MSNdis_Vendordriverversion aufzeichnet.  
```  
logman create cfg cfg_log -mgt "root\wmi:select * FROM MSNdis_Vendordriverversion"  
```  
#### <a name="additional-references"></a>Weitere Verweise  
[logman](logman.md)  
