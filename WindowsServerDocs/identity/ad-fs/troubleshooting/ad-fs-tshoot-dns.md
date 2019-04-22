---
title: AD FS-Problembehandlung – DNS-Auflösung
description: In diesem Dokument wird beschrieben, wie DNS-Aspekte von AD FS-Problembehandlung
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7e0065feac4241b617b8b13c6867d5dc36634bd0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815901"
---
# <a name="ad-fs-troubleshooting---dns"></a>AD FS-Problembehandlung – DNS 
Einer der ersten Dinge, die überprüfen, ob AD FS nicht verwenden oder reagieren, ist, ist der DNS-namensauflösung.  Hierbei handelt es sich um grundlegende Tests aus, um festzustellen, ob die AD FS-Server oder die WAP-Servern im Netzwerk gefunden werden.  Für interne Benutzer gedacht sollte diese Tests in der AD FS-Server (STS) aufgelöst werden.    Für externe Benutzer sollten diese Tests in den WAP-Servern aufgelöst werden.

Im weiteren Verlauf dieses Dokuments zeigen, wie einige kurze Name Resolution Überprüfungen mithilfe von Befehlszeilentools.

## <a name="ping-test"></a>Ping-test
Überprüft die IP-Ebene-Konnektivität zu einem anderen TCP/IP-Computer per Internet Control Message Protocol (ICMP)-Echo Request-Meldungen. Der Empfang der entsprechenden Echo Reply-Meldungen werden angezeigt, zusammen mit Roundtripzeiten.  Weitere Informationen finden Sie unter [Ping](https://technet.microsoft.com/library/ff961503.aspx).


>[!NOTE]
>Beachten Sie, dass einige Organisationen diesen Port auf ihren Servern blockieren, und Sie erhalten möglicherweise eine **Timeout bei Anforderung** Antwort.

### <a name="to-use-a-ping-test"></a>Verwenden ein PING-Tests
1.  Öffnen Sie eine Eingabeaufforderung
2. Geben Sie PING <name of adfs server> ein. Beispiel:  PING "STS.contoso.com"
3. Eine Antwort vom Server sollte angezeigt werden.

![Ping](media/ad-fs-tshoot-dns/dns1.png)

## <a name="nslookup"></a>NSLookup
Zeigt Informationen, die Sie zum Diagnostizieren der Domain Name System (DNS)-Infrastruktur verwenden können.  Weitere Informationen finden Sie unter [NSLookup](https://technet.microsoft.com/library/cc725991.aspx).

### <a name="to-use-a-nslookup"></a>Eine NSLookup verwendet
1.  Öffnen Sie eine Eingabeaufforderung
2. Geben Sie PING <name of adfs server> ein. Beispiel: Nslookup "STS.contoso.com"
3. Daraufhin sollte die DNS-Informationen für den Server ![NSLookup](media/ad-fs-tshoot-dns/dns2.png)

## <a name="tracert"></a>Tracert
Bestimmt den Pfad zu einem Ziel, sendet Internet Control Message Protocol (ICMP)-Echo Request oder ICMPv6-Nachrichten an das Ziel mit inkrementell Zeit erhöhen, um Feldwerte für die Gültigkeitsdauer (TTL) benötigt.   Weitere Informationen finden Sie unter [Tracert](https://technet.microsoft.com/library/ff961507.aspx).


### <a name="to-use-tracert"></a>Tracert verwendet.
1.  Öffnen Sie eine Eingabeaufforderung
2. Geben Sie "tracert" <name of adfs server> ein. Beispiel: Tracert "STS.contoso.com"
3. Daraufhin sollte den angegebene Zielpfad verwendet, um den Server erreichen ![Tracert](media/ad-fs-tshoot-dns/dns3.png)

## <a name="next-steps"></a>Nächste Schritte

- [AD FS-Problembehandlung](ad-fs-tshoot-overview.md)