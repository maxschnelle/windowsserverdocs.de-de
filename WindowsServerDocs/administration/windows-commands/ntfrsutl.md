---
title: ntfrsutl
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d7721a19-5a87-4ab6-b816-65d2da2c811f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 14e718550247b8854073407146456d366d562d2b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837993"
---
# <a name="ntfrsutl"></a>ntfrsutl

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sichert die internen Tabellen-, Thread-und Speicherinformationen für den NT-Datei Replikations Dienst \(NTFRS-\). Sie wird auf lokalen und Remote Servern ausgeführt. Die Wiederherstellungs Einstellung für NTFRS im Dienststeuerungs-Manager \(SCM\) kann für die Suche nach und die Aufbewahrung wichtiger Protokollereignisse auf dem Computer von entscheidender Bedeutung sein. Dieses Tool bietet eine bequeme Methode zum Überprüfen dieser Einstellungen.   
  
## <a name="syntax"></a>Syntax  
  
```  
ntfrsutl[idtable|configtable|inlog|outlog][<computer>]  
ntfrsutl[memory|threads|stage][<computer>]  
ntfrsutl ds[<computer>]  
ntfrsutl [sets][<computer>]  
ntfrsutl [version][<computer>]  
ntfrsutl poll[/quickly[=[<N>]]][/slowly[=[<N>]]][/now][<computer>]  
```  
  
#### <a name="parameters"></a>Parameter  
  
|  Parameter  |                                                                                                                                                                                                                                                                                                                                        Beschreibung                                                                                                                                                                                                                                                                                                                                         |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   IDtable   |                                                                                                                                                                                                                                                                                                                                          ID-Tabelle                                                                                                                                                                                                                                                                                                                                          |
| ConfigTable |                                                                                                                                                                                                                                                                                                                                  FRS-Konfigurations Tabelle                                                                                                                                                                                                                                                                                                                                   |
|    inlog    |                                                                                                                                                                                                                                                                                                                                        Eingehendes Protokoll                                                                                                                                                                                                                                                                                                                                         |
|   OUTLOG    |                                                                                                                                                                                                                                                                                                                                        Ausgeh Endes Protokoll                                                                                                                                                                                                                                                                                                                                        |
| <computer>  |                                                                                                                                                                                                                                                                                                                                  Gibt den Computer an.                                                                                                                                                                                                                                                                                                                                   |
|   Memory    |                                                                                                                                                                                                                                                                                                                                        Speicherauslastung                                                                                                                                                                                                                                                                                                                                        |
|   Threads   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|    Bühne    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|     DS      |                                                                                                                                                                                                                                                                                                                         Listet die Ansicht der DS des NTFRS-dienstanders auf.                                                                                                                                                                                                                                                                                                                          |
|    Mengen     |                                                                                                                                                                                                                                                                                                                             Gibt die aktiven Replikat Gruppen an                                                                                                                                                                                                                                                                                                                              |
|   version   |                                                                                                                                                                                                                                                                                                                       Gibt die API-und NtFrs-Dienst Versionen an.                                                                                                                                                                                                                                                                                                                        |
|    Umfrage     | Gibt die aktuellen Abruf Intervalle an.<p>Parameter:<p><ul><li>**\/schnell**\[ **\=** \[ <N>\]\]\(\)<p><ul><li>**schnelles** \- schneller Abfragen, bis eine stabile Konfiguration wiederholt wird</li><li>**schnell\=** \- in jedem Standard Minuten schnell Abfragen.</li><li>**schnelles\=** <N> \- Abrufe schnell alle *N* Minuten</li></ul></li><li>**\/langsam**\[ **\=** \[ <N>\]\] \(langsam abfragt\)<p><ul><li>**langsam** \- Umfragen langsam, bis eine stabile Konfiguration abgerufen wird.</li><li>**langsam\=** \- werden alle Standard Minuten langsam abgerufen</li><li>**langsam\=** <N> \- alle *N* Minutenschnelle Abfragen</li></ul></li><li>jetzt **\/** \(jetzt abruft\)</li></ul> |
|     \/?     |                                                                                                                                                                                                                                                                                                                            Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                                                                                                                            |
  
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
So bestimmen Sie das Abruf Intervall für die Datei Replikation:  
  
```  
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1  
```  
  
So bestimmen Sie die aktuelle NTFRS-Anwendungsprogramm Schnittstelle \(API-\) Version:  
  
```  
C:\Program Files\SupportTools>ntfrsutl version  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
  
  

