---
title: Quality of Service (QoS)-Richtlinie
description: Dieses Thema enthält eine Übersicht über Quality of Service (QoS)-Richtlinie, die Gruppenrichtlinie zu verwenden, um die Netzwerkbandbreite für Datenverkehr von bestimmten Anwendungen und Diensten in Windows Server 2016 zu priorisieren kann.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 16918506-102c-482e-89d3-004ad8d6aabe
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a3ef81825ef6544bc96506e37bc027e0ac2a78db
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820281"
---
# <a name="quality-of-service-qos-policy"></a>Quality of Service, \(QoS\) Richtlinie

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können die QoS-Richtlinie als zentralen Punkt für die Verwaltung der Netzwerkbandbreite in Ihrer gesamten Active Directory-Infrastruktur verwenden, indem Sie QoS-Profile erstellen, deren Einstellungen mit Gruppenrichtlinien verteilt werden.

>[!NOTE]
>  Zusätzlich zu diesem Thema steht die folgende Dokumentation zum QoS-Richtlinie.  
>   
>  - [Erste Schritte mit QoS-Richtlinie](qos-policy-get-started.md)
>  - [Verwalten von QoS-Richtlinie](qos-policy-manage.md)
>  - [QoS-Richtlinie – häufig gestellte Fragen](qos-policy-faq.md)

QoS-Richtlinien auf eine benutzeranmeldesitzung oder einen Computer angewendet werden, als Teil eines Gruppenrichtlinienobjekts \(GPO\) , die Sie zum Active Directory-Container, z. B. einer Domäne, Site oder Organisationseinheit verknüpft haben \(Organisationseinheit\).

QoS-datenverkehrsverwaltung tritt ein, unter der Anwendungsschicht, was bedeutet, dass Ihre vorhandenen Anwendungen nicht geändert werden, um von den Vorteilen zu profitieren, die von QoS-Richtlinien bereitgestellt werden müssen.

## <a name="operating-systems-that-support-qos-policy"></a>Betriebssysteme, die QoS-Richtlinien unterstützen

Sie können die QoS-Richtlinie verwenden, zum Verwalten der Netzwerkbandbreite für Computer oder Benutzer mit den folgenden Microsoft-Betriebssystemen.

- Windows Server 2016
- Windows 10
- Windows Server 2012 R2
- Windows 8.1
- Windows Server 2012
- Windows 8
- Windows Server 2008 R2
- Windows 7
- WindowsServer 2008
- Windows Vista

### <a name="location-of-qos-policy-in-group-policy"></a>Speicherort der QoS-Richtlinie in der Gruppenrichtlinie

In Windows Server 2016 Gruppenrichtlinienverwaltungs-Editor ist der Pfad zur QoS-Richtlinie für die Computerkonfiguration Folgendes.

**Standarddomänenrichtlinie | Computerkonfiguration | Richtlinien für | Windows-Einstellungen | Richtlinie\-QoS basierend**

Dieser Pfad ist in der folgenden Abbildung dargestellt.

![Speicherort der QoS-Richtlinie in der Gruppenrichtlinie](../../media/QoS/QoS-Gp.jpg)

In Windows Server 2016 Gruppenrichtlinienverwaltungs-Editor ist der Pfad zur QoS-Richtlinie für die Benutzerkonfiguration in der folgenden.

**Standarddomänenrichtlinie | Benutzerkonfiguration | Richtlinien für | Windows-Einstellungen | Richtlinie\-QoS basierend**

Standardmäßig werden keine QoS-Richtlinien konfiguriert.

## <a name="why-use-qos-policy"></a>Gründe für die Verwendung von QoS-Richtlinie
  
Mit zunehmender Datenverkehr in Ihrem Netzwerk wird es zunehmend wichtig, dass Sie die Leistung des Netzwerks mit den Kosten des Diensts - Lastenausgleich des Netzwerkdatenverkehrs ist jedoch nicht normalerweise einfach, zu priorisieren und zu verwalten.

In Ihrem Netzwerk unternehmenswichtige\-kritische und Latenz\-sensible Anwendungen müssen im Wettbewerb stehen, für die Netzwerkbandbreite für Datenverkehr mit niedriger Priorität. Zur gleichen Zeit unterschieden einige Benutzer und Computer mit bestimmten netzwerkleistung, die Anforderungen möglicherweise Servicelevels.

Die Herausforderungen bei der Bereitstellung kostengünstigen, vorhersagbare netzwerkleistungsebenen häufig zunächst den Anschein über wide Area Network \(WAN\) Verbindungen oder latenzempfindliche Anwendungen wie Voice over IP- \(VoIP\) und Streamen von Videos. Allerdings das Endziel für die Bereitstellung von vorhersagbaren Netzwerk-Servicelevel gilt für alle Netzwerkumgebung \(z. B. ein Unternehmen-LAN\), und klicken Sie auf mehr als VoIP-Anwendungen, z. B. Ihres Unternehmens benutzerdefinierten Linie\-von\-Geschäftsanwendungen.
  
Richtlinienbasierte QoS ist das Netzwerk-Bandbreite-Verwaltungstool, das Netzwerkadressen-Steuerelement - basierend auf Anwendungen, Benutzer und Computer stellt. 

Wenn Sie QoS-Richtlinie verwenden, Ihre Anwendungen müssen nicht für bestimmte Application programming Interfaces, geschrieben werden \(APIs\). Dies bietet die Möglichkeit zum Verwenden von QoS mit vorhandenen Anwendungen. Darüber hinaus nutzt richtlinienbasierten QoS Ihrer vorhandenen Verwaltungsinfrastruktur, weil der Richtlinienbasierte QoS in Gruppenrichtlinien integriert ist.

## <a name="define-qos-priority-through-a-differentiated-services-code-point-dscp"></a>Definieren der QoS-Priorität über eine Differentiated Services Code Point- \(DSCP\)
  
Sie können die QoS-Richtlinien, die Priorität von Netzwerk-Datenverkehr mit einer Differentiated Services Code Point-definieren erstellen \(DSCP\) -Wert, der Sie verschiedene Arten von Netzwerkdatenverkehr zuweisen. 

Die DSCP können Sie einen Wert anwenden \(0 und 63\) innerhalb des Typs des Diensts \(: Themen zur Vorgehensweise\) Feld in einer IPv4-Paket-Header, und klicken Sie innerhalb des Traffic Class-Felds in IPv6. 

Der DSCP-Wert enthält, Netzwerk-Datenverkehr Klassifizierung auf das Internetprotokoll \(IP\) Ebene, die Router verwenden, um Datenverkehr warteschlangenverhalten entscheiden. 

Sie können z. B. Router so, dass Pakete mit bestimmten DSCP-Werten in einer der drei Warteschlangen platzieren konfigurieren: hoher Priorität, best-Effort oder niedriger als beste Lösung. 

Unternehmenskritische Netzwerkdatenverkehr, der in der Warteschlange mit hoher Priorität ist, hat die Einstellung über den anderen Datenverkehr.

### <a name="limit-network-bandwidth-use-per-application-with-throttle-rate"></a>Nutzung der Netzwerkbandbreite pro Anwendung mit Drosselungsrate Grenzwert

Sie können auch ausgehende Netzwerkdatenverkehr in einer Anwendung mit einer Drosselungsrate in QoS-Richtlinie einschränken.

Eine QoS-Richtlinie, die drosselungslimits fest definiert bestimmt der Geschwindigkeit des ausgehenden Netzwerkdatenverkehrs. Beispielsweise kann IT-Abteilung um WAN-Kosten zu verwalten, eine Vereinbarung zum Servicelevel implementieren, die angibt, dass ein Dateiserver nie Downloads nach einer bestimmten Rate bereitstellen kann.  

### <a name="use-qos-policy-to-apply-dscp-values-and-throttle-rates"></a>Verwenden von QoS-Richtlinie zum Anwenden von DSCP Werte und Raten einschränken

Sie können auch die QoS-Richtlinie verwenden, zum Anwenden von DSCP-Werten, und Drosselung Gebühren für ausgehenden Netzwerkdatenverkehr für die folgenden:

- Sendende Anwendung und den Verzeichnispfad

- Quelle und Ziel-IPv4- oder IPv6-Adressen oder Adresspräfixe

- Transmission Control Protocol-Protokoll – \(TCP\) und User Datagram-Protokoll \(UDP\)

- Quelle und Ziel-Ports und Portbereiche \(TCP- oder UDP\)

- Bestimmte Gruppen von Benutzern oder Computern über die Bereitstellung in der Gruppenrichtlinie

Mit diesen Steuerelementen können Sie angeben einer QoS-Richtlinie mit einem DSCP-Wert von 46 für eine Anwendung VoIP Router VoIP-Pakete in einer Warteschlange mit geringer Latenz zu platzieren oder Sie können eine QoS-Richtlinie verwenden, einen Satz von Servers ausgehenden Datenverkehr auf 512 KB pro Sekunde drosseln<c1/>Kbit/s\) beim Senden von TCP-Port 443.

Sie können auch eine QoS-Richtlinie für eine bestimmte Anwendung anwenden, die Anforderungen an die speziellen Netzwerkbandbreite verfügt. Weitere Informationen finden Sie unter [QoS-Richtlinie Szenarien](qos-policy-scenarios.md).
  
## <a name="advantages-of-qos-policy"></a>Vorteile der QoS-Richtlinie

Sie können mit QoS-Richtlinie konfigurieren und erzwingen QoS-Richtlinien, die auf dem Router und Switches nicht konfiguriert werden können. QoS-Richtlinie bietet folgende Vorteile.
  
1. **Stufe:** Es ist schwierig, die QoS-Richtlinien auf Benutzerebene auf Routern und Switches, zu erstellen, insbesondere dann, wenn dem Computer des Benutzers entweder wird mithilfe der dynamischen Zuweisung von IP-Adresse konfiguriert ist, oder wenn der Computer nicht mit einem festen Switch oder Routerports verbunden ist, wie häufig der Fall ist tragbare Computer. Im Gegensatz dazu QoS-Richtlinie erleichtert es, einen Benutzer konfigurieren\-Ebene QoS-Richtlinie auf einem Domänencontroller, und geben Sie die Richtlinie auf dem Computer des Benutzers.
2. **Flexibilität**. Unabhängig davon, wo und wie ein Computer mit dem Netzwerk verbunden ist QoS-Richtlinie angewendet wird – der Computer kann eine Verbindung herstellen über WiFi oder Ethernet-von einem beliebigen Standort aus. Für Benutzer\-Ebene QoS-Richtlinien, die QoS-Richtlinie auf praktisch jedem Gerät an einem beliebigen Speicherort angewendet wird, in denen der Benutzer anmeldet.
3. **Sicherheit:** Wenn Ihre IT-Abteilung des Benutzers Datenverkehr von a bis z verschlüsselt mithilfe von Internet Protocol Security \(IPsec\), den Datenverkehr auf Routern, die basierend auf Informationen über die IP-Schicht im Paket kann nicht klassifiziert werden \(z. B. einen TCP-Port\). Jedoch können mithilfe von QoS-Richtlinie können Sie klassifizieren Pakete an das Endgerät, um die Priorität der Pakete in den IP-Header anzugeben, bevor die IP-Nutzlasten verschlüsselt werden, und die Pakete gesendet werden.
4. **Leistung:** Einige QoS-Funktionen, z.B. Drosselung, werden besser ausgeführt werden, wenn sie sich näher an der Datenquelle befinden. QoS-Richtlinie wird diese QoS-Funktionen, die die Quelle am nächsten verschoben.
5. **Verwaltbarkeit:** QoS-Richtlinie erleichtert die Netzwerk-Verwaltbarkeit, gibt es zwei Möglichkeiten:

    **a**. Da es auf Gruppenrichtlinien basiert, können Sie QoS-Richtlinie zum Konfigurieren und verwalten einen Satz von QoS-Richtlinien für Benutzer/Computer bei Bedarf jederzeit und auf einem zentralen-Domänencontroller-Computer.

    **b**. QoS-Richtlinie erleichtert die Benutzer/Computer-Konfiguration durch einen Mechanismus zum Angeben von Richtlinien durch Uniform Resource Locator ermöglicht \(URL\) anstatt Richtlinien basierend auf allen Servern, in denen QoS-Richtlinien müssen, die IP-Adressen angewendet werden. Nehmen wir beispielsweise an, dass Ihr Netzwerk mit einen Cluster von Servern verfügt, die eine allgemeine URL freigeben. Mithilfe von QoS-Richtlinie können Sie eine Richtlinie, die basierend auf der allgemeinen URL, statt jede Richtlinie basierend auf der IP-Adresse der einzelnen Server eine Richtlinie für jeden Server im Cluster erstellen.

Im nächsten Thema in diesem Handbuch finden Sie unter [erste Schritte mit QoS-Richtlinie](qos-policy-get-started.md).

