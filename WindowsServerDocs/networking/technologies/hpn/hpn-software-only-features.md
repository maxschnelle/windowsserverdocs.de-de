---
title: Nur Software (SO)-Features und -Technologien
description: Diese Funktionen werden als Teil des Betriebssystems implementiert und sind unabhängig von den zugrunde liegenden NIC (s). Manchmal erfordern diese Features eine Optimierung der NIC für optimalen Betrieb. Beispiele hierfür sind Hyper-v-Features wie Virtual Machine Quality of Service (vmqos), Access Control Listen (ACLs) und nicht-Hyper-v-Features wie NIC-Team Vorgänge.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/20/2018
ms.openlocfilehash: 27fbbcc5eedb1bc8ee37a85356542335c2eac77a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871930"
---
# <a name="software-only-so-features-and-technologies"></a>Nur Software (SO)-Features und -Technologien
Reine Software Funktionen werden als Teil des Betriebssystems implementiert und sind unabhängig von den zugrunde liegenden NIC (s). Manchmal erfordern diese Features eine Optimierung der NIC für optimalen Betrieb. Beispiele hierfür sind Hyper-v-Features wie Virtual Machine Quality of Service (vmqos), Access Control Listen (ACLs) und nicht-Hyper-v-Features wie NIC-Team Vorgänge.

## <a name="access-control-lists-acls"></a>Access Control Listen (ACLs)

Eine Hyper-V-und SDNv1-Funktion zum Verwalten der Sicherheit für eine VM. Diese Funktion gilt für den nicht virtualisierten Hyper-V-Stapel und den HVNv1-Stapel. Sie können Hyper-V-Switch-ACLs über die PowerShell-Cmdlets " [Add-vmnetworkadapteracl](https://docs.microsoft.com/powershell/module/hyper-v/add-vmnetworkadapteracl?view=win10-ps) " und " [Remove-vmnetworkadapteracl](https://docs.microsoft.com/powershell/module/hyper-v/remove-vmnetworkadapteracl?view=win10-ps) " verwalten.

## <a name="extended-acls"></a>Erweiterte ACLs

Erweiterte ACLs für den virtuellen Hyper-v-Switch ermöglicht Ihnen die Konfiguration der erweiterten Port-ACLs für den virtuellen Hyper-v-Switch, um Firewallschutz bereitzustellen und Sicherheitsrichtlinien für die Mandanten-VMs in Rechenzentren zu erzwingen. Da die Port-ACLs anstelle der virtuellen Computer auf dem virtuellen Hyper-V-Switch konfiguriert sind, kann der Administrator Sicherheitsrichtlinien für alle Mandanten in einer mehr Instanzen fähigen Umgebung verwalten.

Mit den PowerShell-Cmdlets " [Add-vmnetworkadapterextendedacl](https://docs.microsoft.com/powershell/module/hyper-v/add-vmnetworkadapterextendedacl?view=win10-ps) " und " [Remove-vmnetworkadapterextendedacl](https://docs.microsoft.com/powershell/module/hyper-v/remove-vmnetworkadapteracl?view=win10-ps) " können Sie erweiterte ACLs für Hyper-V-Switches verwalten.

>[!TIP] 
>Diese Funktion gilt für den HNVv1-Stapel. Weitere Informationen zu ACLs im SDN-Stapel finden Sie unten in den Sdn-ACLs (Software Defined Networking).

Weitere Informationen zu erweiterten Port Access Control Listen in dieser Bibliothek finden Sie unter [Erstellen von Sicherheitsrichtlinien mit erweiterten Port Access Control Listen](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/Create-Security-Policies-with-Extended-Port-Access-Control-Lists).

## <a name="nic-teaming"></a>NIC-Teamvorgang

Beim NIC-Team Vorgang, auch als NIC-Bindung bezeichnet, handelt es sich um die Aggregation mehrerer NIC-Ports in eine Entität, die der Host als einzelner NIC-Port wahrnimmt. Der NIC-Team Vorgang schützt vor dem Ausfall eines einzelnen NIC-Ports (oder des verbundenen Kabels). Außerdem wird der Netzwerk Datenverkehr für einen schnelleren Durchsatz aggregiert. Weitere Informationen finden Sie unter [NIC](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)-Team Vorgang.

Mit Windows Server 2016 haben Sie zwei Möglichkeiten, Team Vorgänge durchzuführen:

1.  Windows Server 2012-Team Vorgangs Lösung

2.  Windows Server 2016 Switch Embedded Teaming (Set)


## <a name="rsc-in-the-vswitch"></a>RSC im Vswitch

Receive Segment Coalescing (RSC) im Vswitch ist ein Feature, das Pakete annimmt, die Teil desselben Streams sind und zwischen Netzwerk Interrupts eingehen, und Sie in ein einzelnes Paket zusammenfasst, bevor Sie an das Betriebssystem über gestellt werden. Der virtuelle Switch in Windows Server 2019 verfügt über diese Funktion. Weitere Informationen zu dieser Funktion finden Sie unter [Receive Segment Coalescing in the Vswitch](https://docs.microsoft.com/windows-server/networking/technologies/hpn/rsc-in-the-vswitch).

## <a name="software-defined-networking-sdn-acls"></a>SDN-ACLs (Software Defined Networking)

Die Sdn-Erweiterung in Windows Server 2016 verbesserte Möglichkeiten zur Unterstützung von ACLs. Im Windows Server 2016 Sdn v2-Stapel werden Sdn-ACLs anstelle von ACLs und erweiterten ACLs verwendet. Sie können den Netzwerk Controller zum Verwalten von Sdn-ACLs verwenden. 

## <a name="sdn-quality-of-service-qos"></a>SDN-Dienstqualität

Die Sdn-Erweiterung in Windows Server 2016 verbesserte Möglichkeiten zur Bereitstellung von Bandbreitenkontrolle (ausgehender Reservierungen, Ausgangs Grenzen und Eingangs Limits) auf fünf Tupel. Diese Richtlinien werden in der Regel auf der vNIC-oder der Vmnic-Ebene angewendet, Sie können Sie jedoch viel spezifischer machen. Im Windows Server 2016 Sdn v2-Stapel wird Sdn-QoS anstelle von vmqos verwendet. Sie können den Netzwerk Controller zum Verwalten von Sdn-QoS verwenden.

## <a name="switch-embedded-teaming-set"></a>Eingebetteten Teaming wechseln (Set)

Set ist eine Alternative NIC-Team Vorgangs Lösung, die Sie in Umgebungen verwenden können, die Hyper-V und den Sdn-Stapel (Software Defined Networking) in Windows Server 2016 enthalten. Set integriert einige NIC-Team Vorgangs Funktionen in den virtuellen Hyper-V-Switch. Weitere Informationen zu Switch Embedded Teaming in dieser Bibliothek finden Sie unter [Remote Direct Memory Access (RDMA) und Switch Embedded Teaming (Set)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming).

## <a name="virtual-receive-side-scaling-vrss"></a>Virtual Receive Side Scaling (vRSS)

Software vrss dient zum Verteilen des eingehenden Datenverkehrs, der für einen virtuellen Computer über mehrere logische Prozessoren (LPs) der VM bestimmt ist. Software vrss bietet dem virtuellen Computer die Möglichkeit, mehr Netzwerk Datenverkehr zu verarbeiten, als eine einzelne LP verarbeiten kann. Weitere Informationen finden Sie unter [virtuelle Empfangs seitige Skalierung (Virtual Receive Side Scaling, vrss)](https://docs.microsoft.com/windows-server/networking/technologies/vrss/vrss-top).

## <a name="virtual-machine-quality-of-service-vmqos"></a>Virtual Machine Quality of Service (vmqos)

Der virtuelle Computer Quality of Service ist eine Hyper-V-Funktion, die es dem Switch ermöglicht, Grenzwerte für den von jedem virtuellen computergenerierten Datenverkehr festzulegen. Außerdem kann ein virtueller Computer eine Menge an Bandbreite für die externe Netzwerkverbindung reservieren, sodass ein virtueller Computer nicht für die Bandbreite eine andere VM hungern kann. Im Windows Server 2016 Sdn v2-Stapel ersetzt Sdn-QoS vmqos.

vmqos kann Ausgangs Grenzwerte und ausgehende Reservierungen festlegen. Bevor Sie den Hyper-V-Switch erstellen, müssen Sie den ausgehenden Reservierungs Modus (relative Gewichtung oder absolute Bandbreite) bestimmen.

-  Bestimmen Sie den ausgehenden Reservierungs Modus mit dem – minimumbandwidthmode-Parameter des PowerShell-Cmdlets New-VMSwitch.

-  Legen Sie den Wert des Ausgangs Limits mit dem Parameter "– maximumbandwidth" im PowerShell-Cmdlet "Set-vmnetworkadapter" fest.

-  Legen Sie den Wert für die ausgehende Reservierung mit einem der folgenden Parameter des PowerShell-Cmdlets "Set vmnetworkadapter" fest:

   -  Wenn der – minimumbandwidthmode-Parameter des New-VMSwitch-Cmdlets absolut ist, legen Sie den – minimumbandwidthabsolute-Parameter für das Set vmnetworkadapter-Cmdlet fest.

   -  Wenn der – minimumbandwidthmode-Parameter des New-VMSwitch-Cmdlets Weight ist, legen Sie den – minimumbandwidthweight-Parameter für das Set vmnetworkadapter-Cmdlet fest.

Aufgrund der Einschränkungen im Algorithmus, die für dieses Feature verwendet werden, wird empfohlen, dass die höchste Gewichtungs-oder absolute Bandbreite nicht mehr als 20 mal der niedrigsten oder absoluten Bandbreite liegt. Wenn mehr Kontrolle erforderlich ist, sollten Sie die Verwendung des SDN-Stapels und des SDN-QoS-Features in Erwägung gezogen.


---