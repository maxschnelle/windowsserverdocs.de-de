---
title: Remotezugriff
description: Dieses Thema enthält eine Übersicht über die Remotezugriffs-Serverrolle in Windows Server 2016.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 05/18/2018
ms.openlocfilehash: faf12ad22678fa58ea933613759e3e8414966bca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818361"
---
# <a name="remote-access"></a>Remotezugriff

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

Der RAS-Handbuch bietet einen Überblick über die Remotezugriffs-Serverrolle in Windows Server 2016 und umfasst die folgenden Themen:

- [Always On-VPN-Bereitstellungshandbuch](vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)
- [Border Gateway Protocol &#40;BGP&#41;](bgp/Border-Gateway-Protocol-BGP.md)
- [RAS Gateway](ras-gateway/RAS-Gateway.md) 
- [RAS-Server-Rolle-Dokumentation](ras/Remote-Access-Server-Role-Documentation.md)
- [RAS-Gateway für SDN](../../networking/sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)
- [Virtuelle Private Netzwerke (VPN)](vpn/vpn-top.md)
 
Weitere Informationen zu anderen netzwerktechnologien, finden Sie unter [Netzwerkfunktionen in Windows Server 2016](https://docs.microsoft.com/windows-server/networking/networking).

Der RAS-Rolle ist eine logische Gruppierung von folgenden verwandten netzwerkzugriffstechnologien: [Remote Access Service (RAS)](#bkmk_da), [Routing](#bkmk_rras), und [Webanwendungsproxy](#bkmk_proxy). Diese Technologien sind die *Rollendienste* der Serverrolle "Remotezugriff". Bei der Installation der Serverrolle "Remotezugriff" mit der **Hinzufügen von Rollen und Features Assistenten** oder Windows PowerShell können Sie eine oder mehrere dieser drei Rollendienste installieren.

>[!IMPORTANT]
>Versuchen Sie nicht zum Bereitstellen von Remotezugriff auf einem virtuellen Computer \(VM\) in Microsoft Azure. Verwenden Remote Access in Microsoft Azure wird nicht unterstützt. Sie können nicht Remote Access in einer Azure-VM verwenden, zum Bereitstellen von VPN, DirectAccess oder jede andere RAS-Funktion in Windows Server 2016 oder früheren Versionen von Windows Server. Weitere Informationen finden Sie unter [Unterstützung der Microsoft-Serversoftware für Microsoft Azure-Computern](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).

## <a name="bkmk_da"></a>RAS-Dienst \(RAS\) -RAS-Gateway

Bei der Installation der **DirectAccess und VPN (RAS)** Rollendienst Sie das Remote Access Service-Gateway bereitstellen \( **RAS-Gateway**\). Sie können das RAS-Gateway einen einzelnen Mandanten RAS-Gateway virtuelles privates Netzwerk bereitstellen \(VPN\) Server, einem mehrinstanzenfähigen RAS-VPN-Gateway-Server und als DirectAccess-Server.

- **RAS-Gateway – einzelner Mandant**. Mithilfe von RAS-Gateway können Sie VPN-Verbindungen, die Endbenutzern zu ermöglichen, mit dem Remotezugriff, Netzwerk und Ressourcen Ihrer Organisation bereitstellen. Wenn Ihre Clients auf Windows 10 ausgeführt werden, können Sie Always On-VPN-, bereitstellen, die eine dauerhafte Verbindung zwischen Clients und das Netzwerk Ihrer Organisation verwaltet, wenn der Remotecomputer mit dem Internet verbunden sind. Mit RAS-Gateway, Sie können auch eine Standort-zu-Standort-VPN-Verbindung zwischen zwei Servern an verschiedenen Standorten, z. B. zwischen Ihrem primären Büro und einer Zweigstelle, zu erstellen und Network Address Translation \(NAT\) , damit Benutzer in der Netzwerk kann externe Ressourcen, z. B. das Internet zugreifen. Darüber hinaus unterstützt die RAS-Gateway Border Gateway Protocol (BGP), mit der dynamischen routing-Dienste bereitstellt, wenn Ihre Remotestandorten auch Edge-Gateways verfügen, die Unterstützung von BGP.

- **RAS-Gateway - Multitenant**. Sie können RAS-Gateway als mehrinstanzenfähige, softwarebasierte Edge-Gateway und Router bereitstellen, bei der Verwendung von Hyper\-V-Netzwerkvirtualisierung oder Sie haben die VM-Netzwerke, virtuelle lokale Netzwerke bereitgestellt \(VLANs\). Mit dem RAS-Gateway Cloud Service Providers \(CSPs\) und Unternehmen können Datacenter zu aktivieren und cloud-Weiterleitung von Netzwerkdatenverkehr zwischen virtuellen und physischen Netzwerken, die auch über das Internet. Mit dem RAS-Gateway können Ihre Mandanten damit p2s-VPN-Verbindungen von überall aus auf ihre VM-Netzwerkressourcen im Datencenter verwenden. Sie können Mandanten auch Standort-zu-Standort-VPN-Verbindungen zwischen ihren Remotestandorten und Ihrem CSP-Datencenter bereitstellen. Darüber hinaus können Sie das RAS-Gateway mit BGP für dynamisches routing konfigurieren, und Sie können die Netzwerkadressübersetzung \(NAT\) Internetzugriff für virtuelle Computer in VM-Netzwerken bereitstellen.

>[!IMPORTANT]
> Das RAS-Gateway mit mehreren Mandanten ist auch in Windows Server 2012 R2 verfügbar.

- **Always On-VPN**. Always On-VPN-ermöglicht Remotebenutzern den sicheren gemeinsam genutzte Ressourcen, Websites des Unternehmensintranets und -Anwendungen in einem internen Netzwerk zugreifen, ohne eine VPN-Verbindung. 

Weitere Informationen finden Sie unter [RAS-Gateway](ras-gateway/RAS-Gateway.md) und [Border Gateway Protocol (BGP)](bgp/Border-Gateway-Protocol-BGP.md).

## <a name="bkmk_rras"></a>Routing

Sie können den Remotezugriff zum Weiterleiten von Netzwerkdatenverkehr zwischen Subnetzen auf Ihrem lokalen Netzwerk verwenden. Routing bietet Unterstützung für LAN-Router mit BGP, Routing Information Protocol (RIP) und Multicast-fähigen Routern, die mit Internet Group Management Protocol (IGMP)-Routern (Network Address Translation, NAT). Als Router mit vollem Funktionsumfang können Sie RAS bereitstellen, auf einem Server-Computer oder als virtueller Computer (VM) auf einem Computer, auf dem Hyper-V ausgeführt wird.

Zum Installieren von Remote-Zugriff im LAN-Router entweder verwenden Sie das Hinzufügen von Rollen und Features-Assistenten im Server-Manager, und wählen die **RAS** -Serverrolle und die **Routing** Rollendienst; oder geben Sie folgenden Befehl Befehl an einer Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE.

```  
Install-RemoteAccess -VpnType RoutingOnly
```  

## <a name="bkmk_proxy"></a>Webanwendungsproxy

Webanwendungsproxy ist ein Remotezugriff-Rollendienst in Windows Server 2016. Der Webanwendungsproxy bietet Reverseproxyfunktionen für Webanwendungen in Ihrem Unternehmensnetzwerk, damit Benutzer außerhalb des Unternehmensnetzwerks von allen Geräten auf die Anwendungen zugreifen können. Webanwendungsproxy bereits authentifiziert Zugriff auf Webanwendungen mit Active Directory-Verbunddienste (AD FS) und fungiert zudem als AD FS-Proxy.

Um den Remotezugriff als Webanwendungs-Proxyserver installieren zu können, entweder verwenden Sie das Hinzufügen von Rollen und Features-Assistenten im Server-Manager, und wählen die **RAS** -Serverrolle und die **Web Application Proxy** Rollendienst; oder Geben Sie den folgenden Befehl an einer Windows PowerShell-Eingabeaufforderung, und drücken Sie dann die EINGABETASTE.  

```  
Install-RemoteAccess -VpnType SstpProxy  
```  

Weitere Informationen finden Sie unter [Web Application Proxy](https://technet.microsoft.com/windows-server-docs/identity/web-application-proxy/web-application-proxy-windows-server).


---