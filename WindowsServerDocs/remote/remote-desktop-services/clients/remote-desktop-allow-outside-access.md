---
title: Remotedesktop – Gewähren des Zugriffs auf Ihren PC von außerhalb Ihres Netzwerks
description: Informationen zu den Optionen für den Remotezugriff auf Ihren PC von außerhalb des Computernetzwerks
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
author: haley-rowland
manager: dongill
ms.author: elizapo
ms.date: 04/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9cc1b7568006ef9e32132d772702212c5fd78ec4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857423"
---
# <a name="remote-desktop---allow-access-to-your-pc-from-outside-your-pcs-network"></a>Remotedesktop – Gewähren des Zugriffs auf Ihren PC von außerhalb des Computernetzwerks

>Gilt für: Windows 10, Windows Server 2016

Wenn Sie mithilfe eines Remotedesktopclients eine Verbindung mit Ihrem PC herstellen, erstellen Sie eine Peer-zu-Peer-Verbindung. Dies bedeutet, dass Sie direkten Zugriff auf den PC (manchmal als „Host“ bezeichnet) benötigen. Wenn Sie eine Verbindung mit Ihrem PC von außerhalb des Netzwerks herstellen müssen, in dem Ihr PC ausgeführt wird, müssen Sie diesen Zugriff ermöglichen. Dafür stehen Ihnen ein paar Optionen zur Verfügung: Sie können die Portweiterleitung verwenden oder ein virtuelles privates Netzwerk (VPN) einrichten.

## <a name="enable-port-forwarding-on-your-router"></a>Aktivieren der Portweiterleitung auf Ihrem Router

Die Portweiterleitung ordnet den Port der IP-Adresse Ihres Routers (Ihre öffentliche IP-Adresse) einfach dem Port und der IP-Adresse des PCs zu, auf den Sie zugreifen möchten. 

Die jeweiligen Schritte zum Aktivieren der Portweiterleitung hängen vom verwendeten Router ab. Daher müssen Sie online nach den Anweisungen für Ihren Router suchen. Eine allgemeine Erläuterung der Schritte finden Sie im wikiHow-Artikel [How to Set Up Port Forwarding on a Router](https://www.wikihow.com/Set-Up-Port-Forwarding-on-a-Router) (Eine Portweiterleitung einrichten).

Bevor Sie den Port zuordnen, benötigen Sie Folgendes:

- Die interne IP-Adresse des PCs: Wechseln Sie für die Suche zu **Einstellungen > Netzwerk und Internet > Status > Netzwerkeigenschaften anzeigen**. Suchen Sie nach der Netzwerkkonfiguration mit dem Status „Betriebsbereit“, und rufen Sie dann die **IPv4-Adresse** ab.

   ![„Betriebsbereit“ – Netzwerkkonfiguration](../media/rdclient-operational-network.png)

- Ihre öffentliche IP-Adresse (die IP-Adresse des Routers). Es gibt viele Möglichkeiten, diese zu ermitteln. Sie können (in Bing oder Google) nach „Meine IP-Adresse“ suchen oder die [WLAN-Netzwerkeigenschaften](https://binged.it/2Gwob34) (Windows 10) anzeigen.
- Die Nummer des Ports, der zugeordnet wird. In den meisten Fällen ist dies 3389. Das ist der von Remotedesktopverbindungen verwendete Standardport.
- Administratorzugriff auf Ihren Router.  

   >[!WARNING]
   > Sie öffnen Ihren PC für das Internet. Stellen Sie sicher, dass ein sicheres Kennwort für Ihren PC festgelegt ist.

Nachdem Sie den Port zugeordnet haben, können Sie eine Verbindung mit Ihrem Host-PC von außerhalb des lokalen Netzwerks herstellen, indem Sie die Verbindung mit der öffentlichen IP-Adresse Ihres Routers (siehe zweiter Punkt oben) herstellen.

Die IP-Adresse des Routers kann sich ändern – Ihr Internetdienstanbieter (Internet Service Provider, ISP) kann Ihnen jederzeit eine neue IP-Adresse zuweisen. Um dieses Problem zu vermeiden, sollten Sie die Verwendung von dynamischem DNS in Erwägung ziehen. Dadurch können Sie die Verbindung mit dem PC mit einem leicht zu merkenden Domänennamen anstelle der IP-Adresse herstellen. Bei einer Adressänderung aktualisiert der Router den DDNS-Dienst automatisch mit Ihrer neuen IP-Adresse.

Bei den meisten Routern können Sie festlegen, für welche Quell-IP oder welches Quellnetzwerk die Portzuordnung verwendet werden kann. Wenn Sie also wissen, dass Sie nur von Ihrem Arbeitsplatz aus eine Verbindung herstellen, können Sie die IP-Adresse Ihres Arbeitsplatznetzwerks hinzufügen, wodurch Sie es vermeiden, den Port für das gesamte öffentliche Internet zu öffnen. Wenn der Host, den Sie zum Herstellen einer Verbindung nutzen, eine dynamische IP-Adresse verwendet, legen Sie die Quelleinschränkung so fest, dass der Zugriff über den gesamten Bereich dieses bestimmten Internetdienstanbieters zulässig ist.

Sie können auch in Erwägung ziehen, eine [statische IP-Adresse](/windows-hardware/customize/mobile/mcsf/enable-static-ip) auf Ihrem PC einzurichten, damit sich die interne IP-Adresse nicht ändert. Wenn Sie dies tun, dann verweist die Portweiterleitung des Routers immer auf die richtige IP-Adresse.


## <a name="use-a-vpn"></a>Verwenden eines VPNs

Wenn Sie über ein virtuelles privates Netzwerk (VPN) eine Verbindung mit Ihrem lokalen Netzwerk (Local Area Network, LAN) herstellen, müssen Sie Ihren PC nicht für das öffentliche Internet öffnen. Beim Herstellen einer Verbindung mit dem VPN agiert Ihr Remotedesktopclient stattdessen so, als wäre er Teil desselben Netzwerks und könnte auf Ihren PC zugreifen. Es sind zahlreiche VPN-Dienste verfügbar. Sie können den Dienst ermitteln und verwenden, der für Sie am besten geeignet ist.