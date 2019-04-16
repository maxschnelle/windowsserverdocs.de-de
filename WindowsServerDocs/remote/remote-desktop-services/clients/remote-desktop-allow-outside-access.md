---
title: Remotedesktop - zulassen des Zugriffs auf Ihrem PC von außerhalb des Netzwerks
description: Erfahren Sie mehr über die Optionen für den Remotezugriff auf Ihrem PC außerhalb der PC-Netzwerk
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: haley-rowland
manager: dongill
ms.author: elizapo
ms.date: 04/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: d77c362d9d06b70ad0747002ed8853a39e05b7ff
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2018
ms.locfileid: "1708658"
---
# <a name="remote-desktop---allow-access-to-your-pc-from-outside-your-pcs-network"></a>Remotedesktop - Zugriff auf Ihre PC außerhalb Ihres Computers Netzwerk zulassen

>Betrifft: Windows 10, WindowsServer 2016

Wenn Sie mithilfe eines Remotedesktop-Clients an den PC verbinden, erstellen Sie eine Peer-zu-Peer-Verbindung. Dies bedeutet, dass Sie benötigen direkten Zugriff auf den PC (manchmal auch als "Host" bezeichnet). Wenn Sie müssen die Verbindung an den PC von außerhalb des Netzwerks, auf der PC ausgeführt wird, müssen Sie, dass der Zugriff zu aktivieren. Sie haben verschiedene Optionen: Verwenden Sie die Weiterleitung von Port, oder richten Sie ein VPN.

## <a name="enable-port-forwarding-on-your-router"></a>Aktivieren Sie die Weiterleitung von Port auf dem router

Port-Weiterleitung ordnet den Port auf dem Router IP-Adresse (Ihre öffentliche IP-Adresse) einfach die Ports und IP-Adresse des PCs, die Sie zugreifen möchten. 

Spezielle Schritte zum Aktivieren der Weiterleitung Port abhängig von den Router, den Sie verwenden, den daher Sie online nach dem Router Anweisungen zu suchen müssen. Checken Sie [WikiHow zum Festlegen von Port weitergeleitet auf einem Router](https://www.wikihow.com/Set-Up-Port-Forwarding-on-a-Router)eine allgemeine Beschreibung der Schritte aus.

Bevor Sie den Port zuordnen benötigen Sie Folgendes:

- PC interne IP-Adresse: Suchen in **Einstellungen > Netzwerk und Internet > Status > Anzeigen Ihrer Netzwerkeigenschaften**. Suchen Sie die Netzwerkkonfiguration mit dem Status "Operationale", und rufen Sie dann die **IPv4-Adresse**.

   ![Betriebliche Netzwerkkonfiguration](../media/rdclient-operational-network.png)

- Ihre öffentliche IP-Adresse (IP-Adresse des Routers). Es gibt viele Methoden zur Suche – für "Meine IP" (in Bing oder Google) suchen oder die [Wi-Fi-Netzwerk-Eigenschaften](https://binged.it/2Gwob34) (für Windows 10) angezeigt werden können.
- Portnummer zugeordnet wird. In den meisten Fällen ist dies 3389 -, die den Standardport von Remotedesktop-Verbindungen verwendet wird.
- Admin-Zugriff auf dem Router.  

   >[!WARNING]
   > Öffnen Sie Ihren PC bis zu dem Internet - stellen Sie sicher, dass Sie ein sicheres Kennwort für Ihren PC festgelegt haben.

Nachdem Sie den Anschluss zuordnen möchten, benötigen Sie Verbindung mit Ihrem Hostcomputer von außerhalb des lokalen Netzwerks Herstellen einer Verbindung mit öffentlichen IP-Adresse Ihres Routers (das zweite Aufzählungszeichen oben) sein.

Die IP-Adresse des Routers ändern kann – vom Internet-Dienstanbieter (ISP) kann weisen Sie eine neue IP-Adresse zu einem beliebigen Zeitpunkt. Ausführung in dieses Problem vermieden erwogen werden dynamische DNS – auf diese Weise können Sie auf den PC mit einem leicht zu merken Domänennamen anstelle der IP-Adresse eine Verbindung herstellen. Der Router aktualisiert automatisch den DDNS-Dienst mit der neuen IP-Adresse ändern sollten.

Mit den meisten Routern können Sie definieren, welche Quell-IP oder Quellnetzwerk Port Zuordnung verwenden kann. Damit, wenn Sie, dass Sie nur von Arbeit eine Verbindung herstellen möchten wissen, können Sie die IP-Adresse für das Netzwerk - hinzufügen können, die Sie vermeiden, öffnen den Port an das gesamte öffentliche Internet. Wenn der Host für die Verbindung verwendeten dynamische IP-Adresse verwendet wird, legen Sie die Einschränkung Quelle Gewährung des Zugriffs aus dem gesamten Bereich eines bestimmten Ihrem Internetdienstanbieter.

Sie sollten eine [statische IP-Adresse](/windows-hardware/customize/mobile/mcsf/enable-static-ip) einrichten auf Ihrem PC, damit die interne IP-Adresse nicht ändert. Wenn Sie dies, und dann des Routers tun Port Weiterleitung wird immer zeigen Sie auf die richtige IP-Adresse.


## <a name="use-a-vpn"></a>Verwenden Sie ein VPN

Wenn Sie über ein virtuelles privates Netzwerk (VPN) mit Ihrem lokalen Netzwerk verbinden, müssen Sie Ihren PC an das öffentliche Internet zu öffnen. Beim Herstellen der Verbindung zu dem VPN agiert Ihres RD-Clients stattdessen wie es Teil der im gleichen Netzwerk ist und werden auf Ihrem PC zugreifen. Eine Anzahl von VPN-Dienste verfügbar sind – Sie suchen und verwenden können, je nachdem, was für Sie am besten geeignet ist.