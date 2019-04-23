---
title: Verwenden regulärer Ausdrücke in NPS
description: Dieses Thema erläutert die Verwendung von regulären Ausdrücken für Mustervergleiche in NPS in Windows Server 2016. Sie können diese Syntax verwenden, um die Bedingungen der Richtlinie Netzwerkattribute und RADIUS-Bereiche anzugeben.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: bc22d29c-678c-462d-88b3-1c737dceca75
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a985df9fea31e5ee180caef4e69899ae8468ff71
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865261"
---
# <a name="use-regular-expressions-in-nps"></a>Verwenden regulärer Ausdrücke in NPS

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema erläutert die Verwendung von regulären Ausdrücken für Mustervergleiche in NPS in Windows Server 2016. Sie können diese Syntax verwenden, um die Bedingungen der Richtlinie Netzwerkattribute und RADIUS-Bereiche anzugeben.

## <a name="pattern-matching-reference"></a>Musterabgleich – Referenz

Sie können in der folgende Tabelle als Referenz-Quelle verwenden, beim Erstellen von regulärer Ausdrücken mit mustervergleichssyntax.

|Zeichen|Beschreibung|Beispiel|
|---------|-----------|-------|
|`\`  |Markiert das nächste Zeichen als ein Zeichen übereinstimmen. |`/n/ matches the character "n". The sequence /\n/ matches a line feed or newline character.`  |
|`^`  |Mit dem Anfang der Eingabe oder Zeile übereinstimmt. | &nbsp; |
|`$`  |Entspricht das Ende der Eingabe oder Zeile an. | &nbsp; |
|`*`  |Entspricht das vorangehenden Zeichen NULL oder mehr Vorkommen. |`/zo*/ matches either "z" or "zoo."` |
|`+`  |Entspricht das vorangehenden Zeichen einmal oder mehrmals. |`/zo+/ matches "zoo" but not "z."` |
|`?`  |Steht für den vorherigen Zeichen NULL oder ein Vorkommen. |`/a?ve?/ matches the "ve" in "never."` |
|`.`  |Entspricht jedem beliebigen einzelnes Zeichen außer einem Zeilenumbruchzeichen.  | &nbsp; |
|`(pattern)`  |Entspricht "Muster", und speichert die Übereinstimmung.<br />Entsprechend die Literalzeichen `(` und `)` (Klammern), verwenden Sie `\(` oder `\)`.   | &nbsp;  |
|`x|y `  |Entspricht x oder y.  |`/z|food?/ matches "zoo" or "food."` |
|`{n} `  |Entspricht genau n Vorkommen \(n ist ein nicht\-negative ganze Zahl\).  |`/o{2}/ does not match the "o" in "Bob," but matches the first two instances of the letter o in "foooood."`  |
|`{n,}`  |Entspricht mindestens n Vorkommen \(n ist ein nicht\-negative ganze Zahl\).  |`/o{2,}/ does not match the "o" in "Bob" but matches all of the instances of the letter o in "foooood." /o{1,}/ is equivalent to /o+/.`  |
|`{n,m}`  |Entspricht mindestens n und höchstens Mio. Mal \(m und n sind nicht\-negative ganze Zahlen\).  |`/o{1,3}/ matches the first three instances of the letter o in "fooooood."`  |
|`[xyz]`  |Entspricht einem beliebigen die eingeschlossenen Zeichen \(einen Zeichensatz\).  |`/[abc]/ matches the "a" in "plain."`  |
|`[^xyz]`  |Stimmt mit jedem Zeichen, die nicht eingeschlossen sind \(einen negativen Zeichensatz\).  |`/[^abc]/ matches the "p" in "plain."`  |
|`\b`  |Entspricht einer Wortgrenze \(z. B. ein Leerzeichen\).  |`/ea*r\b/ matches the "er" in "never early."`  |
|`\B`  |Entspricht einer Wortgrenze.  |`/ea*r\B/ matches the "ear" in "never early."`  |
|`\d`  |Entspricht einem numerischen Zeichen \(entspricht Ziffern von 0 bis 9\).  | &nbsp; |
|`\D`  |Entspricht einem Zeichen keine Ziffer ist \(entspricht `[^0-9]` \).  | &nbsp; |
|`\f`  |Entspricht einem Seitenvorschubzeichen Zeichen.  | &nbsp; |
|`\n`  |Entspricht einem Zeilenvorschub.  | &nbsp; |
|`\r`  |Entspricht einem Wagenrücklaufzeichen.  | &nbsp; |
|`\s`  |Entspricht einer beliebigen Leerstelle, Leerzeichen, Tabstopp und Seitenvorschubzeichen \(entspricht `[ \f\n\r\t\v]` \).  | &nbsp; |
|`\S`  |Entspricht jedem beliebigen Zeichen ohne Leerraum \(entspricht `[^ \f\n\r\t\v]` \).  | &nbsp; |
|`\t`  |Entspricht einem Tabstoppzeichen.  | &nbsp; |
|`\v`  |Entspricht einem vertikalen Tabulator-Zeichen.  | &nbsp; |
|`\w`  |Entspricht einem beliebigen Wortzeichen, einschließlich des Unterstrichs \(entspricht `[A-Za-z0-9_]` \).  | &nbsp; |
|`\W`  |Entspricht nicht\-Wortzeichen, mit Ausnahme der Unterstrich \(entspricht `[^A-Za-z0-9_]` \).  | &nbsp; |
|`\num`  |Bezieht sich auf gespeicherte Übereinstimmungen \( `?num`, wobei die Anzahl eine positive ganze Zahl ist\).  Diese Option kann verwendet werden, nur in der **ersetzen** Textfeld beim Konfigurieren der Bearbeitung des Attributs.| `\1` ersetzt, was in der ersten gespeicherten Übereinstimmung gespeichert ist.  |
|`/n/ `  |Ermöglicht das Einfügen von ASCII-Codes in regulären Ausdrücken \( `?n`, wobei n eine Oktal-, Hexadezimal- oder Dezimalformat Escapewert ist\).  | &nbsp; |

## <a name="examples-for-network-policy-attributes"></a>Beispiele für die Netzwerk-Richtlinienattribute

Die folgenden Beispiele veranschaulichen die Verwendung von mustervergleichssyntax Netzwerkattribute-Richtlinie angeben:

- Wenn alle Telefonnummern in der Ortskennzahl 899 angeben möchten, müssen Sie die Syntax lautet:

     `899.*`

- Damit geben einen Bereich von IP-Adressen, die beginnen mit 192.168.1 aufweisen, können Sie die Syntax lautet:

    `192\.168\.1\..+`

## <a name="examples-for-manipulation-of-the-realm-name-in-the-user-name-attribute"></a>Beispiele für die Bearbeitung von den Bereichsnamen im Benutzernamen-Attribut

Die folgenden Beispiele veranschaulichen die Verwendung der Mustervergleich Syntax zum Bearbeiten von Bereichsnamen für den Benutzername-Attribut, auf die **Attribut** Registerkarte in den Eigenschaften einer Verbindungsanforderungsrichtlinie.

**Der Bereichsteil das Benutzernamen-Attribut entfernen**

In einem Szenario mit externes DFÜ-Verbindung in der Internet-service-Anbieter \(ISP\) verbindungsanforderungen an ein Unternehmen NPS weiterleitet, der ISP-RADIUS-Proxy möglicherweise Bereichsname zum Weiterleiten der Authentifizierungsanforderung. Allerdings möglicherweise in der NPS den Bereich-Namensteil des Benutzernamens nicht erkannt. Aus diesem Grund müssen Sie der Bereichsnamen ISP RADIUS-Proxy entfernt werden, bevor er an die Organisation NPS weitergeleitet wird.

- Find: @microsoft \.com

- Ersetzen Sie:

**Ersetzen *user@example.microsoft.com* mit *example.microsoft.com\user***

- Suchen Sie nach:`(.*)@(.*)`

- Ersetzen Sie dies:`$2\$1`



**Ersetzen *"Domäne\Benutzer"* mit *Specific_domain\user***

- Suchen Sie nach:`(.*)\\(.*)`

- Replace: *specific_domain*`\$2`



**Ersetzen *Benutzer* mit *user@specific_domain***

- Suchen Sie nach:`$`

- Replace: @*specific_domain*

## <a name="example-for-radius-message-forwarding-by-a-proxy-server"></a>Beispiel für die Weiterleitung von RADIUS-Nachricht von einem Proxyserver

Sie können Routingregeln erstellen, die RADIUS-Nachrichten mit einem angegebenen Bereichsnamen auf einen Satz von RADIUS-Server weiterleiten, wenn NPS als RADIUS-Proxy verwendet wird. Es folgt eine empfohlene Syntax für das Weiterleiten von Anforderungen basierend auf der Bereichsname.

- **NetBIOS-Namen**: `WCOAST`
- **Pattern**:      `^wcoast\\`

Im folgenden Beispiel ist "wcoast.Microsoft.com" eine eindeutige Benutzer-Benutzerprinzipalnamen (UPN)-Suffix für die DNS oder Active Directory Sie Domäne "wcoast.Microsoft.com". Mit dem angegebenen Muster kann Nachrichten basierend auf NetBIOS-Domänenname oder UPN-Suffix der NPS-Proxy weiterleiten.

- **NetBIOS-Namen**: `WCOAST`
- **UPN-Suffix**:   `wcoast.microsoft.com`
- **Pattern**:      `^wcoast\\|@wcoast\.microsoft\.com$`


Weitere Informationen zum Verwalten von NPS finden Sie unter [Verwalten des Netzwerkrichtlinienservers](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
