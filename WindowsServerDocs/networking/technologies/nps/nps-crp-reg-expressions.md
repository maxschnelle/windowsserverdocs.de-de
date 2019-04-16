---
title: Verwenden regulärer Ausdrücke in NPS
description: In diesem Thema erläutert die Verwendung von regulären Ausdrücken für Mustervergleiche in NPS in Windows Server 2016. Diese Syntax können Sie die Bedingungen der Netzwerk-Richtlinienattribute und RADIUS-Bereiche angeben.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: bc22d29c-678c-462d-88b3-1c737dceca75
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f84173f1f51be9fd44995dc41f759bbea4fb3539
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="use-regular-expressions-in-nps"></a>Verwenden regulärer Ausdrücke in NPS

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema erläutert die Verwendung von regulären Ausdrücken für Mustervergleiche in NPS in Windows Server 2016. Diese Syntax können Sie die Bedingungen der Netzwerk-Richtlinienattribute und RADIUS-Bereiche angeben.

## <a name="pattern-matching-reference"></a>Mustervergleich Referenz

Die folgende Tabelle können als Referenzquelle beim Erstellen von regulärer Ausdrücken mit mustervergleichssyntax.

|Zeichen|Beschreibung|Beispiel|
|---------|-----------|-------|
|`\`  |Das nächste Zeichen als ein Zeichen entsprechend gekennzeichnet. |`/n/ matches the character "n". The sequence /\n/ matches a line feed or newline character.`  |
|`^`  |Entspricht dem Beginn der Eingabe oder Zeile. | &nbsp; |
|`$`  |Steht für das Ende der Eingabe oder Zeile. | &nbsp; |
|`*`  |Mit das vorangehenden Zeichen einmal oder mehrmals übereinstimmt. |`/zo*/ matches either "z" or "zoo."` |
|`+`  |Entspricht das vorherige Zeichen ein oder mehrere Male. |`/zo+/ matches "zoo" but not "z."` |
|`?`  |Entspricht dem vorherigen Zeichen NULL oder eins Mal. |`/a?ve?/ matches the "ve" in "never."` |
|`.`  |Stimmt mit einem einzelnen Zeichen mit Ausnahme des Zeilenumbruchzeichens.  | &nbsp; |
|`( pattern )`  |"Muster" entspricht, und speichert die Übereinstimmung.   |`To match ( ) (parentheses), use "\(" or "\)".`  |
|"X | y '  |Entspricht x oder y.  |"/ z|Essen? / entspricht "Zoo" oder "Kochen". ` |
|`{ n } `  |Entspricht genau n Mal \ (n ist ein negativer Integer\).  |`/o{2}/ does not match the "o" in "Bob," but matches the first two instances of the letter o in "foooood."`  |
|`{ n ,}`  |Entspricht mindestens n Mal \ (n ist ein negativer Integer\).  |`/o{2,}/ does not match the "o" in "Bob" but matches all of the instances of the letter o in "foooood." /o{1,}/ is equivalent to /o+/.`  |
|`{ n , m }`  |Entspricht mindestens n und höchstens m-Mal \ (m und n sind negativ Integers\).  |`/o{1,3}/ matches the first three instances of the letter o in "fooooood."`  |
|`[ xyz ]`  |Entspricht einem der angegebenen Zeichen \(a character set\).  |`/[abc]/ matches the "a" in "plain."`  |
|`[^ xyz ]`  |Alle Zeichen, die nicht eingeschlossen sind entspricht \ (ein negativer Zeichen Set).  |`/[^abc]/ matches the "p" in "plain."`  |
|`\b`  |Entspricht einer Wortgrenze \ (z. B. ein Space\).  |`/ea*r\b/ matches the "er" in "never early."`  |
|`\B`  |Entspricht einer Wortgrenze.  |`/ea*r\B/ matches the "ear" in "never early."`  |
|`\d`  |Entspricht einer Ziffer \ (entspricht dem Ziffern von 0 bis 9\).  | &nbsp; |
|`\D`  |Steht für ein beliebiges Zeichen \ (Äquivalent zu `[^0-9]`\).  | &nbsp; |
|`\f`  |Entspricht einem Formular feed Zeichen.  | &nbsp; |
|`\n`  |Entspricht einem Zeilenvorschub.  | &nbsp; |
|`\r`  |Entspricht einem Wagenrücklauf.  | &nbsp; |
|`\s`  |Entspricht einem Leerzeichen Speicherplatz, Registerkarte und Form feed \ (Äquivalent zu `[ \f\n\r\t\v]`\).  | &nbsp; |
|`\S`  |Entspricht einem beliebigen Zeichen ohne Leerraum \ (Äquivalent zu `[^ \f\n\r\t\v]`\).  | &nbsp; |
|`\t`  |Steht für ein Tabulatorzeichen.  | &nbsp; |
|`\v`  |Entspricht einem vertikalen Tabulatorzeichen.  | &nbsp; |
|`\w`  |Entspricht einem beliebigen Buchstaben, einschließlich der Unterstrich \ (Äquivalent zu `[A-Za-z0-9_]`\).  | &nbsp; |
|`\W`  |Entspricht einem beliebigen-Buchstaben, Unterstrich ausgenommen \ (Äquivalent zu `[^A-Za-z0-9_]`\).  | &nbsp; |
|`\ num`  |Bezieht sich auf gespeicherte Übereinstimmungen \ (`?num`, wobei die NUM-Taste eine positive Integer\ ist).  Diese Option kann verwendet werden, nur in der **ersetzen** Textfeld beim Attributmanipulation zu konfigurieren.| `\1` ersetzt, was in der ersten gespeicherten Übereinstimmung gespeichert ist.  |
|`/ n / `  |Ermöglicht das Einfügen von ASCII-Codes in regulären Ausdrücken \ (`?n`, wobei n eine Oktal-, Hexadezimal- oder Dezimalmethoden Escape-Value\ ist).  | &nbsp; |

## <a name="examples-for-network-policy-attributes"></a>Beispiele für die Attribute der Netzwerk-Richtlinie

Die folgenden Beispiele beschreiben die Verwendung von mustervergleichssyntax Netzwerkattribute angeben:

- Um alle Telefonnummern innerhalb der Ortskennzahl 899 anzugeben, lautet die Syntax:

     `899.*`

- So geben Sie einen Bereich von IP-Adressen, die beginnen mit 192.168.1, lautet die Syntax:

    `192\.168\.1\..+`

## <a name="examples-for-manipulation-of-the-realm-name-in-the-user-name-attribute"></a>Beispiele für die Manipulation von den Bereichsnamen im User Name-Attribut

Die folgenden Beispiele beschreiben die Verwendung von mustervergleichssyntax Bereichsnamen für das User Name-Attribut bearbeiten auf den **Attribut** Registerkarte in den Eigenschaften einer Verbindungsanforderungsrichtlinie.

**So entfernen Sie den Bereich Teil der Benutzername-Attribut**

Externes DFÜ-Szenario in dem eine \(ISP\) Routen Verbindung zu einem Internetdienstanbieter Anforderungen für eine Organisation NPS-Server der ISP RADIUS-Proxy ist möglicherweise Bereichsnamen zum Weiterleiten der Authentifizierungsanforderung erforderlich. Der NPS-Server möglicherweise jedoch nicht Teil der Bereich des Benutzernamens erkannt. Aus diesem Grund muss der Bereichsnamen ISP RADIUS-Proxy entfernt werden, bevor er an den Netzwerkrichtlinienserver Organisation weitergeleitet wird.

- Suchen:@microsoft\.com

- Ersetzen Sie:

**Ersetzen * user@example.microsoft.com * mit *example.microsoft.com\user***

- Suchen:`(.*)@(.*)`

- Ersetzen Sie:`$2\$1`



**Ersetzen *Domäne\Benutzer* mit *Specific_domain\user***

- Suchen:`(.*)\\(.*)`

- Ersetzen Sie: *bestimmte_domäne*`\$2`



**Ersetzen *Benutzer* mit*user@specific_domain***

- Suchen:`$`

- Ersetzen Sie: @*bestimmte_domäne*

## <a name="example-for-radius-message-forwarding-by-a-proxy-server"></a>Beispiel für die Weiterleitung von RADIUS-Nachricht über einen Proxyserver

Sie können Routingregeln erstellen, die RADIUS-Nachrichten mit einem angegebenen Bereichsnamen auf eine Gruppe von RADIUS-Server weiterleiten, wenn Sie NPS als RADIUS-Proxy verwendet wird. Es folgt eine empfohlene Syntax Routinganforderungen basierend auf den Bereichsnamen.

- **NetBIOS-Namen**: `WCOAST`
- **Muster**:      `^wcoast\\`

Im folgenden Beispiel ist wcoast.microsoft.com eine eindeutige Benutzer Benutzerprinzipalnamen (UPN) für die DNS- oder Active Directory-Domäne wcoast.microsoft.com. Mit dem angegebenen Muster, kann der NPS-Proxy basierte auf den NetBIOS-Domänennamen oder Benutzerprinzipalnamen-Suffix Nachrichten weiterleiten.

- **NetBIOS-Namen**: `WCOAST`
- **UPN-Suffix**:   `wcoast.microsoft.com`
- **Muster**:      `^wcoast\\|@wcoast\.microsoft\.com$`


Weitere Informationen zum Verwalten von NPS finden Sie unter [Netzwerkrichtlinienserver verwalten](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
