---
title: Netzwerkcontroller
description: Dieses Thema enthält eine Übersicht über den Netzwerk Controller in Windows Server 2016.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 31f3fa4e-cd25-4bf3-89e9-a01a6cec7893
ms.author: anpaul
author: AnirbanPaul
ms.openlocfilehash: f8221c92dc91d0c2e04df906ccd839a2c9895f94
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859663"
---
# <a name="network-controller"></a>Netzwerkcontroller

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Der Netzwerk Controller ist neu in Windows Server 2016 und bietet einen zentralisierten, programmierbaren Automatisierungs Punkt für die Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Daten Center. 

Mithilfe von Netzwerkcontroller können Sie die Konfiguration der Netzwerkinfrastruktur automatisieren und müssen Netzwerkgeräte und -dienste nicht länger manuell konfigurieren.

> [!NOTE]
> Zusätzlich zu diesem Thema ist die folgende Dokumentation zum Netzwerk Controller verfügbar.
> - [Hohe Verfügbarkeit des Netzwerk Controllers](network-controller-high-availability.md)
> - [Installations-und Vorbereitungs Anforderungen für die Bereitstellung des Netzwerk Controllers](../../plan/Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)  
> - [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)  
> - [Installieren der Serverrolle „Netzwerkcontroller“ mit Server-Manager](Install-the-Network-Controller-server-role-using-Server-Manager.md)
> - [Schritte nach der Bereitstellung für den Netzwerk Controller](post-deploy-steps-nc.md)
> - [Cmdlets für Netzwerk Controller](https://technet.microsoft.com/library/mt576401.aspx) 

## <a name="network-controller-overview"></a><a name="bkmk_overview"></a>Netzwerk Controller (Übersicht)

Der Netzwerk Controller ist eine hoch verfügbare und skalierbare Server Rolle, die eine Anwendungsprogrammierschnittstelle \(API-\) bietet, die den Netzwerk Controller für die Kommunikation mit dem Netzwerk und eine zweite API ermöglicht, die Ihnen die Kommunikation mit dem Netzwerk Controller ermöglicht.

Sie können Netzwerk Controller in Domänen-und nicht-Domänen Umgebungen bereitstellen. In Domänen Umgebungen authentifiziert der Netzwerk Controller Benutzer und Netzwerkgeräte mithilfe von Kerberos. in Umgebungen ohne Domänen müssen Sie Zertifikate für die Authentifizierung bereitstellen.

>[!IMPORTANT]
>Stellen Sie die Netzwerk Controller-Server Rolle nicht auf physischen Hosts bereit. Zum Bereitstellen des Netzwerk Controllers müssen Sie die Netzwerk Controller-Server Rolle auf einem virtuellen Hyper-v-Computer \(VM-\) installieren, der auf einem Hyper-v-Host installiert ist. Nachdem Sie den Netzwerk Controller auf virtuellen Computern auf drei verschiedenen Hyper\-V-Hosts installiert haben, müssen Sie die Hyper\-V-Hosts für Software-Defined Networking \(Sdn\) aktivieren, indem Sie die Hosts mithilfe des Windows PowerShell-Befehls **New-networkcontrollerserver**dem Netzwerk Controller hinzufügen. Auf diese Weise aktivieren Sie die Load Balancer der Sdn-Software. Weitere Informationen finden Sie unter [New-networkcontrollerserver](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver).

Netzwerkcontroller kommuniziert mit Netzwerkgeräten, -diensten und -komponenten über die Southbound-API. Mithilfe der Southbound-API kann Netzwerkcontroller Netzwerkgeräte und Dienstkonfigurationen ermitteln und alle benötigten Informationen zum Netzwerk sammeln. Zusätzlich stellt die Southbound-API Netzwerkcontroller einen Pfad zum Senden von Informationen an die Netzwerkinfrastruktur bereit, wenn beispielsweise Änderungen an der Konfiguration vorgenommen wurden.

Die Northbound-API von Netzwerkcontroller ermöglicht das Sammeln von Netzwerkinformationen aus Netzwerkcontroller und wird verwendet, um das Netzwerk zu überwachen und zu konfigurieren.

Mithilfe der Northbound-API des Netzwerk Controllers können Sie neue Geräte im Netzwerk mithilfe von Windows PowerShell, der Representational State Transfer \(Rest\)-API oder einer Verwaltungs Anwendung mit grafischer Benutzeroberfläche, z. b. System Center Virtual Machine Manager, konfigurieren, überwachen, beheben und bereitstellen.

>[!NOTE]
>Die Northbound-API von Netzwerkcontroller wird als REST-Schnittstelle implementiert.

Sie können Ihr Rechenzentrums Netzwerk mit dem Netzwerk Controller verwalten, indem Sie Verwaltungs Anwendungen verwenden, z. b. System Center Virtual Machine Manager \(SCVMM-\), und System Center Operations Manager \(SCOM\), da Sie mit dem Netzwerk Controller die Netzwerkinfrastruktur konfigurieren, überwachen, Programmieren und Probleme beheben können, die unter seiner Kontrolle liegt.

Unter Verwendung von Windows PowerShell, der REST-API oder einer Verwaltungsanwendung können Sie Netzwerkcontroller zum Verwalten der folgenden physischen und virtuellen Netzwerkinfrastrukturkomponenten einsetzen:

- Virtuelle Hyper-V-Computer und -Switches

- Rechenzentrumsfirewall

- RAS-Dienst \(RAS\) mehr Instanzen fähige Gateways, virtuelle Gateways und gatewaypools

- Software Load Balancer

In der folgenden Abbildung verwendet ein Administrator ein Verwaltungstool, das direkt mit Netzwerkcontroller interagiert. Der Netzwerk Controller liefert Informationen zur Netzwerkinfrastruktur, einschließlich virtueller und physischer Infrastruktur, zum Verwaltungs Tool und führt Konfigurationsänderungen gemäß den Aktionen des Administrators durch, wenn das Tool verwendet wird.  

![Netzwerk Controller (Übersicht)](../../../media/Network-Controller/NetController_overview.png)  

Wenn Sie einen Netzwerk Controller in einer Testumgebung bereitstellen, können Sie die Netzwerk Controller-Server Rolle auf einem virtuellen Hyper-v-Computer \(VM-\) ausführen, der auf einem Hyper-v-Host installiert ist.

Für Hochverfügbarkeit in größeren Rechenzentren können Sie einen Cluster mithilfe von drei VMS bereitstellen, die auf drei oder mehr Hyper-V-Hosts installiert sind. Weitere Informationen finden Sie unter [hohe Verfügbarkeit des Netzwerk Controllers](network-controller-high-availability.md).

## <a name="network-controller-features"></a><a name="bkmk_features"></a>Netzwerk Controller Features

Die folgenden Funktionen von Netzwerkcontroller ermöglichen Ihnen das Konfigurieren und Verwalten von virtuellen und physischen Netzwerkgeräten und diensten.  
  
-   [Firewallverwaltung](#bkmk_firewall)  
  
-   [Software Load Balancer Verwaltung](#bkmk_slb)  
  
-   [Virtual Network Verwaltung](#bkmk_virtual)  
  
-   [RAS-Gatewayverwaltung](#bkmk_gateway)

>[!IMPORTANT]
>Die Sicherung und Wiederherstellung des Netzwerk Controllers ist derzeit in Windows Server 2016 nicht verfügbar.
  
### <a name="firewall-management"></a><a name="bkmk_firewall"></a>Firewallverwaltung

Mit dieser Funktion von Netzwerkcontroller können Sie Firewall-Zugriffssteuerungsregeln für die virtuellen Computer für Ihre Arbeitsauslastungen konfigurieren und verwalten (Zulassen/Verweigern), die sowohl für den Ost/West- als auch den Nord/Süd-Netzwerkdatenverkehr in Ihrem Datencenter gelten. Die Firewallregeln werden im vSwitch-Port des virtuellen Computers für die Arbeitsauslastung bereitgestellt, sodass sie auf alle Arbeitsauslastungen im Datencenter angewendet werden. Unter Verwendung der Northbound-API können Sie die Firewallregeln für eingehenden und ausgehenden Datenverkehr über den virtuellen Computer für Ihre Arbeitsauslastungen definieren. Außerdem können Sie jede Firewallregel so konfigurieren, dass der über die Regel zugelassene oder abgelehnte Datenverkehr protokolliert wird.  

Weitere Informationen finden Sie unter [Übersicht über die Datacenter-Firewall](../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md).

### <a name="software-load-balancer-management"></a><a name="bkmk_slb"></a>Software Load Balancer Verwaltung

Diese Funktion von Netzwerkcontroller ermöglicht es Ihnen, mehrere Server zum Hosten derselben Arbeitsauslastung zu aktivieren, um hohe Verfügbarkeit und Skalierbarkeit bereitzustellen.  
  
Weitere Informationen finden Sie unter [Software Lastenausgleich &#40;SLB&#41; für Sdn](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md).  
  
### <a name="virtual-network-management"></a><a name="bkmk_virtual"></a>Virtual Network Verwaltung

Diese Funktion von Netzwerkcontroller ermöglicht es Ihnen, die Hyper-V-Netzwerkvirtualisierung bereitzustellen und zu konfigurieren – virtuelle Hyper-V-Switches und virtuelle Netzwerkadapter auf einzelnen virtuellen Computern eingeschlossen – sowie Richtlinien für virtuelle Netzwerke zu speichern und anzuwenden.

Netzwerkcontroller unterstützt sowohl NVGRE (Network Virtualization Generic Routing Encapsulation) als auch VXLAN (Virtual Extensible Local Area Network).

### <a name="ras-gateway-management"></a><a name="bkmk_gateway"></a>RAS-Gatewayverwaltung

Mit dieser Netzwerk Controller Funktion können Sie virtuelle Computer (VMS), die Mitglieder eines RAS-gatewaypools sind, bereitstellen, konfigurieren und verwalten, wobei Sie Gatewaydienste für Ihre Mandanten bereitstellen. Der Netzwerk Controller ermöglicht das automatische Bereitstellen von virtuellen Computern, auf denen das RAS-Gateway ausgeführt wird, mit den folgenden

> [!NOTE]
> In System Center Virtual Machine Manager wird das RAS-Gateway als Windows Server-Gateway bezeichnet.

- Hinzufügen von Entfernen von virtuellen Gatewaycomputern zum Cluster bzw. aus dem Cluster und Festlegen der erforderlichen Sicherungsstufe

- Standort-zu-Standort-VPN-Gatewaykonnektivität zwischen Remotemandantennetzwerken und Ihrem Datencenter unter Verwendung von IPsec

- Standort-zu-Standort-VPN-Gatewaykonnektivität zwischen Remotemandantennetzwerken und Ihrem Datencenter unter Verwendung von GRE (Generic Routing Encapsulation)

- Schicht 3-Weiterleitungsfunktion

- Border Gateway Protocol (BGP)-Routing, das es Ihnen ermöglicht, das Routing von Netzwerk Datenverkehr zwischen den VM-Netzwerken Ihrer Mandanten und ihren Remote Standorten zu verwalten.

Der Netzwerk Controller kann verschiedene Verbindungen eines Mandanten auf separaten Gateways platzieren. Sie können eine einzelne öffentliche IP-Adresse für alle Gatewayverbindungen verwenden oder über andere öffentliche IP-Adressen für eine Teilmenge der Verbindungen verfügen. Der Netzwerk Controller protokolliert alle gatewaykonfigurations-und Statusänderungen, die zu Überwachungs-und Problem Behandlungszwecken verwendet werden können.

Weitere Informationen zu BGP finden Sie unter [Border Gateway Protocol &#40;BGP&#41;](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md).

Weitere Informationen zum RAS-Gateway finden Sie unter [RAS-Gateway für Sdn](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md).

## <a name="network-controller-deployment-options"></a>Optionen für die Netzwerk Controller Bereitstellung

Informationen zum Bereitstellen eines Netzwerk Controllers mithilfe System Center Virtual Machine Manager \(VMM-\)finden Sie unter [Einrichten eines Sdn-Netzwerk Controllers im VMM-Fabric](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller).

Informationen zum Bereitstellen eines Netzwerk Controllers mithilfe von Skripts finden Sie unter Bereitstellen [einer Software definierten Netzwerkinfrastruktur mit Skripts](../../deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)

Informationen zum Bereitstellen eines Netzwerk Controllers mit Windows PowerShell finden Sie unter Bereitstellen eines [Netzwerk Controllers mit Windows PowerShell](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md) .
