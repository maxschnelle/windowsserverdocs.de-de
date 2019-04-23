---
title: pathping
description: Erfahren Sie, wie Sie die Netzwerklatenz und Verlust-Informationen, die mit dem Befehl Pathping abrufen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec430125-b1dc-4aad-a7c9-b70f486d9e3c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: db3a0f5cd3c711f7df0a13627969dc7b74b3d605
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837241"
---
# <a name="pathping"></a>pathping

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Enthält Informationen über die Netzwerklatenz und Netzwerkverlust an zwischenzeitlichen Hops zwischen Quelle und Ziel. **Pathping** sendet mehrere Echo Request-Meldungen an alle Router zwischen einer Quelle und Ziel über einen Zeitraum und berechnet dann die Ergebnisse basierend auf die von den Routern zurückgegebenen Pakete. Da **Pathping** zeigt den Grad an Paketverlust bei jedem Router oder jeder Verbindung, können Sie bestimmen, welche Router oder ein Subnets Netzwerkprobleme auftreten können. 

**Pathping** führt das äquivalente die **Tracert** Befehl, indem Sie identifizieren, die Router im Pfad sind. Anschließend sendet Ping-Nachrichten in regelmäßigen Abständen an alle Router über einen angegebenen Zeitraum und berechnet die Statistiken, die basierend auf der Anzahl von jedem zurückgegeben. Ohne Parameter verwendet **Pathping** zeigt die Hilfe. 

## <a name="syntax"></a>Syntax
```
pathping [/n] [/h] [/g <Hostlist>] [/p <Period>] [/q <NumQueries> [/w <timeout>] [/i <IPaddress>] [/4 <IPv4>] [/6 <IPv6>][<TargetName>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/n|Verhindert, dass **Pathping** versucht, die Zwischenrouter die IP-Adressen in Namen aufgelöst. Dies kann zu beschleunigen, die Anzeige von **Pathping** Ergebnisse.|
|/ h \<Max. Abschnitte >|Gibt die maximale Anzahl der Hops, die in den Suchpfad für das Ziel (Ziel). Der Standardwert ist 30.|
|/g \<Hostlist>|Gibt an, dass die Echo-Nachrichten verwenden für die Anforderung der Loose Source-Route in der IP-Header mit dem Satz von Zwischenziele, die im angegebenen option *Hostlist*. Mit losen Quell-routing, können nachfolgende Zwischenziele durch einen oder mehrere Router getrennt werden. Die maximale Anzahl von Adressen oder Namen in der Hostliste ist 9. Die *Hostlist* ist eine Reihe von IP-Adressen (in punktierter Dezimalschreibweise), die durch Leerzeichen getrennt.|
|/ p \<Zeitraum >|Gibt die Anzahl der Millisekunden, die Wartezeit zwischen aufeinander folgenden Ping-Nachrichten. Der Standardwert ist 250 Millisekunden (1/4 Sekunden).|
|/q \<NumQueries>|Gibt die Anzahl der Echo Request-Nachrichten an alle Router im Pfad. Der Standardwert ist 100 Abfragen.|
|/w \<timeout>|Gibt die Anzahl der Millisekunden, die für jede Antwort zu warten. Der Standardwert ist 3000 Millisekunden (3 Sekunden).|
|/i \<IPaddress>|Gibt die Quelladresse an.|
|/4 \<IPv4>|Gibt an, dass diese Pathping nur IPv4 verwendet.|
|/6 \<IPv6>|Gibt an, dass diese Pathping nur IPv6 verwendet.|
|\<TargetName>|Gibt an, das Ziel, die entweder über die IP-Adresse oder den Hostnamen identifiziert.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   **Pathping** Parameter Groß-/Kleinschreibung beachtet werden.
-   Um eine Überlastung des Netzwerks zu vermeiden, soll Ping-Nachrichten mit einer ausreichend langsamen Geschwindigkeit gesendet werden.
-   Um die Auswirkungen der Burst-Verluste zu minimieren, werden nicht gesendet-Ping-Nachrichten zu häufig.
-   Bei Verwendung der **/p** Parameter-Ping-Nachrichten werden gesendet einzeln an jeden zwischenzeitlichen Hop. Aus diesem Grund ist das Intervall zwischen zwei Pings gesendet, um den gleichen Hop *Zeitraum* multipliziert die Anzahl der Hops.
-   Bei Verwendung der **/w** -Parameter mehrere Ping-Nachrichten gesendet werden können parallel. Aus diesem Grund der Zeitraum angegeben, der *Timeout* Parameter ist nicht begrenzt, um die Zeitspanne, die im angegebenen die *Zeitraum* Parameter für das Warten zwischen Pings.
-   Dieser Befehl ist nur verfügbar, wenn das Internetprotokoll (TCP/IP)-Protokoll als Komponente in den Eigenschaften eines Netzwerkadapters in den Netzwerkverbindungen installiert ist.

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel zeigt **Pathping** Befehlsausgabe:

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
Wenn **Pathping** wird ausgeführt, die ersten Ergebnisse auflisten des Pfads. Dies ist derselbe Pfad, der angezeigt wird, mit der **Tracert** Befehl. Als Nächstes wird eine Meldung für ungefähr 90 Sekunden angezeigt (die Zeit je nach Anzahl der Hops). Während dieser Zeit werden Informationen über alle oben aufgeführten Router und über die Links zwischen diesen gesammelt. am Ende dieses Zeitraums werden die Testergebnissen angezeigt.

Im obigen Beispielbericht die **Knoten/Verbindung**, **Lost "und" Sent = Pct** und **Adresse** Spalten zeigen, dass die Verbindung zwischen 172.16.87.218 und 192.168.52.1 13 löscht der Prozentsatz der Pakete. Die Router an Hops 2 und 4 sind auch an sie gerichtete Pakete löschen, aber dieser Ausfall wirkt sich nicht auf ihre Fähigkeit zum Weiterleiten des Datenverkehrs, die nicht an sie adressiert ist.

Paketverlust für Verknüpfungen an, als ein senkrechter Strich angezeigt (**|**) in der **Adresse** Spalte angeben des Link-Überlastung, die den Verlust von Paketen verursacht, die auf weitergeleitet wird, werden die der Pfad. Für Router (identifiziert durch ihre IP-Adressen) angezeigte Paketverlust anzugeben, dass diese Router überlastet sein könnte.

## <a name="additional-references"></a>Weitere Verweise
-   [Befehlszeilensyntax](command-line-syntax-key.md)