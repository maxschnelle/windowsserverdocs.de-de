---
title: NPS-Proxy Server für den Netzwerklastenausgleich
description: In diesem Thema können Sie Informationen zu Windows Server2016 und Windows10-VPN-Features und Funktionen.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 528280e6-b47e-489f-b310-b257d434aa0d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9f00eb6575284a69358c58b36d08672cdd69dc18
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="nps-proxy-server-load-balancing"></a>NPS-Proxy Server für den Netzwerklastenausgleich

Gilt für: Windows Server 2016

Remote Authentication Dial-in User Service (RADIUS)-Clients, die Netzwerkzugriffsserver, z.B. Server virtuelle private Netzwerke (VPN) und drahtlosen Zugriffspunkten, Verbindungsanforderungen zu erstellen und an den RADIUS-Server z.B. NPS senden. In einigen Fällen ein NPS-Server zu viele Verbindungsanfragen gleichzeitig ausführen möchten, erhalten möglicherweise Leistungseinbußen oder eine Überladung resultierenden. Wenn Sie ein NPS-Server überlastet ist, ist es empfiehlt sich, dass weitere NPS-Server mit dem Netzwerk und so konfigurieren Sie Lastenausgleich hinzufügen. Wenn Sie eingehende Verbindungsanforderungen auf mehrere NPS-Server zu verhindern, dass die Überladung des einen oder mehrere NPS-Server gleichmäßig verteilen, spricht man den Lastenausgleich.

Lastenausgleich ist besonders nützlich für:

- Organisationen, die Extensible Authentication Protocol-Transport Layer Security \(EAP-TLS\) oder Protected Extensible Authentication Protocol \ (PEAP\)-TLS für die Authentifizierung. Da diese Authentifizierungsmethoden Zertifikate für die Serverauthentifizierung und für Benutzer oder Computer Clientauthentifizierung verwenden, ist die Auslastung auf RADIUS-Proxys und Servern schwerer als wenn kennwortbasierte Authentifizierungsmethoden verwendet werden.
- Organisationen, die Aufrechterhaltung der Verfügbarkeit des Diensts müssen.
- Internet Service Provider \(ISPs\), die den externen VPN-Zugriff für andere Organisationen. Die externe VPN-Dienste können eine große Menge von Authentifizierungsdatenverkehr generieren.

Es gibt zwei Methoden, mit denen Sie den Lastenausgleich von Verbindungsanforderungen an Ihre NPS-Server gesendet:

- Konfigurieren Sie Ihre Netzwerkzugriffsserver, um Verbindungsanforderungen an mehrere RADIUS-Server zu senden. Beispielsweise haben 20 Drahtloszugriffspunkten und zwei RADIUS-Servern konfigurieren Sie jeder Zugriffspunkt zum Senden von Verbindungsanforderungen an beiden RADIUS-Server. Sie können Lastenausgleich und Failover bei jeder Netzwerkzugriffsserver durch Konfigurieren der Access-Server zum Senden von Verbindungsanforderungen an mehrere RADIUS-Server in einer bestimmten Reihenfolge der Priorität. Diese Methode für den Lastenausgleich ist in der Regel am besten für kleine Unternehmen, die eine große Anzahl von RADIUS-Clients nicht bereitstellen.
- Verwenden Sie NPS als RADIUS-Proxy konfiguriert, um für Verbindungsanforderungen zwischen mehreren NPS-Servern oder andere RADIUS-Server zu laden. Wenn Sie über 100 Drahtloszugriffspunkte, einem NPS-Proxy und drei RADIUS-Server verfügen, können Sie z.B. die Zugriffspunkte zum Senden der gesamte Datenverkehr an den NPS-Proxy konfigurieren. Konfigurieren Sie auf dem NPS-Proxy Lastenausgleich, damit der Proxy die Verbindungsanforderungen zwischen den drei RADIUS-Server gleichmäßig verteilt. Diese Methode für den Lastenausgleich ist am besten für mittelgroßen und großen Organisationen mit vielen RADIUS-Clients und Servern.

In vielen Fällen ist der beste Ansatz zum Lastenausgleich Konfigurieren von RADIUS-Clients zum Senden von Verbindungsanforderungen an zwei NPS-Proxyserver, und konfigurieren Sie die NPS-Proxys zum Lastenausgleich zwischen RADIUS-Server. Dieser Ansatz bietet Failover und Lastenausgleich für NPS-Proxys und RADIUS-Server.

## <a name="radius-server-priority-and-weight"></a>RADIUS-Server-Priorität und Gewichtung

Während des Konfigurationsvorgangs von NPS-Proxy können Sie RADIUS-Remoteservergruppen erstellen und dann jede Gruppe RADIUS-Server hinzufügen. Um den Lastenausgleich zu konfigurieren, müssen Sie mehrere RADIUS-Server pro RADIUS-Remoteservergruppe verfügen. Beim Hinzufügen von Gruppenmitgliedern oder nach dem RADIUS-Server als Gruppenmitglied einer erstellen können Sie das Dialogfeld Hinzufügen von RADIUS-Server, um die folgenden Elemente auf der Registerkarte Lastenausgleich konfigurieren zugreifen:

- **Priorität**. Priorität Gibt die Reihenfolge der Bedeutung des RADIUS-Servers mit dem NPS-Proxyserver an. Prioritätsstufe muss ein Wert zugewiesen werden, die ganze Zahl, z.B. 1, 2 oder 3. Je niedriger die Anzahl, die höhere Priorität der NPS-Proxy an den RADIUS-Server erhalten. Wenn beispielsweise der RADIUS-Server mit die höchste Priorität 1 zugewiesen ist, sendet der NPS-Proxy Verbindungsanforderungen an den RADIUS-Server zuerst. Wenn der Server mit der Priorität 1 nicht verfügbar sind, schickt NPS Verbindungsanforderungen an RADIUS-Server mit Priorität 2 usw. Sie können mehrere RADIUS-Server die gleiche Priorität zuweisen und dann die Gewichtung Einstellung für den Lastenausgleich zwischen ihnen.

- **Gewicht**. NPS verwendet diese Einstellung Gewichtung zu bestimmen, wie viele Verbindung zum jeweils senden Anforderungen Gruppe Mitglied bei den Mitgliedern der Gruppe gleicher Prioritätsstufe. Gewicht Einstellung muss einen Wert zwischen 1 und 100 zugewiesen werden, und der Wert gibt einen Prozentsatz von 100Prozent. Wenn die RADIUS-Remoteservergruppe zwei Elemente enthält, über eine Prioritätsstufe 1 und eine Bewertung Gewichtung von 50 verfügen, werden die NPS-Proxy z.B. 50Prozent der Verbindungsanfragen an jeden RADIUS-Server weitergeleitet.

- **Erweiterte Einstellungen**. Diese Failovereinstellungen bieten eine Möglichkeit für den NPS, um festzustellen, ob das RADIUS-Remoteserver nicht verfügbar ist. NPS fest, dass es sich bei ein RADIUS-Server nicht verfügbar ist, können sie beginnen, Senden von Verbindungsanforderungen an andere Mitglieder der Gruppe. Mit diesen Einstellungen können Sie die Anzahl der Sekunden konfigurieren, die der NPS-Proxy auf eine Antwort vom RADIUS-Server wartet, bevor sie die Anforderung als verworfen berücksichtigt. die maximale Anzahl von verworfenen Anfragen vor dem NPS-Proxy identifiziert den Radius-Server als nicht verfügbar. und die Anzahl der Sekunden zwischen Anforderungen, bevor Sie die NPS-Proxy kann den Radius-Server als nicht verfügbar.

## <a name="configure-nps-proxy-load-balancing"></a>Konfigurieren von NPS-Proxy-Lastenausgleich

Erstellen Sie bevor Sie den Lastenausgleich konfigurieren einen Bereitstellungsplan, der wie viele RADIUS-Remoteservergruppen Sie benötigen, enthält die Server Mitglieder der jeweiligen Gruppe, und die Einstellung Priorität und Gewichtung für jeden Server sind.

>[!NOTE]
>Die folgenden Schrittewird davon ausgegangen, dass Sie bereits bereitgestellt und RADIUS-Server konfiguriert haben.

Um NPS fungiert als Proxyserver und Vorwärts Verbindungsanforderungen von RADIUS-Clients, RADIUS-Servern zu konfigurieren, müssen Sie die folgenden Aktionen ausführen:

1. Ihre RADIUS-Clients bereitstellen \ (VPN-Server, DFÜ-Server, Terminaldienstegateway-Server, 802.1X-Authentifizierungsswitches und 802.1X-authentifizierten drahtlosen Zugriff Points\) konfigurieren Sie diese Verbindungsanforderungen an die NPS-Proxyserver zu senden.

2. Konfigurieren Sie die Netzwerkzugriffsserver als RADIUS-Clients, auf dem NPS-Proxy. Weitere Informationen finden Sie unter [Konfigurieren von RADIUS-Clients](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-radius-clients-configure).

3. Erstellen Sie eine oder mehrere RADIUS-Remoteservergruppen auf dem NPS-Proxy. Fügen Sie während dieses Vorgangs RADIUS-Server an den RADIUS-Remoteservergruppen. Weitere Informationen finden Sie unter [Konfigurieren von RADIUS-Remoteservergruppen](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-crp-rrsg-configure).

4. Klicken Sie auf dem RADIUS-Server, auf dem NPS-Proxy für jeden RADIUS-Server, die Sie eine RADIUS-Remoteservergruppe hinzufügen **Lastenausgleich** Registerkarte, und konfigurieren Sie **Priorität**, **Gewicht**, und **Erweiterte Einstellungen**.

5. Konfigurieren Sie Verbindungsanforderungsrichtlinien für die Authentifizierung und Kontoführung auf RADIUS-Remoteservergruppen Weiterleitung, auf dem NPS-Proxy. Sie müssen eine Verbindungsanforderungsrichtlinie pro RADIUS-Remoteservergruppe erstellen. Weitere Informationen finden Sie unter [Konfigurieren von Verbindungsanforderungsrichtlinien](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-crp-configure).


