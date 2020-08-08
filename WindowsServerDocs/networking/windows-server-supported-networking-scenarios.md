---
title: Von Windows Server unterstützte Netzwerkszenarios
description: Dieses Thema enthält Informationen zu neuen unterstützten Netzwerkszenarien in Windows Server 2016 und höher.
manager: brianlic
ms.topic: article
ms.assetid: 6de4232d-b0b3-4e43-8735-ebae35ae4f9f
author: dcuomo
ms.author: dacuo
ms.openlocfilehash: 0059e04b79754a3fb183a51cbd75bc03e9a89ae5
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997543"
---
# <a name="windows-server-supported-networking-scenarios"></a>Von Windows Server unterstützte Netzwerkszenarios

>Gilt für: Windows Server- \( halbjährlicher Kanal \) , Windows Server 2016

Dieses Thema enthält Informationen zu unterstützten und nicht unterstützten Szenarien, die Sie in dieser Version von Windows Server 2016 nicht ausführen können.
>[!IMPORTANT]
>Verwenden Sie für alle Produktionsszenarien die neuesten signierten Hardwaretreiber von Ihrem Originalgerätehersteller \( OEM \) oder unabhängiger Hardwarehersteller \( IHV \) .

## <a name="supported-networking-scenarios"></a><a name="bkmk_supp"></a>Unterstützte Netzwerkszenarien

Dieser Abschnitt enthält Informationen zu den unterstützten Netzwerkszenarien für Windows Server 2016 und umfasst die folgenden Szenariokategorien.

-   [Software-Defined Networking (SDN)-Szenarios](#bkmk_sdn)

-   [Szenarios der Netzwerkplattform](#bkmk_netp)

-   [DNS-Server Szenarios](#bkmk_dns)

-   [IPAM-Szenarien mit DHCP und DNS](#bkmk_ipam)

-   [Nic-Team Vorgangs Szenarios](#bkmk_nicteam)

- [Szenarien für eingebettete Teaming- \( Sets wechseln \)](#bkmk_set)

### <a name="software-defined-networking-sdn-scenarios"></a><a name="bkmk_sdn"></a>Software-Defined Networking (SDN)-Szenarios

In der folgenden Dokumentation finden Sie die Bereitstellung von Sdn-Szenarien mit Windows Server 2016.


-   [Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)

Weitere Informationen finden Sie unter [Software Defined Networking &#40;Sdn&#41;](sdn/software-defined-networking.md).

#### <a name="network-controller-scenarios"></a><a name="bkmk_netc"></a>Netzwerk Controller Szenarios

Die Netzwerk Controller Szenarien ermöglichen Folgendes:

-   Stellen Sie eine Instanz des Netzwerk Controllers mit mehreren Knoten bereit, und verwalten Sie Sie. Weitere Informationen finden Sie unter Bereitstellen eines [Netzwerk Controllers mithilfe von Windows PowerShell](sdn/deploy/Deploy-Network-Controller-using-Windows-PowerShell.md).

-   Verwenden Sie den Netzwerk Controller, um die Netzwerk Richtlinie mithilfe der Rest-Northbound-API Programm gesteuert zu definieren.

-   Verwenden Sie den Netzwerk Controller zum Erstellen und Verwalten von virtuellen Netzwerken mit Hyper-V-Netzwerkvirtualisierung mithilfe von nvgre oder vxlan-Kapselung.

Weitere Informationen finden Sie unter [Network Controller](sdn/technologies/network-controller/Network-Controller.md).

#### <a name="network-function-virtualization-nfv-scenarios"></a><a name="bkmk_netf"></a>Netzwerk funktionsvirtualisierungsszenarien (NFV)
Die NFV-Szenarien ermöglichen Folgendes:

-   Bereitstellen und Verwenden eines Software Lastenausgleichs zum Verteilen von Northbound-und Southbound-Datenverkehr.

-   Bereitstellen und Verwenden eines Software Lastenausgleichs zum Verteilen von Datenverkehr in Ost-und westdaten für virtuelle Netzwerke, die mit der Hyper-V-Netzwerkvirtualisierung erstellt wurden.

-   Bereitstellen und Verwenden eines NAT-Software Lastenausgleichs für virtuelle Netzwerke, die mit der Hyper-V-Netzwerkvirtualisierung erstellt wurden.

-   Bereitstellen und Verwenden eines Layer 3-Weiterleitungs Gateways

-   Bereitstellen und Verwenden eines VPN-Gateways (virtuelles privates Netzwerk) für Standort-zu-Standort-IPSec-Tunnel (IKEv2)

-   Bereitstellen und Verwenden eines allgemeinen Routing Kapselungs Gateways (GRE).

-   Stellen Sie das dynamische Routing und Transit Routing Zwischenstand Orten mithilfe Border Gateway Protocol (BGP) bereit, und konfigurieren Sie es.

-   Konfigurieren von M + N-Redundanz für Layer 3-und Site-to-Site-Gateways sowie für BGP-Routing.

-   Verwenden Sie den Netzwerk Controller zum Angeben von ACLs für virtuelle Netzwerke und Netzwerkschnittstellen.

Weitere Informationen finden Sie unter [netzwerkfunktionsvirtualisierung](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md).

### <a name="network-platform-scenarios"></a><a name="bkmk_netp"></a>Szenarios der Netzwerkplattform

In den Szenarien in diesem Abschnitt unterstützt das Windows Server-Netzwerkteam die Verwendung eines beliebigen Windows Server 2016 Certified-Treibers. Wenden Sie sich an Ihren Netzwerkschnittstellenkarten- \( NIC- \) Hersteller, um sicherzustellen, dass Sie über die neuesten Treiber Updates verfügen.

Die Szenarien für die Netzwerkplattform ermöglichen Folgendes:

-   Verwenden Sie eine konvergierte NIC, um RDMA-und Ethernet-Datenverkehr mithilfe eines einzelnen Netzwerkadapters zu kombinieren.

-   Erstellen Sie einen Datenpfad mit geringer Latenz, indem Sie Paket Direct verwenden, das im virtuellen Hyper-V-Switch aktiviert ist, und einen einzelnen Netzwerkadapter.

-   Konfigurieren Sie, um SMB Direct-und RDMA-Daten Verkehrsflüsse zwischen bis zu zwei Netzwerkadaptern zu verteilen.

Weitere Informationen finden Sie unter [Remote Direct Memory Access &#40;RDMA&#41; und Switch Embedded Teaming &#40;Set&#41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).

#### <a name="hyper-v-virtual-switch-scenarios"></a><a name="bkmk_switch"></a>Szenarien für virtuelle Hyper-V-Switches

Die virtuellen Hyper-V-Switch-Szenarien ermöglichen Folgendes:

-   Erstellen eines virtuellen Hyper-V-Switches mit einem Remote Zugriff auf den direkten Speicher (RDMA) vNIC

-   Erstellen eines virtuellen Hyper-V-Switches mit Switch Embedded Teaming (Set) und RDMA vNICs

-   Erstellen eines Set-Teams in einem virtuellen Hyper-V-Switch

-   Verwalten eines Set-Teams mithilfe von Windows PowerShell-Befehlen

Weitere Informationen finden Sie unter [Remote Direct Memory Access &#40;RDMA&#41; und Switch Embedded Teaming &#40;Set&#41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)

### <a name="dns-server-scenarios"></a><a name="bkmk_dns"></a>DNS-Server Szenarios

DNS-Server Szenarios ermöglichen Folgendes:

-   Angeben der standortbasierten Datenverkehrs Verwaltung mithilfe von DNS-Richtlinien

-   Konfigurieren von Split-Brain-DNS mit DNS-Richtlinien

-   Anwenden von Filtern auf DNS-Abfragen mit DNS-Richtlinien

-   Konfigurieren des Anwendungs Lastenausgleichs mithilfe von DNS-Richtlinien

-   Angeben von intelligenten DNS-Antworten basierend auf der Tageszeit

-   Konfigurieren von DNS-Zonen Übertragungs Richtlinien

-   Konfigurieren von DNS-Server Richtlinien in Active Directory Domain Services integrierten Zonen (AD DS)

-   Konfigurieren der Antwortraten Begrenzung

-   Angeben der DNS-basierten Authentifizierung benannter Entitäten (Dane)

-   Unterstützung für unbekannte Datensätze in DNS konfigurieren

Weitere Informationen finden Sie in den Themen [Neues im DNS-Client unter Windows Server 2016](dns/What-s-New-in-DNS-Client.md) und [Neues in DNS-Server unter Windows Server 2016](dns/What-s-New-in-DNS-Server.md).

### <a name="ipam-scenarios-with-dhcp-and-dns"></a><a name="bkmk_ipam"></a>IPAM-Szenarien mit DHCP und DNS

Die IPAM-Szenarien ermöglichen Folgendes:

-   DNS-und DHCP-Server und IP-Adressierung über mehrere Verbund Active Directory Gesamtstrukturen hinweg ermitteln und verwalten

-   Verwenden Sie IPAM für die zentralisierte Verwaltung von DNS-Eigenschaften, einschließlich Zonen und Ressourcen Datensätzen.

-   Definieren Sie differenzierte Richtlinien für die rollenbasierte Zugriffs Steuerung, und delegieren Sie IPAM-Benutzer oder-Benutzergruppen, um den von Ihnen angegebenen Satz von DNS-Eigenschaften zu verwalten.

-   Verwenden Sie die Windows PowerShell-Befehle für IPAM, um die Zugriffs Steuerungs Konfiguration für DHCP und DNS zu automatisieren.

    Weitere Informationen finden Sie unter [Verwalten von IPAM](technologies/ipam/Manage-IPAM.md).

### <a name="nic-teaming-scenarios"></a><a name="bkmk_nicteam"></a>Nic-Team Vorgangs Szenarios

Mit den NIC-Team Vorgangs Szenarien können Sie folgende Aktionen ausführen:

-   Erstellen eines NIC-Teams in einer unterstützten Konfiguration

-   Löschen eines NIC-Teams

-   Hinzufügen von Netzwerkadaptern zum NIC-Team in einer unterstützten Konfiguration

-   Entfernen von Netzwerkadaptern aus dem NIC-Team

> [!NOTE]
> In Windows Server 2016 können Sie den NIC-Team Vorgang in Hyper-V verwenden. in einigen Fällen werden virtuelle Computer Warteschlangen (VMQ) auf den zugrunde liegenden Netzwerkadaptern jedoch möglicherweise nicht automatisch aktiviert, wenn Sie ein NIC-Team erstellen. Wenn dies auftritt, können Sie den folgenden Windows PowerShell-Befehl verwenden, um sicherzustellen, dass VMQ auf den NIC-Teammitglieds Adaptern aktiviert ist:`Set-NetAdapterVmq -Name <NetworkAdapterName> -Enable`

Weitere Informationen finden Sie unter [NIC](technologies/nic-teaming/NIC-Teaming.md)-Team Vorgang.

### <a name="switch-embedded-teaming-set-scenarios"></a><a name="bkmk_set"></a>Szenarien für eingebettete Teaming- \( Sets wechseln \)

Set ist eine Alternative NIC-Team Vorgangs Lösung, die Sie in Umgebungen verwenden können, die Hyper-V und den Sdn-Stapel (Software Defined Networking) in Windows Server 2016 enthalten. Set integriert einige NIC-Team Vorgangs Funktionen in den virtuellen Hyper-V-Switch.

Weitere Informationen finden Sie unter [Remote Direct Memory Access (RDMA) und Switch Embedded Teaming (Set)](../virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming.md) .



## <a name="unsupported-networking-scenarios"></a><a name="bkmk_unsupp"></a>Nicht unterstützte Netzwerkszenarien
Die folgenden Netzwerkszenarien werden in Windows Server 2016 nicht unterstützt.

-   VLAN-basierte virtuelle Mandanten Netzwerke

-   IPv6 wird weder in der unter-noch in der Überlagerung unterstützt.