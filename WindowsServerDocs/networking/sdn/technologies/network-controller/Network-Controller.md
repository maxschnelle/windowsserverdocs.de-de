---
title: Netzwerkcontroller
description: Dieses Thema enthält eine Übersicht über den Netzwerkcontroller in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 31f3fa4e-cd25-4bf3-89e9-a01a6cec7893
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7ace628c6ae9802c0c65d360aedfac8c80ac5537
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875681"
---
# <a name="network-controller"></a>Netzwerkcontroller

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In Windows Server 2016 bietet neue Netzwerkcontroller einen Punkt zentralen, programmierbaren Automatisierung von Verwaltung, konfigurieren, überwachen und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum an. 

Mithilfe von Netzwerkcontroller können Sie die Konfiguration der Netzwerkinfrastruktur automatisieren und müssen Netzwerkgeräte und -dienste nicht länger manuell konfigurieren.

> [!NOTE]
> Zusätzlich zu diesem Thema wird die folgende Dokumentation zum Netzwerkcontroller verfügbar.
> - [Hohe Netzwerkverfügbarkeit für Controller](network-controller-high-availability.md)
> - [Installation und Anforderungen bei der Vorbereitung für die Bereitstellung des Netzwerkcontrollers](../../plan/Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)  
> - [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)  
> - [Installieren Sie die Netzwerkcontroller-Serverrolle, die mithilfe des Server-Manager](Install-the-Network-Controller-server-role-using-Server-Manager.md)
> - [Schritte nach der Bereitstellung für den Netzwerkcontroller](post-deploy-steps-nc.md)
> - [Netzwerk-Controller-Cmdlets](https://technet.microsoft.com/library/mt576401.aspx) 

## <a name="bkmk_overview"></a>Netzwerkcontroller – Übersicht

Netzwerkcontroller ist eine hoch verfügbare und skalierbare Serverrolle, und bietet eine Anwendungsprogrammierschnittstelle \(API\) Netzwerkcontroller für die Kommunikation mit dem Netzwerk und eine zweite API, die Ihnen ermöglicht, ermöglicht die Kommunikation mit Netzwerkcontroller.

Sie können den Netzwerkcontroller in sowohl domänenbezogene als auch nicht in die Domäne Umgebungen bereitstellen. In domänenumgebungen authentifiziert die Netzwerkcontroller-Benutzer und Geräte mithilfe von Kerberos; in nicht-domänenumgebungen müssen Sie Zertifikate für die Authentifizierung bereitstellen.

>[!IMPORTANT]
>Stellen Sie keine der Serverrolle "Netzwerkcontroller" auf physischen Hosts ausgeführt werden. Sie müssen die Netzwerkcontroller-Serverrolle auf einem virtuellen Hyper-V-Computer installieren, zum Bereitstellen des Netzwerkcontrollers \(VM\) , die auf einem Hyper-V-Host installiert ist. Nach der Installation des Netzwerkcontrollers auf virtuellen Computern für drei verschiedene Hyper\-V-Hosts müssen Sie die Hyper aktivieren\-V-Hosts für die Software Defined Networking \(SDN\) durch Hinzufügen von Hosts mit dem Netzwerkcontroller der Windows PowerShell-Befehl **New-NetworkControllerServer**. Auf diese Weise aktivieren Sie den SDN-Softwarelastenausgleich-Funktion. Weitere Informationen finden Sie unter [New-NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver).

Netzwerkcontroller kommuniziert mit Netzwerkgeräten, -diensten und -komponenten über die Southbound-API. Mithilfe der Southbound-API kann Netzwerkcontroller Netzwerkgeräte und Dienstkonfigurationen ermitteln und alle benötigten Informationen zum Netzwerk sammeln. Zusätzlich stellt die Southbound-API Netzwerkcontroller einen Pfad zum Senden von Informationen an die Netzwerkinfrastruktur bereit, wenn beispielsweise Änderungen an der Konfiguration vorgenommen wurden.

Die Northbound-API von Netzwerkcontroller ermöglicht das Sammeln von Netzwerkinformationen aus Netzwerkcontroller und wird verwendet, um das Netzwerk zu überwachen und zu konfigurieren.

Die Northbound-API von Netzwerkcontroller können Sie konfigurieren, überwachen, beheben und neue Geräte im Netzwerk bereitstellen, indem Sie mithilfe von Windows PowerShell die Representational State Transfer \(REST\) -API oder einer verwaltungsanwendung mit einer grafischen Benutzeroberfläche, z. B. System Center Virtual Machine Manager.

>[!NOTE]
>Die Northbound-API von Netzwerkcontroller wird als REST-Schnittstelle implementiert.

Sie können Ihr datencenternetzwerk mit Netzwerkcontroller verwalten, indem Sie die Verwendung von verwaltungsanwendungen wie System Center Virtual Machine Manager- \(SCVMM\), und System Center Operations Manager \(SCOM\), Da Sie zum Konfigurieren von Netzwerkcontroller ermöglicht es, überwachen, Programmieren und Problembehandlung der kontrollierten Netzwerkinfrastruktur, die unter ihrer Kontrolle ist.

Unter Verwendung von Windows PowerShell, der REST-API oder einer Verwaltungsanwendung können Sie Netzwerkcontroller zum Verwalten der folgenden physischen und virtuellen Netzwerkinfrastrukturkomponenten einsetzen:

- Virtuelle Hyper-V-Computer und -Switches

- Rechenzentrumsfirewall

- RAS-Dienst \(RAS\) mehrinstanzenfähigen Gateways und Gateways für virtuelle gatewaypools

- Software-Lastenausgleichsmodule

In der folgenden Abbildung verwendet ein Administrator ein Verwaltungstool, das direkt mit Netzwerkcontroller interagiert. Netzwerkcontroller bietet Informationen zur Netzwerkinfrastruktur, einschließlich virtuelle und physische Infrastruktur, um das Verwaltungstool und führt konfigurationsänderungen gemäß des Administrators Aktionen aus, wenn das Tool verwenden.  

![Netzwerkcontroller – Übersicht](../../../media/Network-Controller/NetController_overview.png)  

Wenn Sie den Netzwerkcontroller in einer testumgebung bereitstellen, können Sie die Netzwerkcontroller-Serverrolle ausführen, auf einem virtuellen Hyper-V-Computer \(VM\) , die auf einem Hyper-V-Host installiert ist.

Für eine hohe Verfügbarkeit in größeren Datencentern können Sie einen Cluster bereitstellen, mithilfe von drei virtuellen Computern, die auf drei oder mehreren Hyper-V-Hosts installiert sind. Weitere Informationen finden Sie unter [hohe Netzwerkverfügbarkeit für Controller](network-controller-high-availability.md).

## <a name="bkmk_features"></a>Funktionen von Netzwerkcontroller

Die folgenden Funktionen von Netzwerkcontroller ermöglichen Ihnen das Konfigurieren und Verwalten von virtuellen und physischen Netzwerkgeräten und diensten.  
  
-   [Firewallverwaltung](#bkmk_firewall)  
  
-   [Verwalten des Softwarelastenausgleichs](#bkmk_slb)  
  
-   [Verwalten des virtuellen Netzwerks](#bkmk_virtual)  
  
-   [Verwalten des RAS-Gateways](#bkmk_gateway)

>[!IMPORTANT]
>Netzwerk Websitecontroller-Sicherung und Wiederherstellung ist nicht aktuell in Windows Server 2016 verfügbar.
  
### <a name="bkmk_firewall"></a>Firewallverwaltung

Mit dieser Funktion von Netzwerkcontroller können Sie Firewall-Zugriffssteuerungsregeln für die virtuellen Computer für Ihre Arbeitsauslastungen konfigurieren und verwalten (Zulassen/Verweigern), die sowohl für den Ost/West- als auch den Nord/Süd-Netzwerkdatenverkehr in Ihrem Datencenter gelten. Die Firewallregeln werden im vSwitch-Port des virtuellen Computers für die Arbeitsauslastung bereitgestellt, sodass sie auf alle Arbeitsauslastungen im Datencenter angewendet werden. Unter Verwendung der Northbound-API können Sie die Firewallregeln für eingehenden und ausgehenden Datenverkehr über den virtuellen Computer für Ihre Arbeitsauslastungen definieren. Außerdem können Sie jede Firewallregel so konfigurieren, dass der über die Regel zugelassene oder abgelehnte Datenverkehr protokolliert wird.  

Weitere Informationen finden Sie unter [Datacenter Firewall – Übersicht](../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md).

### <a name="bkmk_slb"></a>Verwalten des Softwarelastenausgleichs

Diese Funktion von Netzwerkcontroller ermöglicht es Ihnen, mehrere Server zum Hosten derselben Arbeitsauslastung zu aktivieren, um hohe Verfügbarkeit und Skalierbarkeit bereitzustellen.  
  
Weitere Informationen finden Sie unter [Softwarelastenausgleich &#40;SLB&#41; für SDN](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md).  
  
### <a name="bkmk_virtual"></a>Verwalten des virtuellen Netzwerks

Diese Funktion von Netzwerkcontroller ermöglicht es Ihnen, die Hyper-V-Netzwerkvirtualisierung bereitzustellen und zu konfigurieren – virtuelle Hyper-V-Switches und virtuelle Netzwerkadapter auf einzelnen virtuellen Computern eingeschlossen – sowie Richtlinien für virtuelle Netzwerke zu speichern und anzuwenden.

Netzwerkcontroller unterstützt sowohl NVGRE (Network Virtualization Generic Routing Encapsulation) als auch VXLAN (Virtual Extensible Local Area Network).

### <a name="bkmk_gateway"></a>Verwalten des RAS-Gateways

Diese Funktion von Netzwerkcontroller können Sie bereitstellen, konfigurieren und Verwalten von virtuellen Computern (VMs), die Mitglieder eines RAS-Gateway-Pools und Gatewaydienste für Ihre Mandanten sind. Netzwerkcontroller ermöglicht es Ihnen, zum automatischen Bereitstellen von VMs, die RAS-Gateway mit den folgenden Gateway-Funktionen ausgeführt:

> [!NOTE]
> In System Center Virtual Machine Manager heißt RAS-Gateway dem Windows Server-Gateway.

- Hinzufügen von Entfernen von virtuellen Gatewaycomputern zum Cluster bzw. aus dem Cluster und Festlegen der erforderlichen Sicherungsstufe

- Standort-zu-Standort-VPN-Gatewaykonnektivität zwischen Remotemandantennetzwerken und Ihrem Datencenter unter Verwendung von IPsec

- Standort-zu-Standort-VPN-Gatewaykonnektivität zwischen Remotemandantennetzwerken und Ihrem Datencenter unter Verwendung von GRE (Generic Routing Encapsulation)

- Schicht 3-Weiterleitungsfunktion

- Border Gateway Protocol (BGP) routing, die Sie zum Verwalten des Routings von Netzwerkdatenverkehr zwischen VM-Netzwerken Ihrer Mandanten und Remotestandorten ermöglicht.

Netzwerkcontroller kann verschiedene Verbindungen eines Mandanten auf separaten Gateways platzieren. Sie können eine einzelne öffentliche IP-Adresse für alle Gateway-Verbindungen oder bei anderen öffentlichen IP-Adressen für eine Teilmenge der Verbindungen. Netzwerkcontroller protokolliert alle Gateway-Konfiguration und Zustandsänderungen, die für die Überwachung und Problembehandlung verwendet werden kann.

Weitere Informationen zu BGP finden Sie unter [Border Gateway Protocol &#40;BGP&#41;](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md).

Weitere Informationen auf dem RAS-Gateway finden Sie unter [RAS-Gateway für SDN](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md).

## <a name="network-controller-deployment-options"></a>Optionen zur netzwerkbereitstellung Controller

Um die Bereitstellung des Netzwerkcontrollers mithilfe von System Center Virtual Machine Manager- \(VMM\), finden Sie unter [richten Sie eine SDN-Netzwerkcontroller im VMM-Fabric](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller).

Zum Bereitstellen des Netzwerkcontrollers mithilfe von Skripts finden Sie unter [Bereitstellen von Software definierte Netzwerk-Infrastruktur mithilfe von Skripts](../../deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md).

Zum Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell finden Sie unter [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)
