---
title: tracert
description: Referenz Artikel zu tracert, der den Pfad zu einem Ziel bestimmt, indem ICMP-Echo Anforderungen (Internet Control Message Protocol) oder ICMPv6-Nachrichten an das Ziel gesendet werden, wobei die Werte für die Gültigkeitsdauer (Time to Live, TTL) inkrementell erhöht werden.
ms.topic: reference
ms.assetid: 9032a032-2e5e-49d4-9e86-f821600e4ba6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 767871e9100d8b14c8a893fd9d9dbb5862810ace
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156410"
---
# <a name="tracert"></a>tracert

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Diagnosetool bestimmt den Pfad zu einem Ziel, indem ICMP-Echo Anforderungen (Internet Control Message Protocol) oder ICMPv6-Nachrichten an das Ziel gesendet werden, wobei die Werte für die Gültigkeitsdauer (TTL) inkrementell erhöht werden. Jeder Router entlang des Pfads ist erforderlich, um die Gültigkeitsdauer in einem IP-Paket mindestens 1 zu verringern, bevor es weitergeleitet wird. Tatsächlich handelt es sich bei der Gültigkeitsdauer um einen maximalen Verbindungs Counter. Wenn die Gültigkeitsdauer für ein Paket den Wert 0 erreicht, wird erwartet, dass der Router eine Meldung über die Nachricht "ICMP-Zeitüberschreitung" an den Quellcomputer

Dieser Befehl bestimmt den Pfad, indem die erste Echo Anforderungs Nachricht mit einer Gültigkeitsdauer von 1 gesendet und die Gültigkeitsdauer für jede nachfolgende Übertragung um 1 erhöht wird, bis das Ziel antwortet oder die maximale Anzahl von Hops erreicht wird. Die maximale Anzahl von Hops beträgt standardmäßig 30 und kann mithilfe des **/h** -Parameters angegeben werden.

Der Pfad wird durch die Untersuchung der von zwischen Routern zurückgegebenen ICMP-Zeitüberschreitung und der vom Ziel zurückgegebenen Echo Antwortnachricht bestimmt. Einige Router geben jedoch keine Zeitüberschreitung für die Nachrichten von Paketen mit abgelaufenen TTL-Werten zurück, die für den Befehl **tracert** nicht sichtbar sind. In diesem Fall wird eine Zeile mit Sternchen ( `*` ) für diesen Hop angezeigt. Der angezeigte Pfad ist die Liste der Schnittstellen, die sich im Pfad zwischen einem Quellhost und einem Ziel befinden. Die Near/Side-Schnittstelle ist die Schnittstelle des Routers, die dem sendenden Host im Pfad am nächsten liegt.

> [!IMPORTANT]
> Dieser Befehl ist nur verfügbar, wenn das TCP/IP-Protokoll (Internet Protocol) als Komponente in den Eigenschaften eines Netzwerkadapters in Netzwerkverbindungen installiert ist.
>
> Verwenden Sie den [Befehl "pathping Command](pathping.md) ", um einen Pfad zu verfolgen und Netzwerk Latenz und Paketverlust für jeden Router und Link im Pfad bereitzustellen.

## <a name="syntax"></a>Syntax

```
tracert [/d] [/h <maximumhops>] [/j <hostlist>] [/w <timeout>] [/R] [/S <srcaddr>] [/4][/6] <targetname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /d | Beendet den Versuch, die IP-Adressen der zwischen Router in ihre Namen aufzulösen. Dadurch kann die Rückgabe von Ergebnissen beschleunigt werden. |
| /h `<maximumhops>` | Gibt die maximale Anzahl von Hops in dem Pfad an, der nach dem Ziel (Ziel) gesucht werden soll. Der Standardwert ist 30 Hops. |
| /j `<hostlist>` | Gibt an, dass Echo Request-Nachrichten die lose Quell Route-Option im IP-Header mit dem Satz von zwischen Zielen verwenden, die in angegeben sind `<hostlist>` . Beim losen Quell Routing können aufeinander folgende Zwischenziele durch einen oder mehrere Router getrennt werden. Die maximale Anzahl von Adressen oder Namen in der Liste beträgt *9*. Der `<hostlist>` ist eine Reihe von IP-Adressen (in gepunkteter Dezimal Schreibweise), getrennt durch Leerzeichen. Verwenden Sie diesen Parameter nur bei der Ablauf Verfolgung von IPv4-Adressen. |
| /w `<timeout>` | Gibt die Zeit in Millisekunden an, die auf die überschreiten der ICMP-Zeit gewartet wird, oder eine Echo Antwortnachricht, die einer gegebenen Echo Anforderungs Nachricht entspricht, die empfangen werden soll. Wenn diese nicht innerhalb des Timeouts empfangen werden, wird ein Sternchen ( `*` ) angezeigt. Das Standard Timeout beträgt 4000 (4 Sekunden). |
| /R | Gibt an, dass der IPv6-Routing Erweiterungs Header verwendet wird, um eine Echo Anforderungs Nachricht an den lokalen Host zu senden, wobei das Ziel als Zwischenziel verwendet und die umgekehrte Route getestet wird. |
| /S `<srcaddr>` | Gibt die Quelladresse an, die in den Echo Anforderungs Nachrichten verwendet werden soll. Verwenden Sie diesen Parameter nur bei der Ablauf Verfolgung von IPv6-Adressen. |
| /4 | Gibt an, dass tracert.exe für diese Ablauf Verfolgung nur IPv4 verwenden darf. |
| /6 | Gibt an, dass tracert.exe für diese Ablauf Verfolgung nur IPv6 verwenden kann. |
| `<targetname>` | Gibt das Ziel an, das entweder durch die IP-Adresse oder den Hostnamen identifiziert wird. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Pfad zum Host mit dem Namen *corp7.Microsoft.com*zu verfolgen:

```
tracert corp7.microsoft.com
```

Um den Pfad zum Host mit dem Namen *corp7.Microsoft.com* zu verfolgen und die Auflösung der einzelnen IP-Adressen zu verhindern, geben Sie Folgendes ein:

```
tracert /d corp7.microsoft.com
```

Geben Sie Folgendes ein, um den Pfad zum Host mit dem Namen *corp7.Microsoft.com* zu verfolgen und die lose Quell Route *10.12.0.1/10.29.3.1/10.1.44.1*zu verwenden:

```
tracert /j 10.12.0.1 10.29.3.1 10.1.44.1 corp7.microsoft.com
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [PathPing-Befehl](pathping.md)
