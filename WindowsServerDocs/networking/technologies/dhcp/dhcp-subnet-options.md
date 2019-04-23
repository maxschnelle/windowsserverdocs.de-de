---
title: Auswahloptionen für DHCP-Subnetz
description: Dieses Thema enthält Informationen zu DHCP-Subnetz-Auswahloptionen für Dynamic Host Configuration Protocol (DHCP) in Windows Server 2016.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: ca19e7d1-e445-48fc-8cf5-e4c45f561607
ms.author: pashort
author: shortpatti
ms.date: 08/17/2018
ms.openlocfilehash: 034ca48ef13a6bdac63ca99ac753fc9826460922
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870811"
---
# <a name="dhcp-subnet-selection-options"></a>Auswahloptionen für DHCP-Subnetz

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema können Informationen zu neuen DHCP-Subnetz-Auswahloptionen.

DHCP nun unterstützt 82 option \(untergeordnete option 5\). Sie können diese Optionen verwenden, um DHCP-Proxy-Clients und -Relay-Agents zum Anfordern einer IP-Adresse für ein bestimmtes Subnetz, und von einer bestimmten IP-Adressbereich und den Bereich zu ermöglichen.  Weitere Informationen finden Sie unter **Option 82 unter Option 5**: [RFC 3527 Link untergeordnete Auswahloption für die Relay-Agent Informationen-Option für DHCPv4](https://tools.ietf.org/html/rfc3527).

Wenn Sie einen DHCP-Relay-Agent verwenden, der mit DHCP-Option 82 konfiguriert ist, untergeordnete option 5 der Relay-Agent kann eine IP-Adresslease für DHCP-Clients aus einem bestimmten Bereich von IP-Adresse anfordern.


## <a name="option-82-sub-option-5-link-selection-sub-option"></a>Option 82 Sub-Option 5: Link-Auswahl-Sub-Option

Die untergeordnete Relay-Agent-Link-Auswahl-Option ermöglicht es sich um einen DHCP-Relay-Agent ein IP-Subnetz angeben, von dem der DHCP-Server IP-Adressen und Optionen zugewiesen werden muss.

In der Regel DHCP-Relay-Agents basieren auf der IP-Adresse des Gateways \(GIADDR\) Feld für die Kommunikation mit DHCP-Server. Es ist jedoch GIADDR von seinen zwei operative Funktionen beschränkt:

1. Den DHCP-Server über das Subnetz informieren auf dem der DHCP-Client, der die IP-Adresslease anfordert befindet.
2. Um den DHCP-Server die IP-Adresse zu verwenden, um die Kommunikation mit dem Relay-Agent zu informieren.

In einigen Fällen die IP-Adresse, die der Relay-Agent für die Kommunikation mit dem DHCP-Server verwendet den IP-Adressbereich unterscheidet möglicherweise von dem die DHCP-Client-IP-Adresse zugeordnet werden muss. 

Der Link Auswahl Sub-Option der 82-Option ist nützlich, in diesem Fall der Relay-Agent explizit anzugeben, dass das Subnetz aus dem die IP-Adresse sollen in Form von DHCP-IPv4-Option 82 Sub-Option 5 zugewiesen.

> [!NOTE]
>
> Relay-Agent alle IP-Adressen (GIADDR) müssen einen aktiven DHCP-Bereich IP-Adressbereich gehören. Alle GIADDR außerhalb der DHCP-Bereich IP-Adressbereiche gilt ein Rogue-Relay und Windows-DHCP-Server wird die DHCP-Clientanforderungen aus diesen Relayagents nicht bestätigt.
>
> Ein spezieller Bereich kann erstellt werden, um Relay-Agents "Autorisieren". Erstellen Sie einen Bereich mit der GIADDR (oder mehrere, wenn die GIADDR des sequenziellen IP-Adressen), Verteilung ausgeschlossen Sie der GIADDR Adressen, und aktivieren Sie den Bereich. Dadurch wird die Relay-Agents autorisiert, und verhindert, dass die Adressen GIADDR zugewiesen wird.


### <a name="use-case-scenario"></a>Anwendungsfall-Beispielszenario

In diesem Szenario enthält Netzwerk einer Organisation sowohl eine DHCP-Server und einen drahtlosen Zugriffspunkt \(AP\) für Gastbenutzer. Gäste-Client-IP-Adressen werden zugewiesen, von der Organisation DHCP-Server – jedoch aufgrund von Beschränkungen der Firewall-Richtlinie, die der DHCP-Server kann nicht der Gast-Drahtlosnetzwerk oder drahtlose Clients mit Broadcase Nachrichten zugreifen.

Um diese Einschränkung zu beheben, wird der Zugriffspunkt mit Link Auswahl unter Option 5 an das Subnetz, aus dem sie die IP-Adresse zugeordnet, die für Gastclients in der GIADDR auch die IP-Adresse der internen Schnittstelle, die zu führt angeben möchte, konfiguriert die Unternehmensnetzwerk.
