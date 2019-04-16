---
title: DHCP-Subnetz Auswahloptionen
description: Dieses Thema enthält Informationen zu DHCP-Subnetz Auswahloptionen für Dynamic Host Configuration Protocol (DHCP) in Windows Server2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: ca19e7d1-e445-48fc-8cf5-e4c45f561607
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 43bc3d165f895767ded921b41118ecaccf9734e8
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="dhcp-subnet-selection-options"></a>DHCP-Subnetz Auswahloptionen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Informationen zu neuen DHCP-Subnetz Auswahloptionen.

DHCP unterstützt jetzt Optionen 118 und 82 \(sub-option 5\). Diese Optionen können Sie DHCP-Proxy-Clients und -Relay-Agents eine IP-Adresse für ein bestimmtes Subnetz und von einer bestimmten IP-Adressbereich und Bereich anfordern können.

Wenn Sie einen DHCP-Proxy-Client verwenden, der mit DHCP-Option 118, z.B. ein virtuelles privates Netzwerk (VPN)-Server konfiguriert ist, auf denen Windows Server2016 und die RAS-Serverrolle ausgeführt wird, kann der VPN-Server IP-Adressleases für VPN-Clients aus einer bestimmten IP-Adressbereich anfordern.

Wenn Sie einen DHCP-Relay-Agent verwenden, die mit DHCP-Option 82 konfiguriert ist, untergeordneten Option 5 des Relay-Agent kann eine IP-Adresslease für DHCP-Clients aus einer bestimmten IP-Adressbereich anfordern.

Folgende Links Anforderung für Kommentare Themen für diese Optionen werden.

- **Option 118**: [RFC 3011 IPv4-Subnetz Auswahloption für DHCP](http://www.rfc-base.org/rfc-3011.html)
- **Option 82 Sub Option 5**: [RFC 3527 Link Auswahl untergeordnete Option für die Option Relay-Agent für DHCPv4](https://tools.ietf.org/html/rfc3527)


## <a name="dhcp-option-118-client-subnet-and-relay-agent-link-selection"></a>DHCP-Option 118: Subnetz des Clients und -Relay-Agent-Link-Auswahl

Die Option für DHCP-Subnetz Auswahl bietet einen Mechanismus für die DHCP-Proxys ein IP-Subnetz angeben, von dem der DHCP-Server IP-Adressen und Optionen zugewiesen werden muss.

### <a name="use-case-scenario"></a>Verwendungsszenario

In diesem Szenario weist der Server ein virtuelles privates Netzwerk \(VPN\) IP-Adressen zu VPN-Clients. 

In diesem Fall der VPN-Server sowohl Intranet, in dem der DHCP-Server installiert ist, und mit dem Internet verbunden ist, damit VPN-Clients von Remotestandorten aus eine Verbindung mit dem VPN-Server herstellen können.

Bevor der VPN-Server IP-Adressleases für VPN-Clients bereitstellen kann, wird der Server eine Verbindung mit den DHCP-Server in einem internen Subnetz und einen Textblock IP-Adressen reserviert. Der VPN-Server verwaltet dann die IP-Adressen, die sie aus der DHCP-Server abgerufen. Wenn der VPN-Server in Leases reservierte IP-Adressen zu VPN-Clients bereitstellt, erhält der VPN-Server dann zusätzliche IP-Adressen vom DHCP-Server.

Durch die Konfiguration des VPN-Servers mit DHCP-Option 118, können Sie angeben, die IP-Adressbereich und der Umfang, die Sie für die VPN-Clients verwenden möchten. Nachdem Sie die Option 118 konfigurieren, fordert der VPN-Server IP-Adressen von einem bestimmten IP-Adressbereich und Bereich, von dem DHCP-Server.

### <a name="the-dhcp-subnet-selection-option-field"></a>Der DHCP-Subnetz Auswahlfeld Option

Der DHCP-Subnetz Auswahlfeld Option enthält ein einzelnes IPv4-Adresse verwendet, um die ursprünglichen Subnetzadresse für eine DHCP-Lease-Anforderung darzustellen.  Ein DHCP-Server, der konfiguriert ist, zum Reagieren auf diese Option weist die Adresse aus:

1. Das Subnetz, das die Subnetz-Auswahl-Option angegeben ist.
2. Ein Subnetz, die sich in demselben Netzwerksegment wie das Subnetz, der die Subnetz-Auswahl-Option angegeben ist.

## <a name="option-82-sub-option-5-link-selection-sub-option"></a>Option 82 Sub-Option 5: Link Sub Auswahloption

Die Link-Relay-Agent-Auswahl untergeordnete Option ermöglicht einen DHCP-Relay-Agent an ein IP-Subnetz, von dem der DHCP-Server IP-Adressen und Optionen zugewiesen werden muss.

DHCP-Relay-Agents verwenden in der Regel Feld \(GIADDR\) Gateway-IP-Adresse mit DHCP-Server kommunizieren. Allerdings ist GIADDR von zwei betrieblichen Funktionen beschränkt:

1. Den DHCP-Server über das Subnetz informiert auf dem der DHCP-Client, der die IP-Adresslease anfordert befindet.
2. Um den DHCP-Server die IP-Adresse verwenden, um die Kommunikation mit der Relay-Agent zu informieren.

In einigen Fällen die IP-Adresse des Relay-Agents mit dem DHCP-Server die Kommunikation von unterscheidet sich die IP-Adressbereich möglicherweise von dem die DHCP-Client-IP-Adresse zugewiesen werden muss. 

Verwenden der Option 118, wie ihre Funktionalität beschränkt und können nur Schreibvorgänge GIADDR oder die Option des Relay-Agent-Informationen \(Option 82\) nicht DHCP-Relay-Agents möglich. 

Die Option Link Auswahl Sub-Option 82 eignet sich in diesem Fall kann so Relay explizit angeben, dass das Subnetz, von dem sie die IP-Adresse möchte, in Form von DHCP-v4-Option 82 Sub-Option 5 zugeordnet.

### <a name="use-case-scenario"></a>Verwendungsszenario

In diesem Szenario enthält ein Unternehmensnetzwerk einen DHCP-Server und drahtlosen Zugriffspunkt \(AP\) für die Gastbenutzer. "Gäste" IP-Adressen werden von der Organisation DHCP-Server – jedoch aufgrund von Einschränkungen für Firewall-Richtlinie zugewiesen, der DHCP-Server kann nicht zugegriffen werden, die Gast-Drahtlosnetzwerk oder Drahtlosclients mit Broadcase Nachrichten.

Um diese Einschränkung zu beheben, wird der Zugriffspunkt konfiguriert, mit dem Link Auswahl Sub Option 5 an das Subnetz, von dem die IP-Adresse zugeordnet für Gastclients in der GIADDR auch die IP-Adresse der internen Schnittstelle, die mit dem Unternehmensnetzwerk führt angeben sollen.
