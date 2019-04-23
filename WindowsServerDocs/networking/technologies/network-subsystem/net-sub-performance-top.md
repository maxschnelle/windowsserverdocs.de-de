---
title: Leistungsoptimierung für das Netzwerksubsystem
description: Dieses Thema ist Teil des Leitfadens Netzwerk-Subsystem zur Leistungsoptimierung für Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 45217fce-bfb9-47e8-9814-88ffdb3c7b7d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c0706c6ddbb678eacd3e609cfad3ccdda943fbd3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857411"
---
# <a name="network-subsystem-performance-tuning"></a>Leistungsoptimierung für das Netzwerksubsystem

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema können eine Übersicht über das Netzwerksubsystem sowie Links zu anderen Themen in diesem Handbuch.

>[!NOTE]
>Zusätzlich zu diesem Thema geben die folgenden Abschnitten dieses Handbuchs Leistung optimierungsempfehlungen für Netzwerkgeräte und der Netzwerkstapel.
> - [Wählen einen Netzwerkadapter](net-sub-choose-nic.md)
> - [Die Reihenfolge der Netzwerkschnittstellen konfigurieren](net-sub-interface-metric.md)
> - [Leistungsoptimierung für Netzwerkadapter](net-sub-performance-tuning-nics.md)
> - [Netzwerk-bezogene Leistungsindikatoren](net-sub-performance-counters.md)
> - [Leistungstools für Network-Workloads](net-sub-performance-tools.md)

Das Netzwerksubsystem, insbesondere für netzwerkintensive Workloads, die Optimierung der Leistung kann jede Ebene der Netzwerkarchitektur, umfassen, die auch den Netzwerkstapel aufgerufen wird. Diese Ebenen sind grob in die folgenden Abschnitte unterteilt.

1. **Die Netzwerkschnittstelle**. Dies ist die niedrigste Ebene im Netzwerkstapel und den Netzwerktreiber, mit der kommuniziert direkt mit dem Netzwerkadapter enthält.

2. **Network Driver Interface Specification (NDIS)**. NDIS macht Schnittstellen für den Treiber, darunter und für die Ebenen darüber, wie z. B. den Protokollstapel verfügbar.
  
3. **Stack-Protokoll**. Der Protokollstapel implementiert Protokolle wie TCP/IP und UDP/IP-Adresse. Diese Ebenen verfügbar machen, die Transport-Layer-Schnittstelle für den Ebenen oberhalb von ihnen.
  
4. **Systemtreiber**. Dies sind in der Regel die Clients, die einen Transport-datenerweiterung (TDX) oder eine Schnittstelle Winsock Kernel (WSK) verwenden, um die Schnittstellen für Anwendungen im Benutzermodus verfügbar zu machen. Die WSK-Schnittstelle wurde in Windows Server 2008 und Windows eingeführt&reg; Vista, und es wird von AFD.sys verfügbar gemacht werden. Die Schnittstelle verbessert die Leistung durch Eliminierung der Wechsel zwischen Benutzer und Kernelmodus.
  
5. **Anwendungen im Benutzermodus**. Hierbei handelt es sich in der Regel um Lösungen von Microsoft oder benutzerdefinierte Anwendungen.

Die folgende Tabelle enthält eine vertikale Abbildung die Ebenen des Netzwerkstapels, einschließlich Beispiele für Elemente, die in jeder Ebene ausgeführt.  

![Stack Vermittlungsschichten](../../media/Network-Subsystem/network-layers.jpg)

