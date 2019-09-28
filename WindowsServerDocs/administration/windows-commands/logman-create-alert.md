---
title: Warnung zu logman Create
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 9420c486d4c6161c2c5724384f0d916448164a2a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374579"
---
# <a name="logman-create-alert"></a>Warnung zu logman Create

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellen Sie einen Warnungs Datensammler.  

## <a name="syntax"></a>Syntax  
```  
logman create alert <[-n] <name>> [options]  
```  
## <a name="parameters"></a>Parameter  

|                 Parameter                  |                                                                               Beschreibung                                                                               |
|--------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                     /?                     |                                                                    Zeigt die kontextbezogene Hilfe an.                                                                     |
|             -s <computer name>             |                                                          Führen Sie den Befehl auf dem angegebenen Remote Computer aus.                                                          |
|              -config <value>               |                                                         Gibt die Einstellungsdatei an, die Befehlsoptionen enthält.                                                         |
|                [-n] <name>                 |                                                                       Der Name des Zielobjekts.                                                                        |
|          -[-] u < Benutzer [Kennwort] >           | Gibt den Benutzer an, der als ausgeführt werden soll. Wenn Sie einen \* für das Kennwort eingeben, wird eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, wenn Sie es an der Eingabeaufforderung eingeben. |
| -m < [Start] [Ende] [[Start] [Ende] [...]] > |                                                Wechseln Sie zu "manueller Start" oder "beenden" anstelle eines geplanten Anfangs-oder Endzeit Zeitraums.                                                 |
|             -RF < [[hh:] mm:] SS >             |                                                        Führt den Datensammler für den angegebenen Zeitraum aus.                                                         |
|     -b < M/d/yyyy h:mm: SS [am&#124;pm] >      |                                                              Beginnt mit dem Sammeln von Daten zum angegebenen Zeitpunkt.                                                               |
|     -e < M/d/yyyy h:mm: SS [am&#124;pm] >      |                                                               Beenden Sie die Datensammlung zum angegebenen Zeitpunkt.                                                                |
|             -Si < [[hh:] mm:] SS >             |                                                 Gibt das Stichproben Intervall für Leistungsdaten Sammler an.                                                  |
|           -o < Pfad&#124;DSN! Log >           |                                              Gibt die Ausgabeprotokoll Datei oder den DSN-und Protokoll Satz Namen in einer SQL-Datenbank an.                                               |
|                   -[-] r                    |                                                  Wiederholen Sie den Datensammler täglich zu den angegebenen Anfangs-und Endzeiten.                                                  |
|                   -[-] a                    |                                                                     Fügen Sie an eine vorhandene Protokolldatei an.                                                                     |
|                   -[-] OW                   |                                                                     Hiermit wird eine vorhandene Protokolldatei überschrieben.                                                                     |
|        -[-] v < nnnnnn&#124;mmddhhmm >        |                                                   Fügen Sie Datei Versionsinformationen an das Ende des Protokoll Dateinamens an.                                                   |
|               -[-] RC <task>                |                                                         Führen Sie den Befehl aus, der bei jedem Schließen des Protokolls angegeben wird.                                                          |
|              -[-] max. <value>               |                                                 Maximale Protokolldatei Größe in MB oder maximale Anzahl von Datensätzen für SQL-Protokolle.                                                  |
|           -[-] cnf-< [[hh:] mm:] SS >           |     Wenn Time angegeben ist, wird eine neue Datei erstellt, wenn die angegebene Zeit abgelaufen ist. Wenn Time nicht angegeben ist, erstellen Sie eine neue Datei, wenn die maximale Größe überschritten wird.     |
|                     -y                     |                                                             Antworten Sie auf Ja, um alle Fragen zu beantworten.                                                              |
|               -CF <filename>               |                       Gibt die zu sammelnden Leistungsindikatoren zum Auflisten von Dateien an. Die Datei sollte einen Leistungs Leistungs beendenamen pro Zeile enthalten.                        |
|                   -[-] El                   |                                                                Aktiviert oder deaktiviert die Ereignisprotokoll Berichterstattung.                                                                 |
|     -Th < Schwellenwert [Schwellenwert [...]] >      |                                                        Geben Sie Zähler und deren Schwellenwerte für eine Warnung an.                                                        |
|              -[-] RDCS <name>               |                                                     Gibt den Datensammler Satz an, der gestartet werden soll, wenn eine Warnung ausgelöst wird.                                                      |
|               -[-] TN <task>                |                                                             Gibt die Aufgabe an, die ausgeführt wird, wenn eine Warnung ausgelöst wird.                                                              |
|            -[-] Targ <argument>             |                                               Gibt die Task Argumente an, die für die mit-TN angegebene Aufgabe verwendet werden sollen.                                                |

## <a name="remarks"></a>Hinweise  
Wenn [-] aufgeführt ist, wird die-Option durch ein extra negiert.  
## <a name="BKMK_examples"></a>Beispiele  
Mit dem folgenden Befehl wird eine Warnung namens new_alert erstellt, die ausgelöst wird, wenn der Leistungswert "% Processor Time" in der Leistungs Schwellenwert Gruppe "Prozessor" (_Total) den Wert von 50 überschreitet.  
```  
logman create alert new_alert -th "\Processor(_Total)\% Processor time>50"  
```  
> [!NOTE]
> Der definierte Schwellenwert basiert auf dem Wert, der vom Leistungs Schwellenwert erfasst wird. in diesem Beispiel entspricht der Wert 50 der Prozessorzeit von 50%.  
> #### <a name="additional-references"></a>Weitere Verweise  
> [logman](logman.md)  
