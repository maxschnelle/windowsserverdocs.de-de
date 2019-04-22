---
title: Nur Software (SO)-Features und -Technologien
description: 'Diese Features werden als Teil des Betriebssystems implementiert und sind unabhängig von der Anzahl der zugrunde liegenden NICs. In einigen Fällen erfordern diese Funktionen eine Optimierung der NIC für eine optimale Vorgang. Beispiele: Hyper-V-Features wie VM Quality of Service (VmQoS), Zugriffssteuerungslisten (ACLs) und nicht-Hyper-V-Features wie die NIC-Teamvorgang.'
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/20/2018
ms.openlocfilehash: 504bc92971e778b468812dc4064fa6f0afff87ad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823781"
---
# <a name="software-only-so-features-and-technologies"></a>Nur Software (SO)-Features und -Technologien
Nur Software-Features werden als Teil des Betriebssystems implementiert und sind unabhängig von der Anzahl der zugrunde liegenden NICs. In einigen Fällen erfordern diese Funktionen eine Optimierung der NIC für eine optimale Vorgang. Beispiele: Hyper-V-Features wie VM Quality of Service (VmQoS), Zugriffssteuerungslisten (ACLs) und nicht-Hyper-V-Features wie die NIC-Teamvorgang.

## <a name="access-control-lists-acls"></a>Zugriffssteuerungslisten (ACLs)

Ein Hyper-V und SDNv1 Feature zum Verwalten der Sicherheit für einen virtuellen Computer. Diese Funktion gilt für die nicht virtualisierte Hyper-V-Speicherstapel und den HVNv1-Stapel. Sie können Hyper-V verwalten wechseln von ACLs durch [Add-VMNetworkAdapterAcl](https://docs.microsoft.com/powershell/module/hyper-v/add-vmnetworkadapteracl?view=win10-ps) und [Remove-VMNetworkAdapterAcl](https://docs.microsoft.com/powershell/module/hyper-v/remove-vmnetworkadapteracl?view=win10-ps) PowerShell-Cmdlets.

## <a name="extended-acls"></a>Erweiterte ACLs

Hyper-V-Switches, die erweiterte ACLs können Sie Hyper-V Virtual Switch erweiterte Port-ACLs zum Firewallschutz und Durchsetzung von Sicherheitsrichtlinien für die Mandanten-VMs in Rechenzentren konfigurieren. Da die Port-ACLs konfiguriert sind, auf dem virtuellen Hyper-V-Switch und nicht auf den virtuellen Computern, kann der Administrator Sicherheitsrichtlinien für alle Mandanten in einer mehrinstanzenfähigen Umgebung verwalten.

Sie können erweiterte ACLs über Hyper-V-Switch verwalten die [Add-VMNetworkAdapterExtendedAcl](https://docs.microsoft.com/powershell/module/hyper-v/add-vmnetworkadapterextendedacl?view=win10-ps) und [Remove-VMNetworkAdapterExtendedAcl](https://docs.microsoft.com/powershell/module/hyper-v/remove-vmnetworkadapteracl?view=win10-ps) PowerShell-Cmdlets.

>[!TIP] 
>Diese Funktion gilt für den Stapel HNVv1. Die ACLs im SDN-Stapel, finden Sie in SDN Software Defined Networking) ACLs unten.

Weitere Informationen zu erweiterten Port Access Control Lists in dieser Bibliothek finden Sie unter [Erstellen von Sicherheitsrichtlinien mit erweiterten Port Access Control Lists](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/Create-Security-Policies-with-Extended-Port-Access-Control-Lists).

## <a name="nic-teaming"></a>NIC-Teamvorgang

NIC-Teamvorgang, auch als NIC-Verbindung bezeichnet, ist die Aggregation von mehreren NIC-Ports in einer Entität werden der Host als einen einzigen NIC Anschluss wahrnimmt. NIC-Teamvorgang schützt gegen den Ausfall einer einzelnen NIC-Port (oder das Kabel verbunden). Es werden auch den Netzwerkdatenverkehr für einen schnelleren Durchsatz aggregiert. Weitere Informationen finden Sie unter [NIC-Teamvorgang](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming).

Mit Windows Server 2016 haben Sie zwei Möglichkeiten teaming:

1.  Windows Server 2012-teamvorgangslösung

2.  Windows Server 2016-Switch Embedded Teaming (SET)


## <a name="rsc-in-the-vswitch"></a>RSC in vSwitches

Empfangen von Segment Coalescing (RSC) in der vSwitch ist ein Feature, das dauert-Pakete, die Teil des gleichen Streamen und zwischen Netzwerkinterrupts eingehen, und fügt sie in einem einzelnen Paket vor dem Bereitstellen des Betriebssystems zusammen. Der virtuelle Switch in Windows Server-2019 hat dieses Feature. Weitere Informationen zu diesem Feature finden Sie unter [Empfang zusammengeführter Segmente in der vSwitch](https://docs.microsoft.com/windows-server/networking/technologies/hpn/rsc-in-the-vswitch).

## <a name="software-defined-networking-sdn-acls"></a>Software-Defined Networking (SDN)-ACLs

Die SDN-Erweiterung in Windows Server 2016 verbessert die Möglichkeiten zur Unterstützung von ACLs. In der Windows Server 2016-SDN-v2-Stapel werden die SDN-ACLs anstelle von ACLs und erweiterte ACLs verwendet. Sie können den Netzwerkcontroller verwenden, zum Verwalten von SDN-ACLs. 

## <a name="sdn-quality-of-service-qos"></a>SDN-Quality of Service (QoS)

Die SDN-Erweiterung in Windows Server 2016 verbessert die Möglichkeiten zur Steuerung der Netzwerkbandbreite (ausgehend Reservierungen, ausgangsgrenzwerte und Eingang Grenzwerte) auf einer 5-Tupel-Basis bereitstellen. In der Regel werden diese Richtlinien auf der vNIC oder VmNIC angewendet, jedoch können Sie diese Stellen viel spezifischer. In der Windows Server 2016-SDN-v2-Stapel wird SDN QoS anstelle VmQoS verwendet. Sie können den Netzwerkcontroller verwenden, zum Verwalten von SDN QoS.

## <a name="switch-embedded-teaming-set"></a>Switch Embedded Teaming (SET)

Eine alternative Lösung NIC-Teamvorgang, mit denen Sie in Umgebungen, die Hyper-V und den Stapel Software Defined Networking (SDN) in Windows Server 2016 enthalten ist. SET integriert einige Funktionen mit NIC-Teamvorgang in den virtuellen Hyper-V-Switch. Weitere Informationen zu Switch Embedded Teaming in dieser Bibliothek finden Sie unter [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming).

## <a name="virtual-receive-side-scaling-vrss"></a>Virtual Receive Side Scaling (vRSS)

Software vRSS wird verwendet, um eingehenden Datenverkehr für einen virtuellen Computer auf mehrere logische Prozessoren (LPs) des virtuellen Computers zu verteilen. Software vRSS bietet den virtuelle Computer, die die Möglichkeit, die als eine einzelne LP Weitere Netzwerk-Datenverkehr zu bewältigen, behandeln kann. Weitere Informationen finden Sie unter [virtuelle empfangsseitige Skalierung (vRSS)](https://docs.microsoft.com/windows-server/networking/technologies/vrss/vrss-top).

## <a name="virtual-machine-quality-of-service-vmqos"></a>VM Quality of Service (VmQoS)

VM-Quality of Service ist ein Hyper-V-Feature, können den Schalter, um Grenzwerte für Datenverkehr, der von jedem virtuellen Computer festzulegen. Darüber hinaus können einen virtuellen Computer auf einen Anteil der Bandbreite für die externe Netzwerkverbindung zu reservieren, damit ein virtueller Computer blockieren, kann nicht einem anderen virtuellen Computer für die Bandbreite. In der Windows Server 2016-SDN-v2-Stapel ersetzt SDN QoS VmQoS.

VmQoS können ausgehenden-Grenzwerte und Reservierungen für ausgehende Daten festlegen. Sie müssen den Ausgang Reservierung-Modus (relative Gewichtung oder absolute Bandbreite) bestimmen, vor dem Erstellen von Hyper-V-Switch.

-  Bestimmen Sie den Ausgang Reservierung-Modus mit den – MinimumBandwidthMode-Parameter des New-VMSwitch-PowerShell-Cmdlets.

-  Legen Sie den Wert von den ausgangsgrenzwert für das mit dem Parameter: "maximumbandwidth", auf das Set-VMNetworkAdapter-PowerShell-Cmdlet.

-  Legen Sie den Wert für die Reservierung für ausgehenden Datenverkehr mit einer der folgenden Parameter des VMNetworkAdapter-festlegen-PowerShell-Cmdlets:

   -  Wenn der – MinimumBandwidthMode-Parameter auf das New-VMSwitch-Cmdlet absolut ist, legen Sie den – "minimumbandwidthabsolute"-Parameter auf das Cmdlet VMNetworkAdapter festgelegt.

   -  Wenn Sie der – MinimumBandwidthMode-Parameter auf das New-VMSwitch-Cmdlet die Gewichtung ist, legen Sie den – MinimumBandwidthWeight-Parameter auf das Cmdlet VMNetworkAdapter festgelegt.

Aufgrund der Einschränkungen in den Algorithmus für dieses Feature verwendet empfehlen wir, dass der höchsten Gewichtung oder absolute Bandbreite nicht mehr als 20-Mal die geringsten Gewichtung oder absolute Bandbreite. Wenn Sie mehr Kontrolle erforderlich ist, erwägen Sie den SDN-Stapel und die SDN-QoS-Feature.


---