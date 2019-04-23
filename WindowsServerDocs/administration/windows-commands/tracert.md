---
title: tracert
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9032a032-2e5e-49d4-9e86-f821600e4ba6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6a97c7656e646a22892eee5caa13d0163d05293d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837181"
---
# <a name="tracert"></a>tracert

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Bestimmt den Pfad zu einem Ziel von Internet Control Message Protocol (ICMP)-Echo Request oder ICMPv6-Nachrichten an das Ziel mit schrittweise erhöhen um Feldwerte für die Gültigkeitsdauer (TTL) gesendet. Der angezeigte Pfad ist die Liste der in der Nähe/Routerschnittstellen der Router im Pfad zwischen Quellhost und einem Ziel. Die Schnittstelle in der Nähe/Seite ist die Schnittstelle des Routers, der an den sendenden Host im Pfad am nächsten ist. Tracert zeigt ohne Parameter verwendet wird, die Hilfe.   

## <a name="syntax"></a>Syntax  
```  
tracert [/d] [/h <MaximumHops>] [/j <Hostlist>] [/w <timeout>] [/R] [/S <Srcaddr>] [/4][/6] <TargetName>  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|/d|Verhindert, dass **Tracert** versucht, die Zwischenrouter die IP-Adressen in Namen aufgelöst. Dies kann die Anzeige von beschleunigen **Tracert** Ergebnisse.|  
|/ h \<Max. Abschnitte >|Gibt die maximale Anzahl der Hops, die in den Suchpfad für das Ziel (Ziel). Der Standardwert ist 30.|  
|/j \<Hostlist>|Gibt an, die echo Request-Meldungen verwenden Sie die Option Loose Source Route in der IP-Header mit dem Satz von Zwischenziele, die im angegebenen *Hostlist*. Mit losen Quell-routing, können nachfolgende Zwischenziele durch einen oder mehrere Router getrennt werden. Die maximale Anzahl von Adressen oder Namen in der Hostliste ist 9. Die *Hostlist* ist eine Reihe von IP-Adressen (in punktierter Dezimalschreibweise), die durch Leerzeichen getrennt. Verwenden Sie diesen Parameter nur beim Verfolgen von IPv4-Adressen.|  
|/w \<timeout>|Gibt die Zeitspanne in Millisekunden zu warten, bis die ICMP-Zeit überschritten oder echo Reply-Nachricht, die für einen bestimmten Echo Request-Nachricht empfangen werden kann. Wenn nicht innerhalb des Timeouts eingegangen wird, wird ein Sternchen (*) angezeigt. Das Standardtimeout beträgt 4.000 (4 Sekunden).|  
|/R|Gibt an, dass der Header für die IPv6-Routing-Erweiterung verwendet werden, um ein Echo Request-Nachricht an den lokalen Host das Ziel als eines Zwischenziels verwenden und testen die reverse-Route zu senden.|  
|/S \<Srcaddr>|Gibt die Quelladresse um in das Echo Request-Nachrichten verwenden. Verwenden Sie diesen Parameter nur beim Verfolgen von IPv6-Adressen.|  
|/4|Gibt an, dass diese tracert.exe nur IPv4 für diese Ablaufverfolgung verwenden können.|  
|/6|Gibt an, dass diese tracert.exe nur IPv6 für diese Ablaufverfolgung verwenden können.|  
|\<TargetName>|Gibt an, das Ziel, und identifiziert entweder durch eine IP-Adresse oder den Hostnamen.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Hinweise  
-   Dieses Diagnosetool bestimmt den Pfad zu einem Ziel durch Senden von ICMP-Echo Request-Nachrichten mit unterschiedlichen Werte der Gültigkeitsdauer (TTL) an das Ziel. Jeder Router entlang des Pfads ist von mindestens 1 dekrementiert die Gültigkeitsdauer (TTL) in eine IP-Paket erforderlich, bevor die Weiterleitung. Die Gültigkeitsdauer (TTL) ist effektiv, einen Indikator für die maximale Link. Wenn die Gültigkeitsdauer für ein Paket auf 0 erreicht, wird der Router erwartet eine ICMP-Time Exceeded-Meldung an den Quellcomputer zurückgibt. Tracert bestimmt den Pfad durch Senden der ersten Echo Request-Nachricht mit einer Gültigkeitsdauer von 1 und erhöht, dass die Gültigkeitsdauer (TTL) von 1 auf jeder nachfolgenden Übertragung, bis das Ziel antwortet oder die maximale Anzahl von Hops erreicht ist. Die maximale Anzahl von Hops ist standardmäßig auf 30 und kann angegeben werden, mithilfe der **/h** Parameter. Der Pfad wird bestimmt durch Untersuchen der ICMP-Time Exceeded-Meldungen vom Zwischenrouter und den Echo-Antwortnachricht vom Ziel zurückgegeben. Allerdings einige Router keine Time Exceeded-Meldungen für Pakete mit einer abgelaufenen TTL-Werten zurück und werden Invisile dem Tracert-Befehl. In diesem Fall wird eine Reihe von Sternchen (*) für den betreffenden Hop angezeigt.  
-   Verwenden Sie zum Verfolgen eines Pfades, und geben Sie die Netzwerklatenz und Paketverlusten für die einzelnen Router und Verbindungen im Pfad, der **Pathping** Befehl.  
-   Dieser Befehl ist nur verfügbar, wenn das Internetprotokoll (TCP/IP)-Protokoll als Komponente in den Eigenschaften eines Netzwerkadapters in den Netzwerkverbindungen installiert ist.  

## <a name="BKMK_Examples"></a>Beispiele für  
Um den Pfad zu dem Host namens corp7.microsoft.com verfolgen möchten, geben Sie Folgendes ein:  
```  
tracert corp7.microsoft.com  
```  
Um den Pfad zu dem Host namens corp7.microsoft.com verfolgen und zu verhindern, dass die Auflösung der einzelnen IP-Adresse an den Namen, geben Sie Folgendes ein:  
```  
tracert /d corp7.microsoft.com  
```  
Um den Pfad zu dem Host namens corp7.microsoft.com verfolgen und den losen Quellen Route 10.12.0.1/10.29.3.1/10.1.44.1, geben Sie Folgendes ein:  
```  
tracert /j 10.12.0.1 10.29.3.1 10.1.44.1 corp7.microsoft.com  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
