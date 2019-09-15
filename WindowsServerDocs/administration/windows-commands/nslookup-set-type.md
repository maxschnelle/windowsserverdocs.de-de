---
title: nslookup set type
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5248e314-fac1-413e-81dc-bbe0a0873ba5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc4da57f2e0b8e9727523ed72d55e6042adee5e9
ms.sourcegitcommit: feec5cbe983c8c5800ccd4fc214914084fcceaba
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/13/2019
ms.locfileid: "70975289"
---
# <a name="nslookup-set-type"></a>nslookup set type

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Ressourcen Daten Satz für die Abfrage.
## <a name="syntax"></a>Syntax
```
set type=<ResourceRecordtype>
```
## <a name="parameters"></a>Parameter
<ResourceRecordtype>Gibt einen DNS-Ressourcen eingabentyp an. Der Standard Ressourcen Daten Satz-Typ ist. In der folgenden Tabelle sind die gültigen Werte für diesen Befehl aufgeführt.

| Wert |                                                   Beschreibung                                                   |
|-------|-----------------------------------------------------------------------------------------------------------------|
|   A   |                                      Gibt die IP&#39;-Adresse des Computers an.                                      |
|  IRGENDEINER  |                                     Gibt die IP&#39;-Adresse des Computers an.                                      |
| CNAME |                                    Gibt einen kanonischen Namen für einen Alias an.                                     |
|  Ü  |                                  Gibt einen Gruppen Bezeichner eines Gruppennamens an.                                  |
| HINFO |                          Gibt die CPU&#39;und den Typ des Betriebssystems des Computers an.                           |
|  MB   |                                        Gibt einen Post Fach Domänen Namen an.                                         |
|  0,05   |                                         Gibt ein e-Mail-Gruppenmitglied an.                                          |
| MINFO |                                   Gibt Postfach-oder e-Mail-Listen Informationen an.                                   |
|  MR   |                                     Gibt den Namen der Umbenennungs Domäne an.                                      |
|  MX   |                                          Gibt den e-Mail-Austausch an                                          |
|  NS   |                                 Gibt einen DNS-Namen Server für die benannte Zone an.                                 |
|  PTR  | Gibt einen Computernamen an, wenn die Abfrage eine IP-Adresse ist. Andernfalls gibt den Zeiger auf andere Informationen an. |
|  FREUNDLICHERWEISE  |                                Gibt den Autorisierungs Anfang für eine DNS-Zone an.                                 |
|  TXT  |                                         Gibt die Textinformationen an.                                         |
|  UID  |                                         Gibt die Benutzer-ID an.                                          |
| UINFO |                                         Gibt die Benutzerinformationen an.                                         |
|  WERT  |                                         Beschreibt einen bekannten Dienst.                                         |
| {Hilfe |                                                       ?}                                                        |

Zeigt eine kurze Zusammenfassung der <strong>nslookup</strong> -Unterbefehle an.
## <a name="remarks"></a>Hinweise
- Der <strong>Set Type</strong> -Befehl führt dieselbe Funktion aus wie der <strong>Set QueryType</strong> -Befehl.
- Weitere Informationen zu Ressourcen Daten Satz Typen finden Sie unter Request for Comment (RFC) 1035.
  ## <a name="additional-references"></a>Weitere Verweise
  <a href="command-line-syntax-key.md" data-raw-source="[Command-Line Syntax Key](command-line-syntax-key.md)">Befehlszeilen-Syntax Schlüssel</a>
  <a href="nslookup-set-querytype.md" data-raw-source="[nslookup set querytype](nslookup-set-querytype.md)">nslookup Set QueryType</a>
