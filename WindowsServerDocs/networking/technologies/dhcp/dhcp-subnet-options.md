---
title: Optionen für das DHCP-subnetzauswahl
description: Dieses Thema enthält Informationen zu DHCP-subnetzauswahloptionen für DHCP (Dynamic Host Configuration Protocol) in Windows Server 2016.
manager: dougkim
ms.topic: get-started-article
ms.assetid: ca19e7d1-e445-48fc-8cf5-e4c45f561607
ms.author: lizross
author: eross-msft
ms.date: 08/17/2018
ms.openlocfilehash: 5b7a680c77ee7a9002f674d4fc0266c50551abcc
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949233"
---
# <a name="dhcp-subnet-selection-options"></a>Optionen für das DHCP-subnetzauswahl

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema finden Sie Informationen zu neuen Optionen für das DHCP-subnetzauswahl.

DHCP unterstützt jetzt die Option 82 \( unter Option 5 \) . Mithilfe dieser Optionen können Sie DHCP-Proxy Clients und Relay-Agents gestatten, eine IP-Adresse für ein bestimmtes Subnetz und einen bestimmten IP-Adressbereich und-Bereich anzufordern.  Weitere Informationen finden Sie unter **Option 82 Sub-Option 5**: [RFC 3527 Link Selection-unter Option für die Option Relay-Agent-Informationen für DHCPv4](https://tools.ietf.org/html/rfc3527).

Wenn Sie einen DHCP-Relay-Agent verwenden, der mit der DHCP-Option 82, unter Option 5 konfiguriert ist, kann der Relay-Agent eine IP-Adress Lease für DHCP-Clients von einem bestimmten IP-Adressbereich anfordern.


## <a name="option-82-sub-option-5-link-selection-sub-option"></a>Option 82 unter Option 5: Link Auswahl-unter Option

Mit der unter Option Link Auswahl für Relay-Agent kann ein DHCP-Relay-Agent ein IP-Subnetz angeben, von dem der DHCP-Server IP-Adressen und-Optionen zuweisen soll.

In der Regel greifen DHCP-Relay-Agents auf das GIADDR-Feld der Gateway-IP-Adresse \( \) zurück, um mit DHCP-Servern Allerdings ist GIADDR durch die beiden Betriebsfunktionen beschränkt:

1. Um den DHCP-Server über das Subnetz zu informieren, in dem sich der DHCP-Client befindet, der die IP-Adress Lease anfordert.
2. So informieren Sie den DHCP-Server über die IP-Adresse, die für die Kommunikation mit dem Relay-Agent verwendet werden soll

In einigen Fällen kann sich die IP-Adresse, die der Relay-Agent für die Kommunikation mit dem DHCP-Server verwendet, von dem IP-Adressbereich unterscheiden, von dem die DHCP-Client-IP-Adresse zugewiesen werden muss.

Die Option Link Selection Sub der Option 82 ist in dieser Situation nützlich, sodass der Relay-Agent den Subnetz, von dem die IP-Adresse zugewiesen werden soll, explizit in Form der DHCP V4-Option 82 Sub Option 5 angeben kann.

> [!NOTE]
>
> Alle IP-Adressen für den Relay-Agent (GIADDR) müssen Teil eines aktiven DHCP-Bereichs-IP-Adress Bereichs sein. Alle GIADDR außerhalb der IP-Adressbereiche des DHCP-Bereichs werden als nicht autorisierte Relay betrachtet, und der Windows-DHCP-Server bestätigt keine DHCP-Client Anforderungen von diesen Relayagents.
>
> Ein spezieller Bereich kann zum Autorisieren von Relay-Agents erstellt werden. Erstellen Sie einen Bereich mit der GIADDR (oder mehreren, wenn es sich bei den GIADDR um sequenzielle IP-Adressen handelt), schließen Sie die GIADDR-Adressen aus der Verteilung aus, und aktivieren Sie dann den Bereich. Dadurch werden die Relay-Agents autorisiert, und es wird verhindert, dass die GIADDR-Adressen zugewiesen werden.


### <a name="use-case-scenario"></a>Anwendungsfall

In diesem Szenario enthält ein Organisations Netzwerk sowohl einen DHCP-Server als auch einen drahtlosen Zugriffspunkt \( \) für die Gastbenutzer. Gast-Client-IP-Adressen werden vom DHCP-Server der Organisation zugewiesen. aufgrund von Einschränkungen der Firewallrichtlinie kann der DHCP-Server jedoch nicht auf das Gast Drahtlos Netzwerk oder auf drahtlose Clients mit broadcase-Nachrichten zugreifen.

Um diese Einschränkung zu beheben, wird der AP mit der Link Auswahl unter Option 5 konfiguriert, um das Subnetz anzugeben, aus dem die IP-Adresse für Gast Clients zugewiesen werden soll, während in der GIADDR auch die IP-Adresse der internen Schnittstelle angegeben ist, die zum Unternehmensnetzwerk führt.
