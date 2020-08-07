---
title: nslookup set querytype
description: Referenz Artikel für den Befehl "nslookup Set QueryType", der den Ressourcen Daten Satz für die Abfrage ändert.
ms.topic: article
ms.assetid: 5af54ac5-fc1a-4af6-977b-f8e97c8eba90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9319b5e7de8b31d805114b9d70c9700ee2a033ac
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885637"
---
# <a name="nslookup-set-querytype"></a>nslookup set querytype

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Ressourcen Daten Satz für die Abfrage. Weitere Informationen zu Ressourcen Daten Satz Typen finden Sie unter [Request for Comment (RFC) 1035](https://tools.ietf.org/html/rfc1035).

> [!NOTE]
> Dieser Befehl ist mit dem Befehl " [nslookup Set Type](nslookup-set-type.md) " identisch.

## <a name="syntax"></a>Syntax

```
set querytype=<resourcerecordtype>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<resourcerecordtype>` | Gibt einen DNS-Ressourcen eingabentyp an. Der Standard Ressourcen Daten Satz-Typ ist **ein**, aber Sie können einen der folgenden Werte verwenden:<ul><li>**A:** Gibt die IP-Adresse eines Computers an.</li><li>**Beliebig:** Gibt die IP-Adresse eines Computers an.</li><li>**CNAME:** Gibt einen kanonischen Namen für einen Alias an.</li><li>**Gid** Gibt einen Gruppen Bezeichner eines Gruppennamens an.</li><li>**Hinfo:** Gibt die CPU und den Typ des Betriebssystems eines Computers an.</li><li>**MB:** Gibt einen Post Fach Domänen Namen an.</li><li>**Mg:** Gibt ein e-Mail-Gruppenmitglied an.</li><li>**MINFO:** Gibt Postfach-oder e-Mail-Listen Informationen an.</li><li>**Mr:** Gibt den Namen der Umbenennungs Domäne an.</li><li>**MX:** Gibt den e-Mail-Austausch an</li><li>**NS:** Gibt einen DNS-Namen Server für die benannte Zone an.</li><li>**PTR:** Gibt einen Computernamen an, wenn die Abfrage eine IP-Adresse ist. Andernfalls gibt den Zeiger auf andere Informationen an.</li><li>**SOA:** Gibt den Autorisierungs Anfang für eine DNS-Zone an.</li><li>**Txt:** Gibt die Textinformationen an.</li><li>**UID:** Gibt die Benutzer-ID an.</li><li>**Uinfo:** Gibt die Benutzerinformationen an.</li><li>**Wert:** Beschreibt einen bekannten Dienst.</li></ul> |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup set type](nslookup-set-type.md)
