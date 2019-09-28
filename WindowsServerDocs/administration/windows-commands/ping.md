---
title: ping
description: Verwenden Sie Ping, um die Netzwerk Konnektivität zu überprüfen.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 7d9841c12d403d91e14021ff9df65246d322debd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372307"
---
# <a name="ping"></a>ping

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der **Ping** -Befehl überprüft die Konnektivität auf IP-Ebene zu einem anderen TCP/IP-Computer, indem ICMP-Echo Anforderungs Nachrichten (Internet Control Message Protocol) gesendet werden. Der Empfang entsprechender Echo Antwort Nachrichten wird zusammen mit Roundtrip-Zeiten angezeigt. Ping ist der primäre TCP/IP-Befehl, der verwendet wird, um die Konnektivität, Erreichbarkeit und Namensauflösung zu beheben. Wird ohne Parameter verwendet, **Ping** zeigt Hilfe an.

## <a name="syntax"></a>Syntax

```
ping [/t] [/a] [/n <Count>] [/l <Size>] [/f] [/I <TTL>] [/v <TOS>] [/r <Count>] [/s <Count>] [{/j <Hostlist> | /k <Hostlist>}] [/w <timeout>] [/R] [/S <Srcaddr>] [/4] [/6] <TargetName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|/t|Gibt an, dass der Ping das Senden von Echo Request-Nachrichten an das Ziel fortsetzen soll Um die Statistiken zu unterbrechen und anzuzeigen, drücken Sie Strg + Pause. Drücken Sie STRG + C, um das **Ping**zu unterbrechen und zu beenden.|
|/a|Gibt an, dass die umgekehrte Namensauflösung für die Ziel-IP-Adresse ausgeführt wird. Wenn dies erfolgreich ist, zeigt Ping den entsprechenden Hostnamen an.|
|/n \<count @ no__t-1|Gibt die Anzahl der gesendeten Echo Request-Meldungen an. Der Standardwert ist 4.|
|/l \<size @ no__t-1|Gibt die Länge des Daten Felds in den gesendeten Echo Anforderungs Nachrichten in Bytes an. Der Standardwert ist 32. Die maximale Größe beträgt 65.527.|
|/f|Gibt an, dass Echo Request-Nachrichten mit dem Flag do not Fragment im IP-Header, der auf 1 festgelegt ist, gesendet werden (nur auf IPv4 verfügbar). Die Echo Anforderungs Nachricht kann nicht von Routern im Pfad zum Ziel fragmentiert werden. Dieser Parameter ist für die Problembehandlung bei PMTU-Problemen (maximale Übertragungseinheit) nützlich.|
|/I \<TTL @ NO__T-1|Gibt den Wert des TTL-Felds im IP-Header für gesendete Echo Anforderungs Nachrichten an. Der Standardwert ist der standardmäßige TTL-Wert für den Host. Die maximale Gültigkeitsdauer beträgt 255.|
|/v \<tos @ no__t-1|Gibt den Wert des Felds Type of Service (TOS) im IP-Header für gesendete Echo Anforderungs Nachrichten an (nur auf IPv4 verfügbar). Die Standardeinstellung ist 0. " *TOS* " wird als Dezimalwert zwischen 0 und 255 angegeben.|
|/r \<count @ no__t-1|Gibt an, dass die Daten Satz-Routen Option im IP-Header verwendet wird, um den Pfad aufzuzeichnen, der von der Echo Anforderungs Nachricht und der entsprechenden Echo Antwortnachricht (nur auf IPv4 verfügbar) verwendet wird. Jeder Hop im Pfad verwendet einen Eintrag in der Daten Satz-Routen Option. Geben Sie nach *Möglichkeit eine Anzahl an, die* gleich oder größer als die Anzahl der Hops zwischen Quelle und Ziel ist. Die *Anzahl* muss mindestens 1 und maximal 9 betragen.|
|/s \<count @ no__t-1|Gibt an, dass die Option Internet Zeitstempel im IP-Header verwendet wird, um die Ankunftszeit für die Echo Anforderungs Nachricht und die entsprechende Echo Antwortnachricht für jeden Hop aufzuzeichnen. Die *Anzahl* muss mindestens 1 und maximal 4 betragen. Dies ist für Verbindungs lokale Zieladressen erforderlich.|
|/j \<hostlist @ no__t-1|Gibt an, dass die Echo Anforderungs Nachrichten die Option lose Quell Route im IP-Header mit dem Satz von zwischen Zielen verwenden, die in der *Hostliste* angegeben sind (nur auf IPv4 verfügbar). Beim losen Quell Routing können aufeinander folgende Zwischenziele durch einen oder mehrere Router getrennt werden. Die maximale Anzahl von Adressen oder Namen in der Hostliste beträgt 9. Die Hostliste ist eine Reihe von IP-Adressen (in punktierter Dezimal Schreibweise), getrennt durch Leerzeichen.|
|/k \<hostlist @ no__t-1|Gibt an, dass die Echo Request-Nachrichten die strikte Quell Route-Option im IP-Header mit dem Satz von zwischen Zielen verwenden, die in der *Hostliste* angegeben sind (nur auf IPv4 verfügbar). Beim strengen Quell Routing muss das nächste Zwischenziel direkt erreichbar sein (es muss ein Nachbar auf einer Schnittstelle des Routers sein). Die maximale Anzahl von Adressen oder Namen in der Hostliste beträgt 9. Die Hostliste ist eine Reihe von IP-Adressen (in punktierter Dezimal Schreibweise), getrennt durch Leerzeichen.|
|/w \<timeout @ no__t-1|Gibt die Zeitspanne in Millisekunden an, die auf die Antwortnachricht gewartet werden soll, die einer bestimmten Echo Anforderungs Nachricht entspricht. Wenn die Echo-Antwortnachricht nicht innerhalb des Timeouts empfangen wird, wird die Fehlermeldung "Timeout der Anforderung" angezeigt. Das Standard Timeout beträgt 4000 (4 Sekunden).|
|/R|Gibt an, dass der Roundtrip-Pfad verfolgt wird (nur auf IPv6 verfügbar).|
|/S \<srcaddr @ no__t-1|Gibt die zu verwendende Quelladresse an (nur auf IPv6 verfügbar).|
|/4|Gibt an, dass IPv4 zum Pingen verwendet wird. Dieser Parameter ist nicht erforderlich, um den Zielhost mit einer IPv4-Adresse zu identifizieren. Der Zielhost muss nur anhand des Namens identifiziert werden.|
|/6|Gibt an, dass IPv6 zum Pingen verwendet wird. Dieser Parameter ist nicht erforderlich, um den Zielhost mit einer IPv6-Adresse zu identifizieren. Der Zielhost muss nur anhand des Namens identifiziert werden.|
|\<targetname @ no__t-1|Gibt den Hostnamen oder die IP-Adresse des Ziels an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Mit **Ping** können Sie den Computernamen und die IP-Adresse des Computers testen. Wenn das Pingen der IP-Adresse erfolgreich ist, das Pingen des Computer namens jedoch nicht der Fall ist, liegt möglicherweise ein Problem mit der Namensauflösung vor. Stellen Sie in diesem Fall sicher, dass der Computername, den Sie angeben, über die lokale Hostdatei aufgelöst werden kann, indem Sie Domain Name System (DNS)-Abfragen oder NetBIOS-Namens Auflösungsverfahren verwenden.
-   Dieser Befehl ist nur verfügbar, wenn das TCP/IP-Protokoll (Internet Protocol) als Komponente in den Eigenschaften eines Netzwerkadapters in Netzwerkverbindungen installiert ist.

## <a name="BKMK_Examples"></a>Beispiele

Das folgende Beispiel zeigt die Ausgabe des **Ping** -Befehls:

```
C:\>ping example.microsoft.com       
         pinging example.microsoft.com [192.168.239.132] with 32 bytes of data:       
         Reply from 192.168.239.132: bytes=32 time=101ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=100ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=120ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=120ms TTL=124
```

Geben Sie Folgendes ein, um das Ziel 10.0.99.221 zu pingen und 10.0.99.221 in seinen Hostnamen aufzulösen:

```
ping /a 10.0.99.221
```

Geben Sie Folgendes ein, um das Ziel 10.0.99.221 mit 10 Echo Anforderungs Nachrichten zu pingen, von denen jedes über ein Datenfeld mit einer Größe von 1000 Bytes verfügt:

```
ping /n 10 /l 1000 10.0.99.221
```

Geben Sie Folgendes ein, um das Ziel 10.0.99.221 zu pingen und die Route für vier Hops aufzuzeichnen:

```
ping /r 4 10.0.99.221
```

Geben Sie Folgendes ein, um das Ziel 10.0.99.221 zu pingen und die lose Quell Route von 10.12.0.1-10.29.3.1-10.1.44.1 anzugeben:

```
ping /j 10.12.0.1 10.29.3.1 10.1.44.1 10.0.99.221
```

## <a name="additional-references"></a>Weitere Verweise
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
