---
title: Konfigurationshandbuch für zusammengeführten Netzwerk Schnittstelle Netzwerkschnittstellenkarte (NIC)
description: Dieses Thema ist Teil der zusammengeführten NIC Konfiguration Anleitung für Windows Server2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d7642338-9b33-4dce-8100-8b2c38d7127a
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 42f7ef674da1754253ad72ae30ad505f29ba6a7d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="converged-network-interface-card-nic-configuration-guide"></a>Konfigurationshandbuch für zusammengeführten Netzwerk Schnittstelle Karte \(NIC\)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Zusammengeführte Netzwerkschnittstellenkarte \(NIC\) RDMA über eine Host\-Partition virtuelle NIC \(vNIC\) verfügbar zu machen, damit die Host-Partition Dienste Remote Direct Memory Access \(RDMA\) auf den gleichen NICs zugreifen können, die die Hyper-V-Gäste für TCP/IP-Datenverkehr verwenden können.

Vor der zusammengeführten NIC-Funktion \(Host Partition\)-Verwaltungsdienste, die RDMA verwenden möchten mussten dedizierte RDMA\-fähige NICs verwenden, auch wenn Bandbreite auf die NICs verfügbar war, die mit dem virtuellen Hyper-V-Switch gebunden waren.

Mit zusammengeführten Netzwerkkarte, die zwei Arbeitslasten \ (Verwaltung von RDMA und Gast Traffic\) können Benutzern die gleichen physischen NICs, sodass Sie weniger NICs in Ihren Servern zu installieren.

Bei der Bereitstellung eines zusammengeführten NIC mit Windows Server2016 Hyper-V-Hosts und virtuelle Hyper-V-Switches machen der vNICs in Hyper-V-Host zu Hostprozesse keine RDMA Ethernet\-basierte Technologien RDMA over über RDMA-Dienste verfügbar.

>[!NOTE]
>Um zusammengeführten NIC-Technologie verwenden, müssen die zertifizierten Netzwerkadapter in Ihren Servern RDMA-Unterstützung.

Dieses Handbuch enthält zwei Sätze von Anweisungen, eine für Bereitstellungen, in denen die Server einen einzigen Netzwerkadapter installiert ist, verfügen, einer einfachen Bereitstellung von zusammengeführten NIC; und einen anderen Satz von Anweisungen, in denen die Server mindestens zwei Netzwerkadapter installiert sein, verfügen, die eine Bereitstellung von zusammengeführten NIC über \(SET\) Switch Embedded Teaming-Team RDMA\-fähige Netzwerkadapter ist.

Dieses Handbuch enthält die folgenden Themen.

- [Zusammengeführtes NIC-Konfiguration mit einem einzelnen Netzwerkadapter](cnic-single.md)
- [Zusammengeführtes NIC kombinierten NIC-Konfiguration](cnic-datacenter.md)
- [Physischen Switch-Konfiguration für die zusammengeführten NIC](cnic-app-switch-config.md)
- [Problembehandlung bei zusammengeführten NIC-Konfigurationen](cnic-app-troubleshoot.md)

## <a name="prerequisites"></a>Erforderliche Komponenten

Folgendes sind die Voraussetzungen für die Basic und Datacenter-Bereitstellungen von NIC zusammengefasst.

>[!NOTE]
>Für die Beispiele in diesem Handbuch einen Mellanox ConnectX-3 Pro 40 Gbit/s Ethernet-Adapter wird verwendet, können alle von der Windows Server zertifiziert RDMA\-fähigen Netzwerkadapter, die dieses Feature unterstützen. Weitere Informationen zu kompatiblen Netzwerkadaptern finden Sie im Windows Server-Katalog Thema [LAN-Karten](https://www.windowsservercatalog.com/results.aspx?&bCatID=1468&cpID=0&avc=85&ava=0&avt=0&avq=46&OR=1).

### <a name="basic-converged-nic-prerequisites"></a>Grundlegende zusammengeführten NIC-Voraussetzungen

Um die Schrittein diesem Handbuch für die grundlegende NIC zusammengeführten Konfiguration auszuführen, müssen Sie die folgenden verfügen.

- Zwei Server, auf denen entweder Windows Server2016 Datacenter Edition oder Windows Server2016 Standard Edition ausgeführt werden.
- Eine RDMA-fähig ist, in den einzelnen Servern installierten Netzwerkadapter zertifiziert.
- Die Hyper-V-Serverrolle muss auf jedem Server installiert werden.

### <a name="datacenter-converged-nic-prerequisites"></a>Zusammengeführtes Datacenter-NIC-Voraussetzungen

Um die Schrittein diesem Handbuch für die Netzwerkkarte eines zusammengeführten Datacenters auszuführen, müssen Sie die folgenden verfügen.

- Zwei Server, auf denen entweder Windows Server2016 Datacenter Edition oder Windows Server2016 Standard Edition ausgeführt werden.
- Zwei RDMA-fähig, zertifiziert Netzwerkadapter auf jedem Server installiert.
- Die Hyper-V-Serverrolle muss auf jedem Server installiert werden.
- Sie müssen mit vertraut sein Switch Embedded Teaming \(SET\) Alternative NIC-Teaming-Lösung, die Sie in einer Umgebung verwenden können, die Hyper-V und der Stapel Software Defined Networking (SDN) in Windows Server2016 enthalten ist. SET integriert einige NIC-Teaming-Funktionen in den virtuellen Hyper-V-Switch. Weitere Informationen finden Sie unter [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).

