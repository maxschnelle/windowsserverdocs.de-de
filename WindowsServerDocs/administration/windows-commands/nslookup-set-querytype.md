---
title: nslookup set querytype
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5af54ac5-fc1a-4af6-977b-f8e97c8eba90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc992d83de8537c285b6d2d97e5f44545e2f930f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723606"
---
# <a name="nslookup-set-querytype"></a>nslookup set querytype

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Ressourcen Daten Satz für die Abfrage.
## <a name="syntax"></a>Syntax
```
set querytype=<ResourceRecordtype>
```
### <a name="parameters"></a>Parameter
<ResourceRecordtype>Gibt einen DNS-Ressourcen eingabentyp an. Der Standard Ressourcen Daten Satz-Typ ist. In der folgenden Tabelle sind die gültigen Werte für diesen Befehl aufgeführt.

| Wert |                                                   BESCHREIBUNG                                                   |
|-------|-----------------------------------------------------------------------------------------------------------------|
|   Ein   |                                      Gibt die IP-Adresse eines Computers&#39;s an.                                      |
|  ANY  |                                     Gibt die IP-Adresse eines Computers&#39;s an.                                      |
| CNAME |                                    Gibt einen kanonischen Namen für einen Alias an.                                     |
|  Ü  |                                  Gibt einen Gruppen Bezeichner eines Gruppennamens an.                                  |
| Hinfo |                          Gibt die CPU und den Typ des Betriebssystems eines Computers&#39;s an.                           |
|  MB   |                                        Gibt einen Post Fach Domänen Namen an.                                         |
|  MG   |                                         Gibt ein e-Mail-Gruppenmitglied an.                                          |
| MINFO |                                   Gibt Postfach-oder e-Mail-Listen Informationen an.                                   |
|  MR   |                                     Gibt den Namen der Umbenennungs Domäne an.                                      |
|  MX   |                                          Gibt den e-Mail-Austausch an                                          |
|  NS   |                                 Gibt einen DNS-Namen Server für die benannte Zone an.                                 |
|  PTR  | Gibt einen Computernamen an, wenn die Abfrage eine IP-Adresse ist. Andernfalls gibt den Zeiger auf andere Informationen an. |
|  SOA  |                                Gibt den Autorisierungs Anfang für eine DNS-Zone an.                                 |
|  TXT  |                                         Gibt die Textinformationen an.                                         |
|  UID  |                                         Gibt die Benutzer-ID an.                                          |
| Uinfo |                                         Gibt die Benutzerinformationen an.                                         |
|  Wert  |                                         Beschreibt einen bekannten Dienst.                                         |
| {Hilfe |                                                       ?}                                                        |

Zeigt eine kurze Zusammenfassung der <strong>nslookup</strong> -Unterbefehle an.
## <a name="remarks"></a>Bemerkungen
- Der <strong>Set Type</strong> -Befehl führt dieselbe Funktion aus wie der <strong>Set QueryType</strong> -Befehl.
- Weitere Informationen zu Ressourcen Daten Satz Typen finden Sie unter Request for Comment (RFC) 1035.
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  <a href = Command-Line-Syntax-Key.MD Data-RAW-Source =- [Command-Line Syntax Key](command-line-syntax-key.md)>Befehlszeilen-Syntax Schlüssel</a> <a href = nslookup-Set-Type.MD Data-RAW-Source =[nslookup Set Type](nslookup-set-type.md)>nslookup-fest gelegungstyp</a>
