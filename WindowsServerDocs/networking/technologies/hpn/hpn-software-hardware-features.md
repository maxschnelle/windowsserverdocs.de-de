---
title: Integration von Software und Hardware (SH)-Features und -Technologien
description: Diese Funktionen haben sowohl Software-und Hardwarekomponenten. Die Software ist auf Hardwarefunktionen, die für das Feature funktioniert erforderlich sind-Desktopplattform gebunden. Beispiele dafür sind VMMQ, VMQ, für die sendeseitige IPv4-Prüfsummenoffload und RSS.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/12/2018
ms.openlocfilehash: 98857a5a6d665728c1aab2a6a2df64997d4166b0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446225"
---
# <a name="software-and-hardware-sh-integrated-features-and-technologies"></a>Integration von Software und Hardware (SH)-Features und -Technologien

Diese Funktionen haben sowohl Software-und Hardwarekomponenten. Die Software ist auf Hardwarefunktionen, die für das Feature funktioniert erforderlich sind-Desktopplattform gebunden. Beispiele dafür sind VMMQ, VMQ, für die sendeseitige IPv4-Prüfsummenoffload und RSS.

>[!TIP]
>SH und HO-Features sind verfügbar, wenn die installierte NIC unterstützt. Die folgenden Beschreibungen von Features werden beschrieben, wie mitteilen, ob die NIC die Funktion unterstützt.

## <a name="converged-nic"></a>Zusammengeführte NIC 

Zusammengeführte NIC ist eine Technologie, die virtuelle Netzwerkkarten auf dem Hyper-V-Host RDMA-Dienste zum Hosten von Prozessen verfügbar machen kann. Windows Server 2016 ist mehr getrennter Netzwerkadapter für RDMA erforderlich. Die zusammengeführte NIC-Funktion können die virtuellen NICs in der Hostpartition (vNICs) verfügbar machen RDMA an die Hostpartition, und die Bandbreite der NICs zwischen der RDMA-Datenverkehr und den virtuellen Computer und anderen TCP/UDP-Datenverkehr in eine ausgeglichene und verwaltbare Weise freigeben.

![Zusammengeführte NIC mit SDN](../../media/Converged-NIC/conv-nic-sdn.png)

Sie können die zusammengeführten NIC-Vorgang über VMM oder Windows PowerShell verwalten. Die PowerShell-Cmdlets sind die gleichen-Cmdlets für RDMA (siehe unten) verwendet.

Um die zusammengeführte NIC-Funktion verwenden zu können:

1.  Achten Sie darauf, den Host für DCB festgelegt.

2.  Achten Sie darauf, aktivieren Sie RDMA auf die NIC, oder bei einem SET-Team, die NICs gebunden werden mit dem Hyper-V-Switch. 

3.  Achten Sie darauf, aktivieren RDMA auf vNICs für RDMA auf dem Host festgelegt. 

Weitere Informationen zu RDMA- und SET, finden Sie unter [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming).

## <a name="data-center-bridging-dcb"></a>Data Center Bridging (DCB) 

DCB ist eine Sammlung von Standards Institute of Electrical and Electronics Engineers (IEEE), die Converged Fabrics im Datencenter zu aktivieren. DCB bietet Hardware warteschlangenbasierte bandbreitenverwaltung auf einem Host mit der Zusammenarbeit der angrenzende Switch. Sämtlicher Datenverkehr für den Speicher, Daten, frei Netzwerke prozessübergreifende Kommunikation (IPC), und die gleiche Ethernet-Netzwerkinfrastruktur. In Windows Server 2016 wird DCB einzeln auf jede beliebige NIC angewendet werden können, und wechseln Sie NICs, die an den Hyper-V gebunden.

Für DCB verwendet Windows Server prioritätsbasierte Flow Control (PCF), im IEEE-802.1Qbb standardisiert. PCF erstellt eine (nahezu) verlustfreie netzwerkfabric Überlauf in Datenverkehrsklassen verhindern. Windows Server verwendet auch die erweiterte Übertragung Auswahl (ETS), im IEEE-802.1Qaz standardisiert. ETS ermöglicht die Aufteilung der Bandbreite in reservierten Teile für bis zu acht Klassen des Datenverkehrs. Jeder Datenverkehrsklasse verfügt über eine eigene übertragen, in die Warteschlange und können durch die Verwendung von PCF, starten und Beenden der Übertragung in einer Klasse.

Weitere Informationen finden Sie unter [Data Center Bridging (DCB)](https://docs.microsoft.com/windows-server/networking/technologies/dcb/dcb-top).

## <a name="hyper-v-network-virtualization"></a>Hyper-V-Netzwerkvirtualisierung

|                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **v1 (HNVv1)**       |                     In Windows Server 2012 eingeführt wurde, können die Hyper-V-Netzwerkvirtualisierung (HNV) Virtualisierung von Kundennetzwerken auf der Basis einer gemeinsam genutzten, physischen Netzwerkinfrastruktur. Mit nur minimale Änderungen erforderlich, auf dem physischen Netzwerk-Fabric, bietet HNV-Dienstanbieter die Agilität, bereitstellen und Migrieren von mandantenworkloads an einer beliebigen Stelle in der drei Clouds: der Service Provider-Cloud, die private Cloud oder der öffentlichen Cloud von Microsoft Azure.                     |
| **v2 NVGRE (HNVv2 NVGRE)** | In Windows Server 2016 und System Center Virtual Machine Manager bietet Microsoft eine End-to-End-Lösung für die Netzwerkvirtualisierung, die RAS-Gateway, den Softwarelastenausgleich, dem Netzwerkcontroller und mehr enthält. Weitere Informationen finden Sie unter [Hyper-V-Netzwerkvirtualisierung – Übersicht in Windows Server 2016](https://technet.microsoft.com/windows-server-docs/networking/sdn/technologies/hyper-v-network-virtualization/hyperv-network-virtualization-overview-windows-server). |
| **v2 VxLAN (HNVv2 VxLAN)** |                                                                                                                                                                                        In Windows Server 2016 ist Teil der SDN-Erweiterung, die über den Netzwerkcontroller verwaltet.                                                                                                                                                                                        |

---

## <a name="ipsec-task-offload-ipsecto"></a>IPsec-Aufgabenverlagerung (IPsecTO) 

IPsec Task Offload ist ein NIC-Feature, können das Betriebssystem den Prozessor auf die NIC für die Verarbeitung der IPsec-Verschlüsselung zu verwenden.

>[!IMPORTANT] 
>IPsec Task Offload ist eine veraltete Technologie, die von den meisten Netzwerkadapter unterstützt wird, und, in dem sie vorhanden ist, ist es standardmäßig deaktiviert.

## <a name="private-virtual-local-area-network-pvlan"></a>Private virtuelle Local Area Network (PVLAN). 

PVLANs ermöglichen die Kommunikation nur zwischen virtuellen Computern, auf dem gleichen Virtualisierungsserver. Ein privates virtuelles Netzwerk ist nicht an einen physischen Netzwerkadapter gebunden. Ein privates virtuelles Netzwerk ist von den gesamten externen Netzwerkdatenverkehr auf dem Virtualisierungsserver sowie Netzwerkdatenverkehr zwischen dem Verwaltungsbetriebssystem und im externen Netzwerk isoliert. Dieser Netzwerktyp ist nützlich, wenn Sie eine isolierten Netzwerkumgebung erstellen müssen, wie z. B. eine isolierte Testdomäne. Die Hyper-V und SDN-Stapel unterstützt nur isoliert-Port PVLAN-Modus.

Weitere Informationen zur Isolation von PVLAN finden Sie unter [System Center: Virtual Machine Manager-Engineering-Blog](https://blogs.technet.microsoft.com/scvmm/2013/06/04/logical-networks-part-iv-pvlan-isolation/).

## <a name="remote-direct-memory-access-rdma"></a>Remotezugriff auf den direkten Speicher (RDMA) 

RDMA ist eine Netzwerk-Technologie, die Kommunikation von hohem Durchsatz und geringer Latenz bietet, die CPU-Auslastung minimiert, werden. RDMA unterstützt NULL-Copy-Netzwerke durch Aktivieren des Netzwerkadapters zum Übertragen von Daten direkt in oder aus dem Anwendungsspeicher. RDMA-fähigen bedeutet, dass die NIC (physisch oder virtuell) kann RDMA an eine RDMA-Client bereitstellen. RDMA-fähige, also auf der anderen Seite eine RDMA-fähige Netzwerkkarte im Stapel die RDMA-Schnittstelle verfügbar macht.

Weitere Informationen zu RDMA, finden Sie unter [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming).

## <a name="receive-side-scaling-rss"></a>Receive Side Scaling (RSS) 

RSS ist ein NIC-Funktion, die getrennt werden verschiedene Sätze von Streams und übermittelt sie an die verschiedenen Prozessoren für die Verarbeitung. RSS parallelisiert die Netzwerke, die Verarbeitung, aktivieren einen Host, auf die Kosten für sehr hohe skaliert werden. 

Weitere Informationen finden Sie unter [erhalten empfangsseitige Skalierung (RSS)](https://docs.microsoft.com/windows-hardware/drivers/network/introduction-to-receive-side-scaling).

## <a name="single-root-input-output-virtualization-sr-iov"></a>E / a-Virtualisierung mit Einzelstamm (SR-IOV) 

SR-IOV kann virtuelle Computer Datenverkehr direkt aus die NIC mit dem virtuellen Computer verschieben, ohne Umweg über den Hyper-V-Host. SR-IOV ist eine unglaublich Verbesserung der Leistung für einen virtuellen Computer, aber es verfügt nicht über die Möglichkeit für den Host, der Named Pipe zu verwalten. Verwenden Sie nur SR-IOV, wenn die arbeitsauslastung gut funktionieren, als vertrauenswürdig eingestuft, und in der Regel die einzige VM auf dem Host.

Datenverkehr, der SR-IOV verwendet umgeht, Hyper-V-Switch, der dies, dass alle Richtlinien, z. B. bedeutet, ACLs, oder Verwaltung der Netzwerkbandbreite nicht angewendet werden. SR-IOV-Datenverkehr kann nicht auch über eine Network Virtualization-Funktion übergeben werden, damit NV-GRE- oder VxLAN Kapselung kann nicht angewendet werden. Verwenden Sie SR-IOV nur für höchst vertrauenswürdigen Workloads in bestimmten Situationen. Sie können nicht zusätzlich die Hostrichtlinien, bandbreitenverwaltung und Virtualisierungstechnologien verwenden.

In Zukunft würden zwei Technologien SR-IOV zulassen: Generische Flow Tabellen (GFT) und Hardware-QoS-Abladung (bandbreitenverwaltung in die NIC) – Sobald NICs in unserem Ökosystem unterstützt. Die Kombination dieser beiden Technologien stellen würden SR-IOV ist nützlich für alle VMs, Richtlinien, Virtualisierung und Bandbreite-Management-Regeln angewendet werden können, und konnte zu hervorragenden Bedrohungen weitergeleitet werden, in der allgemeinen Anwendung, der SR-IOV.

Weitere Informationen finden Sie unter [Übersicht der Single Root i/o Virtualization (SR-IOV)](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-single-root-i-o-virtualization--sr-iov-).

## <a name="tcp-chimney-offload"></a>TCP-Chimney-Abladung

TCP-Chimney-Abladung, auch bekannt als TCP-Engine-Offload (TOE), ist eine Technologie, die von der Host alle TCP-Verarbeitung an die NIC Auslagern kann Da der Windows Server-TCP-Stapel fast immer mehr ist effizient als die PO-Engine, mit der TCP-Chimney-Abladung wird nicht empfohlen.

>[!IMPORTANT]
>TCP-Chimney-Abladung ist eine veraltete Technologie. Es wird empfohlen, dass Sie keine TCP-Chimney-Abladung verwenden, da Microsoft beendet möglicherweise in Zukunft unterstützen.

## <a name="virtual-local-area-network-vlan"></a>Virtuelles lokales Netzwerk (VLAN) 

VLAN ist eine Erweiterung des Ethernet-Frame-Headers Partitionierung aktiviert eines LANs in mehrere VLANs, jeweils einen eigenen Adressbereich verwenden. In Windows Server 2016 werden VLANs auf Ports, die von Hyper-V-Switch oder durch Festlegen von teamschnittstellen auf NIC-Teamvorgang Teams festgelegt. Weitere Informationen finden Sie unter [NIC-Teamvorgang und virtuelle lokale Netzwerke (VLANs)](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nict-and-vlans).

## <a name="virtual-machine-queue-vmq"></a>Warteschlange für virtuelle Computer (Virtual Machine Queue, VMQ) 

Vmq wird eine NIC-Funktion, die eine Warteschlange für jeden virtuellen Computer reserviert. Jedes Mal, wenn Sie Hyper-V aktiviert haben. VMQ muss ebenfalls aktiviert werden. In Windows Server 2016 verwenden Vmq NIC Switch vPorts mit einer einzigen Warteschlange zugewiesen wird, um die vPort aus, um die gleiche Funktionalität bereitzustellen. Weitere Informationen finden Sie unter [virtuelle empfangsseitige Skalierung (vRSS)](https://docs.microsoft.com/windows-server/networking/technologies/vrss/vrss-top) und [NIC-Teamvorgang](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming).

## <a name="virtual-machine-multi-queue-vmmq"></a>Virtuellen Computer mit mehreren Warteschlangen (VMMQ) 

VMMQ ist ein NIC-Feature, können Datenverkehr für einen virtuellen Computer über mehrere Warteschlangen verteilt jede von einem anderen physischen Prozessor verarbeitet werden. Der Datenverkehr wird dann an mehreren LPs auf dem virtuellen Computer übergeben, wie in vRSS, die für die Übermittlung von erhebliche Netzwerkbandbreite auf dem virtuellen Computer ermöglicht.

---