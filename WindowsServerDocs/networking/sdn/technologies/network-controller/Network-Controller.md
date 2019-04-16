---
title: Netzwerkcontroller
description: Dieses Thema enthält eine Übersicht über Netzwerkcontroller in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 31f3fa4e-cd25-4bf3-89e9-a01a6cec7893
ms.author: pashort
author: shortpatti
ms.openlocfilehash: acb9abbd716e9930fb01431e7004abb72a7da10c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="network-controller"></a>Netzwerkcontroller

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Neue bietet in Windows Server 2016 Netzwerkcontroller einer zentralen, programmierbaren Automatisierung zu verwalten, Konfiguration, Überwachung und Problembehandlung von virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum. 

Mithilfe von Netzwerkcontroller können Sie die Konfiguration der Netzwerkinfrastruktur, sondern die manuelle Konfiguration von Netzwerkgeräten und Diensten automatisieren.

> [!NOTE]
> Zusätzlich zu diesem Thema ist die folgende Netzwerk-Controller-Dokumentation verfügbar.
> - [Netzwerk-Controller mit hoher Verfügbarkeit](network-controller-high-availability.md)
> - [Installation und Anforderungen an die Vorbereitung für die Bereitstellung von Netzwerkcontroller](../../plan/Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)  
> - [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)  
> - [Installieren Sie die Netzwerk-Controller-Serverrolle mit Server-Manager](Install-the-Network-Controller-server-role-using-Server-Manager.md)
> - [Schritte nach der Bereitstellung für den Netzwerkcontroller](post-deploy-steps-nc.md)
> - [Netzwerk-Controller-Cmdlets](https://technet.microsoft.com/library/mt576401.aspx) 

## <a name="bkmk_overview"></a>Netzwerkcontroller – Übersicht

Netzwerkcontroller ist eine hoch verfügbare und skalierbare Serverrolle, und bietet eine Programmierschnittstellen Benutzeroberfläche \(API\), die Kommunikation zwischen Netzwerkcontroller mit dem Netzwerk ermöglicht, und eine zweite API, die die Kommunikation mit Netzwerkcontroller ermöglicht.

Sie können Netzwerkcontroller in der Domäne und nicht der Domäne Umgebungen bereitstellen. In domänenumgebungen authentifiziert Netzwerkcontroller Benutzern und Geräten mithilfe von Kerberos; in einer Umgebung nicht in einer Domäne müssen Sie Zertifikate für die Authentifizierung bereitstellen.

>[!IMPORTANT]
>Stellen Sie die Serverrolle "Netzwerkcontroller" auf physischen Hosts nicht. Sie müssen die Netzwerk-Controller-Serverrolle auf einem virtuellen Hyper-V-Computer installieren, zum Bereitstellen von Netzwerkcontroller \(VM\), die auf einem Hyper-V-Host installiert ist. Nachdem Sie Netzwerkcontroller auf virtuellen Computern auf drei verschiedenen Hyper\-V-Hosts installiert haben, müssen Sie die Hyper\-V-Hosts für die Software Defined Networking \(SDN\) durch Hinzufügen von Hosts des Netzwerkcontrollers mithilfe von Windows PowerShell-Befehl aktivieren **neu NetworkControllerServer**. Auf diese Weise aktivieren Sie das Lastenausgleichsmodul für SDN-Software funktioniert. Weitere Informationen finden Sie unter [neu NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver).

Netzwerkcontroller kommuniziert mit Netzwerkgeräten, Dienste und Komponenten mithilfe der Southbound-API. Mit der Southbound-API kann Netzwerkcontroller Netzwerkgeräte zu ermitteln, Dienstkonfigurationen und alle benötigten Informationen über das Netzwerk zu sammeln. Zusätzlich stellt die Southbound-API Netzwerkcontroller einen Pfad zum Senden von Informationen an der Netzwerkinfrastruktur, z. B. Änderungen an der Konfiguration, die Sie erstellt haben.

Die Northbound-API von Netzwerkcontroller bietet Ihnen die Möglichkeit zum Sammeln von Netzwerkinformationen aus Netzwerkcontroller und verwenden es zum Überwachen und Konfigurieren des Netzwerks.

Die Northbound-API von Netzwerkcontroller können Sie konfigurieren, überwachen, Problembehandlung und neue Geräte im Netzwerk mithilfe von Windows PowerShell, die Representational State Transfer \(REST\)-API oder einer verwaltungsanwendung mit einer grafischen Benutzeroberfläche, z. B. System Center Virtual Machine Manager bereitstellen.

>[!NOTE]
>Die Northbound-API von Netzwerkcontroller wird als REST-Schnittstelle implementiert.

Sie können Ihr datencenternetzwerk mit Netzwerkcontroller verwalten, mithilfe von verwaltungsanwendungen wie System Center Virtual Machine Manager-\(SCVMM\) und System Center Operations Manager-\(SCOM\), da Netzwerkcontroller können Sie konfigurieren, überwachen, Programmieren und Problembehandlung der Netzwerkinfrastruktur, die von ihr gesteuert werden.

Mit Windows PowerShell, der REST-API oder einer verwaltungsanwendung, können Sie Netzwerkcontroller zum Verwalten der folgenden physischen und virtuellen Netzwerkinfrastruktur verwenden:

- Hyper-V-VMs und virtuelle switches

- Datacenter Firewall

- Remote Access Service \(RAS\) mehrinstanzenfähige Gateways, virtuelle Gateways und Gateway-pools

- Software-Lastenausgleich

In der folgenden Abbildung verwendet ein Administrator ein Verwaltungstool, die interagiert direkt mit Netzwerkcontroller. Netzwerkcontroller enthält Informationen zur Netzwerkinfrastruktur, einschließlich der virtuellen und physischen Infrastruktur, um das Verwaltungstool und führt konfigurationsänderungen gemäß der Administrator Aktionen aus, wenn das Tool verwenden.  

![Netzwerkcontroller – Übersicht](../../../media/Network-Controller/NetController_overview.png)  

Wenn Sie Netzwerkcontroller in einer testumgebung bereitstellen, können Sie die Netzwerk-Controller-Serverrolle ausführen, auf einem virtuellen Hyper-V-\(VM\), die auf einem Hyper-V-Host installiert ist.

Für hohe Verfügbarkeit in größeren Datencentern können Sie einen Cluster bereitstellen, mithilfe von drei virtuellen Maschinen, die auf drei oder mehreren Hyper-V-Hosts installiert sind. Weitere Informationen finden Sie unter [Netzwerk Netzwerkcontroller – hohe Verfügbarkeit](network-controller-high-availability.md).

## <a name="bkmk_features"></a>Funktionen von Netzwerkcontroller

Die folgenden Funktionen von Netzwerkcontroller können Sie konfigurieren und Verwalten von virtuellen und physischen Netzwerkgeräten und Diensten.  
  
-   [Firewall-Verwaltung](#bkmk_firewall)  
  
-   [Verwalten des Softwarelastenausgleichs](#bkmk_slb)  
  
-   [Des virtuellen Netzwerks](#bkmk_virtual)  
  
-   [RAS-Gateway-Management](#bkmk_gateway)

>[!IMPORTANT]
>Netzwerk-Controller-Sicherung und Wiederherstellung ist derzeit nicht verfügbar in Windows Server 2016.
  
### <a name="bkmk_firewall"></a>Firewall-Verwaltung

Diese Funktion von Netzwerkcontroller können Sie konfigurieren und Verwalten von Zulassen/Verweigern Firewall-Zugriffssteuerungsregeln für Ihre Workload VMs für OST-West und Nord/Süd-Netzwerkdatenverkehr in Ihrem Rechenzentrum. Die Firewallregeln werden im vSwitch-Port des virtuellen angewandten und damit sie auf Ihre Workload im Datencenter verteilt werden. Die Northbound-API verwenden, können Sie die Firewallregeln für eingehenden und ausgehenden Datenverkehr über den virtuellen Computer definieren. Sie können auch konfigurieren, dass jede Firewallregel, um den Datenverkehr zu protokollieren, der zugelassen oder verweigert werden, indem Sie die Regel wurde.  

Weitere Informationen finden Sie unter [Datacenter Firewall (Übersicht)](../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md).

### <a name="bkmk_slb"></a>Verwalten des Softwarelastenausgleichs

Diese Funktion von Netzwerkcontroller können Sie mehrere Server zum Hosten derselben Workload hohe Verfügbarkeit und Skalierbarkeit zu aktivieren.  
  
Weitere Informationen finden Sie unter [Lastenausgleich & #40; SLB & #41; für SDN](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md).  
  
### <a name="bkmk_virtual"></a>Des virtuellen Netzwerks

Diese Funktion von Netzwerkcontroller können Sie zum Bereitstellen und Konfigurieren von Hyper-V-Netzwerkvirtualisierung, einschließlich des virtuellen Hyper-V-Switches und virtuelle Netzwerkadapter auf einzelnen virtuellen Computern, und speichern und Richtlinien für virtuelle Netzwerke zu verteilen.

Netzwerkcontroller unterstützt sowohl die Network Virtualization Generic Routing Encapsulation (NVGRE) als auch die Virtual Extensible Local Area Network (VXLAN).

### <a name="bkmk_gateway"></a>RAS-Gateway-Management

Diese Funktion von Netzwerkcontroller können Sie bereitstellen, konfigurieren und Verwalten von virtuellen Computern (VMs), die Mitglieder einer RAS-Gateway-Pool Gatewaydienste für Ihre Mandanten sind. Netzwerkcontroller ermöglicht es Ihnen automatisch ausgeführter virtueller Maschinen auf RAS-Gateway mit den folgenden Gateway-Funktionen bereitstellen:

> [!NOTE]
> In System Center Virtual Machine Manager wird RAS-Gateway mit Windows Server-Gateway bezeichnet.

- Hinzufügen und Entfernen von Gateway-VMs aus dem Cluster angeben, inwieweit der Sicherung erforderlich.

- Standort-zu-Standort virtuelles privates Netzwerk (VPN)-gatewaykonnektivität zwischen remotemandantennetzwerken und Ihrem Datencenter unter Verwendung von IPsec.

- Standort-zu-Standort-VPN-gatewaykonnektivität zwischen remotemandantennetzwerken und Ihrem Datencenter unter Verwendung von Generic Routing Encapsulation (GRE).

- Layer-3-Weiterleitungsfunktion.

- Border Gateway Protocol (BGP) weiterleiten, können Sie zum Verwalten des Routings von Netzwerkdatenverkehr zwischen VM-Netzwerken Ihrer Mandanten und Remotestandorten.

Netzwerkcontroller kann weitere Verbindungen einen Mandanten auf separaten Gateways platzieren. Sie können eine einzelne öffentliche IP-Adresse für alle Gateway-Verbindungen verwenden oder anderen öffentlichen IP-Adressen für eine Teilmenge der Verbindungen. Netzwerkcontroller protokolliert alle Gatewaykonfiguration und Zustandsänderungen, die für die Überwachung und Problembehandlung verwendet werden können.

Weitere Informationen zu BGP finden Sie unter [Border Gateway Protocol & #40; BGP & #41; ](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md).

Weitere Informationen auf dem RAS-Gateway finden Sie unter [RAS-Gateway für SDN](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md).

## <a name="network-controller-deployment-options"></a>Netzwerk-Controller-Bereitstellungsoptionen

Zum Bereitstellen von Netzwerkcontroller mithilfe von System Center Virtual Machine Manager-\(VMM\) finden Sie unter [richten Sie ein SDN-Netzwerkcontroller in der VMM-Fabric](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller).

Zum Bereitstellen des Netzwerkcontrollers mithilfe von Skripts finden Sie unter [Bereitstellen einer Software definiert Netzwerk-Infrastruktur mithilfe von Skripts](../../deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md).

Zum Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell finden Sie unter [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)
