---
title: ntfrsutl
description: Referenz Artikel zum NTFRSUTL-Befehl, der die internen Tabellen, den Thread und die Arbeitsspeicher Informationen für den NT-Datei Replikations Dienst (NTFRS) absichert.
ms.topic: reference
ms.assetid: d7721a19-5a87-4ab6-b816-65d2da2c811f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6fdbb82322e2aaa130d396b4917f01e7b4391a31
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037258"
---
# <a name="ntfrsutl"></a>ntfrsutl

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sichert die internen Tabellen-, Thread-und Speicherinformationen für den NT-Datei Replikations Dienst (NTFRS) sowohl vom lokalen Server als auch vom Remote Server. Die Wiederherstellungs Einstellung für NTFRS im Dienststeuerungs-Manager (Service Control Manager, SCM) kann für die Suche und Aufbewahrung wichtiger Protokollereignisse auf dem Computer von entscheidender Bedeutung sein. Dieses Tool bietet eine bequeme Methode zum Überprüfen dieser Einstellungen.

## <a name="syntax"></a>Syntax

```
ntfrsutl[idtable|configtable|inlog|outlog][<computer>]
ntfrsutl[memory|threads|stage][<computer>]
ntfrsutl ds[<computer>]
ntfrsutl [sets][<computer>]
ntfrsutl [version][<computer>]
ntfrsutl poll[/quickly[=[<n>]]][/slowly[=[<n>]]][/now][<computer>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| IDtable | Gibt die ID-Tabelle an. |
| ConfigTable | Gibt die FRS-Konfigurations Tabelle an. |
| inlog | Gibt das eingehende Protokoll an. |
| OUTLOG | Gibt das ausgehende Protokoll an. |
| `<computer>` | Gibt den Computer an. |
| Arbeitsspeicher | Gibt die Speicherauslastung an. |
| Threads | Gibt die Speicherauslastung an. |
| Stufe | Gibt die Speicherauslastung an. |
| ds | Listet die Ansicht der DS des NTFRS-dienstanders auf. |
| Mengen | Gibt die aktiven Replikat Sätze an. |
| version | Gibt die API-und NtFrs-Dienst Versionen an. |
| Umfrage | Gibt die aktuellen Abruf Intervalle an.<ul><li>`/quickly` -Ruft schnell ab, bis eine stabile Konfiguration abgerufen wird.</li><li>`/quickly=` -Ruft schnell jede Standard Anzahl von Minuten ab.</li><li>`/quickly=<n>` -Ruft schnell alle *n* Minuten ab.</li><li>`/slowly` -Ruft langsam ab, bis eine stabile Konfiguration abgerufen wird.</li><li>`/slowly=` -Ruft langsam jede Standard Anzahl von Minuten ab.</li><li>`/slowly=<n>` -Ruft alle *n* Minuten langsam ab.</li><li>`/now` -Ruft jetzt ab.</li></ul>|
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie zum Bestimmen des Abruf Intervalls für die Datei Replikation Folgendes ein:

```
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1
```

Geben Sie Folgendes ein, um die aktuelle API-Version (Application Program Interface) von NTFRS zu ermitteln:

```
C:\Program Files\SupportTools>ntfrsutl version
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
