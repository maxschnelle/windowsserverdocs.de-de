---
title: Remotedesktop - zulassen des Zugriffs auf Ihren PC von außerhalb Ihres Netzwerks
description: Erfahren Sie mehr über die Optionen für den Remotezugriff auf Ihren PC von außerhalb des PC Netzwerks
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888151"
---
# <a name="remote-desktop---allow-access-to-your-pc-from-outside-your-pcs-network"></a>Remotedesktop - zulassen des Zugriffs auf Ihren PC von außerhalb Ihrer PC Netzwerks

>Gilt für: Windows 10, WindowsServer 2016

Wenn Sie mithilfe eines Remotedesktopclients auf Ihren PC verbinden, erstellen Sie eine Peer-zu-Peer-Verbindung. Dies bedeutet, dass Sie direkten Zugriff auf den PC (manchmal als "Host" bezeichnet). Wenn Sie müssen die Verbindung mit Ihrem PC von außerhalb des Netzwerks, auf dem PC ausgeführt wird, müssen Sie diesen Zugriff zu aktivieren. Sie haben mehrere Optionen zur Verfügung: Verwenden Sie die portweiterleitung oder richten Sie ein VPN.

## <a name="enable-port-forwarding-on-your-router"></a>Portweiterleitung auf dem Router aktivieren

Portweiterleitung ordnet den Port auf dem Router die IP-Adresse (Ihre öffentliche IP-Adresse) einfach den Port und IP-Adresse des Computers, die Sie zugreifen möchten. 

Bestimmte Schritte zum Aktivieren der portweiterleitung hängen von der Router, die, den Sie verwenden, den sodass Sie für die Onlinesuche Ihres Routers Anweisungen müssen. Eine allgemeine Erläuterung der Schritte, sehen Sie sich [WikiHow legen Sie Port die Weiterleitung auf einem Router](https://www.wikihow.com/Set-Up-Port-Forwarding-on-a-Router).

Bevor Sie den Port zuordnen benötigen Sie Folgendes:

- Interne IP-Adresse des PCs: Suchen Sie im **Einstellungen > Netzwerk und Internet > Status > Anzeigen von den Eigenschaften Ihres Netzwerks**. Suchen Sie die Netzwerkkonfiguration mit dem Status "Betriebsbereit", und rufen Sie anschließend die **IPv4-Adresse**.

   ![Operational-Netzwerkkonfiguration](../media/rdclient-operational-network.png)

- Ihre öffentliche IP-Adresse (der Router IP). Es gibt viele Möglichkeiten, diese Angaben finden – Sie können für "Meine IP-Adresse" (in Bing oder Google) suchen oder Anzeigen der [Wi-Fi-Netzwerkeigenschaften](https://binged.it/2Gwob34) (für Windows 10).
- Die Nummer des Ports, die zugeordnet wird. In den meisten Fällen ist dies 3389 - ist der Standardport von Remotedesktopverbindungen verwendet.
- Der Administratorzugriff auf den Router.  

   >[!WARNING]
   > Stellen Sie Ihren PC auf das Internet geöffnet werden: Stellen Sie sicher, dass Sie ein sicheres Kennwort für Ihren PC festgelegt haben.

Nachdem Sie den Port zugeordnet haben, werden Sie Verbindung mit Ihrem Host-PC außerhalb des lokalen Netzwerks, durch das Verbinden mit der öffentlichen IP-Adresse des Routers (die zweite Aufzählungszeichen oben).

Die IP-Adresse des Routers ändern kann – Ihr Internetdienstanbieter (ISP) kann weisen Sie eine neue IP-Adresse zu einem beliebigen Zeitpunkt. Um dieses Problem zu vermeiden sollten Sie mithilfe von dynamischem DNS – so können Sie die Verbindung mit des PCs mit einem leicht zu merken Domänennamen anstelle der IP-Adresse. Der Router aktualisiert automatisch den DDNS-Dienst mit der neuen IP-Adresse geändert werden sollte.

Mit den meisten Router können Sie definieren, welche IP-Quelladresse oder Quellnetzwerk Port-Zuordnung verwenden kann. Also, wenn Sie, dass Sie nur aus dem Arbeitselement eine Verbindung herstellen wollen wissen, können Sie die IP-Adresse für Ihr Arbeitsnetzwerk - hinzufügen, mit der Sie zu vermeiden, öffnen den Port an, das gesamte öffentliche Internet. Wenn der Host, die, den Sie verwenden, um eine Verbindung herstellen, über dynamische IP-Adresse verwendet, legen Sie die Quelle-Einschränkung, um Zugriff auf das gesamte Spektrum, bestimmte Internetdienstanbieter erlauben.

Sie könnten auch erwägen, das Einrichten einer [statische IP-Adresse](/windows-hardware/customize/mobile/mcsf/enable-static-ip) auf Ihrem PC, damit die interne IP-Adresse nicht ändert. Wenn Sie dies, und dann des Routers die tun portweiterleitung verweist immer auf die richtige IP-Adresse.


## <a name="use-a-vpn"></a>Ein VPN verwenden

Wenn Sie über ein virtuelles privates Netzwerk (VPN) auf Ihrem lokalen Netzwerk verbinden, müssen Sie Ihren PC mit dem öffentlichen Internet zu öffnen. Stattdessen fungiert der Remotedesktop-Client, wenn Sie eine Verbindung mit dem VPN herstellen, wie sie Teil des gleichen Netzwerk ist und auf Ihrem PC zugreifen können. Stehen eine Reihe von VPN-Diensten zur Verfügung – Sie finden können, und verwenden, je nachdem, was für Sie am besten geeignet ist.