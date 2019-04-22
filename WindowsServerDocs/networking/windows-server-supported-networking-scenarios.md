---
title: Windows Server unterstützte Netzwerkszenarios
description: Dieses Thema enthält Informationen zu neuen unterstützte Netzwerkszenarien in Windows Server 2016 und höher
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.date: ''
ms.assetid: 6de4232d-b0b3-4e43-8735-ebae35ae4f9f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 85f73f1f7caf833d23d3d693c0d754f52c4aa27d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812231"
---
# <a name="windows-server-supported-networking-scenarios"></a>Windows Server unterstützte Netzwerkszenarios

>Gilt für: WindowsServer \(Halbjährlicher Kanal\), WindowsServer 2016

Dieses Thema enthält Informationen zu unterstützten und nicht unterstützten Szenarien, die mit dieser Version von Windows Server 2016 kann nicht ausgeführt werden oder können.  
>[!IMPORTANT]
>Für Produktionsszenarien, verwenden Sie die neueste signierte Hardware-Treiber von Ihrem Originalgerätehersteller \(OEM\) oder unabhängiger Hardwarehersteller \(IHV\).
  
## <a name="bkmk_supp"></a>Unterstützte Szenarien für Netzwerke

Dieser Abschnitt enthält Informationen zu den unterstützten Szenarien für Netzwerken für Windows Server 2016, und enthält die folgenden Szenariokategorien.  
  
-   [Software-Defined Networking (SDN)-Szenarien](#bkmk_sdn)  
  
-   [Plattform-Netzwerkszenarien](#bkmk_netp)  
  
-   [DNS-Server-Szenarien](#bkmk_dns)  
  
-   [IPAM-Szenarien mit DHCP und DNS](#bkmk_ipam)  
  
-   [NIC-Teamvorgang-Szenarien](#bkmk_nicteam)

- [Switch Embedded Teaming \(festgelegt\) Szenarien](#bkmk_set)
  
### <a name="bkmk_sdn"></a>Software-Defined Networking (SDN)-Szenarien
 
Sie können die folgende Dokumentation zum Bereitstellen von SDN-Szenarien mit Windows Server 2016 verwenden.  
  
  
-   [Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)  
  
Weitere Informationen finden Sie unter [Software Defined Networking &#40;SDN&#41;](sdn/software-defined-networking.md).  
  
#### <a name="bkmk_netc"></a>Controller-Netzwerkszenarien

Die Netzwerkcontroller-Szenarien ermöglichen:  
  
-   Bereitstellen Sie und verwalten Sie eine Instanz mehrere Knoten des Netzwerkcontrollers. Weitere Informationen finden Sie unter [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](sdn/deploy/Deploy-Network-Controller-using-Windows-PowerShell.md).  
  
-   Verwenden Sie den Netzwerkcontroller Netzwerkrichtlinie programmgesteuert definiert, mit der Northbound REST-API.  
  
-   Verwenden Sie Netzwerkcontroller zum Erstellen und Verwalten von virtuellen Netzwerken mit Hyper-V-Netzwerkvirtualisierung – NVGRE oder VXLAN Kapselung verwenden.  
  
Weitere Informationen finden Sie unter [Network Controller](sdn/technologies/network-controller/Network-Controller.md).  
  
#### <a name="bkmk_netf"></a>Szenarien für Netzwerk-Funktion Virtualisierung NFV)  
Die NFV Szenarien können Sie:  
  
-   Bereitstellen und Verwenden eines Software Load Balancers, um sowohl die northbound als auch die southbound-Datenverkehr zu verteilen.  
  
-   Bereitstellen und Verwenden eines Software Load Balancers eastbound und westbound-Datenverkehr für virtuelle Netzwerke erstellt wurden, mit Hyper-V-Netzwerkvirtualisierung zu verteilen.  
  
-   Bereitstellen Sie und verwenden Sie einen NAT-Software-Lastenausgleich für virtuelle Netzwerke, die mit Hyper-V-Netzwerkvirtualisierung erstellt.  
  
-   Bereitstellen Sie und verwenden Sie eine Layer 3-weiterleitungs-gateway  
  
-   Bereitstellen Sie und verwenden Sie ein virtuelles privates Netzwerk (VPN)-Gateway für Standort-zu-Standort-IPsec (IKEv2)-Tunnel  
  
-   Bereitstellen Sie und verwenden Sie einen Gateway Generic Routing Encapsulation (GRE).  
  
-   Bereitstellen und Konfigurieren von dynamischen Routings und transitrouting zwischen Standorten mithilfe von Border Gateway Protocol (BGP).  
  
-   Konfigurieren Sie M + N-Redundanz für Schicht 3 und Standort-zu-Standort-Gateways und für die BGP-routing.  
  
-   Verwenden Sie den Netzwerkcontroller ACLs für virtuelle Netzwerke und Netzwerkschnittstellen angeben.  
  
Weitere Informationen finden Sie unter [Netzwerkfunktionsvirtualisierung](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md).  
  
### <a name="bkmk_netp"></a>Plattform-Netzwerkszenarien

Für die Szenarien in diesem Abschnitt, der die Windows Server Networking unterstützt Team für die Verwendung von jedem Windows Server 2016-zertifizierten Treiber. Überprüfen Sie mit Ihrem Netzwerk-Schnittstellenkarte \(NIC\) Hersteller, um sicherzustellen, dass die neuesten Treiber aktualisiert.
  
Die Netzwerk-Plattform-Szenarien ermöglichen:  
  
-   Verwenden Sie eine zusammengeführte NIC, um sowohl RDMA- und Ethernet-Datenverkehr mit einem einzelnen Netzwerkadapter zu kombinieren.  
  
-   Erstellen Sie einen Datenpfad zu mit niedriger Latenz mit Packetdirect, in den virtuellen Hyper-V-Switch, und einem einzelnen Netzwerkadapter aktiviert.  
  
-   Konfigurieren Sie die SET, SMB Direct "und" RDMA-Datenverkehrsfluss zwischen bis zu zwei Netzwerkadaptern zu verteilen.  
  
Weitere Informationen finden Sie unter [Remote Direct Memory Access &#40;RDMA&#41; und Switch Embedded Teaming &#40;festgelegt&#41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).  
  
#### <a name="bkmk_switch"></a>Szenarien für virtuelle Hyper-V-Switches

Die Szenarien für virtuelle Hyper-V-Switch können Sie:  
  
-   Erstellen Sie einen virtuellen Hyper-V-Switch mit einer vNIC (Remote Direct Memory Access, RDMA)  
  
-   Erstellen Sie einen virtuellen Hyper-V-Switch mit Switch Embedded Teaming (SET) und RDMA-vNICs  
  
-   Erstellen Sie ein SET-Team im Hyper-V-Switch  
  
-   Verwalten Sie ein SET-Team mithilfe von Windows PowerShell-Befehle  
  
Weitere Informationen finden Sie unter [Remote Direct Memory Access &#40;RDMA&#41; und Switch Embedded Teaming &#40;festlegen&#41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)  
  
### <a name="bkmk_dns"></a>DNS-Server-Szenarien

DNS-Server-Szenarien ermöglichen:  
  
-   Geben Sie die GeoLocation-Verwaltung des Datenverkehrs mithilfe von DNS-Richtlinien basierten  
  
-   Konfigurieren Sie mithilfe von DNS-Richtlinien-Brain-DNS  
  
-   Anwenden von Filtern auf DNS-Abfragen mithilfe von DNS-Richtlinien  
  
-   Konfigurieren Sie die Anwendung den Lastenausgleich mithilfe von DNS-Richtlinien  
  
-   Geben Sie abhängig von der Tageszeit intelligente DNS-Antworten  
  
-   Konfigurieren von Richtlinien für die Übertragung von DNS-Zone  
  
-   Konfigurieren von DNS-Server-Richtlinien auf Active Directory Domain Services (AD DS) integriert Zonen  
  
-   Konfigurieren von Antwortquote beschränken  
  
-   Angeben von DNS-basierte Authentifizierung von benannten Entitäten (DANE)  
  
-   Konfigurieren Sie Unterstützung für unbekannte Datensätze im DNS.  
  
Weitere Informationen finden Sie unter den Themen [Neuigkeiten in DNS-Client unter Windows Server 2016](dns/What-s-New-in-DNS-Client.md) und [Neuigkeiten in DNS-Server unter Windows Server 2016](dns/What-s-New-in-DNS-Server.md).  
  
### <a name="bkmk_ipam"></a>IPAM-Szenarien mit DHCP und DNS

Die IPAM-Szenarien ermöglichen:  
  
-   Ermitteln und Verwalten von DNS und DHCP-Server und IP-Adressierung in mehreren verbundenen Active Directory-Gesamtstrukturen  
  
-   Verwenden von IPAM für die zentrale Verwaltung von DNS-Eigenschaften, einschließlich von Zonen und Ressourceneinträge.  
  
-   Granulare rollenbasierte Access Control-Richtlinien zu definieren, und Delegieren von IPAM-Benutzer oder Benutzergruppen, um den Satz von DNS-Eigenschaften zu verwalten, die Sie angeben.  
  
-   Verwenden Sie die Windows PowerShell-Befehle für IPAM zum Automatisieren der Konfiguration der Zugriffssteuerung für DHCP- und DNS.  
  
    Weitere Informationen finden Sie unter [Verwalten von IPAM](technologies/ipam/Manage-IPAM.md).  
  
### <a name="bkmk_nicteam"></a>NIC-Teamvorgang-Szenarien

Die NIC-Teamvorgang-Szenarien ermöglichen:  
  
-   Erstellen eines NIC-Teams in einer unterstützten Konfiguration  
  
-   Löschen eines NIC-Teams  
  
-   Hinzufügen von Netzwerkadaptern an das NIC-Team in einer unterstützten Konfiguration  
  
-   Entfernen Sie die Netzwerkadapter des NIC-Teams  
  
> [!NOTE]  
> In Windows Server 2016 können Sie NIC-Teamvorgang in Hyper-V, verwenden jedoch in einigen Fällen Virtual Machine-Warteschlangen (VMQ) nicht automatisch auf den zugrunde liegenden Netzwerkadaptern beim Erstellen eines NIC-Teams aktiviert kann. In diesem Fall können Sie den folgenden Windows PowerShell-Befehl, um sicherzustellen, dass VMQ für den NIC-Team-mitgliederadapter aktiviert ist: `Set-NetAdapterVmq -Name <NetworkAdapterName> -Enable`  

Weitere Informationen finden Sie unter [NIC-Teamvorgang](technologies/nic-teaming/NIC-Teaming.md). 

### <a name="bkmk_set"></a>Switch Embedded Teaming \(festgelegt\) Szenarien

Eine alternative Lösung NIC-Teamvorgang, mit denen Sie in Umgebungen, die Hyper-V und den Stapel Software Defined Networking (SDN) in Windows Server 2016 enthalten ist. SET integriert einige Funktionen mit NIC-Teamvorgang in den virtuellen Hyper-V-Switch. 

Weitere Informationen finden Sie unter [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](https://technet.microsoft.com/windows-server-docs/networking/technologies/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)
  
 
  
## <a name="bkmk_unsupp"></a>Nicht unterstützte Szenarien für Netzwerke  
Die folgenden Szenarien für Netzwerken werden in Windows Server 2016 nicht unterstützt.  
  
-   VLAN-basierten virtuellen mandantennetzwerken.  
  
-   IPv6 wird im Overlay oder dabei nicht unterstützt.  
  


