---
title: NPS-Proxy-Server den Lastenausgleich
description: Sie können in diesem Thema verwenden, um mehr über Windows Server 2016 und Windows 10-VPN-Features und Funktionen erfahren.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 528280e6-b47e-489f-b310-b257d434aa0d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 04f466f7646fc5109af7379cab1240d8cd6829ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874401"
---
# <a name="nps-proxy-server-load-balancing"></a>NPS-Proxy-Server den Lastenausgleich

Gilt für: Windows Server 2016

Remote Authentication Dial-in User Service (RADIUS)-Clients, die Netzwerkzugriffsserver, z. B. virtuelles privates Netzwerk (VPN)-Servern und drahtlose Zugriffspunkte sind, erstellen die Weiterleitung von verbindungsanforderungen und senden sie, wie z. B. NPS RADIUS-Server. In einigen Fällen ein NPS zu vielen verbindungsanforderungen gleichzeitig ausführen möchten, möglicherweise zu Leistungseinbußen oder eine Überladung. Wenn ein NPS überladen ist, ist es eine gute Idee, weitere NPSs mit dem Netzwerk hinzufügen und Konfigurieren des Lastenausgleichs. Wenn Sie zwischen mehreren NPSs um zu verhindern, die Überladung von ein oder mehrere NPSs eingehende verbindungsanforderungen gleichmäßig verteilen, spricht man den Lastenausgleich.

Lastenausgleich ist besonders nützlich für:

- Organisationen, Extensible Authentication Protocol-Transport Layer Security \(EAP-TLS\) oder Protected Extensible Authentication Protocol \(PEAP\)- TLS für die Authentifizierung. Da dieser zwei Authentifizierungsmethoden Zertifikate für Server-Authentifizierung und für Benutzer oder Clientcomputer-Authentifizierung verwenden, ist die Last auf RADIUS-Proxys und Servern größer ist als wenn kennwortbasierte Authentifizierungsmethoden verwendet werden.
- Organisationen, die ununterbrochene Verfügbarkeit des Diensts zu bewältigen müssen.
- Internetdienstanbieter \(ISPs\) , die VPN-Zugriff für andere Organisationen ausgelagert. Die externe VPN-Dienste können eine große Anzahl von Authentifizierungsdatenverkehr generieren.

Es gibt zwei Methoden, die Sie verwenden können, um den Lastenausgleich von verbindungsanforderungen an Ihre NPSs gesendet:

- Konfigurieren Sie Ihre Netzwerkzugriffsserver zum Senden von verbindungsanforderungen an mehrere RADIUS-Server. Wenn Sie 20 Drahtloszugriffspunkten und zwei RADIUS-Server haben, konfigurieren Sie z. B. jeden Zugriffspunkt zum Senden von verbindungsanforderungen an beide RADIUS-Server. Sie können Lastenausgleich und Failover in jeden Netzwerkzugriffsserver bereitstellen, indem Sie den Access-Server zum Senden von verbindungsanforderungen an mehrere RADIUS-Server in einer bestimmten Reihenfolge ihrer Priorität konfigurieren. Diese Methode für den Lastenausgleich ist in der Regel sich am besten für kleine Unternehmen, die keine große Anzahl von RADIUS-Clients bereitstellen.
- Verwenden Sie NPS als RADIUS-Proxy konfiguriert, um verbindungsanforderungen für Lastenausgleich zwischen mehreren NPSs oder andere RADIUS-Server zu laden. Wenn Sie 100 Drahtloszugriffspunkten, einem NPS-Proxy und drei RADIUS-Server verfügen, können Sie z. B. die Zugriffspunkte zum Senden von sämtlichen Datenverkehr an den NPS-Proxy konfigurieren. Konfigurieren Sie auf dem NPS-Proxy Lastenausgleich, damit der Proxy gleichmäßig auf die Anforderungen von Verbindungen zwischen den drei RADIUS-Servern verteilt. Diese Methode für den Lastenausgleich ist am besten für mittlere und große Organisationen, die viele RADIUS-Clients und Servern verfügen.

In vielen Fällen ist der beste Ansatz für den Lastenausgleich so konfigurieren Sie RADIUS-Clients zum Senden von verbindungsanforderungen an zwei NPS-Proxyserver, und konfigurieren Sie die NPS-Proxys für den Lastenausgleich zwischen RADIUS-Server. Dieser Ansatz bietet sowohl für Failover als auch für den Lastenausgleich für die NPS-Proxys und RADIUS-Server.

## <a name="radius-server-priority-and-weight"></a>RADIUS-Server-Priorität und Gewichtung

Während des Konfigurationsvorgangs der NPS-Proxy können Sie remote-RADIUS-Servergruppen erstellen und klicken Sie dann die RADIUS-Server für jede Gruppe hinzuzufügen. Um einen Lastenausgleich konfigurieren, müssen Sie mehrere RADIUS-Server pro remote-RADIUS-Servergruppe verfügen. Beim Hinzufügen von Gruppenmitgliedern oder nach dem RADIUS-Server als Mitglied einer Gruppe zu erstellen können Sie das Hinzufügen von RADIUS-Server-Dialogfeld zum Konfigurieren die folgenden Elemente auf der Registerkarte "Lastenausgleich" zugreifen:

- **Priorität**. Priorität Gibt die Reihenfolge der Wichtigkeit des RADIUS-Servers mit dem NPS-Proxyserver an. Prioritätsstufe muss ein Wert zugewiesen werden, der eine ganze Zahl, z. B. 1, 2 oder 3 ist. Je niedriger die Zahl, die höhere Priorität der NPS-Proxy an den RADIUS-Server erhalten. Z. B. wenn der RADIUS-Server mit die höchste Priorität 1 zugewiesen ist, sendet der NPS-Proxy verbindungsanforderungen an den RADIUS-Server zuerst; Wenn Server mit Priorität 1 nicht verfügbar sind, schickt NPS verbindungsanforderungen an RADIUS-Servern mit Priorität 2 und So weiter. Sie können mehrere RADIUS-Server die gleiche Priorität zuweisen, und klicken Sie dann die Einstellung der Gatewaygewichtung verwenden, für den Lastenausgleich zwischen ihnen.

- **Gewichtung**. NPS-verwendet, die diese Gewichtung-Einstellung, um zu bestimmen, wie viele-Anforderungen an die einzelnen gesendet Gruppenmitglied, wenn die Mitglieder der Gruppe dieselbe Prioritätsstufe aufweisen. Einstellung der gatewaygewichtung muss einen Wert zwischen 1 und 100 zugewiesen werden, und der Wert stellt einen Prozentsatz von 100 Prozent. Wenn der remote-RADIUS-Servergruppe zwei Member enthält, dass beide verfügen über eine Prioritätsstufe 1 und eine Bewertung von Gewichtung von 50, leitet der NPS-Proxy z. B. 50 Prozent der verbindungsanforderungen an jeden RADIUS-Server weiter.

- **Erweiterte Einstellungen**. Diese Failovereinstellungen bieten eine Möglichkeit für den NPS, um festzustellen, ob der remote-RADIUS-Server nicht verfügbar ist. NPS fest, dass es sich bei ein RADIUS-Server nicht verfügbar ist, können sie beginnen, Senden von verbindungsanforderungen an andere Mitglieder der Gruppe. Mit diesen Einstellungen können Sie die Anzahl der Sekunden konfigurieren, die der NPS-Proxy auf eine Antwort vom RADIUS-Server wartet, bevor sie die Anforderung als verworfen berücksichtigt. die maximale Anzahl von gelöschten Anforderungen vor der NPS-Proxy identifiziert den RADIUS-Server als nicht verfügbar. und die Anzahl der Sekunden, die zwischen Anforderungen, bevor Sie die NPS-Proxy vergehen kann, identifiziert den RADIUS-Server als nicht verfügbar.

## <a name="configure-nps-proxy-load-balancing"></a>Konfigurieren Sie die NPS-Proxy-Lastenausgleich

Vor dem Konfigurieren des Lastenausgleichs, erstellen Sie einen Bereitstellungsplan, der wie viele RADIUS-Remoteservergruppen Sie benötigen, enthält die Server der einzelnen Gruppe und die Einstellung Priorität und-Gewichtung für jeden Server angehören.

>[!NOTE]
>Die folgenden Schritte wird davon ausgegangen, dass Sie bereits bereitgestellt und RADIUS-Server konfiguriert haben.

Zum Konfigurieren von NPS, fungiert als Proxy-Server und Weiterleiten von verbindungsanforderungen von RADIUS-Clients, RADIUS-Remoteserver müssen Sie die folgenden Aktionen ausführen:

1. Ihre RADIUS-Clients bereitstellen \(VPN-Server, DFÜ-Server, Terminaldienste-Gateway-Server, 802.1X-Authentifizierungsswitches und 802.1X-authentifizierte drahtloser Zugriffspunkte\) und konfigurieren sie zum Senden von verbindungsanforderungen an den NPS-Proxy Server.

2. Konfigurieren Sie der Netzwerkzugriffsserver auf dem Proxy NPS als RADIUS-Clients. Weitere Informationen finden Sie unter [Konfigurieren von RADIUS-Clients](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-radius-clients-configure).

3. Erstellen Sie eine oder mehrere RADIUS-Remoteservergruppen auf dem NPS-Proxy. Während dieses Vorgangs wird die RADIUS-Remoteservergruppen RADIUS-Server hinzugefügt. Weitere Informationen finden Sie unter [konfigurieren Sie RADIUS-Remoteservergruppen](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-crp-rrsg-configure).

4. Klicken Sie auf dem RADIUS-Server, auf dem NPS-Proxy, für jeden RADIUS-Server, mit denen Sie eine remote-RADIUS-Servergruppe hinzugefügt **Lastenausgleich** Registerkarte, und konfigurieren Sie **Priorität**, **Gewichtung** , und **Erweiterte Einstellungen**.

5. Konfigurieren Sie Verbindungsanforderungsrichtlinien, die zum Weiterleiten von Authentifizierungs- und kontoführungsanforderungen an remote-RADIUS-Servergruppen, auf dem NPS-Proxy. Sie müssen eine Verbindungsanforderungsrichtlinie pro remote-RADIUS-Servergruppe erstellen. Weitere Informationen finden Sie unter [Konfigurieren von Verbindungsanforderungsrichtlinien](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-crp-configure).


