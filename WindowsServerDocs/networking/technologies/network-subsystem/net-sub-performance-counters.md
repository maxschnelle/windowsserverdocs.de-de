---
title: Netzwerkbezogene Leistungsindikatoren
description: Dieses Thema ist Teil des Leitfadens Netzwerk-Subsystem zur Leistungsoptimierung für Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 7ebaa271-2557-4c24-a679-c3d863e6bf9e
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e5e8abbc19482bcd0dd5670065cde59d5be3169a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824351"
---
# <a name="network-related-performance-counters"></a>Netzwerkbezogene Leistungsindikatoren

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält die Leistungsindikatoren, die für das Verwalten der Leistung des Netzwerks und enthält die folgenden Abschnitte.  
  
-   [Ressourcenverwendung](#bkmk_ru)  
  
-   [Potenzielle Netzwerkprobleme](#bkmk_np)  
  
-   [Empfangsseitige Zusammenfügung (RSC) Leistung erhalten](#bkmk_rsc)  
  
##  <a name="bkmk_ru"></a> Ressourcenverwendung  

Die folgenden Leistungsindikatoren sind für netzwerkressourcenauslastung relevant.  
  
-   IPv4, IPv6  
  
    -   Empfangene Datagramme/Sek.  
  
    -   Gesendete Datagramme/Sek.  
  
-   TCPv4, TCPv6  
  
    -   Segmente empfangen/s  
  
    -   Segmente gesendet/s  
  
    -   Segmente übertragen/Sekunde  
  
-   Netzwerkschnittstelle(*), Netzwerkadapter (\*)  
  
    -   Empfangene Bytes/Sekunde  
  
    -   Gesendete Bytes/Sek.  
  
    -   Empfangene Pakete/Sek.  
  
    -   Gesendete Pakete/Sek.  
  
    -   Ausgabewarteschlangenlänge  
  
     Dieser Leistungsindikator ist die Länge der Ausgabepaketwarteschlange \(in Paketen\). Wenn dies länger als 2 ist, treten Verzögerungen. Sie finden den Engpass, und vermeiden sie wenn möglich. Da NDIS-Anforderungen Warteschlangen, sollte diese Länge immer 0 sein.  
  
-   Prozessorinformationen  
  
    -   % Processor Time  
  
    -   Interrupts/Sekunde  
  
    -   DPCs in Warteschlange/Sekunde  
  
     Dieser Leistungsindikator ist einer durchschnittlichen Rate, mit der DPCs der logische Prozessor-DPC-Warteschlange hinzugefügt wurden. Jeden logischer Prozessor verfügt über eine eigene DPC-Warteschlange. Dieser Leistungsindikator misst die Rate, mit der DPCs an die Warteschlange für nicht die Anzahl der DPCs in der Warteschlange hinzugefügt werden. Es zeigt den Unterschied zwischen den Werten, die in den letzten zwei Beispielen geteilt durch die Dauer des Messintervalls beobachtet wurden.  
  
##  <a name="bkmk_np"></a> Potenzielle Netzwerkprobleme  

Die folgenden Leistungsindikatoren sind für potenzielle Netzwerkprobleme relevant.  
  
-   Netzwerkschnittstelle(*), Netzwerkadapter (\*)  
  
    -   Verworfene empfangene Pakete  
  
    -   Empfangene Pakete mit Fehlern  
  
    -   Ausgehende verworfene Pakete  
  
    -   Ausgehende Pakete mit Fehlern  
  
-   WFPv4, WFPv6  
  
    -   Verworfene Pakete/Sekunde

-   UDPv4, UDPv6

    -   Empfangene Datagramme Fehler  
  
-   TCPv4, TCPv6  
  
    -   Verbindungsfehler  
  
    -   Zurückgesetzte Verbindungen  
  
-   Netzwerk-QoS-Richtlinie  
  
    -   Pakete verworfen werden  
  
    -   Verworfene Pakete/Sek.  
  
-   Pro Processor Network Interface Card Activity  
  
    -   Unzureichende verfügbare Ressourcen empfangen Anzeichen/Sekunde  
  
    -   Unzureichende verfügbare Ressourcen empfangene Pakete/Sek.  
  
-   Microsoft Winsock BSP  
  
    -   Gelöschten Datagramme  
  
    -   Gelöschten Datagramme/Sekunde  
  
    -   Zurückgewiesene Verbindungen  
  
    -   Abgelehnte Verbindungen/Sek.  
  
##  <a name="bkmk_rsc"></a> Empfangsseitige Zusammenfügung (RSC) Leistung erhalten  

Die folgenden Leistungsindikatoren sind für die RSC-Leistung relevant.  
  
-   Network Adapter(*)  
  
    -   TCP-Verbindungen, aktive RSC  
  
    -   Durchschnittliche TCP-RSC-Paketgröße  
  
    -   TCP-RSC vereinigt Pakete/Sek.  
  
    -   TCP-RSC Ausnahmen/s

Links zu allen Themen in diesem Handbuch finden Sie [Optimieren der Leistung mit Subsystem](net-sub-performance-top.md).