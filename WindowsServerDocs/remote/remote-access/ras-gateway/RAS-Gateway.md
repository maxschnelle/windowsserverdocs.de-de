---
title: RAS-Gateway
description: Diese Thema ausgetauscht, das für Informationstechnologie (IT)-Experten vorgesehen ist, bietet allgemeine Informationen zum RAS-Gateway, einschließlich der RAS-Gateway-Bereitstellungsmodus und welche Features in Windows Server 2016.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: acaa46b7-09b1-4707-9562-116df8db17eb
ms.author: pashort
author: shortpatti
ms.date: 05/23/2018
ms.openlocfilehash: 8fc1c97d7c2a8694e56cc36b5501a82081b3db23
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812341"
---
# <a name="ras-gateway"></a>RAS-Gateway

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

RAS-Gateway ist ein Softwarerouter und Gateway, das Sie in den einzelnen Mandanten oder mehrinstanzenfähigen Modus verwenden können.  
  
- **Einzelinstanzanwendung** Modus können Organisationen jeder Größe das Gateway als äußere, oder Internetzugriff Edge virtuelles privates Netzwerk (VPN) und DirectAccess-Server bereitstellen. Im einzelmandantenmodus können Sie die RAS-Gateway auf einem physischen Server oder virtuellen Computer (VM) unter Windows Server 2016 bereitstellen.  
  
- **Mehrinstanzenmodus** können Clouddienstanbieter (CSPs) und Unternehmen RAS-Gateway zum Aktivieren von Rechenzentrum und cloud Weiterleitung von Netzwerkdatenverkehr zwischen virtuellen und physischen Netzwerken, die auch über das Internet verwenden. Für mehrinstanzenmodus empfiehlt es sich, dass Sie RAS-Gateway für virtuelle Computer bereitstellen, auf denen Windows Server 2016 ausgeführt werden.  
  
> [!NOTE]  
> RAS-Gateway unterstützt IPv4 und IPv6, einschließlich der IPv4- und IPv6-Weiterleitung. Wenn Sie RAS-Gateway mit den Netzwerkzugriffsschutz (Network Address Translation, NAT) konfigurieren, wird nur NAT44 unterstützt.  
  
## <a name="who-will-be-interested-in-ras-gateway"></a>Wer ist beim RAS-Gateway interessant?
  
Wenn Sie ein Systemadministrator, Netzwerkarchitekten oder andere IT-Professionals sind, möglicherweise RAS-Gateways Sie in eine oder mehrere der folgenden Situationen von Bedeutung sein:  
  
-   Sie entwerfen oder unterstützen eine IT-Infrastruktur für eine Organisation, die Hyper-V zum Bereitstellen virtueller Computer (VMs) in virtuellen Netzwerken nutzt oder die Nutzung plant.  
  
-   Sie entwerfen oder unterstützen IT-Infrastruktur für eine Organisation, die Cloudtechnologie bereitgestellt hat oder die Bereitstellung plant.  
  
-   Sie möchten eine umfassende Netzwerkverbindung zwischen physischen und virtuellen Netzwerken bereitstellen.  
  
-   Sie möchten Kunden Ihrer Organisation Zugriff auf ihren virtuellen Netzwerken über das Internet bereitzustellen.  
  
-   Möchten Sie die Mitarbeiter Ihres Unternehmens mit Remotezugriff auf das Netzwerk Ihrer Organisation bereitstellen.  
  
-   Möchten Sie Büros an verschiedenen physischen Standorten über das Internet zu verbinden.  
 
Diese Thema ausgetauscht, das für Informationstechnologie (IT)-Experten vorgesehen ist, bietet allgemeine Informationen zum RAS-Gateway, einschließlich der RAS-Gateway-Bereitstellungsmodus und welche Features. 
  
Dieses Thema enthält die folgenden Abschnitte:  
  
  
-   [RAS-Gateway-Bereitstellungsmodi](#bkmk_modes)  
  
-   [Clustering von RAS-Gateway für hohe Verfügbarkeit](#bkmk_clustering)  
  
-   [RAS-Gateway – Features](#bkmk_features)  
  
-   [RAS-Gateway-Bereitstellungsszenarien](#bkmk_deploy)  
  
-   [RAS-Gateway-Verwaltungstools](#bkmk_manage)  
  


  
## <a name="bkmk_modes"></a>RAS-Gateway-Bereitstellungsmodi  
RAS-Gateway enthält die folgenden Bereitstellungsmodi.  
  
### <a name="single-tenant-mode"></a>Einzelmandantenmodus  
Für die meisten Organisationen ist die Verwendung von RAS-Gateway im einzelmandantenmodus die typische Konfiguration. Im einzelmandantenmodus können Sie gleichzeitig die RAS-Gateway als ein Edge-VPN-Server, ein Edge-DirectAccess-Server oder beides bereitstellen. In dieser Konfiguration bietet RAS-Gateway Remotemitarbeiter konnektivitätspunkt für Ihr Netzwerk über VPN oder DirectAccess-Verbindungen. Darüber hinaus können mit einzelmandantenmodus Sie Büros an verschiedenen physischen Standorten über das Internet zu verbinden.  
  
### <a name="multitenant-mode"></a>Mehrinstanzenmodus  
Wenn Ihre Organisation über ein CSP oder in einem Unternehmen mit mehreren Mandanten ist, können Sie die RAS-Gateway im mehrinstanzenfähigen Modus verwenden, geben Sie die Weiterleitung von Netzwerkdatenverkehr zu und von virtuellen und physischen Netzwerken bereitstellen.  
  
Mehrinstanzenfähigkeit ist die Fähigkeit einer Cloud-Infrastruktur zur Unterstützung von arbeitsauslastungen virtueller Computer mehrerer Mandanten isolieren sie noch voneinander, während alle arbeitsauslastungen in der gleichen Infrastruktur ausgeführt. Mehrere Arbeitsauslastungen eines einzelnen Mandanten können miteinander verbunden und remote verwaltet werden. Es gibt jedoch keine Verbindung zwischen diesen Systemen und den Arbeitsauslastungen anderer Mandanten, und auch die Remoteverwaltung durch andere Mandanten ist nicht möglich.  
  
Ein Unternehmen kann beispielsweise über viele verschiedene virtuelle Subnetze verfügen, die jeweils einer bestimmten Abteilung zugeordnet sind, z. B. Forschung und Entwicklung oder der Buchhaltung. In einem weiteren Beispiel verfügt ein CSP über viele Mandanten mit isolierten virtuellen Subnetzen in demselben physischen Rechenzentrum. In beiden Fällen können RAS-Gateway Datenverkehr zu und von den einzelnen Mandanten weiterleiten und gleichzeitig die bestehende Isolation für jeden Mandanten. Diese Funktion macht das RAS-Gateway mehrinstanzenfähig.  
  
Virtuelle Netzwerke werden erstellt, mit Hyper-V-Netzwerkvirtualisierung eine Technologie handelt, die wurde in Windows Server 2012 eingeführt und wird in Windows Server 2016 verbessert. RAS-Gateway ist mit Hyper-V-Netzwerkvirtualisierung integriert und kann Netzwerkdatenverkehr effektiv weiterleiten, wo es gibt viele unterschiedliche Kunden – oder Mandanten - isoliert haben virtuellen Netzwerke im gleichen Datencenter.  
  
Hyper-V-Netzwerkvirtualisierung bietet die Möglichkeit, einem Netzwerk virtueller Maschinen (VM) bereitzustellen, die unabhängig von dem zugrunde liegenden physischen Netzwerk ist. Bei VM-Netzwerke, die sich von einem oder mehreren virtuellen Subnetzen zusammensetzen, wird der exakte physische Speicherort eines IP-Subnetzes von der Topologie des virtuellen Netzwerks entkoppelt. Daher können Sie die auf lokale Subnetze problemlos verschieben, auf die Cloud, während Sie gleichzeitig Ihre IP-Adressen und die Topologie in der Cloud. Dank dieser Möglichkeit zur Aufrechterhaltung der Infrastruktur können vorhandene Dienste weiterhin verwendet werden, und zwar unabhängig von deren physischem Speicherort in den Subnetzen. Dies bedeutet, dass mit der Hyper-V-Netzwerkvirtualisierung eine nahtlose Hybrid-Cloud zur Verfügung steht.  
  
> [!NOTE]  
> Hyper-V-Netzwerkvirtualisierung ist eine Overlay-netzwerktechnologie mit Network Virtualization Generic Routing Encapsulation ([NVGRE](https://tools.ietf.org/html/draft-sridharan-virtualization-nvgre-00)), damit können Mandanten ihren eigenen Adressraum nutzen, und CSPs erhalten eine bessere Skalierbarkeit als mögliche Verwendung von VLANs zur mandantenisolation.  
  
In Windows Server 2016 leitet die RAS-Gateway Netzwerkdatenverkehr zwischen dem physischen Netzwerk und VM-Netzwerkressourcen, unabhängig davon, wo sich die Ressourcen befinden. Sie können die RAS-Gateway verwenden, den Netzwerkdatenverkehr zwischen physischen und virtuellen Netzwerken an demselben physischen Standort oder an vielen verschiedenen physischen Standorten weiterleiten.  
  
Z. B. Wenn Sie sowohl auf einem physischen Netzwerk und ein virtuelles Netzwerk am selben physischen Speicherort verfügen, können Sie bereitstellen einen Computer unter Hyper-V, die mit einer RAS-Gateway-VM als weiterleitungsgateway dienen und Weiterleiten von Datenverkehr zwischen virtuellen und physischen konfiguriert ist Netzwerke.  
  
In ein weiteres Beispiel: Wenn Ihre virtuellen Netzwerke in der Cloud befinden kann Ihren CSP ein RAS-Gateway bereitstellen, damit Sie eine virtuelles privates Netzwerk (VPN)-Standort-zu-Standort-Verbindung zwischen Ihrem VPN-Server und CSPs-RAS-Gateway erstellen können; Wenn dieser Link eingerichtet wird, die Sie mit die virtuellen Ressourcen in der Cloud über die VPN-Verbindung verbinden können.  
  
Weitere Informationen finden Sie unter [RAS-Gateway: hohe Verfügbarkeit](../../../networking/sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md).  
  
## <a name="bkmk_clustering"></a>Clustering von RAS-Gateway für hohe Verfügbarkeit  
RAS-Gateway wird auf einem dedizierten Computer bereitgestellt, die Hyper-V ausgeführt wird und mit einem virtuellen Computer konfiguriert ist. Der virtuelle Computer wird dann als RAS-Gateway konfiguriert.  
  
Für hohe Verfügbarkeit von Netzwerkressourcen können Sie RAS-Gateway mit Failover bereitstellen, mithilfe von zwei physische Hostserver mit Hyper-V, die jede auch Ausführen eines virtuellen Computers (VM), das als Gateway konfiguriert ist. Die virtuellen Gatewaycomputer werden dann als Cluster konfiguriert, um einen Failoverschutz vor Netzwerkausfällen und Hardwarefehlern zu bieten.  
  
Z. B. können Ihre Organisation ein Unternehmen mit einer privaten Cloudbereitstellung ist, Sie nur zwei RAS-Gateway-VMs benötigen, von denen jede auf einem anderen Computer mit Hyper-V installiert ist. In diesem Szenario werden die RAS-Gateway-VMs in einem Cluster für hohe Verfügbarkeit hinzugefügt.  
  
Ein weiteres Beispiel wenn Ihre Organisation über einen Cloud-Dienstanbieter (CSP) mit 200 Mandanten in Ihrem Datencenter, ist können acht RAS-Gateway-VMs, für jedes Paar an gruppierten RAS-Gateway-VMs bereitstellen Routingdienste für 50 Mandanten Sie. In diesem Szenario müssen zwei Computer, auf denen Hyper-V jedes vier virtuelle Computer, der als RAS-Gateways konfiguriert werden. Anschließend konfigurieren Sie vier RAS-Gateway-VM-Cluster, jeder mit einem virtuellen Computer für jeden Computer mit Hyper-V-Cluster.  
  
Wenn Sie RAS-Gateways bereitstellen den Hostservern mit Hyper-V und die virtuellen Computer, die Sie konfigurieren, wie Gateways Windows Server 2012 R2 oder Windows Server 2016 ausgeführt werden müssen.  
  
## <a name="bkmk_features"></a>RAS-Gateway – Features  
RAS-Gateway enthält die folgenden Funktionen.  
  
-   **Standort-zu-Standort-VPN-**. Dieses Feature für die RAS-Gateway können Sie zwei Netzwerke an verschiedenen physischen Standorten mit einer Standort-zu-Standort-VPN-Verbindung über das Internet zu verbinden. Wenn Sie eine zentrale und mehreren Zweigniederlassungen verfügen, können bereitstellen eine Edge-RAS-Gateway an jedem Standort und Standort-zu-Standort-Verbindungen zum Bereitstellen des Netzwerkdatenverkehrs zwischen den Standorten erstellen. Für CSPs, die viele Mandanten in ihren Rechenzentren hosten, stellt der RAS-Gateway eine mehrinstanzenfähige gatewaylösung Mandanten zugreifen auf und verwalten ihre Ressourcen über Standort-zu-Standort-VPN-Verbindungen von Remotestandorten aus, und, mit der Fluss von Netzwerkdatenverkehr zwischen virtuellen Ressourcen in Ihrem Datencenter und dem physischen Netzwerk.  
  
-   **Punkt-zu-Standort-VPN-**. Dieses Feature für die RAS-Gateway kann Mitarbeiter des Unternehmens "oder" Administratoren ", von Remotestandorten aus eine Verbindung mit dem Netzwerk Ihrer Organisation. Für einzelnen Mandanten Bereitstellungen des RAS-Gateways können Remotemitarbeiter eine VPN-Verbindung mit dem Netzwerk Ihrer Organisation verbinden. Diese Verbindung können sie interne Netzwerkressourcen, z. B. Intranet-Websites und Dateiservern zu verwenden. Bei mehrinstanzenfähigen Bereitstellungen können Netzwerk Mandantenadministratoren Punkt-zu-Standort-VPN-Verbindungen Sie Ressourcen des virtuellen Netzwerks im CSP-Datencenter zugreifen.  
  
-   **Dynamisches routing mit Border Gateway Protocol (BGP)**. BGP verringert den Bedarf an manueller Routingkonfiguration auf Routern, da es ein dynamisches Routingprotokoll ist, das automatisch Routen zwischen Standorten lernt, die über die Standort-zu-Standort-VPN-Verbindungen verbunden sind. Wenn Ihre Organisation über mehrere Standorte, die verfügt mithilfe von BGP-fähigen Routern, z. B. RAS-Gateway verbunden sind, kann BGP die Router automatisch berechnen und verwenden die gültige Routen miteinander im Falle einer Störung des Netzwerks oder Fehler. Weitere Informationen finden Sie unter [RFC 4271](https://tools.ietf.org/html/rfc4271).  
  
-   **Netzwerkadressübersetzung (NAT)**. Netzwerkadressübersetzung (NAT) können Sie eine Verbindung mit dem öffentlichen Internet über eine einzelne Schnittstelle für eine einzelne öffentliche IP-Adresse freigeben. Verwenden Sie die Computer im privaten Netzwerk private, nicht routingfähige Adressen. NAT wird die privaten Adressen in die öffentliche Adresse zugeordnet. Dieses Feature für die RAS-Gateway kann Mitarbeiter der Organisation mit der Bereitstellung der einzelnen Mandanten, den Zugriff auf Internetressourcen über das Gateway. Für CSPs können Anwendungen, die auf die Mandanten-VMs, die Zugriff auf das Internet ausgeführt werden. Beispielsweise kann ein Mandanten-VM, der als Webserver konfiguriert ist externe finanzielle Ressourcen zum Verarbeiten von Kreditkartentransaktionen wenden Sie sich an.  

  
## <a name="bkmk_deploy"></a>RAS-Gateway-Bereitstellungsszenarien  
Es folgen die empfohlenen Bereitstellungsszenarien für RAS-Gateway.  
  
-   **Enterprise Edge: Bereitstellung der einzelnen Mandanten**. Mit den einzelnen Mandanten Enterprise-Bereitstellung, Sie können eine Verbindung herstellen physisch auf mehreren physischen Standorten über das Internet mithilfe des Standort-zu-Standort-VPN feature - und Border Gateway Protocol (BGP) können Sie mit dynamischem routing. Sie können auch remote Mitarbeitern den Zugriff auf das Netzwerk Ihrer Organisation mit Punkt-zu-Standort-VPN-Verbindungen und DirectAccess-Verbindungen bereitstellen. (DirectAccess-Verbindungen sind immer aktiviert, und geben Sie außerdem den Vorteil, den Sie problemlos Computer verwalten können, die über DirectAccess möglich, verbunden sind, da sie verbunden sind, wenn sie auf und Internet verbunden sind.) Sie können auch einzelinstanzanwendung Enterprise-RAS-Gateways mit NAT, konfigurieren, damit Computer in Ihrem Intranet problemlos mit dem Internet kommunizieren können.  
  
-   **Cloud-Service-Anbieter-Edge - mehrinstanzenfähige Bereitstellung**. RAS-Gateway mehrinstanzenfähige Bereitstellung für CSPs können Sie Ihre Mandanten bieten alle Funktionen, die mit der Enterprise-Edge-Bereitstellung einzelner Mandant verfügbar sind. Standort-zu-Standort-VPN-Verbindungen zwischen virtuellen mandantennetzwerken in Ihrem Datencenter und die Mandanten-Netzwerkadressen, über das Internet bedeuten, dass es sich bei Mandanten nahtlosen Zugriff auf ihre Cloudressourcen immer verfügen. Punkt-zu-Standort-VPN-Zugriff für Mandanten bedeutet, dass Mandantenadministratoren immer auf ihre virtuellen Netzwerke in Ihrem Rechenzentrum zum Verwalten ihrer Ressourcen eine Verbindung herstellen können. BGP bietet dynamisches routing und Mandanten, die mit ihren Ressourcen verbunden werden, selbst wenn Netzwerkprobleme, auf das Internet oder an anderer Stelle auftreten speichert. Und NAT ermöglicht die Mandanten-VMs in Verbindung mit Ressourcen im Internet, wie z. B. Kreditkarte Verarbeitungsressourcen.  
  
## <a name="bkmk_manage"></a>RAS-Gateway-Verwaltungstools  
Es folgen die Verwaltungstools für RAS-Gateway.  
  
-   In Windows Server 2016 zum Bereitstellen eines RAS-Gateway-Routers, müssen Sie Windows PowerShell-Befehle verwenden. Weitere Informationen finden Sie unter [Remotezugriff-Cmdlets](https://technet.microsoft.com/library/hh918399.aspx) für Windows Server 2016 und Windows 10.  
  
-   In System Center 2012 R2 Virtual Machine Manager (VMM), heißt das RAS-Gateway dem Windows Server-Gateway. Eine begrenzte Anzahl von Border Gateway Protocol (BGP)-Konfigurationsoptionen sind verfügbar, in der VMM-Softwareschnittstelle, einschließlich **lokale BGP-IP-Adresse** und **autonome Systemnummern (ASN)**,  **Liste der BGP-Peer-IP-Adressen**, und **ASN Werte**. Sie können jedoch Windows PowerShell-BGP-Befehle per Remotezugriff verwenden, um alle anderen Features des Windows Server-Gateways zu konfigurieren. Weitere Informationen finden Sie unter [Virtual Machine Manager (VMM)](https://technet.microsoft.com/system-center-docs/vmm/vmm) und [Remotezugriff-Cmdlets](https://technet.microsoft.com/library/hh918399.aspx) für Windows Server 2016 und Windows 10.  
  
## <a name="related-topics"></a>Verwandte Themen
- [RAS-Gateway: Hohe Verfügbarkeit](../../../networking/sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)  
- [GRE-Tunneling in WindowsServer](gre-tunneling-windows-server.md)
- [RAS-Gateway-GRE-Tunnel-Durchsatz und Leistung](RAS-Gateway-GRE-Perf.md)
