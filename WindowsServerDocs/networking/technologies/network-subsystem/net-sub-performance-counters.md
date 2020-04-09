---
title: Netzwerkbezogene Leistungsindikatoren
description: Dieses Thema ist Teil des Handbuch zur Leistungsoptimierung des Netzwerk Subsystems für Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 7ebaa271-2557-4c24-a679-c3d863e6bf9e
manager: dcscontentpm
ms.author: v-tea
author: Teresa-Motiv
ms.openlocfilehash: e3350d476b9bfe8ef38cab610a225dcffe0bd02a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862193"
---
# <a name="network-related-performance-counters"></a>Netzwerkbezogene Leistungsindikatoren

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema werden die Leistungsindikatoren aufgelistet, die für die Verwaltung der Netzwerkleistung relevant sind, und die folgenden Abschnitte sind enthalten.  
  
-   [Ressourcenverwendung](#bkmk_ru)  
  
-   [Potenzielle Netzwerkprobleme](#bkmk_np)  
  
-   [Empfangs seitige zusammen Fügung (Receive Side Coalescing, RSC)](#bkmk_rsc)  
  
##  <a name="resource-utilization"></a><a name="bkmk_ru"></a>Ressourcenverwendung  

Die folgenden Leistungsindikatoren sind für die Verwendung von Netzwerkressourcen relevant.  
  
- IPv4, IPv6  
  
  -   Empfangene Datagramme/Sek.  
  
  -   Gesendete Datagramme/Sek.  
  
- TCPv4, TCPv6  
  
  -   Empfangene Segmente/Sek.  
  
  -   Gesendete Segmente/Sek.  
  
  -   Erneut übertragene Segmente/Sek.  
  
- Netzwerkschnittstelle (*), Netzwerk Adapter (\*)  
  
  - Empfangene Bytes/Sekunde  
  
  - Gesendete Bytes/Sek.  
  
  - Empfangene Pakete/Sek.  
  
  - Gesendete Pakete/Sek.  
  
  - Ausgabewarteschlangenlänge  
  
    Dabei handelt es sich um die Länge der Ausgabe Paket Warteschlange \(in den Paketen\). Wenn dieser Wert länger als 2 ist, treten Verzögerungen auf. Sie sollten den Engpass ermitteln und ihn ggf. entfernen. Da NDIS die Anforderungen in die Warteschlange eingereiht, sollte diese Länge immer 0 sein.  
  
- Prozessor Informationen  
  
  - Prozessorzeit (%)  
  
  - Interrupts/Sek.  
  
  - DPCs in Warteschlange/Sekunde  
  
    Dieser Wert ist eine durchschnittliche Rate, mit der DPCs der DPC-Warteschlange des logischen Prozessors hinzugefügt wurden. Jeder logische Prozessor verfügt über eine eigene DPC-Warteschlange. Dieser Wert misst die Rate, mit der DPCs der Warteschlange hinzugefügt werden, nicht die Anzahl der DPCs in der Warteschlange. Es zeigt den Unterschied zwischen den Werten, die in den letzten beiden Beispielen beobachtet wurden, dividiert durch die Dauer des Stichproben Intervalls an.  
  
##  <a name="potential-network-problems"></a><a name="bkmk_np"></a>Potenzielle Netzwerkprobleme  

Die folgenden Leistungsindikatoren sind für potenzielle Netzwerkprobleme relevant.  
  
-   Netzwerkschnittstelle (*), Netzwerk Adapter (\*)  
  
    -   Empfangene Pakete verworfen  
  
    -   Fehler beim Empfangen von Paketen  
  
    -   Ausgehende ausgehende Pakete  
  
    -   Ausgehende Pakete mit Fehlern  
  
-   WFPv4, WFPv6  
  
    -   Verworfene Pakete/Sek.

-   UDPv4, UDPv6

    -   Empfangene Datagramme-Fehler  
  
-   TCPv4, TCPv6  
  
    -   Verbindungsfehler  
  
    -   Zurückgesetzte Verbindungen  
  
-   Netzwerk-QoS-Richtlinie  
  
    -   Gelöschte Pakete  
  
    -   Verworfene Pakete/Sek.  
  
-   Netzwerkschnittstellenkarten-Aktivität pro Prozessor  
  
    -   Geringe Ressourcen Empfangs Hinweise/Sek.  
  
    -   Wenig empfangene Ressourcen empfangene Pakete/Sek.  
  
-   Microsoft Winsock BSP  
  
    -   Gelöschte Datagramme  
  
    -   Gelöschte Datagramme/Sek.  
  
    -   Zurückgewiesene Verbindungen  
  
    -   Abgelehnte Verbindungen/Sek.  
  
##  <a name="receive-side-coalescing-rsc-performance"></a><a name="bkmk_rsc"></a>Empfangs seitige zusammen Fügung (Receive Side Coalescing, RSC)  

Die folgenden Leistungsindikatoren sind für die RSC-Leistung relevant.  
  
-   Netzwerk Adapter (*)  
  
    -   TCP aktiv RSC-Verbindungen  
  
    -   TCP RSC, durchschnittliche Paketgröße  
  
    -   Von TCP RSC zusammengeführte Pakete/Sek.  
  
    -   TCP RSC-Ausnahmen/Sek.

Links zu allen Themen in diesem Handbuch finden Sie unter [Network Subsystem Performance Tuning](net-sub-performance-top.md).