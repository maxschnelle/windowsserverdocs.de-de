---
title: nslookup set type
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5248e314-fac1-413e-81dc-bbe0a0873ba5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9a9ccc7dde40b93db5f331930bc405c98764483d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723535"
---
# <a name="nslookup-set-type"></a>nslookup set type

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Ressourcen Daten Satz für die Abfrage.
## <a name="syntax"></a>Syntax
```
set type=<ResourceRecordtype>
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
  <a href = Command-Line-Syntax-Key.MD Data-RAW-Source =- [Command-Line Syntax Key](command-line-syntax-key.md)>Befehlszeilen-Syntax Schlüssel</a> <a href = nslookup-Set-QueryType.MD Data-RAW-Source =[nslookup Set QueryType](nslookup-set-querytype.md)>nslookup Set QueryType</a>
