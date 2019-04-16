---
title: Konfigurieren von Quality of Service (QoS) für einen Mandanten VM-Netzwerkadapter
description: Dieses Thema ist Teil der Software Defined Networking-Anleitung für zum Verwalten von Mandantenworkloads und virtuellen Netzwerken in Windows Server2016.
manager: brianlic
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
ms.openlocfilehash: cde4e21beaec58a98a5d5fbe5c4631e2f113dbf7
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-quality-of-service-qos-for-a-tenant-vm-network-adapter"></a>Konfigurieren von Quality of Service (QoS) für einen Mandanten VM-Netzwerkadapter

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Wenn Sie QoS für einen Mandanten VM-Netzwerkadapter konfigurieren, Sie haben die Wahl zwischen Data Center Bridging \ (DCB\) oder Software Defined Networking \(SDN\) QoS.

1.  **DCB**. Sie können DCB mit den NetQoS von Windows PowerShell-Cmdlets konfigurieren. Ein Beispiel finden Sie im Abschnitt "Aktivieren Data Center Bridging" im Thema [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).

2.  **SDN QoS**. Sie können mithilfe von Netzwerkcontroller, die festgelegt werden können, um Bandbreite auf eine virtuelle Schnittstelle, um zu verhindern, dass eine VM mit hoher Auslastung blockieren andere Benutzer zu beschränken, SDN QoS aktivieren.  Sie können auch konfigurieren, dass SDN QoS reservieren Sie eine bestimmte Menge an Bandbreite für eine virtuelle Maschine, um sicherzustellen, dass die virtuelle Maschine unabhängig von der Menge des Netzwerkverkehrs zugänglich ist.  

Über die Port-Einstellungen der Netzwerkschnittstelle Eigenschaften entsprechend der folgenden Tabelle werden alle SDN-Qos-Einstellungen angewendet.

|Elementname|Beschreibung|
|------------|-----------| 
|macSpoofing|Gibt an, ob virtuelle Computer die Quelle Mac-\(MAC\) Adresse in ausgehenden Paketen in eine MAC-Adresse ändern können, die nicht mit dem virtuellen Computer zugewiesen ist. Zulässige Werte sind "aktiviert" \ (ermöglicht den virtuellen Computer auf einen anderen MAC Address\ verwenden) und "deaktiviert" \ (ermöglicht den virtuellen Computer nur die zugewiesene MAC-Adresse It\ verwenden).|
|arpGuard|Gibt an, ob ARP Guard aktiviert ist.  ARP Guard kann nur Adressen, die in ArpFilter über den Port angegeben werden.  Zulässige Werte sind "aktiviert" oder "deaktiviert".
|dhcpGuard|Gibt an, ob DHCP-Nachrichten von einem virtuellen Computer gelöscht werden, die sich tatsächlich um einen DHCP-Server. Zulässige Werte sind "aktiviert" die DHCP-Nachrichten gelöscht werden, da der virtuelle DHCP-Server gilt als nicht vertrauenswürdig eingestuft wird, oder "deaktiviert", wodurch die Nachricht empfangen werden, da der virtuelle DHCP-Server als vertrauenswürdig eingestuft wird.
|stormLimit|Gibt die Anzahl der Broadcast-, Multicast- und unbekannten Unicastpakete pro Sekunde, die ein virtuellen Computer über den angegebenen virtuellen Netzwerkadapter senden darf. Broadcast-, Multicast- und unbekannte Unicastpakete außerhalb des Grenzwerts während dieses Intervalls von einer Sekunde werden gelöscht. Der Wert 0 (null) \(0\) bedeutet, dass es keine Begrenzung.
|portFlowLimit|Gibt die maximale Anzahl der Flüsse, die für den Port ausgeführt werden können.  Der Wert leer oder NULL \(0\) bedeutet, dass es keine Begrenzung.
|vmqWeight|Gibt an, ob die Warteschlange für virtuelle Computer (VMQ) auf dem virtuellen Netzwerkadapter aktiviert ist. Die relative Gewichtung beschreibt die Affinität des virtuellen Netzwerkadapters zur Verwendung der VMQ. Der Bereich der Wert ist 0 bis 100. Geben Sie 0 an, um VMQ auf dem virtuellen Netzwerkadapter zu deaktivieren.
|iovWeight|Gibt an, ob Single-Root-e/a-Virtualisierung \(SR-IOV\) ist auf diesem virtuellen Netzwerkadapter aktiviert. Die relative Gewichtung legt die Affinität des virtuellen Netzwerkadapters an, die zugewiesenen virtuellen SR-IOV-Funktion. Der Bereich der Wert ist 0 bis 100. Geben Sie 0 an, um SR-IOV auf dem virtuellen Netzwerkadapter zu deaktivieren. 
|iovInterruptModeration|Gibt den Wert der interruptüberprüfung für eine Single-Root-e/a-Virtualisierung \(SR-IOV\) virtuelle Funktion mit einem virtuellen Netzwerkadapter zugewiesen. Zulässige Werte sind "Default", "adaptive", "off", "Niedrig", "Mittel" und "Hoch".   Wenn standardmäßig ausgewählt ist, wird der Wert von physischen Netzwerk Hersteller des Adapters die Einstellung bestimmt.  Wenn Adaptive ausgewählt wird, basiert die Rate der interruptüberprüfung auf dem Laufzeit-Verkehrsmuster. 
|iovQueuePairsRequested|Gibt die Anzahl der Hardware-warteschlangenpaaren an eine virtuelle SR-IOV-Funktion zugeordnet werden soll. Wenn empfangsseitige Skalierung \(RSS\) erforderlich ist und der physischen Netzwerkadapter, der mit dem virtuellen Switch gebunden ist RSS für virtuelle SR-IOV unterstützt Funktionen, mehr als ein warteschlangenpaar erforderlich ist. Zulässige Werte liegen zwischen 1 und 4294967295. 
|QosSettings|Sie können die folgenden Qos-Einstellungen konfigurieren, die optional sind:  <br/><br />**OutboundReservedValue:**<br/>Wenn OutboundReservedMode auf "absolut" festgelegt ist, gibt den Wert der Bandbreite in Mbit/s, mit dem virtuellen Port für die Übertragung (ausgehende) garantiert. Wenn OutboundReservedMode "seid" ist, gibt den Wert den gewichteten Teil der Bandbreite garantiert. <br/><br />**OutboundMaximumMbps:**  <br/>Gibt an, dass die maximal zulässige Sendeseite Bandbreite in Mbit/s, für den virtuellen Port (ausgehende). <br/><br/>**InboundMaximumMbps:**  <br/>Gibt an, dass die maximale empfangsseitige Bandbreite für den virtuellen Port (Ausgang) in Mbit/s zulässig. |