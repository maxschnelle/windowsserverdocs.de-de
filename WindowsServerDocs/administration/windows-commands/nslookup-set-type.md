---
title: nslookup set type
description: Referenz Artikel für den Befehl "nslookup Set Type", der den Ressourcen Daten Satz für die Abfrage ändert.
ms.topic: reference
ms.assetid: 5248e314-fac1-413e-81dc-bbe0a0873ba5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2e4d5466880991f79d58bd8553932309595da7a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033898"
---
# <a name="nslookup-set-type"></a>nslookup set type

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Ressourcen Daten Satz für die Abfrage. Weitere Informationen zu Ressourcen Daten Satz Typen finden Sie unter [Request for Comment (RFC) 1035](https://tools.ietf.org/html/rfc1035).

> [!NOTE]
> Dieser Befehl ist mit dem Befehl [nslookup Set QueryType](nslookup-set-querytype.md) identisch.

## <a name="syntax"></a>Syntax

```
set type=<resourcerecordtype>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<resourcerecordtype>` | Gibt einen DNS-Ressourcen eingabentyp an. Der Standard Ressourcen Daten Satz-Typ ist **ein**, aber Sie können einen der folgenden Werte verwenden:<ul><li>**A:** Gibt die IP-Adresse eines Computers an.</li><li>**Beliebig:** Gibt die IP-Adresse eines Computers an.</li><li>**CNAME:** Gibt einen kanonischen Namen für einen Alias an.</li><li>**Gid** Gibt einen Gruppen Bezeichner eines Gruppennamens an.</li><li>**Hinfo:** Gibt die CPU und den Typ des Betriebssystems eines Computers an.</li><li>**MB:** Gibt einen Post Fach Domänen Namen an.</li><li>**Mg:** Gibt ein e-Mail-Gruppenmitglied an.</li><li>**MINFO:** Gibt Postfach-oder e-Mail-Listen Informationen an.</li><li>**Mr:** Gibt den Namen der Umbenennungs Domäne an.</li><li>**MX:** Gibt den e-Mail-Austausch an</li><li>**NS:** Gibt einen DNS-Namen Server für die benannte Zone an.</li><li>**PTR:** Gibt einen Computernamen an, wenn die Abfrage eine IP-Adresse ist. Andernfalls gibt den Zeiger auf andere Informationen an.</li><li>**SOA:** Gibt den Autorisierungs Anfang für eine DNS-Zone an.</li><li>**Txt:** Gibt die Textinformationen an.</li><li>**UID:** Gibt die Benutzer-ID an.</li><li>**Uinfo:** Gibt die Benutzerinformationen an.</li><li>**Wert:** Beschreibt einen bekannten Dienst.</li></ul> |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup set type](nslookup-set-querytype.md)
