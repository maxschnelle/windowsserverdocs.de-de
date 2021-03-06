---
title: Leitfaden für die Konfiguration der Netzwerkschnittstellenkarte (Network Interface Card, NIC)
description: Die konvergierte Netzwerkschnittstellenkarte (Network Interface Card, NIC) ermöglicht das verfügbar machen von RDMA über eine virtuelle NIC (Virtual NIC, VNIC) mit Host Partitionen, sodass die Host Partitions Dienste auf die gleichen Netzwerkkarten zugreifen können, die von den Hyper-V-Gast Computern für TCP/IP-Datenverkehr verwendet werden.
ms.topic: article
ms.assetid: d7642338-9b33-4dce-8100-8b2c38d7127a
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/13/2018
ms.openlocfilehash: 2b077b911d3721907e70b198c62970aafe25e58d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944754"
---
# <a name="converged-network-interface-card-nic-configuration-guidance"></a>\(Leitfaden zur NIC-Konfiguration für konvergierte Netzwerkschnittstellenkarten \)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Konvergierte Netzwerkschnittstellenkarten-NIC ermöglicht das verfügbar machen \( \) von RDMA über eine \- virtuelle NIC \( -vNIC von Host Partitionen, \) damit die Host Partitions Dienste auf die RDMA zugreifen können, die für den Remote Zugriff \( auf den direkten Speicher \) auf denselben NICs verwendet werden, die die Hyper-V-Gast Betriebssysteme für TCP/IP

Vor der konvergierten NIC-Funktion \( mussten Verwaltungs Host-Partitions \) Dienste, die RDMA verwenden wollten, dedizierte RDMA- \- fähige NICs verwenden, auch wenn die Bandbreite auf den NICs verfügbar war, die an den virtuellen Hyper-V-Switch gebunden waren.

Mit konvergierter NIC können die beiden Workloads \( Verwaltungs Benutzer von RDMA und Gast Datenverkehr \) die gleichen physischen NICs gemeinsam nutzen, sodass Sie weniger NICs auf Ihren Servern installieren können.

Wenn Sie konvergierte NIC mit Windows Server 2016 Hyper-v-Hosts und virtuellen Hyper-v-Switches bereitstellen, machen die vNICs auf den Hyper-v-Hosts RDMA-Dienste zum Hosten von Prozessen mithilfe von RDMA über eine beliebige Ethernet- \- basierte RDMA-Technologie verfügbar.

>[!NOTE]
>Um die konvergierte NIC-Technologie verwenden zu können, müssen die zertifizierten Netzwerkadapter auf Ihren Servern RDMA unterstützen.

Dieses Handbuch enthält zwei Sätze von Anweisungen, eine für bereit Stellungen, bei denen auf Ihren Servern ein einzelner Netzwerkadapter installiert ist. Hierbei handelt es sich um eine grundlegende Bereitstellung von konvergierter NIC. und eine weitere Anleitung, bei der auf Ihren Servern mindestens zwei Netzwerkadapter installiert sind. Hierbei handelt es sich um eine Bereitstellung von konvergenten NIC über ein Switch Embedded Teaming \( Set- \) Team von RDMA- \- fähigen Netzwerkadaptern.


## <a name="prerequisites"></a>Voraussetzungen

Im folgenden sind die Voraussetzungen für die grundlegenden und Daten Center Bereitstellungen von konvergiertem NIC angegeben.

>[!NOTE]
>In den bereitgestellten Beispielen wird ein Mellanox ConnectX-3 pro 40 Gbit/s-Ethernet-Adapter verwendet, Sie können jedoch jeden der Windows Server Certified RDMA- \- fähigen Netzwerkadapter verwenden, die diese Funktion unterstützen. Weitere Informationen zu kompatiblen Netzwerkadaptern finden Sie im Windows Server-Katalog Thema [LAN-Karten](https://www.windowsservercatalog.com/results.aspx?&bCatID=1468&cpID=0&avc=85&ava=0&avt=0&avq=46&OR=1).

### <a name="basic-converged-nic-prerequisites"></a>Grundlegende zusammen geteilte NIC-Komponenten

Zum Ausführen der Schritte in dieser Anleitung für die grundlegende konvergierte NIC-Konfiguration benötigen Sie Folgendes:

- Zwei Server, auf denen Windows Server 2016 Datacenter Edition oder Windows Server 2016 Standard Edition ausgeführt wird.
- Ein RDMA-fähiger, zertifizierter Netzwerkadapter, der auf jedem Server installiert ist.
- Auf jedem Server ist die Hyper-V-Server Rolle installiert.

### <a name="datacenter-converged-nic-prerequisites"></a>Voraussetzungen für Rechenzentrums konvergierte NIC

Zum Ausführen der Schritte in dieser Anleitung für die konvergierte NIC-Konfiguration im Daten Center müssen Sie über Folgendes verfügen:

- Zwei Server, auf denen Windows Server 2016 Datacenter Edition oder Windows Server 2016 Standard Edition ausgeführt wird.
- Zwei RDMA-fähige, zertifizierte Netzwerkadapter, die auf jedem Server installiert sind.
- Auf jedem Server ist die Hyper-V-Server Rolle installiert.
- Sie müssen mit Switch Embedded Teaming Set vertraut \( sein \) , einer alternativen NIC-Team Vorgangs Lösung, die in Umgebungen verwendet wird, die Hyper-V und den Sdn-Stapel (Software Defined Networking) in Windows Server 2016 enthalten. Set integriert einige NIC-Team Vorgangs Funktionen in den virtuellen Hyper-V-Switch. Weitere Informationen finden Sie unter [Remote Direct Memory Access (RDMA) und Switch Embedded Teaming (Set)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).

## <a name="related-topics"></a>Verwandte Themen
- [Konvergierte NIC-Konfiguration mit einem einzelnen Netzwerk Adapter](cnic-single.md)
- [Konvergierte NIC-Konfiguration mit Nic](cnic-datacenter.md)
- [Konfiguration des physischen Switches für konvergierte NIC](cnic-app-switch-config.md)
- [Problembehandlung bei zusammen getauschten NIC](cnic-app-troubleshoot.md)

---