---
title: pathping
description: Referenz Artikel für den Befehl "pathping", der Informationen zu Netzwerk Latenz und Netzwerk Verlust bei zwischen Hops zwischen einer Quelle und einem Ziel abruft.
ms.topic: reference
ms.assetid: ec430125-b1dc-4aad-a7c9-b70f486d9e3c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: ed63467c8eba2d65a6408e08762357275dfef7f8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628631"
---
# <a name="pathping"></a>pathping

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Bietet Informationen zu Netzwerk Latenz und Netzwerk Verlust bei zwischen Hops zwischen einer Quelle und einem Ziel. Dieser Befehl sendet mehrere Echo Anforderungs Nachrichten an jeden Router zwischen einer Quelle und einem Ziel über einen bestimmten Zeitraum und berechnet dann die Ergebnisse auf der Grundlage der von den einzelnen Routern zurückgegebenen Pakete. Da mit diesem Befehl der Grad des Paket Verlusts bei einem beliebigen Router oder Link angezeigt wird, können Sie bestimmen, welche Router oder Subnetze Netzwerkprobleme aufweisen können. Wird ohne Parameter verwendet, zeigt dieser Befehl die Hilfe an.

> [!NOTE]
> Dieser Befehl ist nur verfügbar, wenn das TCP/IP-Protokoll (Internet Protocol) als Komponente in den Eigenschaften eines Netzwerkadapters in Netzwerkverbindungen installiert ist.
>
> Darüber hinaus wird mit diesem Befehl identifiziert, welche Router sich auf dem Pfad befinden. Dies gilt auch für die Verwendung des [Befehls tracert](tracert.md). Mit diesem Befehl werden Pings in regelmäßigen Abständen über einen angegebenen Zeitraum an alle Router gesendet und Statistiken auf der Grundlage der von den einzelnen zurückgegebenen Nummern berechnet.

## <a name="syntax"></a>Syntax

```
pathping [/n] [/h <maximumhops>] [/g <hostlist>] [/p <Period>] [/q <numqueries> [/w <timeout>] [/i <IPaddress>] [/4 <IPv4>] [/6 <IPv6>][<targetname>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /n | Verhindert, dass der **pfadping** versucht, die IP-Adressen der zwischen Router in ihre Namen aufzulösen. Dadurch wird möglicherweise die Anzeige von **pathping** -Ergebnissen beschleunigt. |
| /h `<maximumhops>` | Gibt die maximale Anzahl von Hops in dem Pfad an, der nach dem Ziel (Ziel) gesucht werden soll. Der Standardwert ist 30 Hops. |
| /g `<hostlist>` | Gibt an, dass die Echo Anforderungs Nachrichten die Option **lose Quell Route** im IP-Header mit dem Satz von zwischen Zielen verwenden, die in der *Hostliste*angegeben sind. Beim losen Quell Routing können aufeinander folgende Zwischenziele durch einen oder mehrere Router getrennt werden. Die maximale Anzahl von Adressen oder Namen in der Hostliste beträgt **9**. Die *Hostliste* ist eine Reihe von IP-Adressen (in punktierter Dezimal Schreibweise), getrennt durch Leerzeichen. |
| /p `<period>` | Gibt die Anzahl von Millisekunden an, die zwischen aufeinander folgenden Pings gewartet werden soll. Der Standardwert ist 250 Millisekunden (1/4 Sekunde). Dieser Parameter sendet individuelle Pings an jeden Zwischenhop. Aus diesem Grund wird das Intervall zwischen zwei an denselben Hop gesendeten Pings mit der Anzahl der *Hops multipliziert.* |
| /q `<numqueries>` | Gibt die Anzahl der Echo Request-Meldungen an, die an jeden Router im Pfad gesendet werden. Der Standardwert ist 100-Abfragen. |
| /w `<timeout>` | Gibt die Anzahl der Millisekunden an, die auf jede Antwort gewartet werden soll. Der Standardwert ist 3000 Millisekunden (3 Sekunden). Dieser Parameter sendet mehrere Pings parallel. Aus diesem Grund ist die im *Timeout* -Parameter angegebene Zeitspanne nicht durch die Zeitspanne begrenzt, die im *Period* -Parameter für das warten zwischen Pings angegeben ist. |
| /i `<IPaddress>` | Gibt die Quelladresse an. |
| /4 `<IPv4>` | Gibt an, dass pathping ausschließlich IPv4 verwendet. |
| /6 `<IPv6>` | Gibt an, dass für pathping nur IPv6 verwendet wird. |
| `<targetname>` | Gibt das Ziel an, das entweder durch die IP-Adresse oder den Hostnamen identifiziert wird. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Bei allen Parametern wird Groß-/Kleinschreibung beachtet.

- Um eine Überlastung des Netzwerks zu vermeiden und die Auswirkungen von Burst Verlusten zu minimieren, sollten Pings mit ausreichend langsamer Geschwindigkeit gesendet werden.

### <a name="example-of-the-pathping-command-output"></a>Beispiel für die Ausgabe des pathping-Befehls

```
D:\>pathping /n contoso1
Tracing route to contoso1 [10.54.1.196]
over a maximum of 30 hops:
  0  172.16.87.35
  1  172.16.87.218
  2  192.168.52.1
  3  192.168.80.1
  4  10.54.247.14
  5  10.54.1.196
computing statistics for 125 seconds...
            Source to Here   This Node/Link
Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  address
  0                                           172.16.87.35
                                0/ 100 =  0%   |
  1   41ms     0/ 100 =  0%     0/ 100 =  0%  172.16.87.218
                               13/ 100 = 13%   |
  2   22ms    16/ 100 = 16%     3/ 100 =  3%  192.168.52.1
                                0/ 100 =  0%   |
  3   24ms    13/ 100 = 13%     0/ 100 =  0%  192.168.80.1
                                0/ 100 =  0%   |
  4   21ms    14/ 100 = 14%     1/ 100 =  1%  10.54.247.14
                                0/ 100 =  0%   |
  5   24ms    13/ 100 = 13%     0/ 100 =  0%  10.54.1.196
Trace complete.
```

Beim Ausführen von **pathping** wird der Pfad in den ersten Ergebnissen aufgelistet. Als nächstes wird eine ausgelastete Nachricht für ungefähr 90 Sekunden angezeigt (die Zeit variiert je nach Hopanzahl). Während dieser Zeit werden Informationen von allen zuvor aufgelisteten Routern und von den Verknüpfungen zwischen Ihnen gesammelt. Am Ende dieses Zeitraums werden die Testergebnisse angezeigt.

Im obigen Beispiel Bericht zeigt die Spalten **This Node/Link**, **Lost/Sent = PCT** und **Address** an, dass der Link zwischen *172.16.87.218* und *192.168.52.1* 13% der Pakete entfernt. Die Router bei Hops 2 und 4 verwerfen auch an Sie adressierte Pakete, aber dieser Verlust wirkt sich nicht auf ihre Fähigkeit aus, Datenverkehr weiterzuleiten, der nicht an Sie adressiert ist.

Die für die Verknüpfungen angezeigten Verlustraten, die als senkrechter Strich ( **|** ) in der **Adress** Spalte identifiziert werden, geben eine Link Überlastung an, die den Verlust von Paketen verursacht, die an den Pfad weitergeleitet werden. Die für Router angezeigten Verlustraten (identifiziert durch Ihre IP-Adressen) geben an, dass diese Router überladen werden können.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Tracert-Befehl](tracert.md)
