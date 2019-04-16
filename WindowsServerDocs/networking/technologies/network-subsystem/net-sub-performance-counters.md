---
title: Netzwerkbezogene Leistungsindikatoren
description: Dieses Thema ist Teil der Netzwerk-Subsystem-Leistungsoptimierung Anleitung für Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 7ebaa271-2557-4c24-a679-c3d863e6bf9e
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 33551dfd4f76bc13ba69863b782ddae279e0ad16
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="network-related-performance-counters"></a>Netzwerkbezogene Leistungsindikatoren

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Thema enthält die Leistungsindikatoren, die zum Verwalten der netzwerkleistung relevant sind, und enthält die folgenden Abschnitte.  
  
-   [Ressourcenverwendung](#bkmk_ru)  
  
-   [Potenzielle Netzwerkprobleme](#bkmk_np)  
  
-   [Leistung (Side Coalescing, RSC) erhalten](#bkmk_rsc)  
  
##  <a name="bkmk_ru"></a>Ressourcenverwendung  

Die folgenden Leistungsindikatoren sind für netzwerkressourcenauslastung relevant.  
  
-   IPv4, IPv6  
  
    -   Datagramme empfangen/s  
  
    -   Datagramme gesendet/s  
  
-   TCPv4, TCPv6  
  
    -   Segmente empfangen/s  
  
    -   Segmente gesendet/s  
  
    -   Segmente gesendet/s  
  
-   Netzwerk-Interface(*), Adapter(\*)  
  
    -   Bytes empfangen/s  
  
    -   Bytes gesendet/s  
  
    -   Pakete empfangen/s  
  
    -   Pakete gesendet/s  
  
    -   Ausgabewarteschlangenlänge  
  
     Dieser Leistungsindikator ist die Länge der die Ausgabe Paket Warteschlange \(in packets\). Ist dies mehr als 2, treten Verzögerungen. Sie finden den Engpass, und vermeiden sie wenn möglich. Da NDIS Anfragen Warteschlangen, sollte diese Länge immer 0 sein.  
  
-   Prozessorinformationen  
  
    -   Prozessorzeit (%)  
  
    -   Verarbeiten von Interrupts/s  
  
    -   DPCs in Warteschlange/s  
  
     Dieser Leistungsindikator ist ein die durchschnittliche Rate, mit der DPC-Warteschlange der logische Prozessor DPCs hinzugefügt wurden. Jeder logischer Prozessor verfügt über eine eigene DPC-Warteschlange. Dieser Indikator gibt die Rate, mit der DPCs in die Warteschlange, nicht die Anzahl der DPCs, die sich in der Warteschlange hinzugefügt werden. Zeigt den Unterschied zwischen den Werten, die in den letzten beiden Abtastintervallen dividiert durch die Dauer des Abtastintervalls ermittelt wurden.  
  
##  <a name="bkmk_np"></a>Potenzielle Netzwerkprobleme  

Die folgenden Leistungsindikatoren sind für potenzielle Netzwerkprobleme relevant.  
  
-   Netzwerk-Interface(*), Adapter(\*)  
  
    -   Empfangene Pakete, verworfen  
  
    -   Empfangene Pakete, Fehler  
  
    -   Ausgehende verworfene Pakete  
  
    -   Ausgehende Pakete, Fehler  
  
-   WFPv4 WFPv6  
  
    -   Pakete verworfen/Sek.

-   UDPv4 UDPv6

    -   Datagramme Fehlermeldungen angezeigt werden  
  
-   TCPv4, TCPv6  
  
    -   Verbindungsfehler  
  
    -   Verbindungen zurücksetzen  
  
-   Netzwerk-QoS-Richtlinie  
  
    -   Verworfene Pakete  
  
    -   Verworfene Pakete/Sek.  
  
-   Pro Prozessor Network Interface Card Aktivität  
  
    -   Unzureichender Ressourcen empfangen Angaben/s  
  
    -   Unzureichender Ressourcen empfangene Pakete/s  
  
-   Microsoft Winsock BSP  
  
    -   Gelöschte Datagramme  
  
    -   Gelöschte Datagramme/s  
  
    -   Abgelehnte Verbindungen  
  
    -   Abgelehnte Verbindungen/s  
  
##  <a name="bkmk_rsc"></a>Leistung (Side Coalescing, RSC) erhalten  

Die folgenden Leistungsindikatoren sind relevant RSC die Leistung.  
  
-   Netzwerk-Adapter(*)  
  
    -   TCP-Verbindungen, aktive RSC  
  
    -   Durchschnittliche Paketgröße TCP RSC  
  
    -   TCP-RSC zusammengefügten Pakete/s  
  
    -   TCP-RSC Ausnahmen/Sek.

Links zu allen Themen in diesem Handbuch finden Sie [Optimieren der Leistung mit Subsystem](net-sub-performance-top.md).