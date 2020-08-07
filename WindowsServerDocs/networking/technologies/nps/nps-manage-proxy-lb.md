---
title: NPS-Proxy Server-Lastenausgleich
description: In diesem Thema erfahren Sie mehr über Windows Server 2016-und Windows 10-VPN-Features und-Funktionen.
ms.topic: article
ms.assetid: 528280e6-b47e-489f-b310-b257d434aa0d
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8710723c397744f3ba937ac863cf5ab45dc8a4f1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952157"
---
# <a name="nps-proxy-server-load-balancing"></a>NPS-Proxy Server-Lastenausgleich

Gilt für: Windows Server 2016

Remote Authentication Dial-in User Service (RADIUS)-Clients, bei denen es sich um Netzwerk Zugriffs Server wie VPN-Server (virtuelles privates Netzwerk) und drahtlos Zugriffspunkte handelt, werden Verbindungsanforderungen erstellt und an RADIUS-Server wie NPS gesendet. In einigen Fällen kann ein NPS zu viele Verbindungsanforderungen gleichzeitig empfangen, was zu einer Beeinträchtigung der Leistung oder einer Überlastung führt. Wenn ein NPS überladen ist, empfiehlt es sich, dem Netzwerk weitere NPSS hinzuzufügen und den Lastenausgleich zu konfigurieren. Wenn Sie eingehende Verbindungsanforderungen gleichmäßig auf mehrere NPSS verteilen, um zu verhindern, dass ein oder mehrere NPSS überladen werden, wird dies als Lastenausgleich bezeichnet.

Der Lastenausgleich ist besonders nützlich für:

- Organisationen, die das Extensible Authentication-Protokoll Transport Layer Security \( EAP-TLS \) oder das Protected Extensible Authentication Protocol \( PEAP \) -TLS für die Authentifizierung verwenden. Da diese Authentifizierungsmethoden Zertifikate für die Server Authentifizierung und entweder für die Authentifizierung von Benutzern oder Client Computern verwenden, ist die Auslastung von RADIUS-Proxys und-Servern schwerer als bei der Verwendung von Kenn Wort basierten Authentifizierungsmethoden.
- Organisationen, die die fortlaufende Dienst Verfügbarkeit aufrechterhalten müssen.
- Internet Dienstanbieter- \( ISPs \) , die den VPN-Zugriff für andere Organisationen auslagern. Die ausgelagerten VPN-Dienste können eine große Menge an Authentifizierungs Datenverkehr generieren.

Es gibt zwei Methoden, mit denen Sie die Last von Verbindungsanforderungen, die an Ihren NPSS gesendet werden, ausgleichen können:

- Konfigurieren Sie Ihre Netzwerk Zugriffs Server so, dass Verbindungsanforderungen an mehrere RADIUS-Server gesendet werden. Wenn Sie z. b. über 20 drahtlos Zugriffspunkte und zwei RADIUS-Server verfügen, konfigurieren Sie jeden Zugriffspunkt so, dass Verbindungsanforderungen an beide RADIUS-Server gesendet werden. Sie können einen Lastenausgleich auf jedem Netzwerk Zugriffs Server ausführen und ein Failover bereitstellen, indem Sie den Zugriffs Server so konfigurieren, dass Verbindungsanforderungen in einer bestimmten Reihenfolge der Priorität an mehrere RADIUS-Server gesendet werden. Diese Methode des Lasten Ausgleichs ist für kleine Unternehmen, die keine große Anzahl von RADIUS-Clients bereitstellen, in der Regel am besten geeignet.
- Verwenden Sie als RADIUS-Proxy konfigurierte NPS für den Lastenausgleich von Verbindungsanforderungen zwischen mehreren NPSS-oder anderen RADIUS-Servern. Wenn Sie z. b. über 100 drahtlose Zugriffspunkte, einen NPS-Proxy und drei RADIUS-Server verfügen, können Sie die Zugriffspunkte so konfigurieren, dass der gesamte Datenverkehr an den NPS-Proxy gesendet wird. Konfigurieren Sie den Lastenausgleich auf dem NPS-Proxy so, dass der Proxy die Verbindungsanforderungen zwischen den drei RADIUS-Servern gleichmäßig verteilt. Diese Methode des Lasten Ausgleichs eignet sich am besten für mittelgroße und große Unternehmen, die über viele RADIUS-Clients und-Server verfügen.

In vielen Fällen besteht die beste Methode für den Lastenausgleich darin, RADIUS-Clients so zu konfigurieren, dass Verbindungsanforderungen an zwei NPS-Proxy Server gesendet werden, und dann die NPS-Proxys für den Lastenausgleich zwischen RADIUS-Servern zu konfigurieren Dieser Ansatz ermöglicht sowohl Failover als auch Lastenausgleich für NPS-Proxys und RADIUS-Server.

## <a name="radius-server-priority-and-weight"></a>Priorität und Gewichtung des RADIUS-Servers

Während der Konfiguration des NPS-Proxys können Sie RADIUS-Remote Server Gruppen erstellen und dann jeder Gruppe RADIUS-Server hinzufügen. Zum Konfigurieren des Lasten Ausgleichs müssen Sie über mehr als einen RADIUS-Server pro RADIUS-Remote Server Gruppe verfügen. Beim Hinzufügen von Gruppenmitgliedern oder nach dem Erstellen eines RADIUS-Servers als Gruppenmitglied können Sie auf das Dialogfeld RADIUS-Server hinzufügen zugreifen, um die folgenden Elemente auf der Registerkarte Lastenausgleich zu konfigurieren:

- **Priorität**. Priorität gibt die Reihenfolge der Wichtigkeit des RADIUS-Servers zum NPS-Proxy Server an. Der Prioritätsstufe muss ein Wert zugewiesen werden, der eine ganze Zahl ist, z. b. 1, 2 oder 3. Je niedriger die Zahl, desto höher die Priorität des NPS-Proxys für den RADIUS-Server. Wenn dem RADIUS-Server z. b. die höchste Priorität 1 zugewiesen wird, sendet der NPS-Proxy zuerst Verbindungsanforderungen an den RADIUS-Server. Wenn Server mit Priorität 1 nicht verfügbar sind, sendet NPS Verbindungsanforderungen an RADIUS-Server mit Priorität 2 usw. Sie können mehreren RADIUS-Servern dieselbe Priorität zuweisen und dann die Gewichtungs Einstellung verwenden, um einen Lastenausgleich zwischen den Servern durchführen.

- **Gewichtung**. NPS verwendet diese Gewichtungs Einstellung, um zu bestimmen, wie viele Verbindungsanforderungen an die einzelnen Gruppenmitglieder gesendet werden sollen, wenn die Gruppenmitglieder die gleiche Prioritätsstufe haben. Der Gewichtungs Einstellung muss ein Wert zwischen 1 und 100 zugewiesen werden, und der Wert stellt einen Prozentsatz von 100 Prozent dar. Wenn z. b. die Remote-RADIUS-Server Gruppe zwei Mitglieder mit der Prioritätsstufe 1 und der Gewichtungs Bewertung 50 enthält, leitet der NPS-Proxy 50 Prozent der Verbindungsanforderungen an die einzelnen RADIUS-Server weiter.

- **Erweiterte Einstellungen**. Mit diesen Failovereinstellungen kann NPS ermitteln, ob der Remote-RADIUS-Server nicht verfügbar ist. Wenn der NPS feststellt, dass ein RADIUS-Server nicht verfügbar ist, kann er mit dem Senden von Verbindungsanforderungen an andere Gruppenmitglieder beginnen. Mit diesen Einstellungen können Sie die Anzahl der Sekunden konfigurieren, die der NPS-Proxy auf eine Antwort vom RADIUS-Server wartet, bevor die Anforderung abgewartet wird. die maximale Anzahl von gelöschten Anforderungen, bevor der NPS-Proxy den RADIUS-Server als nicht verfügbar identifiziert. und die Anzahl der Sekunden, die zwischen Anforderungen vergehen kann, bevor der RADIUS-Server vom NPS-Proxy als nicht verfügbar identifiziert wird.

## <a name="configure-nps-proxy-load-balancing"></a>Konfigurieren des NPS-Proxy Lastenausgleichs

Erstellen Sie vor dem Konfigurieren des Lasten Ausgleichs einen Bereitstellungs Plan, der enthält, wie viele RADIUS-Remote Server Gruppen Sie benötigen, welche Server Mitglieder einer bestimmten Gruppe sind und welche Priorität und Gewichtung für die einzelnen Server bestehen.

>[!NOTE]
>Bei den folgenden Schritten wird davon ausgegangen, dass Sie bereits RADIUS-Server bereitgestellt und konfiguriert haben.

Wenn Sie NPS als Proxy Server konfigurieren und Verbindungsanforderungen von RADIUS-Clients an Remote-RADIUS-Server weiterleiten möchten, müssen Sie die folgenden Aktionen ausführen:

1. Stellen Sie Ihre RADIUS \( -Clients-VPN-Server, DFÜ-Server, Terminal Dienste-Gatewayserver, 802.1 x-authentifizier Ende Switches und drahtlose 802.1 x-Zugriffspunkte bereit, \) und konfigurieren Sie Sie für das Senden von Verbindungsanforderungen an Ihre NPS-Proxy Server

2. Konfigurieren Sie auf dem NPS-Proxy die Netzwerk Zugriffs Server als RADIUS-Clients. Weitere Informationen finden Sie unter [Konfigurieren von RADIUS-Clients](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-radius-clients-configure).

3. Erstellen Sie auf dem NPS-Proxy eine oder mehrere RADIUS-Remote Server Gruppen. Fügen Sie während dieses Vorgangs RADIUS-Server zu den RADIUS-Remote Server Gruppen hinzu. Weitere Informationen finden Sie unter [Konfigurieren von Remote-RADIUS-Server Gruppen](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-crp-rrsg-configure).

4. Klicken Sie auf dem NPS-Proxy für jeden RADIUS-Server, den Sie einer RADIUS-Remote Server Gruppe hinzufügen, auf die Registerkarte RADIUS-Server- **Lastenausgleich** , und konfigurieren Sie dann die Einstellungen für **Priorität**, **Gewichtung**und **erweitert**.

5. Konfigurieren Sie auf dem NPS-Proxy Verbindungs Anforderungs Richtlinien, um Authentifizierungs-und Buchhaltungs Anforderungen an Remote-RADIUS-Server Gruppen weiterzuleiten. Sie müssen eine Verbindungs Anforderungs Richtlinie pro RADIUS-Remote Server Gruppe erstellen. Weitere Informationen finden Sie unter [Konfigurieren von Verbindungs Anforderungs Richtlinien](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-crp-configure).


