---
title: Konfigurieren von Quality of Service (QoS) für einen Mandanten-VM-Netzwerkadapter
description: Wenn Sie QoS für einen Mandanten-VM-Netzwerkadapter konfigurieren, Sie haben die Wahl zwischen Data Center Bridging \(DCB\)oder Software Defined Networking \(SDN\) QoS.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6d783ff6-7dd5-496c-9ed9-5c36612c6859
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 0b9ce318c3d249b23d7560e0b6bb90a83e60d64d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880601"
---
# <a name="configure-quality-of-service-qos-for-a-tenant-vm-network-adapter"></a>Konfigurieren von Quality of Service (QoS) für einen Mandanten-VM-Netzwerkadapter

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Wenn Sie QoS für einen Mandanten-VM-Netzwerkadapter konfigurieren, Sie haben die Wahl zwischen Data Center Bridging \(DCB\)oder Software Defined Networking \(SDN\) QoS.

1.  **DCB**. Sie können mithilfe der Cmdlets für Windows PowerShell NetQoS DCB konfigurieren. Ein Beispiel finden Sie im Abschnitt "Data Center Bridging aktivieren" im Thema [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).

2.  **SDN QoS**. Sie können die SDN QoS ermöglichen, mithilfe von Netzwerkcontroller, der festgelegt werden, um die Bandbreite für eine virtuelle Schnittstelle, um zu verhindern, dass eine VM mit hohem Datenverkehr andere Benutzer zu blockieren.  Sie können auch konfigurieren, dass SDN QoS, um eine bestimmte Menge an Bandbreite für einen virtuellen Computer, um sicherzustellen, dass die virtuellen Computer zugegriffen werden kann, unabhängig von der Menge des Netzwerkverkehrs zu reservieren.  

Alle SDN QoS-Einstellungen über die Porteinstellungen der Netzwerkschnittstelle Eigenschaften anwenden. Finden Sie in der Tabelle unten für weitere Details.

|Elementname|Beschreibung|
|------------|-----------| 
|macSpoofing| Sind die virtuellen Computer so ändern Sie die Source Media-Zugriffssteuerung \(MAC\) Adresse in ausgehenden Paketen auf einem MAC-Adresse, die nicht mit dem virtuellen Computer zugewiesen.<p>Zulässige Werte:<ul><li>Aktiviert – verwenden Sie eine andere MAC-Adresse.</li><li>Deaktiviert – verwenden Sie nur die MAC-Adresse zugewiesen.</li></ul>|
|arpGuard| Ermöglicht die ARP-Guard nur Adressen in ArpFilter für die Übergabe über den Port angegeben.<p>Zulässige Werte:<ul><li>Aktiviert – zulässig</li><li>Deaktiviert – nicht zulässig</li></ul>|
|dhcpGuard| Ermöglicht es, oder löscht DHCP-Nachrichten von einem virtuellen Computer, der vorgibt ein DHCP-Server. <p>Zulässige Werte:<ul><li>Aktiviert – löscht DHCP-Nachrichten, da der virtuelle DHCP-Server als nicht vertrauenswürdig eingestuft wird.</li><li>Deaktiviert – kann die Nachricht empfangen werden, da der virtuelle DHCP-Server als vertrauenswürdig eingestuft wird.</li></ul>|
|stormLimit| Die Anzahl der Pakete (Unicast Broadcast-, Multicast- und unbekannten) pro Sekunde einen virtuellen Computer ist zulässig, über den virtuellen Netzwerkadapter gesendet wird. Pakete, die außerhalb des Grenzwerts während dieses Intervalls von einer Sekunde gelöscht. Der Wert 0 (null) \(0\) bedeutet, es gibt keine Beschränkung...|
|portFlowLimit| Die maximale Anzahl der Datenflüsse, die für den Port ausgeführt werden soll. Ein Wert leer oder NULL \(0\) bedeutet, es gibt keine Beschränkung. |
|vmqWeight| Die relative Gewichtung beschreibt die Affinität des virtuellen Netzwerkadapters Warteschlange für virtuelle Computer (VMQ) verwenden. Der Wertebereich ist 0 bis 100.<p>Zulässige Werte:<ul><li>0 – deaktiviert die VMQ auf dem virtuellen Netzwerkadapter an.</li><li>1 bis 100 – ermöglicht die VMQ auf dem virtuellen Netzwerkadapter.</li></ul>|
|iovWeight| Die relative Gewichtung legt die Affinität des virtuellen Netzwerkadapters auf dem zugewiesenen Single-Root-e/a-Virtualisierung \(SR-IOV\) virtuelle Funktion. <p>Zulässige Werte:<ul><li>0 – SR-IOV auf dem virtuellen Netzwerkadapter deaktiviert.</li><li>1 bis 100 – können SR-IOV auf dem virtuellen Netzwerkadapter.</li></ul>|
|iovInterruptModeration|<p>Zulässige Werte:<ul><li>Standard – Einstellung für den physischen Adapter des Herstellers des Werts bestimmt.</li><li>Adaptive- </li><li>Ortung erlauben </li><li>Niedrig</li><li>mittel</li><li>Hohe</li></ul><p>Auf Wunsch **Standard**, dem physischen Adapter herstellereinstellung des bestimmt den Wert.  Wenn Sie sich entscheiden, **adaptive**, des Musters Rate der interruptüberprüfung des Common Language Runtime-Datenverkehrs bestimmt.|
|iovQueuePairsRequested| Die Anzahl der Hardware-warteschlangenpaaren, die einer virtuellen SR-IOV-Funktion zugeordnet. Wenn empfangsseitige Skalierung \(RSS\) ist erforderlich, und wenn dem physischen Netzwerkadapter, die mit dem virtuellen Switch gebunden unterstützt RSS für virtuelle SR-IOV-Funktionen, und klicken Sie dann mehr als ein warteschlangenpaar erforderlich ist. <p>Zulässige Werte: 1 bis 4294967295.|
|QosSettings| Konfigurieren Sie die folgenden Qos-Einstellungen, die alle optional sind: <ul><li>**OutboundReservedValue** – Wenn OutboundReservedMode "absolut" ist, und klicken Sie dann der Wert der Bandbreite in Mbit/s, auf den virtuellen Port für die Übertragung (ausgehend) garantiert angibt. Ist OutboundReservedMode "Weight" gibt den Wert den gewichteten Teil der Bandbreite garantiert.</li><li>**OutboundMaximumMbps** – gibt an, der maximal zulässige für die sendeseitige Bandbreite in Mbit/s, für den virtuellen Port (ausgehend).</li><li>**InboundMaximumMbps** – gibt an, der maximal zulässige empfangsseitige Bandbreite für den virtuellen Port (Eingang) in Mbit/s.</li></ul> |

---