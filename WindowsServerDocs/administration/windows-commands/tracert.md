---
title: tracert
description: Windows-Befehls Thema für tracert, das den Pfad zu einem Ziel bestimmt, indem ICMP-Echo Anforderungen (Internet Control Message Protocol) oder ICMPv6-Nachrichten an das Ziel gesendet werden, wobei die Werte für die Gültigkeitsdauer (TTL) inkrementell erhöht werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9032a032-2e5e-49d4-9e86-f821600e4ba6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a4485763aecf46aa91664c6a6a42c437be518f02
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832643"
---
# <a name="tracert"></a>tracert

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Bestimmt den Pfad zu einem Ziel, indem ICMP-Echo Anforderungen (Internet Control Message Protocol) oder ICMPv6-Nachrichten an das Ziel gesendet werden, wobei die Werte für die Gültigkeitsdauer (TTL) inkrementell erhöht werden. Der angezeigte Pfad ist die Liste der Schnittstellen, die sich im Pfad zwischen einem Quellhost und einem Ziel befinden. Die Near/Side-Schnittstelle ist die Schnittstelle des Routers, die dem sendenden Host im Pfad am nächsten liegt. Wird ohne Parameter verwendet, zeigt tracert die Hilfe an.   

## <a name="syntax"></a>Syntax  
```  
tracert [/d] [/h <MaximumHops>] [/j <Hostlist>] [/w <timeout>] [/R] [/S <Srcaddr>] [/4][/6] <TargetName>  
```  
#### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|/d|Verhindert, dass **tracert** versucht, die IP-Adressen der zwischen Router in ihre Namen aufzulösen. Dadurch kann die Anzeige von **tracert** -Ergebnissen beschleunigt werden.|  
|/h \<maximumhops >|Gibt die maximale Anzahl von Hops in dem Pfad an, der nach dem Ziel (Ziel) gesucht werden soll. Der Standardwert ist 30 Hops.|  
|/j \<hostlist >|Gibt an, dass Echo Request-Nachrichten die lose Quell Route-Option im IP-Header mit dem Satz von zwischen Zielen verwenden, die in der *Hostliste*angegeben sind. Beim losen Quell Routing können aufeinander folgende Zwischenziele durch einen oder mehrere Router getrennt werden. Die maximale Anzahl von Adressen oder Namen in der Hostliste beträgt 9. Die *Hostliste* ist eine Reihe von IP-Adressen (in punktierter Dezimal Schreibweise), getrennt durch Leerzeichen. Verwenden Sie diesen Parameter nur bei der Ablauf Verfolgung von IPv4-Adressen.|  
|/w \<Timeout >|Gibt die Zeit in Millisekunden an, die auf die überschreiten der ICMP-Zeit gewartet wird, oder eine Echo Antwortnachricht, die einer gegebenen Echo Anforderungs Nachricht entspricht, die empfangen werden soll. Wenn Sie nicht innerhalb des Timeouts empfangen werden, wird ein Sternchen (*) angezeigt. Das Standard Timeout beträgt 4000 (4 Sekunden).|  
|/R|Gibt an, dass der IPv6-Routing Erweiterungs Header verwendet wird, um eine Echo Anforderungs Nachricht an den lokalen Host zu senden, wobei das Ziel als Zwischenziel verwendet und die umgekehrte Route getestet wird.|  
|/S \<srcaddr >|Gibt die Quelladresse an, die in den Echo Anforderungs Nachrichten verwendet werden soll. Verwenden Sie diesen Parameter nur bei der Ablauf Verfolgung von IPv6-Adressen.|  
|/4|Gibt an, dass tracert. exe für diese Ablauf Verfolgung nur IPv4 verwenden kann.|  
|/6|Gibt an, dass tracert. exe für diese Ablauf Verfolgung nur IPv6 verwenden kann.|  
|\<TargetName >|Gibt das Ziel an, das entweder durch die IP-Adresse oder den Hostnamen identifiziert wird.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Hinweise  
-   Dieses Diagnosetool bestimmt den Pfad zu einem Ziel, indem ICMP-Echo Anforderungs Nachrichten mit unterschiedlichen Gültigkeitsdauer (Time to Live, TTL) an das Ziel gesendet werden. Jeder Router entlang des Pfads ist erforderlich, um die Gültigkeitsdauer in einem IP-Paket mindestens 1 zu verringern, bevor es weitergeleitet wird. Tatsächlich handelt es sich bei der Gültigkeitsdauer um einen maximalen Verbindungs Counter. Wenn die Gültigkeitsdauer für ein Paket den Wert 0 erreicht, wird erwartet, dass der Router eine Meldung über die Nachricht "ICMP-Zeitüberschreitung" an den Quellcomputer tracert legt den Pfad fest, indem die erste Echo Anforderungs Nachricht mit einer Gültigkeitsdauer von 1 gesendet und die Gültigkeitsdauer für jede nachfolgende Übertragung um 1 erhöht wird, bis das Ziel antwortet oder die maximale Anzahl von Hops erreicht wird. Die maximale Anzahl von Hops beträgt standardmäßig 30 und kann mithilfe des **/h** -Parameters angegeben werden. Der Pfad wird durch die Untersuchung der von zwischen Routern zurückgegebenen ICMP-Zeitüberschreitung und der vom Ziel zurückgegebenen Echo Antwortnachricht bestimmt. Einige Router geben jedoch keine Zeitüberschreitung für die Nachrichten von Paketen mit abgelaufenen TTL-Werten zurück und sind für den Tracert-Befehl invisile. In diesem Fall wird für diesen Hop eine Zeile mit Sternchen (*) angezeigt.  
-   Verwenden Sie den Befehl **pathping** , um einen Pfad zu verfolgen und Netzwerk Latenz und Paketverlust für jeden Router und Link im Pfad bereitzustellen.  
-   Dieser Befehl ist nur verfügbar, wenn das TCP/IP-Protokoll (Internet Protocol) als Komponente in den Eigenschaften eines Netzwerkadapters in Netzwerkverbindungen installiert ist.  

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Geben Sie Folgendes ein, um den Pfad zum Host mit dem Namen corp7.Microsoft.com zu verfolgen:  
```  
tracert corp7.microsoft.com  
```  
Um den Pfad zum Host mit dem Namen corp7.Microsoft.com zu verfolgen und die Auflösung der einzelnen IP-Adressen zu verhindern, geben Sie Folgendes ein:  
```  
tracert /d corp7.microsoft.com  
```  
Geben Sie Folgendes ein, um den Pfad zum Host mit dem Namen corp7.Microsoft.com zu verfolgen und die lose Quell Route 10.12.0.1/10.29.3.1/10.1.44.1 zu verwenden:  
```  
tracert /j 10.12.0.1 10.29.3.1 10.1.44.1 corp7.microsoft.com  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
