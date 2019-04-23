---
title: RAS-Gateway GRE-Tunneling Durchsatz und Leistung
description: Diese Thema ausgetauscht, das für Informationstechnologie (IT)-Experten vorgesehen ist, bietet Durchsatz Leistungsinformationen zu Tunneln für RAS-Gateway Generic Routing Encapsulation (GRE).
manager: brianlic
ms.prod: windows-server-threshold
ms.date: ''
ms.technology: networking-ras
ms.topic: article
ms.assetid: c051b2ec-de0f-49d1-82b9-5742b259cd7c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 73ae4e573d926f4a77b076c880c1d74ed69f032d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880761"
---
# <a name="ras-gateway-gre-tunnel-throughput-and-performance"></a>RAS-Gateway GRE-Tunneling Durchsatz und Leistung

>Gilt für: WindowsServer \(Halbjährlicher Kanal\)

Können Sie in diesem Thema erfahren Sie RAS-Server \(RAS\) Gateway Generic Routing Encapsulation \(GRE\) Leistung unter Windows Server, Version 1709, die in einer nicht - Software Defined Networking Tunneln\( SDN\) basierend Test-Umgebung.

RAS-Gateway ist ein Softwarerouter und Gateway, das Sie in den einzelnen Mandanten oder mehrinstanzenfähigen Modus verwenden können. Dieses Thema beschreibt eine einzelmandantenmodus, die hohe Verfügbarkeit mit Failover-Clusterunterstützung. Die Leistungsstatistik GRE-Tunnel, die in diesem Thema präsentiert werden gelten für RAS-Gateway im Singele Mandanten und mehrinstanzenfähige Modus zur Verfügung.

>[!NOTE]
>Failoverclustering ist eine Windows Server-Funktion, die Ihnen ermöglicht, mehrere Server in einem fehlertoleranten Cluster gruppieren. Weitere Informationen finden Sie unter [Failover-Clusterunterstützung](../../../failover-clustering/failover-clustering-overview.md)

Einzelmandantenmodus ermöglicht es Organisationen jeder Größe Bereitstellen des Gatewayservers als einem äußeren oder Internet\-gegenüberliegenden Edge virtuelles privates Netzwerk \(VPN\) Server. Sie können RAS-Gateway auf einem physischen Server oder virtuellen Computer bereitstellen, im einzelmandantenmodus, \(VM\). Dieses Thema beschreibt die Bereitstellung eines RAS-Gateways auf zwei virtuellen Computern \(VMs\) , die in einem Failovercluster konfiguriert sind.

>[!IMPORTANT]
>Da GRE-Tunnel-Kapselung jedoch keine Verschlüsselung bereitstellen, sollten Sie die RAS-Gateway mit GRE als ein Internet-Edge-Gateway konfiguriert nicht verwenden. Weitere Informationen zu den besten Einsatzbereiche für das RAS-Gateway mit GRE-Tunnel finden Sie unter [GRE Tunneling in Windows Server](gre-tunneling-windows-server.md).

GRE ist ein Lightweight-Tunneling-Protokoll, die eine Vielzahl von Netzwerkschichtprotokolle in virtuelle Punkt kapseln kann\-zu\-Links über eine IP-Internetwork zeigen. Die Microsoft-GRE-Implementierung kapselt IPv4 und IPv6.

Weitere Informationen finden Sie im Abschnitt **RAS-Gateway-Bereitstellungsszenarien** im Thema [RAS-Gateway](https://docs.microsoft.com/windows-server/remote/remote-access/ras-gateway/ras-gateway#bkmk_deploy). 

In diesem Testszenario, die in der folgenden Abbildung dargestellt ist, verschiebt der Datenverkehr, der gemessen werden aus der Organisation Intranet 2, in der Organisation Intranet-1. Workload-VMs der Mandanten Senden des Netzwerkdatenverkehrs von Intranet-2 an Intranet-1 mithilfe von RAS-Gateway.

![RAS-Gateway-GRE-Tunnel Test – szenarioübersicht](../../media/GRE-Tunnel-Perf/Gre-Infrastructure.jpg)

## <a name="test-environment-configuration"></a>Konfiguration des Test-Umgebung

Dieser Abschnitt enthält Informationen zu den Test-Umgebung und der RAS-Gateway-Konfiguration.

In der testumgebung werden die RAS-Gateway-VMs auf Hyper bereitgestellt\-V-Hosts in einem Failovercluster für hohe Verfügbarkeit Clustern.

### <a name="hyper-v-host-configuration"></a>Hyper\-V-Hostkonfiguration

Zwei Hyper\-V-Hosts sind so konfiguriert, dass das Testszenario auf folgende Weise unterstützen. 

- Zwei Dual\-verwaltet physischen Computer mit Windows Server, Version 1709 konfiguriert sind
- Die beiden physischen Netzwerkadapter in jedem der beiden Server sind mit anderen Subnetzwerken - verbunden, die beide Subnetze Intranet einer Organisation darstellen. Sowohl die Netzwerke als auch die unterstützende Hardware haben eine Kapazität von 10 Gbit/s an.
- Hyperthreading auf physischen Servern deaktiviert ist. Dadurch wird den maximalen Durchsatz über die physischen NICs.
- Die Hyper\-V-Serverrolle auf beiden Servern installiert und konfiguriert, die mit zwei externe Hyper\-V virtuellen Switches, einen für jeden physischen Netzwerkadapter.
- Da beide Server mit demselben Intranet verbunden sind, können die Server miteinander kommunizieren.
- Die Hyper\-V-Hosts in einem Failovercluster konfiguriert sind, über das Intranet. 

>[!NOTE]
>Weitere Informationen finden Sie unter [Hyper-V Virtual Switch](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/hyper-v-virtual-switch).

### <a name="vm-configuration"></a>Konfiguration des virtuellen Computers

Zwei virtuelle Computer werden konfiguriert, um das Testszenario auf folgende Weise zu unterstützen.

- Ausführen von Windows Server, Version 1709 auf jedem Server, die ein virtuellen Computer installiert ist. Jeder virtuelle Computer wird mit 10 Kerne und 8 GB RAM konfiguriert.
- Jeder virtuelle Computer wird auch mit zwei virtuelle Netzwerkadapter konfiguriert. Einen virtuellen Netzwerkadapter mit dem Intranet 1 virtuellen Switch verbunden ist, und der virtuelle Netzwerkadapter mit dem Intranet-2-Switch verbunden ist.
- Jede VM verfügt über RAS-Gateway installiert und konfiguriert werden, als eine GRE\-basierte VPN-Server.
- Die virtuellen Gatewaycomputer sind in einem Failovercluster konfiguriert. Wenn gruppiert, für einen virtuellen Computer aktiv ist, und der anderen virtuellen Computer ist passiv.

### <a name="workload-hyper-v-hosts-and-vms"></a>Arbeitsauslastung Hyper\-V-Hosts und virtuellen Computern

Für diesen Test zwei Workload Hyper\-V-Hosts im Intranet installiert sind, und jeder Host hat einen virtuellen Computer installiert. Wenn Sie diesen Test in Ihrer eigenen testumgebung duplizieren, können Sie beliebig viele Workload-Servern und VMs, da für Ihre Zwecke angemessen ist installieren.

- Arbeitsauslastung Hyper\-V-Hosts verfügen, einen physischen Netzwerkadapter installiert ist, wird mit dem Unternehmensintranet verbunden.
- Auf virtuellen Hyper\-virtuellen V-Switch, einen virtueller Switch auf jedem Host erstellt. Der Schalter ist "External" und an die ein mit dem Intranet verbundenen Netzwerkadapter gebunden ist.
- Der arbeitsauslastungs-VMs werden mit 2 GB RAM und 2 Kerne konfiguriert.
- Der Arbeitsauslastungs-VMs haben jeweils einen virtuellen Netzwerkadapter, der mit dem Intranet virtuellen Switch verbunden ist.

### <a name="traffic-generator-tool"></a>Tool zum Generieren von Datenverkehr

Das Tool zum Generieren von Datenverkehr, das in diesem Test verwendet wird ist das Tool CtsTraffic. Das Git-Repository für dieses Tool befindet sich unter [ https://github.com/Microsoft/ctsTraffic ](https://github.com/Microsoft/ctsTraffic).

## <a name="ras-gateway-performance"></a>RAS-Gateway-Leistung

Die Abbildungen in diesem Abschnitt sehen wir, Task-Manager zeigt GRE-Tunnel Durchsatz mit mehreren TCP-Verbindungen.

Erreichen Sie, bis zu 2,0 Gbit/s Durchsatz auf mehreren\-core-VMs, die als GRE-RAS-Gateways konfiguriert sind.

### <a name="gre-tunnel-performance-with-multiple-tcp-sessions"></a>GRE-Tunnel-Leistung mit mehreren TCP-Sitzungen

Klicken Sie mit mehreren TCP-Sitzungen die CPU-Auslastung 100 % erreicht, und der maximale Durchsatz auf den GRE-Tunnel ist 2.0 Gbit/s.

Die folgende Abbildung zeigt die CPU-Auslastung auf der RAS-Gateway-VMs. Die aktive virtuellen Computer, die RAS-Gateway-VM-1, ist auf der linken Seite, während die passive VM 2 für RAS-Gateway-VM, auf der rechten Seite ist.

![Gateway-VM-CPU-Auslastung im Task-Manager](../../media/GRE-Tunnel-Perf/Gre-Tunnel-01.jpg)

Die folgende Abbildung zeigt die Ethernet-Netzwerkdurchsatz auf den RAS-Gateway-VMs. Die aktive virtuellen Computer, die RAS-Gateway-VM-1, ist auf der linken Seite, während die passive VM 2 für RAS-Gateway-VM, auf der rechten Seite ist.

![Gateway-VM-Ethernet-Netzwerkdurchsatz im Task-Manager](../../media/GRE-Tunnel-Perf/Gre-Tunnel-02.jpg)


### <a name="gre-tunnel-performance-with-one-tcp-connection"></a>GRE-Tunnel-Leistung mit einem TCP-Verbindung

Mit der Testkonfiguration, die von mehreren TCP-Sitzungen in einer einzelnen TCP-Sitzung geändert wird erreicht nur eine CPU-Kern maximale Kapazität auf dem RAS-Gateway-VMs.

Der maximale Durchsatz auf den GRE-Tunnel wird zwischen 400 – 500 Mbit/s auf.

Die folgende Abbildung zeigt die CPU-Auslastung auf der RAS-Gateway-VMs. Die aktive virtuellen Computer, die RAS-Gateway-VM-1, ist auf der linken Seite, während die passive VM 2 für RAS-Gateway-VM, auf der rechten Seite ist.

![Gateway-VM-CPU-Auslastung im Task-Manager](../../media/GRE-Tunnel-Perf/Gre-Tunnel-03.jpg)


Die folgende Abbildung zeigt die Ethernet-Netzwerkdurchsatz auf den RAS-Gateway-VMs. Die aktive virtuellen Computer, die RAS-Gateway-VM-1, ist auf der linken Seite, während die passive VM 2 für RAS-Gateway-VM, auf der rechten Seite ist.

![Gateway-VM-Ethernet-Netzwerkdurchsatz im Task-Manager](../../media/GRE-Tunnel-Perf/Gre-Tunnel-04.jpg)

Weitere Informationen zur Leistung von RAS-Gateway finden Sie unter [hnv-Gateway zur Leistungsoptimierung in Softwaredefinierten Netzwerken](https://docs.microsoft.com/windows-server/administration/performance-tuning/subsystem/software-defined-networking/hnv-gateway-performance).