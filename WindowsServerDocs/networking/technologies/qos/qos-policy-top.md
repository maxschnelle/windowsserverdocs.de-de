---
title: Quality of Service (QoS)-Richtlinie
description: Dieses Thema bietet einen Überblick über die Richtlinie für Quality of Service (QoS), mit der Sie Gruppenrichtlinie die Bandbreite von Netzwerk Datenverkehr für bestimmte Anwendungen und Dienste in Windows Server 2016 priorisieren können.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 16918506-102c-482e-89d3-004ad8d6aabe
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8854197b11f6533681d8f842af816ca0776d7040
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315463"
---
# <a name="quality-of-service-qos-policy"></a>Quality of Service \(QoS-\)-Richtlinie

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Sie können die QoS-Richtlinie als zentralen Punkt für die Verwaltung der Netzwerkbandbreite in Ihrer gesamten Active Directory-Infrastruktur verwenden, indem Sie QoS-Profile erstellen, deren Einstellungen mit Gruppenrichtlinien verteilt werden.

>[!NOTE]
>  Zusätzlich zu diesem Thema ist die folgende Dokumentation zu QoS-Richtlinien verfügbar.  
>   
>  - [Die ersten Schritte mit der QoS-Richtlinie](qos-policy-get-started.md)
>  - [Verwalten der QoS-Richtlinie](qos-policy-manage.md)
>  - [Häufig gestellte Fragen zu QoS-Richtlinien](qos-policy-faq.md)

QoS-Richtlinien werden für eine Benutzer Anmelde Sitzung oder einen Computer als Teil eines Gruppenrichtlinie Objekts \(GPO\), das Sie mit einem Active Directory Container verknüpft haben, z. b. eine Domäne, einen Standort oder eine Organisationseinheit \(ou\), angewendet.

Die QoS-Datenverkehrs Verwaltung erfolgt unter der Anwendungsschicht, was bedeutet, dass vorhandene Anwendungen nicht geändert werden müssen, um von den Vorteilen der QoS-Richtlinien profitieren zu können.

## <a name="operating-systems-that-support-qos-policy"></a>Betriebssysteme, die QoS-Richtlinien unterstützen

Sie können die QoS-Richtlinie verwenden, um die Bandbreite für Computer oder Benutzer mit den folgenden Microsoft-Betriebssystemen zu verwalten.

- Windows Server 2016
- Windows 10
- Windows Server 2012 R2
- Windows 8.1
- Windows Server 2012
- Windows 8
- Windows Server 2008 R2
- Windows 7
- WindowsServer 2008
- Windows Vista

### <a name="location-of-qos-policy-in-group-policy"></a>Speicherort der QoS-Richtlinie in Gruppenrichtlinie

In Windows Server 2016 Gruppenrichtlinienverwaltungs-Editor lautet der Pfad zur QoS-Richtlinie für die Computer Konfiguration wie folgt.

**Standard Domänen Richtlinie | Computer Konfiguration | Richtlinien | Windows-Einstellungen | Richtlinien\-basiertes QoS**

Dieser Pfad ist in der folgenden Abbildung dargestellt.

![Speicherort der QoS-Richtlinie in Gruppenrichtlinie](../../media/QoS/QoS-Gp.jpg)

In Windows Server 2016 Gruppenrichtlinienverwaltungs-Editor lautet der Pfad zur QoS-Richtlinie für die Benutzerkonfiguration wie folgt.

**Standard Domänen Richtlinie | Benutzerkonfiguration | Richtlinien | Windows-Einstellungen | Richtlinien\-basiertes QoS**

Standardmäßig sind keine QoS-Richtlinien konfiguriert.

## <a name="why-use-qos-policy"></a>Gründe für die Verwendung der QoS-Richtlinie
  
Wenn der Datenverkehr in Ihrem Netzwerk zunimmt, ist es immer wichtiger, dass Sie die Netzwerkleistung mit den dienstkosten ausgleichen, aber der Netzwerkverkehr ist normalerweise nicht einfach zu priorisieren und zu verwalten.

In Ihrem Netzwerk müssen Unternehmens\-kritisch und Latenz\-sensible Anwendungen um Netzwerkbandbreite gegen Datenverkehr mit niedrigerer Priorität konkurrieren. Gleichzeitig können einige Benutzer und Computer mit spezifischen Anforderungen an die Netzwerkleistung differenziertere Dienst Ebenen erfordern.

Die Herausforderungen bei der Bereitstellung kostengünstiger, vorhersag barer Netzwerk Leistungsstufen werden häufig über Wide Area Network \(WAN\) Verbindungen oder mit Latenz sensiblen Anwendungen, wie Voice-over-IP \(VoIP-\) und Video Streaming, angezeigt. Das Ziel der Bereitstellung vorhersag barer Netzwerkdienst Ebenen gilt jedoch für jede Netzwerkumgebung \(z. b. für das lokale Netzwerk eines Unternehmens\)und für mehr als VoIP-Anwendungen, wie z. b. die benutzerdefinierte\-Leitung Ihres Unternehmens\-Geschäftsanwendungen.
  
Die Richtlinien basierte QoS ist das Verwaltungs Tool für Netzwerkbandbreite, mit dem Sie Netzwerksteuerung basierend auf Anwendungen, Benutzern und Computern bereitstellen können. 

Wenn Sie die QoS-Richtlinie verwenden, müssen Ihre Anwendungen nicht für bestimmte Anwendungs Programmierschnittstellen \(APIs\)geschrieben werden. Dadurch haben Sie die Möglichkeit, QoS mit vorhandenen Anwendungen zu verwenden. Außerdem nutzt das Richtlinien basierte QoS die vorhandene Verwaltungsinfrastruktur, da das Richtlinien basierte QoS in Gruppenrichtlinie integriert ist.

## <a name="define-qos-priority-through-a-differentiated-services-code-point-dscp"></a>Definieren Sie die QoS-Priorität über einen differenzierte Dienste Codepunkt \(DSCP\)
  
Sie können QoS-Richtlinien erstellen, die die Priorität des Netzwerk Datenverkehrs mit einem differenzierte Dienste Codepunkt \(DSCP-\) Wert definieren, den Sie unterschiedlichen Arten von Netzwerk Datenverkehr zuweisen. 

Der DSCP ermöglicht das Anwenden eines Werts \(0 – 63\) innerhalb des Typs \(TOS\) Feld in einem IPv4-Paket-Header und innerhalb des Felds "Traffic Class" in IPv6. 

Der DSCP-Wert ermöglicht die Klassifizierung des Netzwerk Datenverkehrs auf dem Internet Protokoll \(IP-\) Ebene, die von Routern verwendet wird, um das Verhalten der Traffic Queuing 

Beispielsweise können Sie Router so konfigurieren, dass Sie Pakete mit bestimmten DSCP-Werten in einer von drei Warteschlangen platzieren: mit hoher Priorität, dem besten Aufwand oder niedriger als der bestmögliche Aufwand. 

Unternehmens kritischer Netzwerk Datenverkehr, der sich in der Warteschlange mit hoher Priorität befindet, hat Vorrang vor anderem Datenverkehr.

### <a name="limit-network-bandwidth-use-per-application-with-throttle-rate"></a>Begrenzen der Nutzung der Netzwerkbandbreite pro Anwendung mit Drosselungs Rate

Sie können auch den ausgehenden Netzwerk Datenverkehr einer Anwendung einschränken, indem Sie eine Drosselungs Rate in der QoS-Richtlinie angeben.

Eine QoS-Richtlinie, die Drosselungs Grenzwerte definiert, bestimmt die Rate des ausgehenden Netzwerk Datenverkehrs. Zum Verwalten von WAN-Kosten könnte eine IT-Abteilung beispielsweise eine Vereinbarung zum Service Level implementieren, die angibt, dass ein Dateiserver nie Downloads über eine bestimmte Rate hinaus bereitstellen kann.  

### <a name="use-qos-policy-to-apply-dscp-values-and-throttle-rates"></a>Anwenden von DSCP-Werten und Drosselungs Raten mithilfe der QoS-Richtlinie

Sie können auch die QoS-Richtlinie verwenden, um DSCP-Werte und Drosselungs Raten für ausgehenden Netzwerk Datenverkehr auf Folgendes anzuwenden:

- Anwendungs-und Verzeichnispfad werden gesendet

- IPv4-oder IPv6-Quell-und IPv6-Adressen oder Adress Präfixe

- Protokoll-Transmission Control Protocol \(TCP\) und User Datagram Protocol \(UDP\)

- Quell-und Zielports und Port Bereiche \(TCP oder UDP\)

- Bestimmte Gruppen von Benutzern oder Computern durch Bereitstellung in Gruppenrichtlinie

Mithilfe dieser Steuerelemente können Sie eine QoS-Richtlinie mit dem DSCP-Wert 46 für eine VoIP-Anwendung angeben. Dadurch können Router VoIP-Pakete in einer Warteschlange mit geringer Latenz platzieren, oder Sie können eine QoS-Richtlinie verwenden, um den ausgehenden Datenverkehr eines Satzes von Servern auf 512 Kilobyte pro Sekunde \(Kbit/s zu drosseln\) beim Senden von 443 TCP-

Sie können auch eine QoS-Richtlinie auf eine bestimmte Anwendung anwenden, die über besondere Bandbreitenanforderungen verfügt. Weitere Informationen finden Sie unter [Szenarien für die QoS-Richtlinie](qos-policy-scenarios.md).
  
## <a name="advantages-of-qos-policy"></a>Vorteile der QoS-Richtlinie

Mit der QoS-Richtlinie können Sie QoS-Richtlinien konfigurieren und erzwingen, die auf Routern und Switches nicht konfiguriert werden können. Die QoS-Richtlinie bietet die folgenden Vorteile:
  
1. **Detailstufe:** Es ist schwierig, QoS-Richtlinien auf Benutzerebene auf Routern oder Switches zu erstellen. Dies gilt insbesondere, wenn der Computer des Benutzers entweder mithilfe der dynamischen IP-Adresszuweisung konfiguriert ist oder wenn der Computer nicht mit einem festgelegten Switch oder Routerports verbunden ist, wie es bei tragbaren Computern häufig der Fall ist. Im Gegensatz dazu erleichtert die QoS-Richtlinie das Konfigurieren einer Benutzer\-Ebene-QoS-Richtlinie auf einem Domänen Controller und die Weitergabe der Richtlinie an den Computer des Benutzers.
2. **Flexibilität**. Unabhängig davon, wo oder wie ein Computer eine Verbindung mit dem Netzwerk herstellt, wird die QoS-Richtlinie angewendet. der Computer kann über WiFi oder Ethernet von einem beliebigen Standort aus eine Verbindung herstellen. Für QoS-Richtlinien auf Benutzer\-Ebene wird die QoS-Richtlinie auf jedem kompatiblen Gerät an einem beliebigen Speicherort angewendet, an dem sich der Benutzer anmeldet.
3. **Sicherheit:** Wenn Ihre IT-Abteilung den Datenverkehr von Benutzern mithilfe von Internet Protokoll Sicherheit \(IPSec\)von End-to-End verschlüsselt, können Sie den Datenverkehr auf Routern nicht auf der Grundlage von Informationen klassifizieren, die über der IP-Ebene im Paket liegen \(z. b. einem TCP-Port\). Mithilfe der QoS-Richtlinie können Sie jedoch Pakete auf dem Endgerät klassifizieren, um die Priorität der Pakete im IP-Header anzugeben, bevor die IP-Nutzlasten verschlüsselt und die Pakete gesendet werden.
4. **Leistung:** Einige QoS-Funktionen, wie z. b. Drosselung, werden besser ausgeführt, wenn Sie sich näher an der Quelle befinden. QoS-Richtlinie verschiebt solche QoS-Funktionen, die der Quelle am nächsten sind.
5. **Verwaltbarkeit:** Die QoS-Richtlinie verbessert die Netzwerk Verwaltbarkeit auf zwei Arten:

    **ein**. Da es auf Gruppenrichtlinie basiert, können Sie eine QoS-Richtlinie verwenden, um eine Gruppe von Benutzer-/Computer-QoS-Richtlinien zu konfigurieren und zu verwalten, wenn dies erforderlich ist, und auf einem zentralen Domänen Controller Computer.

    **b**. Die QoS-Richtlinie vereinfacht die Benutzer-/Computerkonfiguration durch Bereitstellung eines Mechanismus zum Angeben von Richtlinien Uniform Resource Locator \(-URL\) anstelle der Angabe von Richtlinien basierend auf den IP-Adressen der einzelnen Server, auf die QoS-Richtlinien angewendet werden müssen. Nehmen Sie beispielsweise an, dass Ihr Netzwerk über einen Cluster von Servern verfügt, die eine gemeinsame URL gemeinsam verwenden. Mithilfe der QoS-Richtlinie können Sie eine Richtlinie basierend auf der allgemeinen URL erstellen, anstatt eine Richtlinie für jeden Server im Cluster zu erstellen, wobei jede Richtlinie auf der IP-Adresse der einzelnen Server basiert.

Das nächste Thema in dieser Anleitung finden Sie unter [Getting Started with QoS Policy](qos-policy-get-started.md).

