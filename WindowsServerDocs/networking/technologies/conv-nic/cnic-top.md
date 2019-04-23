---
title: Zusammengeführte (Network Interface Card, NIC)-Konfigurationsrichtlinien
description: Zusammengeführte Netzwerkschnittstellenkarte (NIC) kann RDMA über eine virtuelle Netzwerkkarte (vNIC) von Host-Partition verfügbar zu machen, damit die Partition Hostdienste Remote Direct Memory Access (RDMA) auf den gleichen NICs zugreifen können, die die Hyper-V-Gäste für TCP/IP-Datenverkehr verwenden.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d7642338-9b33-4dce-8100-8b2c38d7127a
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: e9f5180285dda790e11cec543a109d0cb58edd2d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838841"
---
# <a name="converged-network-interface-card-nic-configuration-guidance"></a>Converged Network Interface Card \(NIC\) Konfigurationsrichtlinien

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Zusammengeführtes Netzwerk-Schnittstellenkarte \(NIC\) können Sie RDMA über einen Host verfügbar machen\-Partitionieren Sie die virtuellen NIC \(vNIC\) , damit die Partition Hostdienste Remote Direct Memory Access zugreifen können \(RDMA\) auf den gleichen Netzwerkkarten, die die Hyper-V-Gäste für TCP/IP-Datenverkehr verwenden.

Bevor Sie die zusammengeführte NIC-Funktion, Management \(hosten Partitions\) Dienste, die RDMA verwenden möchten, verwenden Sie dedizierte RDMA mussten\-fähige NICs, selbst wenn die Bandbreite auf den Netzwerkkarten verfügbar war, die an den Hyper-V gebunden wurden Virtuellen Switch.

Zusammengeführte NIC, die zwei Workloads \(Management-Benutzer, der RDMA und Gastdatenverkehr\) können teilen den gleichen physischen NICs, sodass Sie weniger Netzwerkkarten in Ihren Servern zu installieren.

Bei der Bereitstellung NIC Converged mit Windows Server 2016 Hyper-V-Hosts und virtuellen Hyper-V-Switches, wird der vNIC auf den Hyper-V-Hosts verfügbar zu machen RDMA-Dienste zum Hosten von Prozessen mit RDMA über alle Ethernet\-RDMA-Technologie basiert.

>[!NOTE]
>Um zusammengeführte NIC-Technologie verwenden zu können, müssen die zertifizierte Netzwerkadapter auf Ihren Servern RDMA-Unterstützung.

Dieses Handbuch enthält zwei Sätze von Anweisungen für Bereitstellungen, in dem Ihre Server einen einzigen Netzwerkadapter installiert ist, verfügen, der eine grundlegende Bereitstellung von zusammengeführten NIC ist; und einen anderen Satz von Anweisungen, die Ihre Server, in denen mindestens zwei Netzwerkadapter installiert ist haben, wird eine Bereitstellung von zusammengeführten NIC über einen Switch Embedded Teaming \(festgelegt\) Team von RDMA\-fähigen Netzwerkadaptern.


## <a name="prerequisites"></a>Vorraussetzungen

Es folgen die Voraussetzungen für die Basic- und Datacenter-Bereitstellungen Converged Netzwerkkarte.

>[!NOTE]
>Für den bereitgestellten Beispielen verwenden wir ein Mellanox ConnectX-3 Pro 40 Gbit/s Ethernet-Adapter, jedoch können Sie eines der Windows Server zertifiziert RDMA\-fähigen Netzwerkadaptern, die dieses Feature zu unterstützen. Weitere Informationen zu kompatiblen Netzwerkadaptern finden Sie im Windows Server-Katalog Thema [LAN-Karten](https://www.windowsservercatalog.com/results.aspx?&bCatID=1468&cpID=0&avc=85&ava=0&avt=0&avq=46&OR=1).

### <a name="basic-converged-nic-prerequisites"></a>Grundlegende Converged NIC-Voraussetzungen

Um die Schritte in diesem Handbuch für die Basiskonfiguration Converged NIC ausführen zu können, müssen Sie die folgenden verfügen.

- Zwei Server, auf denen Windows Server 2016 Datacenter-Edition oder Windows Server 2016 Standard Edition ausgeführt wird.
- Eine RDMA-fähigen, zertifiziert Netzwerkadapter auf jedem Server installiert.
- Hyper-V-Serverrolle auf jedem Server installiert.

### <a name="datacenter-converged-nic-prerequisites"></a>Zusammengeführtes Datacenter-NIC-Voraussetzungen

Um die Schritte in diesem Handbuch für die NIC zusammengeführten Datacenters ausführen zu können, müssen Sie die folgenden verfügen.

- Zwei Server, auf denen Windows Server 2016 Datacenter-Edition oder Windows Server 2016 Standard Edition ausgeführt wird.
- Zwei RDMA-fähigen, zertifiziert Netzwerkadapter auf jedem Server installiert.
- Hyper-V-Serverrolle auf jedem Server installiert.
- Sie müssen mit Switch Embedded Teaming vertraut sein \(festgelegt\), eine alternative NIC-Teaming-Lösung, die in Umgebungen, die Hyper-V und den Stapel Software Defined Networking (SDN) in Windows Server 2016 enthalten verwendet. SET integriert einige Funktionen mit NIC-Teamvorgang in den virtuellen Hyper-V-Switch. Weitere Informationen finden Sie unter [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).

## <a name="related-topics"></a>Verwandte Themen
- [Zusammengeführte NIC-Konfiguration mit einem einzelnen Netzwerkadapter](cnic-single.md)
- [Zusammengeführte NIC in einem Team verwendete NIC-Konfiguration](cnic-datacenter.md)
- [Konfiguration der physischen Switch für zusammengeführte NIC](cnic-app-switch-config.md)
- [Problembehandlung bei Converged NIC-Konfigurationen](cnic-app-troubleshoot.md)

---