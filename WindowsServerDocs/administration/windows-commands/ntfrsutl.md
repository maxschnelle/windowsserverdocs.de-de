---
title: ntfrsutl
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d7721a19-5a87-4ab6-b816-65d2da2c811f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc1275b7936a88b14b7658e2fe27d3958a035a04
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820924"
---
# <a name="ntfrsutl"></a>ntfrsutl

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sichert die internen Tabellen-, Thread-und Speicherinformationen für den NT-Datei Replikations Dienst \( NTFRS \) . Sie wird auf lokalen und Remote Servern ausgeführt. Die Wiederherstellungs Einstellung für NTFRS im Dienststeuerungs-Manager \( SCM \) kann für die Suche und Aufbewahrung wichtiger Protokollereignisse auf dem Computer von entscheidender Bedeutung sein. Dieses Tool bietet eine bequeme Methode zum Überprüfen dieser Einstellungen.

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

|  Parameter  |                                                                                                                                                                                                                                                                                                                                        BESCHREIBUNG                                                                                                                                                                                                                                                                                                                                         |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   IDtable   |                                                                                                                                                                                                                                                                                                                                          ID-Tabelle                                                                                                                                                                                                                                                                                                                                          |
| ConfigTable |                                                                                                                                                                                                                                                                                                                                  FRS-Konfigurations Tabelle                                                                                                                                                                                                                                                                                                                                   |
|    inlog    |                                                                                                                                                                                                                                                                                                                                        Eingehendes Protokoll                                                                                                                                                                                                                                                                                                                                         |
|   OUTLOG    |                                                                                                                                                                                                                                                                                                                                        Ausgeh Endes Protokoll                                                                                                                                                                                                                                                                                                                                        |
| <computer>  |                                                                                                                                                                                                                                                                                                                                  Gibt den Computer an.                                                                                                                                                                                                                                                                                                                                   |
|   memory    |                                                                                                                                                                                                                                                                                                                                        Speicherauslastung                                                                                                                                                                                                                                                                                                                                        |
|   Threads   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|    Stufe    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|     ds      |                                                                                                                                                                                                                                                                                                                         Listet die Ansicht der DS des NTFRS-dienstanders auf.                                                                                                                                                                                                                                                                                                                          |
|    Mengen     |                                                                                                                                                                                                                                                                                                                             Gibt die aktiven Replikat Gruppen an                                                                                                                                                                                                                                                                                                                              |
|   version   |                                                                                                                                                                                                                                                                                                                       Gibt die API-und NtFrs-Dienst Versionen an.                                                                                                                                                                                                                                                                                                                        |
|    Umfrage     | Gibt die aktuellen Abruf Intervalle an.<p>Parameter:<p><ul><li>** \/ schnell** \[ **\=** \[ <N>\]\]\( Schnelle Umfragen  \)<p><ul><li>**schnell** \- Ruft schnell auf, bis eine stabile Konfiguration wiederholt wird.</li><li>**schnell \= ** Ruft \- schnell alle Standard Minuten ab.</li><li>**schnell \= ** <N> \-Schneller Abruf alle *N* Minuten</li></ul></li><li>** \/ langsam** \[ **\=** \[ <N>\]\] \(Langsam Abfragen\)<p><ul><li>**langsam** \- Ruft langsam auf, bis eine stabile Konfiguration abgerufen wird.</li><li>**langsam \= ** Ruft \- alle Standard Minuten langsam ab</li><li>**langsam \= ** <N> \-Schneller Abruf alle *N* Minuten</li></ul></li><li>** \/ jetzt** \( Jetzt abfragt\)</li></ul> |
|     \/?     |                                                                                                                                                                                                                                                                                                                            Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                                                                                                                            |

## <a name="examples"></a>Beispiele
So bestimmen Sie das Abruf Intervall für die Datei Replikation:

```
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1
```

So bestimmen Sie die aktuelle API-Version der NTFRS-Anwendungsprogramm Schnittstelle \( \) :

```
C:\Program Files\SupportTools>ntfrsutl version
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)




