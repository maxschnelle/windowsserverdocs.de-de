---
title: Verwenden regulärer Ausdrücke in NPS
description: In diesem Thema wird die Verwendung regulärer Ausdrücke für den Musterabgleich in NPS unter Windows Server erläutert. Mit dieser Syntax können Sie die Bedingungen von Netzwerk Richtlinien Attributen und RADIUS-Bereichen angeben.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: bc22d29c-678c-462d-88b3-1c737dceca75
ms.author: jgerend
author: jasongerend
msdate: 08/16/2019
ms.openlocfilehash: 76615fcccfe06333a76f872b52d2e88182fd60e5
ms.sourcegitcommit: e2b565ce85a97c0c51f6dfe7041f875a265b35dd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2019
ms.locfileid: "69584790"
---
# <a name="use-regular-expressions-in-nps"></a>Verwenden regulärer Ausdrücke in NPS

> Gilt für:  Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal)

In diesem Thema wird die Verwendung regulärer Ausdrücke für den Musterabgleich in NPS unter Windows Server erläutert. Mit dieser Syntax können Sie die Bedingungen von Netzwerk Richtlinien Attributen und RADIUS-Bereichen angeben.

## <a name="pattern-matching-reference"></a>Muster Vergleichs Verweis

Sie können die folgende Tabelle als Verweis Quelle verwenden, wenn Sie reguläre Ausdrücke mit Muster Vergleichs Syntax erstellen. Beachten Sie, dass Muster für reguläre Ausdrücke häufig durch Schrägstriche (/) eingeschlossen werden.

|  Zeichen  |  Beschreibung  |   Beispiel                                                                 |
| ----------- | ------------- | ------------------------------------------------------------------------  |
|     `\ `     | Gibt an, dass das nachfolgende Zeichen ein Sonderzeichen ist oder wörtlich interpretiert werden soll.  | `/n/ matches the character "n" while the sequence /\n/ matches a line feed or newline character.`  |
|     `^`     |                                                                 Entspricht dem Anfang der Eingabe oder Zeile.                                                                  |                                                                 &nbsp;                                                                  |
|     `$`     |                                                                    Entspricht dem Ende der Eingabe oder Zeile.                                                                     |                                                                 &nbsp;                                                                  |
|     `*`     |                                                             Gleicht das vorangehende Zeichen NULL oder mehrmals ab.                                                              |                                                  `/zo*/ matches either "z" or "zoo."`                                                   |
|     `+`     |                                                              Gleicht das vorangehende Zeichen einmal oder mehrmals ab.                                                              |                                                   `/zo+/ matches "zoo" but not "z."`                                                    |
|     `?`     |                                                              Entspricht dem vorangehenden Zeichen NULL oder einmal.                                                              |                                                 `/a?ve?/ matches the "ve" in "never."`                                                  |
|     `.`     |                                                           Entspricht einem beliebigen einzelnen Zeichen außer einem Zeilen Umleitungs Zeichen.                                                           |                                                                 &nbsp;                                                                  |
| `(pattern)` |                         Entspricht "Pattern" und speichert die Übereinstimmung.<br />`(` `)` Verwenden Sieoder`\)`, um die Literalzeichen und (Klammern) abzugleichen. `\(`                         |                                                                 &nbsp;                                                                  |
|   `x | y `  |                                                                               Entspricht entweder x oder y.                                                          |
|   `{n} `    |                                                          Entspricht genau n Uhrzeiten \(n ist eine nicht\-negative\)ganze Zahl.                                                           |               `/o{2}/ does not match the "o" in "Bob," but matches the first two instances of the letter o in "foooood."`               |
|   `{n,}`    |                                                          Entspricht mindestens n-Mal \(n ist eine nicht\-negative ganze\)Zahl.                                                          | `/o{2,}/ does not match the "o" in "Bob" but matches all of the instances of the letter o in "foooood." /o{1,}/ is equivalent to /o+/.` |
|   `{n,m}`   |                                                Entspricht mindestens n und höchstens m Mal \(m und n keine\-negativen\)ganzen Zahlen.                                                |                               `/o{1,3}/ matches the first three instances of the letter o in "fooooood."`                               |
|   `[xyz]`   |                                                       Entspricht einem beliebigen der eingeschlossenen Zeichen \(als Zeichensatz\).                                                        |                                                  `/[abc]/ matches the "a" in "plain."`                                                  |
|  `[^xyz]`   |                                                  Entspricht allen Zeichen, die nicht als \(negativer Zeichensatz\)eingeschlossen sind.                                                  |                                                 `/[^abc]/ matches the "p" in "plain."`                                                  |
|    `\b`     |                                                              Entspricht einer Wort Grenze \(, z. b.\)einem Leerzeichen.                                                               |                                              `/ea*r\b/ matches the "er" in "never early."`                                              |
|    `\B`     |                                                                         Entspricht einer nicht Wort Grenze.                                                                          |                                             `/ea*r\B/ matches the "ear" in "never early."`                                              |
|    `\d`     |                                                       Entspricht einem Ziffern Zeichen \(, das Ziffern zwischen 0 und 9\)entspricht.                                                        |                                                                 &nbsp;                                                                  |
|    `\D`     |                                                           Entspricht einem nicht Ziffern Zeichen \(, `[^0-9]` \)das entspricht.                                                           |                                                                 &nbsp;                                                                  |
|    `\f`     |                                                                        Entspricht einem Formular Vorschub Zeichen.                                                                        |                                                                 &nbsp;                                                                  |
|    `\n`     |                                                                        Entspricht einem Zeilenvorschub Zeichen.                                                                        |                                                                 &nbsp;                                                                  |
|    `\r`     |                                                                     Entspricht einem Wagen Rücklauf Zeichen.                                                                     |                                                                 &nbsp;                                                                  |
|    `\s`     |                                   Entspricht einem beliebigen leer Raum Zeichen, einschließlich Leerzeichen, Tabstopps \(und Formular `[ \f\n\r\t\v]`Feed, der \)entspricht.                                   |                                                                 &nbsp;                                                                  |
|    `\S`     |                                                  Entspricht einem beliebigen nicht-leer \(Zeichen, `[^ \f\n\r\t\v]` \)das entspricht.                                                   |                                                                 &nbsp;                                                                  |
|    `\t`     |                                                                           Entspricht einem Tabstopp Zeichen.                                                                           |                                                                 &nbsp;                                                                  |
|    `\v`     |                                                                      Entspricht einem vertikalen Tabstopp Zeichen.                                                                       |                                                                 &nbsp;                                                                  |
|    `\w`     |                                              Entspricht einem beliebigen Wort Zeichen, einschließlich \(unter `[A-Za-z0-9_]` \)Strich, der entspricht.                                              |                                                                 &nbsp;                                                                  |
|    `\W`     |                                           Entspricht einem beliebigen\-nicht-Wort Zeichen ohne \(unterstrich `[^A-Za-z0-9_]`, der entspricht \).                                           |                                                                 &nbsp;                                                                  |
|   `\num`    | Bezieht sich auf gespeicherte \(Übereinstimmungen `?num`, wobei num eine positive\)Ganzzahl ist.  Diese Option kann nur im Textfeld **ersetzen** beim Konfigurieren von Attribut Manipulationen verwendet werden. |                                       `\1`ersetzt, was in der ersten gespeicherten Übereinstimmung gespeichert wird.                                       |
|   `/n/ `    |                      Ermöglicht das Einfügen von ASCII-Codes in reguläre \(Ausdrücke `?n`, wobei n ein oktal-, Hexadezimal-oder Dezimal\)Escapewert ist.                       |                                                                 &nbsp;                                                                  |

## <a name="examples-for-network-policy-attributes"></a>Beispiele für Netzwerk Richtlinien Attribute

In den folgenden Beispielen wird die Verwendung der Muster Vergleichs Syntax zum Angeben von Netzwerk Richtlinien Attributen beschrieben:

- Wenn Sie alle Telefonnummern innerhalb des 899-Bereichs Codes angeben möchten, lautet die Syntax wie folgt:

     `899.*`

- Um einen Bereich von IP-Adressen anzugeben, die mit 192.168.1 beginnen, lautet die Syntax wie folgt:

    `192\.168\.1\..+`

## <a name="examples-for-manipulation-of-the-realm-name-in-the-user-name-attribute"></a>Beispiele für die Bearbeitung des Bereichs namens im User Name-Attribut

In den folgenden Beispielen wird die Verwendung der Muster Vergleichs Syntax zum Bearbeiten von Bereichs Namen für das Attribut "Benutzer Name" beschrieben, das sich auf der Registerkarte " **Attribut** " in den Eigenschaften einer Verbindungs Anforderungs Richtlinie befindet.

**So entfernen Sie den Bereichs Teil des Attributs "Benutzer Name"**

In einem ausgelagerten DFÜ-Szenario, in dem ein Internet \(Dienstanbieter ISP\) Verbindungsanforderungen an eine Organisation NPS weiterleitet, benötigt der ISP-RADIUS-Proxy möglicherweise einen Bereichs Namen, um die Authentifizierungsanforderung weiterzuleiten. Der Bereichs Namensteil des Benutzernamens wird vom NPS jedoch möglicherweise nicht erkannt. Daher muss der Bereichs Name vom ISP-RADIUS-Proxy entfernt werden, bevor er an die NPS der Organisation weitergeleitet wird.

- Suchen: @microsoft \.com

- Ersetzen Sie:

**So ersetzen <em>user@example.microsoft.com</em> Sie durch _example. Microsoft. com\user_**

- Sich`(.*)@(.*)`

- Stelle`$2\$1`



**So ersetzen Sie " _Domäne \ Benutzer_ " durch _specific_domain\user_**

- Sich`(.*)\\(.*)`

- Ersetzen: *specific_domain*`\$2`



<strong>So ersetzen Sie *User* durch *user@specific_domain</strong>*

- Sich`$`

- Replace: @*specific_domain*

## <a name="example-for-radius-message-forwarding-by-a-proxy-server"></a>Beispiel für RADIUS-Nachrichten Weiterleitung durch einen Proxy Server

Sie können Routing Regeln erstellen, die RADIUS-Nachrichten mit einem angegebenen Bereichs Namen an einen Satz von RADIUS-Servern weiterleiten, wenn NPS als RADIUS-Proxy verwendet wird. Im folgenden finden Sie eine empfohlene Syntax für das Routing von Anforderungen basierend auf dem Bereichs Namen.

- **NetBIOS-Name**:`WCOAST`
- **Muster**:`^wcoast\\`

Im folgenden Beispiel ist wcoast.Microsoft.com ein eindeutiges Benutzer Prinzipal Namen-Suffix (UPN) für den DNS-oder Active Directory Domäne wcoast.Microsoft.com. Mit dem angegebenen Muster kann der NPS-Proxy Nachrichten basierend auf dem NetBIOS-Domänen Namen oder UPN-Suffix weiterleiten.

- **NetBIOS-Name**:`WCOAST`
- **UPN-Suffix**:`wcoast.microsoft.com`
- **Muster**:`^wcoast\\|@wcoast\.microsoft\.com$`


Weitere Informationen zum Verwalten von NPS finden Sie unter [Verwalten des Netzwerk Richtlinien Servers](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).
