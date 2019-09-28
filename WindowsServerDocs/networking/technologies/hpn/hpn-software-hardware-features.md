---
title: Integration von Software und Hardware (SH)-Features und -Technologien
description: Diese Features verfügen sowohl über Software-als auch Hardwarekomponenten. Die Software ist eng an Hardwarefunktionen gebunden, die für die Funktionsfähigkeit des Features erforderlich sind. Beispiele hierfür sind vmmq, VMQ, sende seitige IPv4-Prüfsumme Offload und RSS.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/12/2018
ms.openlocfilehash: f032717b9f4dca65454d8251083b73ff2d57dba7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355322"
---
# <a name="software-and-hardware-sh-integrated-features-and-technologies"></a>Integration von Software und Hardware (SH)-Features und -Technologien

Diese Features verfügen sowohl über Software-als auch Hardwarekomponenten. Die Software ist eng an Hardwarefunktionen gebunden, die für die Funktionsfähigkeit des Features erforderlich sind. Beispiele hierfür sind vmmq, VMQ, sende seitige IPv4-Prüfsumme Offload und RSS.

>[!TIP]
>Die Funktionen sh und Ho sind verfügbar, wenn Sie von der installierten NIC unterstützt werden. Die Funktionsbeschreibungen unten beschreiben, wie Sie festzustellen, ob Ihre NIC das Feature unterstützt.

## <a name="converged-nic"></a>Konvergierte NIC 

Konvergierte NIC ist eine Technologie, die es virtuellen NICs auf dem Hyper-V-Host ermöglicht, RDMA-Dienste zum Hosten von Prozessen verfügbar zu machen. Für Windows Server 2016 sind keine separaten NICs mehr für RDMA erforderlich. Mit dem Feature "konvergierte NIC" können die virtuellen NICs in der Host Partition (vNICs) RDMA für die Host Partition verfügbar machen und die Bandbreite der NICs zwischen RDMA-Datenverkehr und der VM sowie anderen TCP/UDP-Datenverkehr auf eine faire und überschaubare Weise freigeben.

![Konvergierte NIC mit Sdn](../../media/Converged-NIC/conv-nic-sdn.png)

Sie können den konvergierten NIC-Vorgang über VMM oder Windows PowerShell verwalten. Die PowerShell-Cmdlets sind dieselben Cmdlets, die für RDMA verwendet werden (siehe unten).

So verwenden Sie die konvergierte NIC-Funktion:

1.  Stellen Sie sicher, dass der Host für DCB festgelegt ist.

2.  Stellen Sie sicher, dass RDMA auf der NIC aktiviert ist. im Fall eines Set-Teams sind die NICs an den Hyper-V-Switch gebunden. 

3.  Stellen Sie sicher, dass Sie RDMA auf den vNICs aktivieren, die für RDMA im Host festgelegt sind. 

Weitere Informationen zu RDMA und Set finden Sie unter [Remote Direct Memory Access (RDMA) und Switch Embedded Teaming (Set)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming).

## <a name="data-center-bridging-dcb"></a>Data Center Bridging (DCB) 

DCB ist eine Suite aus IEEE-Standards (Institute of Electrical and Electronics Engineers), die konvergierte Fabrics in Rechenzentren ermöglichen. DCB ermöglicht die Verwaltung von Hardware Warteschlangen auf einem Host mit Zusammenarbeit mit dem angrenzenden Switch. Der gesamte Datenverkehr für Speicher, Daten Netzwerke, Cluster übergreifende Kommunikation (Inter-Process Communication, IPC) und Verwaltung nutzen dieselbe Ethernet-Netzwerkinfrastruktur. In Windows Server 2016 kann DCB einzeln auf eine beliebige NIC und auf NICs angewendet werden, die an den Hyper-V-Switch gebunden sind.

Für DCB verwendet Windows Server die Prioritäts basierte Fluss Steuerung (PFC), die in IEEE 802.1 qbb standardisiert ist. PFC erstellt ein (fast) verlustloses netzwerkfabric, indem es einen Überlauf innerhalb von Datenverkehrs Klassen verhindert. Windows Server verwendet auch erweiterte Übertragungs Auswahl (ETS), standardisiert in IEEE 802.1 QAZ. ETS ermöglicht die Division der Bandbreite in reservierte Teile für bis zu acht Klassen von Datenverkehr. Jede Datenverkehrs Klasse verfügt über eine eigene Übertragungs Warteschlange und kann durch die Verwendung von PFC die Übertragung innerhalb einer Klasse starten und Abbrechen.

Weitere Informationen finden Sie unter [Data Center Bridging (DCB)](https://docs.microsoft.com/windows-server/networking/technologies/dcb/dcb-top).

## <a name="hyper-v-network-virtualization"></a>Hyper-V-Netzwerkvirtualisierung

|                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **V1 (HNVv1)**       |                     Hyper-v Network Virtualization (HNV) wurde in Windows Server 2012 eingeführt und ermöglicht die Virtualisierung von Kunden Netzwerken auf einer freigegebenen, physischen Netzwerkinfrastruktur. Bei minimalen Änderungen, die auf dem physischen netzwerkfabric erforderlich sind, bietet HNV Dienstanbietern die Flexibilität, mandantenworkloads überall in den drei Clouds bereitzustellen und zu migrieren: die Dienstanbieter-Cloud, die Private Cloud oder die Microsoft Azure Public Cloud.                     |
| **V2 nvgre (HNVv2 nvgre)** | In Windows Server 2016 und System Center Virtual Machine Manager bietet Microsoft eine End-to-End-Lösung für die Netzwerkvirtualisierung, die RAS-Gateway, Software Lastenausgleich, Netzwerk Controller und vieles mehr umfasst. Weitere Informationen finden Sie [unter Übersicht über die Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016](https://technet.microsoft.com/windows-server-docs/networking/sdn/technologies/hyper-v-network-virtualization/hyperv-network-virtualization-overview-windows-server). |
| **V2 vxlan (HNVv2 vxlan)** |                                                                                                                                                                                        In Windows Server 2016 ist Teil der Sdn-Erweiterung, die Sie über den Netzwerk Controller verwalten.                                                                                                                                                                                        |

---

## <a name="ipsec-task-offload-ipsecto"></a>IPSec-Task Offload (ipsecto) 

IPSec-Task Abladung ist eine NIC-Funktion, mit der das Betriebssystem den Prozessor auf der NIC für die IPSec-Verschlüsselung verwenden kann.

>[!IMPORTANT] 
>Die IPSec-Task Abladung ist eine Legacy Technologie, die von den meisten Netzwerkadaptern nicht unterstützt wird und wo Sie vorhanden ist. Sie ist standardmäßig deaktiviert.

## <a name="private-virtual-local-area-network-pvlan"></a>Privates virtuelles lokales Netzwerk (pvlan). 

Pvlans ermöglichen die Kommunikation nur zwischen virtuellen Maschinen auf demselben Virtualisierungsserver. Ein privates virtuelles Netzwerk ist nicht an einen physischen Netzwerkadapter gebunden. Ein privates virtuelles Netzwerk ist von dem gesamten externen Netzwerk Datenverkehr auf dem Virtualisierungsserver sowie von Netzwerk Datenverkehr zwischen dem Verwaltungs Betriebssystem und dem externen Netzwerk isoliert. Dieser Netzwerktyp ist nützlich, wenn Sie eine isolierten Netzwerkumgebung erstellen müssen, wie z. B. eine isolierte Testdomäne. Die Hyper-V-und Sdn-Stapel unterstützen nur den isolierten pvlan-Port Modus.

Weitere Informationen zur pvlan-Isolation finden [Sie unter System Center: Virtual Machine Manager Engineering-](https://blogs.technet.microsoft.com/scvmm/2013/06/04/logical-networks-part-iv-pvlan-isolation/)Blog.

## <a name="remote-direct-memory-access-rdma"></a>Remotezugriff auf den direkten Speicher (RDMA) 

RDMA ist eine Netzwerktechnologie, die eine Kommunikation mit hohem Durchsatz und geringer Latenz bietet, die die CPU-Auslastung minimiert. RDMA unterstützt Netzwerke mit Nullen, indem der Netzwerkadapter die direkte Übertragung von Daten in den oder aus dem Anwendungs Speicher ermöglicht. RDMA-fähig bedeutet, dass die NIC (physisch oder virtuell) RDMA für einen RDMA-Client verfügbar machen kann. RDMA-aktiviert hingegen bedeutet, dass eine RDMA-fähige NIC die RDMA-Schnittstelle im Stapel nach oben verfügbar macht.

Weitere Informationen zu RDMA finden Sie unter [Remote Direct Memory Access (RDMA) und Switch Embedded Teaming (Set)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming).

## <a name="receive-side-scaling-rss"></a>Receive Side Scaling (RSS) 

RSS ist eine NIC-Funktion, die unterschiedliche Sätze von Streams trennt und Sie zur Verarbeitung an verschiedene Prozessoren übergibt. RSS parallelisiert die Netzwerk Verarbeitung, sodass ein Host auf sehr hohe Datenraten skaliert werden kann. 

Weitere Informationen finden Sie unter [Empfangs seitige Skalierung (Receive Side Scaling, RSS)](https://docs.microsoft.com/windows-hardware/drivers/network/introduction-to-receive-side-scaling).

## <a name="single-root-input-output-virtualization-sr-iov"></a>Single root Input-Output Virtualization (SR-IOV) 

SR-IOV ermöglicht es dem VM-Datenverkehr, direkt von der NIC zum virtuellen Computer zu wechseln, ohne den Hyper-V-Host zu übergeben. SR-iov ist eine unglaubliche Verbesserung der Leistung eines virtuellen Computers, aber es ist nicht möglich, diese Pipe durch den Host zu verwalten. Verwenden Sie nur SR-IOV, wenn die Arbeitsauslastung ordnungsgemäß und vertrauenswürdig ist, und in der Regel die einzige VM auf dem Host.

Datenverkehr, der SR-IOV verwendet, umgeht den Hyper-V-Switch, was bedeutet, dass alle Richtlinien, z. b. ACLs oder die Bandbreiten Verwaltung, nicht angewendet werden. SR-IOV-Datenverkehr kann auch nicht über eine netzwerkvirtualisierungsfunktion durchgeführt werden, daher können NV-GRE oder vxlan-Kapselung nicht angewendet werden. Verwenden Sie SR-IOV nur für gut vertrauenswürdige Workloads in bestimmten Situationen. Darüber hinaus können Sie die Host Richtlinien, die Bandbreiten Verwaltung und die Virtualisierungstechnologien nicht verwenden.

In Zukunft ermöglichen zwei Technologien SR-IOV: Generische Fluss Tabellen (GFT) und Hardware-QoS-Auslagerung (Bandbreiten Verwaltung in der NIC) – Sobald die NICs in unserem Ökosystem diese unterstützen. Durch die Kombination dieser beiden Technologien könnte SR-IOV für alle virtuellen Computer nützlich sein, Richtlinien für die Verwaltung von Richtlinien, Virtualisierung und Bandbreiten Verwaltung ermöglichen und in der allgemeinen Anwendung von SR-IOV hervorragend vorankommen.

Weitere Informationen finden Sie unter [Übersicht über Single root I/O Virtualization (SR-IOV)](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-single-root-i-o-virtualization--sr-iov-).

## <a name="tcp-chimney-offload"></a>TCP-Chimney-Abladung

TCP-Chimney-Abladung, auch als "TCP-Engine-Auslagerung (TOE)" bezeichnet, ist eine Technologie, die es dem Host ermöglicht, die gesamte TCP-Verarbeitung auf die NIC zu übertragen. Da der Windows Server-TCP-Stapel fast immer effizienter ist als die Toe-Engine, wird die Verwendung der TCP-Chimney-Abladung nicht empfohlen.

>[!IMPORTANT]
>Die TCP-Chimney-Abladung ist eine veraltete Technologie. Es wird empfohlen, die TCP-Chimney-Abladung nicht zu verwenden, da Microsoft Sie in Zukunft möglicherweise nicht mehr unterstützt.

## <a name="virtual-local-area-network-vlan"></a>Virtuelles lokales Netzwerk (VLAN) 

VLAN ist eine Erweiterung des Ethernet-Frame-Headers, um die Partitionierung eines LANs in mehrere VLANs zu ermöglichen, die jeweils einen eigenen Adressraum verwenden. In Windows Server 2016 werden VLANs auf Ports des Hyper-V-Switches oder durch Festlegen von Team Schnittstellen auf NIC-Team Vorgangs Teams festgelegt. Weitere Informationen finden Sie unter [NIC-Team Vorgang und virtuelle lokale Netzwerke (Virtual Local Area Networks, VLANs)](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nict-and-vlans).

## <a name="virtual-machine-queue-vmq"></a>Warteschlange für virtuelle Computer (Virtual Machine Queue, VMQ) 

Vmqs ist eine NIC-Funktion, die eine Warteschlange für jeden virtuellen Computer bereitstellt. Wenn Sie Hyper-V aktiviert haben, Sie müssen auch VMQ aktivieren. In Windows Server 2016 verwendet vmqs NIC-Switch-VPORTS mit einer einzelnen Warteschlange, die dem VPort zugewiesen ist, um die gleiche Funktionalität bereitzustellen. Weitere Informationen finden Sie unter [virtuelle Empfangs seitige Skalierung (vrss)](https://docs.microsoft.com/windows-server/networking/technologies/vrss/vrss-top) und [NIC](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)-Team Vorgang.

## <a name="virtual-machine-multi-queue-vmmq"></a>Virtual Machine multiqueue (vmmq) 

Vmmq ist eine NIC-Funktion, mit der Datenverkehr für eine VM auf mehrere Warteschlangen verteilt werden kann, die jeweils von einem anderen physischen Prozessor verarbeitet werden. Der Datenverkehr wird dann an mehrere LPs auf dem virtuellen Computer weitergeleitet, wie er in vrss wäre, was die Bereitstellung einer beträchtlichen Netzwerkbandbreite für den virtuellen Computer ermöglicht.

---