---
title: Windows Server unterstützte Szenarien für Netzwerke
description: Dieses Thema enthält Informationen zu neuen unterstützten Szenarien für Netzwerke in Windows Server2016 und höher
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.date: ''
ms.assetid: 6de4232d-b0b3-4e43-8735-ebae35ae4f9f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 70198f97c4ec39de4b78de28ab196dc3e86a684c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="windows-server-supported-networking-scenarios"></a>Windows Server unterstützte Szenarien für Netzwerke

>Gilt für: Windows Server-\(Semi-Annual Channel\), Windows Server 2016

Dieses Thema enthält Informationen zu unterstützten und nicht unterstützten Szenarien, die in dieser Version von Windows Server2016 nicht möglich oder können.  
>[!IMPORTANT]
>Verwenden Sie für alle Produktionsszenarien, die neuesten signierte Hardwaretreiber aus den Originalgerätehersteller \(OEM\) oder unabhängige Hardwarehersteller \(IHV\).
  
## <a name="bkmk_supp"></a>Unterstützte Szenarien für Netzwerke

Dieser Abschnittenthält Informationen zu den unterstützten Netzwerkszenarien für Windows Server2016 und umfasst die folgenden Szenariokategorien.  
  
-   [Software-Defined Networking (SDN)-Szenarien](#bkmk_sdn)  
  
-   [Plattform-Netzwerkszenarien](#bkmk_netp)  
  
-   [Szenarien für die DNS-Server](#bkmk_dns)  
  
-   [IPAM-Szenarien mit DHCP und DNS](#bkmk_ipam)  
  
-   [NIC-Teaming-Szenarien](#bkmk_nicteam)

- [Switch Embedded Teaming \(SET\) Szenarien](#bkmk_set)
  
### <a name="bkmk_sdn"></a>Software-Defined Networking (SDN)-Szenarien
 
Die folgende Dokumentation können SDN-Szenarien mit Windows Server2016 bereitgestellt werden.  
  
  
-   [Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)  
  
Weitere Informationen finden Sie unter [Software Defined Networking & 40; SDN & 41;](sdn/software-defined-networking.md).  
  
#### <a name="bkmk_netc"></a>Netzwerk-Controller-Szenarien

Die Netzwerk-Controller-Szenarien können Sie:  
  
-   Bereitstellen und Verwalten einer Instanz mehreren Knoten Netzwerkcontroller. Weitere Informationen finden Sie unter [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](sdn/deploy/Deploy-Network-Controller-using-Windows-PowerShell.md).  
  
-   Verwenden Sie Netzwerkcontroller Netzwerkrichtlinie programmgesteuert definieren, mit der Northbound REST-API.  
  
-   Verwenden Sie Netzwerkcontroller zum Erstellen und Verwalten von virtuellen Netzwerken mit Hyper-V-Netzwerkvirtualisierung – NVGRE oder VXLAN Kapselung verwenden.  
  
Weitere Informationen finden Sie unter [Netzwerkcontroller](sdn/technologies/network-controller/Network-Controller.md).  
  
#### <a name="bkmk_netf"></a>Netzwerkszenarien Funktion Virtualization (NFV)  
Die NFV Szenarien können Sie:  
  
-   Bereitstellen Sie und verwenden Sie eine Software Load Balancers northbound und southbound-Datenverkehr zu verteilen.  
  
-   Bereitstellen Sie und verwenden Sie eine Software Load Balancers zum Verteilen von eastbound und westbound Datenverkehr für virtuelle Netzwerke mit Hyper-V-Netzwerkvirtualisierung erstellt.  
  
-   Bereitstellen Sie und verwenden Sie ein NAT-Software zum Lastenausgleich für virtuelle Netzwerke mit Hyper-V-Netzwerkvirtualisierung erstellt.  
  
-   Bereitstellen Sie und verwenden Sie ein weiterleitungsgateway Layer 3  
  
-   Bereitstellen Sie und verwenden Sie ein virtuelles privates Netzwerk (VPN)-Gateway für Standort-zu-Standort IPsec (IKEv2)-Tunnel  
  
-   Bereitstellen Sie und verwenden Sie ein Gateway Generic Routing Encapsulation (GRE).  
  
-   Bereitstellen Sie und konfigurieren Sie dynamisches Routing und während der Übertragung zwischen Standorten Border Gateway Protocol (BGP) mit Routing.  
  
-   Konfigurieren Sie M+N Redundanz für Ebene-3 und Standort-zu-Standort-Gateways und BGP-Routing.  
  
-   Verwenden Sie Netzwerkcontroller ACLs für virtuelle Netzwerke und Netzwerkschnittstellen angeben.  
  
Weitere Informationen finden Sie unter [Netzwerkfunktionsvirtualisierung](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md).  
  
### <a name="bkmk_netp"></a>Plattform-Netzwerkszenarien

Für die Szenarien in diesem Abschnittder Windows Server-Netzwerke unterstützt Team die Verwendung von allen Windows Server2016-zertifizierten Treiber. Überprüfen Sie mit Ihrer Karte \(NIC\) Hersteller um sicherzustellen, dass Sie die neuesten Treiber aktualisiert haben.
  
Die Netzwerk-Plattform-Szenarien können Sie:  
  
-   Verwenden Sie eine zusammengeführte NIC RDMA und Ethernet-Datenverkehr über einen einzelnen Netzwerkadapter zu kombinieren.  
  
-   Erstellen Sie einen Datenpfad mit geringer Wartezeit, mit Paket direkt in den virtuellen Hyper-V-Switch und einem einzelnen Netzwerkadapter aktiviert.  
  
-   Verteilen von SMB Direct und RDMA-Datenverkehr fließt zwischen bis zu zwei Netzwerkadapter konfigurieren.  
  
Weitere Informationen finden Sie unter [Remote Direct Memory Access & 40; RDMA & 41; und Switch Embedded Teaming & 40; SET & 41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).  
  
#### <a name="bkmk_switch"></a>Szenarien für virtuelle Hyper-V-Switch

Die Hyper-V Virtual Switch Szenarien können Sie:  
  
-   Erstellen Sie einen virtuellen Hyper-V-Switch mit einem vNIC (Remote Direct Memory Access, RDMA)  
  
-   Erstellen Sie einen virtuellen Hyper-V-Switch mit Switch Embedded Teaming (SET) und RDMA-vNICs  
  
-   Erstellen eines SET-Teams beim virtuellen Hyper-V-Switch  
  
-   Verwalten Sie ein SET-Team mithilfe von Windows PowerShell-Befehle  
  
Weitere Informationen finden Sie unter [Remote Direct Memory Access & 40; RDMA & 41; und Switch Embedded Teaming & 40; SET & 41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)  
  
### <a name="bkmk_dns"></a>Szenarien für die DNS-Server

Szenarien für die DNS-Server können Sie:  
  
-   Geben Sie GeoLocation Verwaltung mithilfe von DNS-Richtlinien basiert  
  
-   Konfigurieren des Split-Brain-DNS mithilfe von DNS-Richtlinien  
  
-   Anwenden von Filtern auf DNS-Abfragen, die mithilfe von DNS-Richtlinien  
  
-   Konfigurieren Sie die Anwendung den Lastenausgleich mithilfe von DNS-Richtlinien  
  
-   Geben Sie anhand von der Tageszeit intelligente DNS-Antworten  
  
-   Konfigurieren Sie DNS-Zone Übertragung Richtlinien  
  
-   Konfigurieren von DNS-Server-Richtlinien auf Active Directory-Domänendienste (AD DS) integriert Zonen  
  
-   Konfigurieren von Antworten begrenzen  
  
-   Geben Sie die DNS-basierte Authentifizierung von benannten Entitäten (DANE)  
  
-   Konfigurieren der Unterstützung für unbekannte Datensätze in DNS  
  
Weitere Informationen finden Sie unter den Themen [What's New in DNS-Client unter Windows Server2016](dns/What-s-New-in-DNS-Client.md) und [What's New in DNS-Server unter Windows Server2016](dns/What-s-New-in-DNS-Server.md).  
  
### <a name="bkmk_ipam"></a>IPAM-Szenarien mit DHCP und DNS

Die IPAM-Szenarien können Sie:  
  
-   Ermitteln und Verwalten von DNS- und DHCP-Server und IP-Adressierung in mehreren federated Active Directory-Gesamtstrukturen  
  
-   Verwenden von IPAM für die zentralisierte Verwaltung der DNS-Eigenschaften einschließlich Zonen und Ressourceneinträge.  
  
-   Präzise rollenbasierte Zugriffsrichtlinien definieren und Delegieren von IPAM-Benutzer oder Benutzergruppen, um die DNS-Eigenschaften zu verwalten, die Sie angeben.  
  
-   Verwenden Sie Windows PowerShell-Befehle für IPAM zum Automatisieren der Konfiguration für DHCP- und DNS-Steuerelement.  
  
    Weitere Informationen finden Sie unter [Verwalten von IPAM](technologies/ipam/Manage-IPAM.md).  
  
### <a name="bkmk_nicteam"></a>NIC-Teaming-Szenarien

Der NIC-Teaming Szenarien können Sie:  
  
-   Erstellen Sie ein NIC-Team in einer unterstützten Konfiguration  
  
-   Löschen eines NIC-Teams  
  
-   Hinzufügen von Netzwerkadaptern zu einer unterstützten Konfiguration der NIC-Team  
  
-   Entfernen von Netzwerkadaptern des NIC-Teams  
  
> [!NOTE]  
> In Windows Server2016 können NIC-Teamvorgang in Hyper-V, Sie jedoch in einigen Fällen Warteschlangen, virtuellen Computer (VMQ) nicht automatisch auf den zugrunde liegenden Netzwerkadaptern ermöglichen könnte bei der Erstellung eines NIC-Teams. In diesem Fall können Sie den folgenden Windows PowerShell-Befehl, um sicherzustellen, dass VMQ für den NIC-Team mitgliederadapter aktiviert ist: `Set-NetAdapterVmq -Name <NetworkAdapterName> -Enable`  

Weitere Informationen finden Sie unter [NIC-Teaming](technologies/nic-teaming/NIC-Teaming.md). 

### <a name="bkmk_set"></a>Switch Embedded Teaming \(SET\) Szenarien

Eine alternative NIC-Teaming-Lösung, die Sie in einer Umgebung verwenden können, die Hyper-V und der Stapel Software Defined Networking (SDN) in Windows Server2016 enthalten ist. SET integriert einige NIC-Teaming-Funktionen in den virtuellen Hyper-V-Switch. 

Weitere Informationen finden Sie unter [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](https://technet.microsoft.com/windows-server-docs/networking/technologies/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)
  
 
  
## <a name="bkmk_unsupp"></a>Nicht unterstützte Szenarien für Netzwerke  
Die folgenden Szenarios werden in Windows Server2016 nicht unterstützt.  
  
-   VLAN-basierten virtuellen mandantennetzwerken.  
  
-   IPv6 wird im Overlay oder dabei nicht unterstützt.  
  


