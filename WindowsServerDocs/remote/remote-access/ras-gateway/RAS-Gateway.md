---
title: RAS-Gateway
description: Dieses Thema, das für IT-Experten gedacht ist, enthält eine Übersicht über das RAS-Gateway, einschließlich der Bereitstellungs Modi und Features des RAS-Gateways in Windows Server 2016.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: acaa46b7-09b1-4707-9562-116df8db17eb
ms.author: pashort
author: shortpatti
ms.date: 05/23/2018
ms.openlocfilehash: ebf2cc840be771707f23d7976b670baae96c1343
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367494"
---
# <a name="ras-gateway"></a>RAS-Gateway

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

RAS-Gateway ist ein Software Router und ein Gateway, das Sie im Einzel Mandanten Modus oder im mehr Instanzen fähigen Modus verwenden können.  
  
- Der **Modus mit nur einem Mandanten** ermöglicht Organisationen beliebiger Größe das Bereitstellen des Gateways als Außendienst (virtuelles privates Netzwerk, VPN) und DirectAccess-Server mit Internet Zugriff. Im Einzel Mandanten Modus können Sie das RAS-Gateway auf einem physischen Server oder virtuellen Computer (VM) bereitstellen, auf dem Windows Server 2016 ausgeführt wird.  
  
- Der mehr Instanzen fähige **Modus** ermöglicht clouddienstanbietern (Cloud Service Providers, CSPs) und Unternehmen die Verwendung des RAS-Gateways, um das Routing von Daten Center-und cloudnetzwerkdatenverkehr zwischen virtuellen und physischen Netzwerken, Bei einem mehr Instanzen fähigen Modus empfiehlt es sich, das RAS-Gateway auf virtuellen Computern bereitzustellen, auf denen Windows Server 2016 ausgeführt wird.  
  
> [!NOTE]  
> RAS-Gateway unterstützt IPv4 und IPv6, einschließlich IPv4-und IPv6-Weiterleitung. Wenn Sie das RAS-Gateway mit Network Address Translation (NAT) konfigurieren, wird nur NAT44 unterstützt.  
  
## <a name="who-will-be-interested-in-ras-gateway"></a>Wer ist für das RAS-Gateway interessiert?
  
Wenn Sie ein Systemadministrator, ein Netzwerk Architekt oder ein anderer IT-Experte sind, kann das RAS-Gateway unter einem oder mehreren der folgenden Umstände von Interesse sein:  
  
-   Sie entwerfen oder unterstützen eine IT-Infrastruktur für eine Organisation, die Hyper-V zum Bereitstellen virtueller Computer (VMs) in virtuellen Netzwerken nutzt oder die Nutzung plant.  
  
-   Sie entwerfen oder unterstützen IT-Infrastruktur für eine Organisation, die Cloudtechnologie bereitgestellt hat oder die Bereitstellung plant.  
  
-   Sie möchten eine umfassende Netzwerkverbindung zwischen physischen und virtuellen Netzwerken bereitstellen.  
  
-   Sie möchten den Kunden Ihrer Organisation Zugriff auf Ihre virtuellen Netzwerke über das Internet bereitstellen.  
  
-   Sie möchten den Mitarbeitern Ihrer Organisation Remote Zugriff auf Ihr Unternehmensnetzwerk bieten.  
  
-   Sie möchten Niederlassungen an verschiedenen physischen Standorten über das Internet verbinden.  
 
Dieses Thema, das für IT-Experten gedacht ist, enthält eine Übersicht über das RAS-Gateway, einschließlich Bereitstellungs Modi und Features für RAS-Gateways. 
  
Dieses Thema enthält die folgenden Abschnitte:  
  
  
-   [RAS-Gateway-Bereitstellungs Modi](#bkmk_modes)  
  
-   [Clustering des RAS-Gateways für hohe Verfügbarkeit](#bkmk_clustering)  
  
-   [RAS-Gatewayfeatures](#bkmk_features)  
  
-   [Bereitstellungs Szenarien für RAS-Gateways](#bkmk_deploy)  
  
-   [RAS-Gateway-Verwaltungs Tools](#bkmk_manage)  
  


  
## <a name="bkmk_modes"></a>RAS-Gateway-Bereitstellungs Modi  
RAS-Gateway umfasst die folgenden Bereitstellungs Modi:  
  
### <a name="single-tenant-mode"></a>Einzel Mandanten Modus  
In den meisten Organisationen ist die Verwendung des RAS-Gateways im Modus mit nur einem Mandanten die typische Konfiguration. Im Einzel Mandanten Modus können Sie das RAS-Gateway als Edge-VPN-Server, Edge-DirectAccess-Server oder beides gleichzeitig bereitstellen. In dieser Konfiguration stellt das RAS-Gateway Remote Mitarbeitern eine Verbindung mit Ihrem Netzwerk mithilfe von VPN-oder DirectAccess-Verbindungen bereit. Außerdem können Sie mit dem Modus für einzelne Mandanten Niederlassungen an verschiedenen physischen Standorten über das Internet verbinden.  
  
### <a name="multitenant-mode"></a>Mehr Instanzen fähiger Modus  
Wenn Ihre Organisation ein CSP oder ein Unternehmen mit mehreren Mandanten ist, können Sie das RAS-Gateway im mehrinstanzfähigen Modus bereitstellen, um Netzwerk Datenverkehr zu und von virtuellen und physischen Netzwerken bereitzustellen.  
  
Mehr Instanzen Fähigkeit ist die Fähigkeit einer cloudinfrastruktur, die Arbeits Auslastungen virtueller Computer mehrerer Mandanten zu unterstützen, Sie aber voneinander zu isolieren, während alle Arbeits Auslastungen in der gleichen Infrastruktur ausgeführt werden. Mehrere Arbeitsauslastungen eines einzelnen Mandanten können miteinander verbunden und remote verwaltet werden. Es gibt jedoch keine Verbindung zwischen diesen Systemen und den Arbeitsauslastungen anderer Mandanten, und auch die Remoteverwaltung durch andere Mandanten ist nicht möglich.  
  
Ein Unternehmen kann beispielsweise über viele verschiedene virtuelle Subnetze verfügen, die jeweils einer bestimmten Abteilung zugeordnet sind, z. B. Forschung und Entwicklung oder der Buchhaltung. In einem weiteren Beispiel verfügt ein CSP über viele Mandanten mit isolierten virtuellen Subnetzen in demselben physischen Rechenzentrum. In beiden Fällen kann das RAS-Gateway Datenverkehr an einen und von jedem Mandanten weiterleiten, während gleichzeitig die entworfene Isolation der einzelnen Mandanten gewahrt bleibt. Diese Funktion macht das RAS-Gateway mehr Instanzen fähig.  
  
Virtuelle Netzwerke werden mithilfe der Hyper-V-Netzwerkvirtualisierung erstellt, bei der es sich um eine Technologie handelt, die in Windows Server 2012 eingeführt wurde und in Windows Server 2016 verbessert wurde. RAS-Gateway ist in die Hyper-V-Netzwerkvirtualisierung integriert und kann Netzwerk Datenverkehr effektiv weiterleiten, wenn es viele verschiedene Kunden oder Mandanten gibt, die über isolierte virtuelle Netzwerke im selben Rechenzentrum verfügen.  
  
Die Hyper-V-Netzwerkvirtualisierung bietet die Möglichkeit, ein virtuelles Computernetzwerk (VM) bereitzustellen, das unabhängig vom zugrunde liegenden physischen Netzwerk ist. Bei VM-Netzwerken, die sich aus einem oder mehreren virtuellen Subnetzen zusammensetzen, wird der exakte physische Speicherort eines IP-Subnetzes von der Topologie des virtuellen Netzwerks entkoppelt. Daher können Sie Ihre lokalen Subnetze problemlos in die Cloud verschieben und gleichzeitig Ihre vorhandenen IP-Adressen und die Topologie in der Cloud beibehalten. Dank dieser Möglichkeit zur Aufrechterhaltung der Infrastruktur können vorhandene Dienste weiterhin verwendet werden, und zwar unabhängig von deren physischem Speicherort in den Subnetzen. Dies bedeutet, dass mit der Hyper-V-Netzwerkvirtualisierung eine nahtlose Hybrid-Cloud zur Verfügung steht.  
  
> [!NOTE]  
> Die Hyper-V-Netzwerkvirtualisierung ist eine netzwerküberlagerungs Technologie, die eine generische Routing Kapselung ([nvgre](https://tools.ietf.org/html/draft-sridharan-virtualization-nvgre-00)) für die Netzwerkvirtualisierung verwendet, die es Mandanten ermöglicht, ihren eigenen Adressraum zu nutzen und CSPs eine bessere Skalierbarkeit zu ermöglichen. VLANs für die Mandanten Isolation.  
  
In Windows Server 2016 leitet das RAS-Gateway Netzwerk Datenverkehr zwischen dem physischen Netzwerk und den VM-Netzwerkressourcen weiter, unabhängig davon, wo sich die Ressourcen befinden. Mithilfe des RAS-Gateways können Sie Netzwerk Datenverkehr zwischen physischen und virtuellen Netzwerken am selben physischen Standort oder an vielen verschiedenen physischen Standorten weiterleiten.  
  
Wenn Sie z. b. über ein physisches Netzwerk und ein virtuelles Netzwerk am gleichen physischen Standort verfügen, können Sie einen Computer, auf dem Hyper-V ausgeführt wird, der mit einer RAS-Gateway-VM konfiguriert ist, als Weiterleitungs Gateway bereitstellen und den Datenverkehr zwischen dem virtuellen und physischen Gas.  
  
Wenn Ihre virtuellen Netzwerke in der Cloud vorhanden sind, kann Ihr CSP ein RAS-Gateway bereitstellen, sodass Sie eine VPN-Site-to-Site-Verbindung zwischen dem VPN-Server und dem RAS-Gateway des virtuellen Netzwerks herstellen können. Wenn Sie diesen Link eingerichtet haben, können Sie über die VPN-Verbindung eine Verbindung mit Ihren virtuellen Ressourcen in der Cloud herstellen.  
  
Weitere Informationen finden Sie unter [hohe Verfügbarkeit des RAS-Gateways](../../../networking/sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md).  
  
## <a name="bkmk_clustering"></a>Clustering des RAS-Gateways für hohe Verfügbarkeit  
RAS-Gateway wird auf einem dedizierten Computer bereitgestellt, auf dem Hyper-V ausgeführt wird und der mit einem virtuellen Computer konfiguriert ist. Der virtuelle Computer wird dann als RAS-Gateway konfiguriert.  
  
Für hohe Verfügbarkeit von Netzwerkressourcen können Sie RAS-Gateway mit Failover bereitstellen, indem Sie zwei physische Host Server mit Hyper-V verwenden, die jeweils auch einen virtuellen Computer (VM) ausführen, der als Gateway konfiguriert ist. Die virtuellen Gatewaycomputer werden dann als Cluster konfiguriert, um einen Failoverschutz vor Netzwerkausfällen und Hardwarefehlern zu bieten.  
  
Wenn Ihre Organisation z. b. ein Unternehmen mit einer Private Cloud-Bereitstellung ist, benötigen Sie möglicherweise nur zwei RAS-Gateway-VMS, die jeweils auf einem anderen Computer installiert sind, auf dem Hyper-V ausgeführt wird. In diesem Szenario werden die virtuellen RAS-Gateway-Computer zu einem Cluster hinzugefügt, um Hochverfügbarkeit zu gewährleisten.  
  
Ein weiteres Beispiel: Wenn Ihre Organisation ein clouddienstanbieter (Cloud Service Provider, CSP) mit 200 Mandanten in Ihrem Daten Center ist, können Sie acht RAS-Gateway-VMS verwenden, wobei jedes Paar von gruppierten RAS-Gateway-VMS Routing Dienste für 50 Mandanten bereitstellt. In diesem Szenario haben zwei Computer, auf denen Hyper-V ausgeführt wird, jeweils vier VMS, die als RAS-Gateways konfiguriert sind. Anschließend konfigurieren Sie vier RAS-Gateway-VM-Cluster, die jeweils einen virtuellen Computer auf jedem Computer mit Hyper-V enthalten.  
  
Beim Bereitstellen des RAS-Gateways muss auf den Host Servern, auf denen Hyper-V ausgeführt wird, und den virtuellen Computern, die Sie als Gateways konfigurieren, Windows Server 2012 R2 oder Windows Server 2016 ausgeführt werden.  
  
## <a name="bkmk_features"></a>RAS-Gatewayfeatures  
RAS-Gateway umfasst die folgenden Funktionen:  
  
-   **Site-to-Site-VPN**. Diese RAS-Gatewayfunktion ermöglicht es Ihnen, zwei Netzwerke an verschiedenen physischen Standorten über das Internet mithilfe einer Site-to-Site-VPN-Verbindung zu verbinden. Wenn Sie über eine zentrale und mehrere Zweigstellen verfügen, können Sie an jedem Standort ein Edge-RAS-Gateway bereitstellen und Site-to-Site-Verbindungen erstellen, um den Netzwerk Datenverkehr zwischen den Standorten bereitzustellen. Für CSPs, die viele Mandanten in Ihrem Rechenzentrum hosten, bietet das RAS-Gateway eine mehrinstanzfähige Gatewaylösung, die ihren Mandanten den Zugriff auf und die Verwaltung Ihrer Ressourcen über Standort-zu-Standort-VPN-Verbindungen von Remote Standorten ermöglicht und den Netzwerk Datenverkehr zwischen virtuelle Ressourcen in Ihrem Daten Center und in Ihrem physischen Netzwerk.  
  
-   **Punkt-zu-Standort-VPN**. Diese RAS-Gatewayfunktion ermöglicht es Organisations Mitarbeitern oder Administratoren, von Remote Standorten aus eine Verbindung mit dem Netzwerk Ihrer Organisation herzustellen. Bei bereit Stellungen mit einem Mandanten des RAS-Gateways können Remote Mitarbeiter über eine VPN-Verbindung eine Verbindung mit Ihrem Unternehmensnetzwerk herstellen. Diese Verbindung ermöglicht es Ihnen, interne Netzwerkressourcen wie Intranetwebsites und Dateiserver zu verwenden. Für bereit Stellungen mit mehreren Mandanten können Mandanten Netzwerkadministratoren Punkt-zu-Standort-VPN-Verbindungen verwenden, um auf virtuelle Netzwerkressourcen im CSP-Daten Center zuzugreifen.  
  
-   **Dynamisches Routing mit Border Gateway Protocol (BGP)** . BGP verringert den Bedarf an manueller Routingkonfiguration auf Routern, da es ein dynamisches Routingprotokoll ist, das automatisch Routen zwischen Standorten lernt, die über die Standort-zu-Standort-VPN-Verbindungen verbunden sind. Wenn Ihre Organisation über mehrere Standorte verfügt, die mithilfe von BGP-fähigen Routern wie RAS-Gateway verbunden sind, ermöglicht BGP den Routern die automatische Berechnung und Verwendung gültiger Routen untereinander im Falle einer Netzwerk Unterbrechung oder eines Fehlers. Weitere Informationen finden Sie unter [RFC 4271](https://tools.ietf.org/html/rfc4271).  
  
-   **Netzwerk Adressübersetzung (Network Address Translation, NAT)** . Mithilfe der Netzwerk Adressübersetzung (Network Address Translation, NAT) können Sie eine Verbindung mit dem öffentlichen Internet über eine einzige Schnittstelle mit einer einzelnen öffentlichen IP-Adresse gemeinsam nutzen. Von den Computern im privaten Netzwerk werden private, nicht Routing fähige Adressen verwendet. In NAT werden die privaten Adressen der öffentlichen Adresse zugeordnet. Mithilfe dieses RAS-Gatewayfeatures können Organisations Mitarbeiter mit einzelinstanzbereitstellungen über das Gateway auf Internet Ressourcen zugreifen. Für CSPs ermöglicht diese Funktion Anwendungen, die auf Mandanten-VMS ausgeführt werden, auf das Internet zuzugreifen. Beispielsweise kann eine als Webserver konfigurierte Mandanten-VM externe Finanzressourcen kontaktieren, um Kreditkartentransaktionen zu verarbeiten.  

  
## <a name="bkmk_deploy"></a>Bereitstellungs Szenarien für RAS-Gateways  
Im folgenden finden Sie die empfohlenen Bereitstellungs Szenarien für das RAS-Gateway.  
  
-   **Unternehmens Edge-Bereitstellung**mit nur einem Mandanten Mit der Enterprise-Bereitstellung für einen einzelnen Mandanten können Sie mithilfe des Standort-zu-Standort-VPN-Features eine physische Verbindung mit mehreren anderen physischen Standorten über das Internet herstellen, und Border Gateway Protocol (BGP) ermöglicht Ihnen die Verwendung des dynamischen Routings. Sie können Remote Mitarbeitern auch den Zugriff auf Ihr Organisations Netzwerk mit Punkt-zu-Standort-VPN-Verbindungen und DirectAccess-Verbindungen ermöglichen. (DirectAccess-Verbindungen sind immer eingeschaltet. Außerdem bieten Sie den Vorteil, dass Sie Computer, die über DirectAccess verbunden sind, problemlos verwalten können, weil Sie immer verbunden sind, wenn Sie sich auf dem Internet befinden und mit dem Internet verbunden sind.) Sie können auch Single Tenant Enterprise RAS-Gateways mit NAT konfigurieren, damit Computer in Ihrem Intranet problemlos mit dem Internet kommunizieren können.  
  
-   **Edge-Bereitstellung des clouddienstanbieters**. Mit der mehr Instanzen fähigen RAS-Gateway-Bereitstellung für CSPs können Sie Ihren Mandanten alle Features anbieten, die bei der Bereitstellung von einem Unternehmen mit nur einem Mandanten zur Verfügung stehen. Standort-zu-Standort-VPN-Verbindungen zwischen virtuellen Mandanten Netzwerken in Ihrem Rechenzentrum und den Netzwerk Standorten des Mandanten über das Internet bedeuten, dass Mandanten immer nahtlos auf Ihre cloudressourcen zugreifen können. Der Punkt-zu-Standort-VPN-Zugriff für Mandanten bedeutet, dass Mandanten Administratoren jederzeit eine Verbindung mit Ihren virtuellen Netzwerken in Ihrem Rechenzentrum herstellen können, um Ihre Ressourcen zu verwalten. BGP bietet dynamisches Routing und behält die Mandanten mit ihren Assets, auch wenn Netzwerkprobleme im Internet oder an anderen Orten auftreten. Mit NAT können Mandanten-VMS eine Verbindung mit Ressourcen im Internet herstellen, z. b. Kreditkarten-Verarbeitungs Ressourcen.  
  
## <a name="bkmk_manage"></a>RAS-Gateway-Verwaltungs Tools  
Im folgenden finden Sie die Verwaltungs Tools für das RAS-Gateway.  
  
-   In Windows Server 2016 müssen Sie zum Bereitstellen eines RAS-gatewayrouters Windows PowerShell-Befehle verwenden. Weitere Informationen finden Sie unter [Remote Zugriffs-Cmdlets](https://docs.microsoft.com/powershell/module/remoteaccess) für Windows Server 2016 und Windows 10.  
  
-   In System Center 2012 R2 Virtual Machine Manager (VMM) wird das RAS-Gateway als Windows Server-Gateway bezeichnet. In der VMM-Softwareschnittstelle stehen eine begrenzte Anzahl von Border Gateway Protocol (BGP)-Konfigurationsoptionen zur Verfügung, einschließlich **lokaler BGP-IP-Adresse** und **autonomer System Nummern (ASN)** , **Liste der BGP-Peer-IP-Adressen**und **ASN-Werte.** . Sie können jedoch Windows PowerShell-BGP-Befehle per Remotezugriff verwenden, um alle anderen Features des Windows Server-Gateways zu konfigurieren. Weitere Informationen finden Sie unter [Virtual Machine Manager (VMM)](https://technet.microsoft.com/system-center-docs/vmm/vmm) und [Remote Zugriffs-Cmdlets](https://technet.microsoft.com/library/hh918399.aspx) für Windows Server 2016 und Windows 10.  
  
## <a name="related-topics"></a>Verwandte Themen
- [RAS-Gateway: Hohe Verfügbarkeit](../../../networking/sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)  
- [GRE-Tunneling in Windows Server](gre-tunneling-windows-server.md)
- [GRE-Tunneling für RAS-Gateway: Durchsatz und Leistung](RAS-Gateway-GRE-Perf.md)
