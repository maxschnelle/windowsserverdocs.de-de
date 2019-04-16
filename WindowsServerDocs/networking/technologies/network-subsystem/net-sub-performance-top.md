---
title: Leistung optimieren
description: Dieses Thema ist Teil der Netzwerk-Subsystem-Leistungsoptimierung Anleitung für Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 45217fce-bfb9-47e8-9814-88ffdb3c7b7d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c7ef50335a6dcc7dc5187cc30ff1b2dc2c5cdfed
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="network-subsystem-performance-tuning"></a>Leistung optimieren

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können eine Übersicht über das Netzwerk-Subsystem und Links zu anderen Themen in diesem Handbuch.

>[!NOTE]
>Geben zusätzlich zu diesem Thema in den folgenden Abschnitten dieses Handbuchs optimierenden leistungsempfehlungen für Netzwerkgeräte und der Netzwerkstapel.
> - [Auswählen einer Netzwerkkarte](net-sub-choose-nic.md)
> - [Konfigurieren Sie die Reihenfolge von Netzwerkschnittstellen](net-sub-interface-metric.md)
> - [Leistung optimieren von Netzwerkadaptern](net-sub-performance-tuning-nics.md)
> - [Netzwerkbezogene Leistungsindikatoren](net-sub-performance-counters.md)
> - [Leistungstools für Netzwerkauslastungen](net-sub-performance-tools.md)

Das Netzwerksubsystem, insbesondere für Netzwerk intensiven Arbeitslasten optimieren der Leistung beinhalten jede Ebene der Netzwerkarchitektur, die auch den Netzwerkstapel aufgerufen wird. Diese Ebenen werden in den folgenden Abschnitten dargestellten unterteilt.

1. **Netzwerkschnittstelle**. Dies ist die unterste Ebene im Netzwerkstapel und enthält den Netzwerkkarten-Treiber, der direkt mit dem Netzwerkadapter kommuniziert.

2. **Network Driver Interface Specification (NDIS)**. NDIS stellt Schnittstellen, die für den Treiber, darunter und für die Ebenen darüber, wie z. B. Protokollstapel bereit.
  
3. **Protokoll Stapel**. Protokollstapel implementiert z. B. TCP/IP und UDP/IP-Protokolle. Diese Ebenen verfügbar machen, die Transport Layer-Schnittstelle für diese Ebenen.
  
4. **Systemtreiber**. Dies sind i. d. r. Clients, die eine Transport-Daten-Erweiterung (TDX) oder Winsock Kernel (WSK)-Schnittstelle verwenden, um Schnittstellen zu Benutzermodus-Apps verfügbar zu machen. Die Schnittstelle WSK wurde in Windows Server 2008 und Windows eingeführt&reg; Vista, und es wird von AFD.sys verfügbar gemacht. Die Schnittstelle verbessert die Leistung durch den Wegfall der Wechsel zwischen Benutzermodus und Kernelmodus.
  
5. **User-Mode Applications**. Dies sind i. d. r. Microsoft Solutions oder benutzerdefinierte Anwendungen.

Die folgende Tabelle enthält eine vertikale Darstellung der Ebenen des Netzwerkstapels, einschließlich der Beispiele für Elemente, die in jeder Ebene ausgeführt.  

![Netzwerk-Stapel Ebenen](../../media/Network-Subsystem/network-layers.jpg)

