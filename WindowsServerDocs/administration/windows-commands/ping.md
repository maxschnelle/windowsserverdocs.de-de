---
title: ping
description: Verwenden Sie Ping, um die Netzwerkverbindung zu überprüfen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49272671-2eec-4fa5-881f-65c24cfbef52
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 1ac02a148061cd6eb8480c67f15e934f5fd57768
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816751"
---
# <a name="ping"></a>ping

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Die **Ping** Befehl überprüft die Konnektivität auf IP-Ebene auf einen anderen TCP/IP-Computer per Internet Control Message Protocol (ICMP)-Echo Request-Meldungen. Die Bestätigung des entsprechenden echo Reply-Meldungen angezeigt werden, zusammen mit Roundtripzeiten. Ping ist der wichtigste TCP/IP-Befehl verwendet, um die Konnektivität, namensauflösung und Erreichbarkeit zu beheben. Ohne Parameter verwendet **Ping** zeigt die Hilfe.

## <a name="syntax"></a>Syntax

```
ping [/t] [/a] [/n <Count>] [/l <Size>] [/f] [/I <TTL>] [/v <TOS>] [/r <Count>] [/s <Count>] [{/j <Hostlist> | /k <Hostlist>}] [/w <timeout>] [/R] [/S <Srcaddr>] [/4] [/6] <TargetName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|/t|Gibt an, Ping weiterhin Echo Request-Meldungen an das Ziel, bis unterbrochen gesendet. Zum Unterbrechen und Statistiken anzuzeigen, drücken Sie STRG + UNTBR. Unterbrechen und **Ping**, drücken Sie STRG + C.|
|/a|Gibt an, dass Reversenamensauflösung für die Ziel-IP-Adresse ausgeführt wird. Wenn dies erfolgreich ist, zeigt Ping an den entsprechenden Hostnamen an.|
|/ n \<Anzahl\>|Gibt die Anzahl der Echo gesendeten Daten anzufordern. Der Standardwert ist 4.|
|/ l \<Größe\>|Gibt die Länge in Bytes des Datenfelds in der Echo-Anforderung gesendete Nachrichten. Der Standardwert ist 32. Die maximale Größe beträgt 65,527.|
|/f|Gibt an, die echo Request-Nachrichten werden gesendet, mit dem nicht fragmentiert-Kennzeichen in den IP-Header auf 1 (verfügbar auf nur IPv4) festgelegt. Das Echo Request-Nachricht kann nicht von Routern im Pfad für das Ziel nicht fragmentiert werden. Dieser Parameter ist hilfreich zur Problembehebung bei der Path-Maximum Transmission Unit (PMTU).|
|/I \<TTL\>|Gibt den Wert des TTL-Felds in die IP-Header für Echo gesendeten Daten anzufordern. Der Standardwert ist der Standardwert der Gültigkeitsdauer (TTL) für den Host. Die maximale *Gültigkeitsdauer (TTL)* ist 255.|
|/ v \<: Themen zur Vorgehensweise\>|Gibt den Wert des Typs des Diensts (TOS)-Felds in die IP-Header für Echo Anforderungsnachrichten gesendet (verfügbar auf nur IPv4). Der Standardwert ist 0. *Themen zur Vorgehensweise* als Dezimalwert zwischen 0 und 255 angegeben ist.|
|/ r \<Anzahl\>|Gibt an, dass der Datensatz-Routing-Option im IP-Header verwendet wird, um den Pfad, indem das Echo Request-Nachricht aufzeichnen und entsprechende echoantwortmeldung (verfügbar auf nur IPv4). Jeden Hop im Pfad verwendet einen Eintrag in die Datensatz-Route-Option. Geben Sie möglichst ein *Anzahl* ist gleich oder größer als die Anzahl der Hops zwischen Quelle und Ziel. Die *Anzahl* muss mindestens 1 und maximal 9.|
|/ s \<Anzahl\>|Gibt an, dass die Internet-Timestamp-Option in der IP-Header verwendet wird, um den Zeitpunkt des Eingangs für das Echo Request-Nachricht aufzeichnen und entsprechende echoantwortmeldung für jeden Hop. Die *Anzahl* muss mindestens 1 und maximal 4 sein. Dies ist für Link-Local-Zieladressen erforderlich.|
|/j \<Hostlist\>|Gibt an, dass die Echo-Nachrichten verwenden für die Anforderung der Loose Source-Route in der IP-Header mit dem Satz von Zwischenziele, die im angegebenen option *Hostlist* (verfügbar auf nur IPv4). Mit losen Quell-routing, können nachfolgende Zwischenziele durch einen oder mehrere Router getrennt werden. Die maximale Anzahl von Adressen oder Namen in der Hostliste ist 9. Die Hostliste wird eine Reihe von IP-Adressen (in punktierter Dezimalschreibweise), die durch Leerzeichen getrennt.|
|/k \<Hostlist\>|Gibt an, dass die Echo-Nachrichten verwenden für die Anforderung der Strict Source-Route in der IP-Header mit dem Satz von Zwischenziele, die im angegebenen option *Hostlist* (verfügbar auf nur IPv4). Mit strict-Quell-routing, das nächste intermediate-Ziel direkt erreicht werden (es muss ein Nachbar für eine Schnittstelle des Routers sein). Die maximale Anzahl von Adressen oder Namen in der Hostliste ist 9. Die Hostliste wird eine Reihe von IP-Adressen (in punktierter Dezimalschreibweise), die durch Leerzeichen getrennt.|
|/w \<timeout\>|Gibt die Zeitspanne in Millisekunden, für das Echo Reply-Nachricht, die einen angegebenen Echo Request-Nachricht für den Empfang entspricht. Wenn das Echo Reply-Nachricht nicht innerhalb des Timeouts empfangen wird, wird die Fehlermeldung "Timeout der Anforderung" angezeigt. Das Standardtimeout beträgt 4.000 (4 Sekunden).|
|/R|Gibt an, dass es sich bei der Round-Trip-Pfad (verfügbar nur in IPv6) verfolgt werden.|
|/S \<Srcaddr\>|Gibt die Quelladresse (verfügbar nur in IPv6) verwenden.|
|/4|Gibt an, dass IPv4 verwendet wird, ein Pingsignal an. Dieser Parameter ist nicht erforderlich, auf den Zielhost mit einer IPv4-Adresse zu identifizieren. Es ist nur erforderlich, den Zielhost identifizieren anhand des Namens.|
|/6|Gibt an, dass IPv6 verwendet wird, ein Pingsignal an. Dieser Parameter ist nicht erforderlich, auf den Zielhost mit einer IPv6-Adresse zu identifizieren. Es ist nur erforderlich, den Zielhost identifizieren anhand des Namens.|
|\<TargetName\>|Gibt den Hostnamen oder IP-Adresse des Ziels.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Sie können **Ping** sowohl den Computernamen und die IP-Adresse des Computers zu testen. Wenn die IP-Adresse Ping erfolgreich ist, aber Pingen den Namen des Computers nicht ist, Sie möglicherweise ein Problem beim Auflösen von Namen. In diesem Fall sicher, dass der Computername, die Sie angegeben haben, können auch über die lokale Hosts-Datei, aufgelöst werden, mithilfe von Domain Name System (DNS) Abfragen, oder benennen mit NetBIOS-Verfahren zur Auflösung an.
-   Dieser Befehl ist nur verfügbar, wenn das Internetprotokoll (TCP/IP)-Protokoll als Komponente in den Eigenschaften eines Netzwerkadapters in den Netzwerkverbindungen installiert ist.

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel zeigt **Ping** Befehlsausgabe:

```
C:\>ping example.microsoft.com       
         pinging example.microsoft.com [192.168.239.132] with 32 bytes of data:       
         Reply from 192.168.239.132: bytes=32 time=101ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=100ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=120ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=120ms TTL=124
```

Um eine pinganforderung an die Ziels 10.0.99.221 auszuführen und 10.0.99.221 in seinen Hostnamen, geben Sie Folgendes ein:

```
ping /a 10.0.99.221
```

Das Ziel 10.0.99.221 auszuführen mit 10-Echo Request-Meldungen, einen Ping, von das jedes ein Datenfeld von 1000 Bytes aufweist, geben Sie Folgendes ein:

```
ping /n 10 /l 1000 10.0.99.221
```

Um eine pinganforderung an die Ziels 10.0.99.221 auszuführen, und notieren Sie die Route für 4 Hops, geben Sie Folgendes ein:

```
ping /r 4 10.0.99.221
```

Pingen das Ziel 10.0.99.221 auszuführen, und geben Sie die Route losen Quellen 10.12.0.1-10.29.3.1-10.1.44.1, geben Sie Folgendes ein:

```
ping /j 10.12.0.1 10.29.3.1 10.1.44.1 10.0.99.221
```

## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Befehlszeilensyntax](command-line-syntax-key.md)
