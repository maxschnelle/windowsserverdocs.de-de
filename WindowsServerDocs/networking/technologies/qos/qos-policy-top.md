---
title: Quality of Service (QoS)-Richtlinie
description: Dieses Thema enthält eine Übersicht über die Richtlinie für Quality of Service (QoS), können Sie mithilfe einer Gruppenrichtlinie um Datenverkehr Netzwerkbandbreite von bestimmten Anwendungen und Diensten in Windows Server2016 priorisieren.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 16918506-102c-482e-89d3-004ad8d6aabe
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 76405c677fe7eb4d51f9c190499b909ac2fe4a0c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="quality-of-service-qos-policy"></a>Quality of Service \(QoS\)-Richtlinie

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können QoS-Richtlinie als eine zentrale Verwaltung der Netzwerkbandbreite in Ihrer gesamten Active Directory-Infrastruktur verwenden, durch das Erstellen von QoS-Profile, deren Einstellungen mit der Gruppenrichtlinie verteilt werden.

>[!NOTE]
>  Zusätzlich zu diesem Thema wird die folgende Dokumentation zum QoS-Richtlinie zur Verfügung.  
>   
>  - [Erste Schrittemit QoS-Richtlinie](qos-policy-get-started.md)
>  - [Verwalten von QoS-Richtlinie](qos-policy-manage.md)
>  - [QoS-Richtlinie-häufig gestellte Fragen](qos-policy-faq.md)

QoS-Richtlinien werden als Teil eines Gruppenrichtlinienobjekts auf eine Sitzung des Benutzers oder einen Computer angewendet, die mit Active Directory-Container, z.B. eine Domäne, Site oder Organisationseinheit verknüpft sind, \(GPO\) \(OU\).

QoS-datenverkehrsverwaltung tritt ein, unter der Anwendungsschicht, was bedeutet, dass Ihre vorhandenen Anwendungen nicht geändert werden, um von den Vorteilen profitieren, die von QoS-Richtlinien bereitgestellt werden müssen.

## <a name="operating-systems-that-support-qos-policy"></a>Betriebssysteme, die QoS-Richtlinie unterstützen.

QoS-Richtlinie können Sie um Bandbreite für Computer oder Benutzer mit den folgenden Microsoft-Betriebssystemen verwalten.

- Windows Server 2016
- Windows10
- Windows Server2012 R2
- Windows 8.1
- Windows Server 2012
- Windows 8
- Windows Server2008 R2
- Windows 7
- Windows Server 2008
- Windowsvista

### <a name="location-of-qos-policy-in-group-policy"></a>Speicherort der QoS-Richtlinie in der Gruppenrichtlinie

In Windows Server2016 Gruppenrichtlinienverwaltungs-Editor ist der Pfad zur QoS-Richtlinie für die Computerkonfiguration Folgendes.

**Standarddomänenrichtlinie | Computerkonfiguration | Richtlinien | Windows-Einstellungen | Wird-basierter QoS**

Dieser Pfad ist in der folgenden Abbildungdargestellt.

![Speicherort der QoS-Richtlinie in der Gruppenrichtlinie](../../media/QoS/QoS-Gp.jpg)

In Windows Server2016 Gruppenrichtlinienverwaltungs-Editor ist der Pfad zur QoS-Richtlinie für die Benutzerkonfiguration Folgendes.

**Standarddomänenrichtlinie | Benutzerkonfiguration | Richtlinien | Windows-Einstellungen | Wird-basierter QoS**

Standardmäßig werden keine QoS-Richtlinien konfiguriert.

## <a name="why-use-qos-policy"></a>Gründe für die Verwendung von QoS-Richtlinie
  
Mit zunehmender Datenverkehr im Netzwerk, es ist immer wichtig, dass Sie die netzwerkleistung durch die Kosten für Service - Lastenausgleich des Netzwerkdatenverkehrs ist jedoch nicht normalerweise leicht zu priorisieren und zu verwalten.

In Ihrem Netzwerk müssen Mission\ kritische und Latency\ sensible Anwendungen für die Netzwerkbandbreite für Datenverkehr mit niedriger Priorität konkurrieren. Einige Benutzer und -Computer mit bestimmten netzwerkleistung, die erfüllt werden möglicherweise nicht gleichzeitig Service-Levelunterschieden.

Die sichere Bereitstellung kostengünstigen, vorhersehbare netzwerkleistungsebenen werden häufig zunächst über WAN-Netzwerkverbindungen \(WAN\) oder mit latenzempfindliche Anwendungen, wie z.B. Voice over IP \(VoIP\) und Video-Streaming angezeigt. Allerdings End-Ziel, vorhersehbare Netzwerk-Servicelevel gilt für alle Netzwerkumgebung \ (z.B. ein Unternehmen LAN vom Netzwerk), und auf mehrere VoIP-Anwendungen, z.B. benutzerdefinierte Ihres Unternehmens Modi für Zeilen--Of\-Business-Anwendungen.
  
Richtlinienbasierte QoS ist das Netzwerkbandbreite Management-Tool, das Sie Netzwerk - Steuerelement, basierend auf Anwendungen, Benutzer und Computer bietet. 

Wenn Sie QoS-Richtlinie verwenden, müssen die Anwendung nicht für bestimmte Application programming Schnittstellen \(APIs\) geschrieben werden. Dadurch werden die Möglichkeit, die QoS mit vorhandenen Anwendungen verwenden. Darüber hinaus nutzt richtlinienbasierten QoS Ihrer vorhandenen Verwaltungsinfrastruktur, da die Richtlinienbasierte QoS in die Gruppenrichtlinie integriert ist.

## <a name="define-qos-priority-through-a-differentiated-services-code-point-dscp"></a>Definieren Sie QoS-Priorität über einen Differentiated Services Code-Punkt \(DSCP\)
  
Sie können die QoS-Richtlinien erstellen, die mit dem differenzierte Services Code Point \(DSCP\) Wert Priorität Datenverkehr im Netzwerk zu definieren, die verschiedene Arten von Netzwerkdatenverkehr zugeordnet. 

Der DSCP können Sie eine \(0–63\) Wert im Feld Type of Service \(TOS\) in eine IPv4-Paket-Header, und klicken Sie im Feld Datenverkehrsklasse in IPv6 anwenden. 

Der DSCP-Wert enthält die Klassifizierung von Netzwerk-Datenverkehr auf der Ebene \(IP\) Internet Protocol Router verwenden, um Datenverkehr queuing Verhalten festlegen. 

Sie können z.B. Router so, dass Pakete mit bestimmten DSCP-Werten an einem der drei Warteschlangen Ort konfigurieren: hoher Priorität, bestmöglicher oder niedriger als die beste Leistung. 

Unternehmenskritische Netzwerkdatenverkehr, der in der Warteschlange mit hoher Priorität ist, hat Präferenz gegenüber anderen Datenverkehr.

### <a name="limit-network-bandwidth-use-per-application-with-throttle-rate"></a>Begrenzen der Bandbreitennutzung pro Anwendung mit der Drosselungsrate

Sie können auch eine Anwendung ausgehendem Netzwerkdatenverkehr einschränken, durch Angeben einer Drosselungsrate in QoS-Richtlinie.

Eine QoS-Richtlinie, die Drosselung Grenzen definiert bestimmt die Rate der ausgehenden Netzwerkverkehr. Beispielsweise kann die IT-Abteilung zum Verwalten von WAN-Kosten eine Vereinbarung zum Servicelevel implementieren, die gibt an, dass ein Dateiserver nie Downloads nach einem bestimmten Satz bereitstellen kann.  

### <a name="use-qos-policy-to-apply-dscp-values-and-throttle-rates"></a>Mit QoS-Richtlinie zum Anwenden von DSCP-Werte und drosseln Sätze

Sie können auch die QoS-Richtlinie verwenden, DSCP-Werten und drosseln Verarbeitungsraten für ausgehenden Netzwerkdatenverkehr wie folgt:

- Sendenden Anwendung und Verzeichnispfad

- Quell- und Ziel-IPv4- oder IPv6-Adressen oder Adresspräfixe

- Transmission Control-Protokoll - Protokoll \(TCP\) und User Datagram-Protokoll \(UDP\)

- Quell- und Zielports und Portbereiche \(TCP or UDP\)

- Bestimmte Gruppen von Benutzern oder Computern durch Bereitstellung in der Gruppenrichtlinie

Diese Steuerelemente verwenden, Sie können eine QoS-Richtlinie angeben, mit dem DSCP-Wert 46 für eine VoIP-Anwendung aktivieren Router VoIP-Pakete in einer Warteschlange mit geringer Wartezeit zu platzieren, oder Sie können eine QoS-Richtlinie verwenden, um eine Reihe von 512 Kilobytes pro Sekunde \(KBps\) ausgehender Datenverkehr Server drosseln beim Senden von TCP-Port 443.

Sie können auch eine QoS-Richtlinie auf eine bestimmte Anwendung anwenden, die spezielle Netzwerkbandbreite erforderlich ist. Weitere Informationen finden Sie unter [QoS-Richtlinie Szenarien](qos-policy-scenarios.md).
  
## <a name="advantages-of-qos-policy"></a>Vorteile der QoS-Richtlinie

Sie können mit QoS-Richtlinie konfigurieren und erzwingen QoS-Richtlinien, die auf Routern und Switches konfiguriert werden können. QoS-Richtlinie bietet die folgenden Vorteile.
  
1. **Ebene der Detail:** ist es schwierig, Benutzerebene QoS-Richtlinien auf Routern und Switches, vor allem bei dem Computer des Benutzers entweder mithilfe von dynamischen IP konfiguriert-Adresszuweisung oder wenn der Computer nicht mit festen Switch oder Routerports verbunden ist wie häufig der Fall bei tragbaren Computern zu erstellen. Im Gegensatz dazu erleichtert QoS-Richtlinie auf, um eine durch den Benutzer-Level-QoS-Richtlinie auf einem Domänencontroller konfigurieren und die Richtlinie auf dem Computer des Benutzers.
2. **Flexibilität**. Unabhängig davon, wo und wie ein Computer mit dem Netzwerk verbunden ist QoS-Richtlinie wird angewendet: der Computer kann sich über WiFi oder Ethernet-von einem beliebigen Standort verbinden. Für QoS-Richtlinien durch den Benutzer auf wird die QoS-Richtlinie auf allen kompatiblen Geräten an einem beliebigen Speicherort angewendet, in denen der Benutzer anmeldet.
3. **Sicherheit:** Wenn Ihre IT-Abteilung Benutzer Datenverkehr von Anfang bis Ende mit Internet Protocol Security \(IPsec\) verschlüsselt, können nicht Sie den Datenverkehr auf Routern, die basierend auf alle Informationen über die IP-Ebene im Paket klassifiziert \ (z.B. einen TCP-Port\). Mithilfe von QoS-Richtlinie können Sie jedoch Pakete an das Ende-Gerät an die Priorität der Pakete in der IP-Header, bevor die IP-Nutzlast verschlüsselt sind und die Pakete gesendet werden klassifizieren.
4. **Leistung:** einige QoS-Funktionen, z.B. Drosselung, sind besser ausgeführt werden, wenn sie näher an der Quelle sind. QoS-Richtlinie wird diese QoS-Funktionen, die Quelle am nächsten verschoben.
5. **Verwaltbarkeit:** QoS-Richtlinie verbessert die Netzwerk-Verwaltung auf zwei Arten:

    **a**. Da es auf Gruppenrichtlinien basiert, können Sie QoS-Richtlinie konfigurieren und verwalten eine Reihe von QoS-Richtlinien für Benutzer/Computer jederzeit und auf einen zentralen-Domänencontroller-Computer.

    **b**. QoS-Richtlinie erleichtert Benutzer/Computer-Konfiguration durch Bereitstellen eines Mechanismus zum Festlegen von Richtlinien von Uniform Resource Locator \(URL\) anstelle von Richtlinien auf Grundlage von IP-Adressen der Server, in denen die QoS-Richtlinien angewendet werden müssen. Nehmen wir beispielsweise an, dass Ihr Netzwerk einen Cluster von Servern verfügt, eine allgemeine URL gemeinsam verwenden. Mithilfe von QoS-Richtlinie können Sie eine Richtlinie basierend auf der allgemeinen URL, anstatt eine Richtlinie für jeden Server im Cluster erstellen, mit jeder Richtlinie basierend auf der IP-Adresse der einzelnen Server erstellen.

Im nächsten Thema in diesem Handbuch, finden Sie unter [erste Schrittemit QoS-Richtlinie](qos-policy-get-started.md).

