---
title: pathping
description: Erfahren Sie, wie Sie mithilfe des Befehls pathping Informationen zur Netzwerk Latenz und zum Verlust von Daten erhalten.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ec430125-b1dc-4aad-a7c9-b70f486d9e3c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 3f853ef430207c08e78e0446ce67c6b5bec4c1db
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837694"
---
# <a name="pathping"></a>pathping

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Bietet Informationen zu Netzwerk Latenz und Netzwerk Verlust bei zwischen Hops zwischen einer Quelle und einem Ziel. der **pathping** sendet über einen bestimmten Zeitraum mehrere Echo Anforderungs Nachrichten an jeden Router zwischen einer Quelle und einem Ziel und berechnet dann die Ergebnisse basierend auf den von jedem Router zurückgegebenen Paketen. Da **pathping** den Grad des Paket Verlusts bei einem beliebigen Router oder Link anzeigt, können Sie feststellen, welche Router oder Subnetze Netzwerkprobleme aufweisen können. 

**pathping** führt die Entsprechung des Befehls **tracert** aus, indem identifiziert wird, welche Router sich im Pfad befinden. Anschließend werden Pings innerhalb eines angegebenen Zeitraums in regelmäßigen Abständen an alle Router gesendet und Statistiken auf Grundlage der von den einzelnen zurückgegebenen Zahlen berechnet. Wird ohne Parameter verwendet, zeigt **pathping** die Hilfe an. 

## <a name="syntax"></a>Syntax
```
pathping [/n] [/h] [/g <Hostlist>] [/p <Period>] [/q <NumQueries> [/w <timeout>] [/i <IPaddress>] [/4 <IPv4>] [/6 <IPv6>][<TargetName>]
```
#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/n|Verhindert, dass der **pfadping** versucht, die IP-Adressen der zwischen Router in ihre Namen aufzulösen. Dadurch wird möglicherweise die Anzeige von **pathping** -Ergebnissen beschleunigt.|
|/h \<maximumhops >|Gibt die maximale Anzahl von Hops in dem Pfad an, der nach dem Ziel (Ziel) gesucht werden soll. Der Standardwert ist 30 Hops.|
|/g \<hostlist >|Gibt an, dass die Echo Anforderungs Nachrichten die Option lose Quell Route im IP-Header mit dem Satz von zwischen Zielen verwenden, die in der *Hostliste*angegeben sind. Beim losen Quell Routing können aufeinander folgende Zwischenziele durch einen oder mehrere Router getrennt werden. Die maximale Anzahl von Adressen oder Namen in der Hostliste beträgt 9. Die *Hostliste* ist eine Reihe von IP-Adressen (in punktierter Dezimal Schreibweise), getrennt durch Leerzeichen.|
|/p \<Zeitraum >|Gibt die Anzahl von Millisekunden an, die zwischen aufeinander folgenden Pings gewartet werden soll. Der Standardwert ist 250 Millisekunden (1/4 Sekunde).|
|/q \<numqueries >|Gibt die Anzahl der Echo Request-Meldungen an, die an jeden Router im Pfad gesendet werden. Der Standardwert ist 100-Abfragen.|
|/w \<Timeout >|Gibt die Anzahl der Millisekunden an, die auf jede Antwort gewartet werden soll. Der Standardwert ist 3000 Millisekunden (3 Sekunden).|
|/i \<IPAddress->|Gibt die Quelladresse an.|
|/4 \<IPv4->|Gibt an, dass pathping ausschließlich IPv4 verwendet.|
|/6 \<IPv6->|Gibt an, dass für pathping nur IPv6 verwendet wird.|
|\<TargetName >|Gibt das Ziel an, das entweder durch die IP-Adresse oder den Hostnamen identifiziert wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   für **pathping** -Parameter wird die Groß-/Kleinschreibung
-   Um Netzwerk Überlastung zu vermeiden, sollten Pings mit ausreichend langsamer Geschwindigkeit gesendet werden.
-   Um die Auswirkungen von Burst Verlusten zu minimieren, sollten Sie keine Pings zu häufig senden.
-   Wenn Sie den **/p** -Parameter verwenden, werden Pings einzeln an jeden zwischen-Hop gesendet. Aus diesem Grund wird das Intervall zwischen zwei an denselben Hop gesendeten Pings mit der Anzahl der *Hops multipliziert.*
-   Wenn Sie den **/w** -Parameter verwenden, können mehrere Pings parallel gesendet werden. Aus diesem Grund wird die im *Timeout* -Parameter angegebene Zeitspanne nicht durch den Zeitraum begrenzt, der im *Period* -Parameter für das warten zwischen Pings angegeben ist.
-   Dieser Befehl ist nur verfügbar, wenn das TCP/IP-Protokoll (Internet Protocol) als Komponente in den Eigenschaften eines Netzwerkadapters in Netzwerkverbindungen installiert ist.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Das folgende Beispiel zeigt die Ausgabe des **pathping** -Befehls:

```
D:\>pathping /n corp1
Tracing route to corp1 [10.54.1.196]
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
Beim Ausführen von **pathping** wird der Pfad in den ersten Ergebnissen aufgelistet. Dies ist derselbe Pfad, der mit dem Befehl **tracert** angezeigt wird. Als nächstes wird eine ausgelastete Nachricht für ungefähr 90 Sekunden angezeigt (die Zeit variiert je nach Hopanzahl). Während dieser Zeit werden Informationen von allen zuvor aufgelisteten Routern und von den Verknüpfungen zwischen Ihnen gesammelt. am Ende dieses Zeitraums werden die Testergebnisse angezeigt.

Im obigen Beispiel Bericht zeigt die Spalten **This Node/Link**, **Lost/Sent = PCT** und **Address** an, dass der Link zwischen 172.16.87.218 und 192.168.52.1 13 Prozent der Pakete entfernt. Die Router bei Hops 2 und 4 verwerfen auch an Sie adressierte Pakete, aber dieser Verlust wirkt sich nicht auf ihre Fähigkeit aus, Datenverkehr weiterzuleiten, der nicht an Sie adressiert ist.

Die für die Verknüpfungen angezeigten Verlustraten, die als senkrechter Strich ( **|** ) in der **Adress** Spalte identifiziert werden, geben eine Link Überlastung an, die den Verlust von Paketen verursacht, die im Pfad weitergeleitet werden. Die für Router angezeigten Verlustraten (identifiziert durch Ihre IP-Adressen) geben an, dass diese Router überladen werden können.

## <a name="additional-references"></a>Weitere Verweise
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)