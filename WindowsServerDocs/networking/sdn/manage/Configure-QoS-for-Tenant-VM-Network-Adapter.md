---
title: Konfigurieren von Quality of Service (QoS) für einen Mandanten-VM-Netzwerkadapter
description: Wenn Sie QoS für einen Mandanten-VM-Netzwerkadapter konfigurieren, haben Sie die Wahl zwischen Data Center Bridging \( DCB \) oder Software Defined Networking \( Sdn \) QoS.
manager: grcusanz
ms.topic: article
ms.assetid: 6d783ff6-7dd5-496c-9ed9-5c36612c6859
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/23/2018
ms.openlocfilehash: 95307dafd077f1efc3b44131494ced709334a2d8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962226"
---
# <a name="configure-quality-of-service-qos-for-a-tenant-vm-network-adapter"></a>Konfigurieren von Quality of Service (QoS) für einen Mandanten-VM-Netzwerkadapter

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Wenn Sie QoS für einen Mandanten-VM-Netzwerkadapter konfigurieren, haben Sie die Wahl zwischen Data Center Bridging \( DCB \) oder Software Defined Networking \( Sdn \) QoS.

1.    **DCB**. Sie können DCB mithilfe der Windows PowerShell-NetQoS-Cmdlets konfigurieren. Ein Beispiel finden Sie im Abschnitt "Aktivieren von Data Center Bridging" im Thema [Remote Direct Memory Access (RDMA) und Switch Embedded Teaming (Set)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).

2.    **Sdn-QoS**. Sie können Sdn-QoS mithilfe des Netzwerk Controllers aktivieren, der so festgelegt werden kann, dass die Bandbreite auf einer virtuellen Schnittstelle eingeschränkt wird, um zu verhindern, dass eine VM mit hohem Datenverkehr andere Benutzer blockiert  Sie können Sdn-QoS auch so konfigurieren, dass eine bestimmte Menge an Bandbreite für einen virtuellen Computer reserviert wird, um sicherzustellen, dass der virtuelle Computer unabhängig von der Menge des Netzwerk Datenverkehrs zugänglich ist.

Wenden Sie alle Sdn-QoS-Einstellungen über die Port Einstellungen der Eigenschaften der Netzwerkschnittstelle an. Weitere Informationen finden Sie in der folgenden Tabelle.

|Elementname|BESCHREIBUNG|
|------------|-----------|
|macspoofing| Ermöglicht es virtuellen Computern, die Quell Media Access Control \( Mac- \) Adresse in ausgehenden Paketen in eine Mac-Adresse zu ändern, die nicht der VM zugewiesen ist.<p>Zulässige Werte:<ul><li>Aktiviert – verwenden Sie eine andere Mac-Adresse.</li><li>Deaktiviert – verwenden Sie nur die zugeordnete Mac-Adresse.</li></ul>|
|arpguard| Ermöglicht, dass nur die in arpfilter angegebenen Adressen von ARP Guard den Port passieren.<p>Zulässige Werte:<ul><li>Aktiviert-zulässig</li><li>Deaktiviert – nicht zulässig</li></ul>|
|dhcpGuard| Ermöglicht oder löscht DHCP-Nachrichten von einem virtuellen Computer, der als DHCP-Server verwendet wird. <p>Zulässige Werte:<ul><li>Aktiviert – löscht DHCP-Nachrichten, da der virtualisierte DHCP-Server als nicht vertrauenswürdig eingestuft wird.</li><li>Deaktiviert – ermöglicht das Empfangen der Nachricht, da der virtualisierte DHCP-Server als vertrauenswürdig eingestuft wird.</li></ul>|
|stormlimit| Die Anzahl der Pakete (Broadcast, Multicast und Unbekanntes Unicast) pro Sekunde, die ein virtueller Computer über den virtuellen Netzwerkadapter senden darf. Pakete außerhalb des Limits während dieses Intervalls werden gelöscht. Der Wert 0 (null) bedeutet, dass \( \) es keine Beschränkung gibt.|
|portflowlimit| Die maximale Anzahl von Flows, die für den Port ausgeführt werden dürfen. Der Wert "blank" oder " \( 0 0" bedeutet, dass \) es keine Beschränkung gibt. |
|vmqweight| Die relative Gewichtung beschreibt die Affinität des virtuellen Netzwerkadapters für die Verwendung der Warteschlange für virtuelle Maschinen (Virtual Machine Queue, VMQ). Der Wertebereich ist 0 bis 100.<p>Zulässige Werte:<ul><li>0 – deaktiviert VMQ auf dem virtuellen Netzwerkadapter.</li><li>1-100 – aktiviert VMQ auf dem virtuellen Netzwerkadapter.</li></ul>|
|iovweight| Die relative Gewichtung legt die Affinität des virtuellen Netzwerkadapters auf die zugewiesene \( virtuelle SR-IOV-Funktion mit Einzel Stamm-e/a-Virtualisierung fest \) . <p>Zulässige Werte:<ul><li>0 – deaktiviert SR-IOV auf dem virtuellen Netzwerkadapter.</li><li>1-100 – aktiviert SR-IOV auf dem virtuellen Netzwerkadapter.</li></ul>|
|iovinterruptmode|<p>Zulässige Werte:<ul><li>Standard – die Einstellung des Anbieters des physischen Netzwerkadapters bestimmt den Wert.</li><li>anpasst </li><li>aus </li><li>niedrig</li><li>mittel</li><li>high</li></ul><p>Wenn Sie **Standard**auswählen, wird der Wert durch die Einstellung des Anbieters des physischen Netzwerkadapters bestimmt.  Wenn Sie **Adaptive**auswählen, bestimmt das Laufzeitdaten Verkehrsmuster die Unterbrechungs Moderations Rate.|
|iovqueuepairrsangefordert| Die Anzahl der der virtuellen SR-IOV-Funktion zugeordneten Hardware Warteschlangen Paare. Wenn RSS für die Empfangs seitige Skalierung \( \) erforderlich ist und der physische Netzwerkadapter, der an den virtuellen Switch gebunden ist, RSS auf virtuellen SR-IOV-Funktionen unterstützt, ist mehr als ein Warteschlangen paar erforderlich. <p>Zulässige Werte: 1 bis 4294967295.|
|Qossettings| Konfigurieren Sie die folgenden QoS-Einstellungen, die alle optional sind: <ul><li>**outboundreservedvalue** : Wenn outboundreservedmode "absolute" ist, gibt der Wert die Bandbreite in Mbit/s an, die dem virtuellen Port für die Übertragung (Ausgang) garantiert wird. Wenn outboundreservedmode "Weight" ist, gibt der Wert den gewichteten Teil der garantierten Bandbreite an.</li><li>**outboundmaximummbit** /s: gibt die maximal zulässige Sende Seiten Bandbreite in Mbit/s für den virtuellen Port (Ausgang) an.</li><li>**Inboundmaximummbit** /s: gibt die maximal zulässige Empfangs seitige Bandbreite für den virtuellen Port (Input) in Mbit/s an.</li></ul> |

---