---
title: Neuerungen beim RAS-Gateway
description: In diesem Thema erfahren Sie mehr über die neuen Features für das RAS-Gateway, ein softwarebasierter, mehr Instanzen fähiger, Border Gateway Protocol (BGP)-fähiger Router in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 709cb192-313a-47b5-954e-eb5f6fee51a7
ms.author: lizross
author: eross-msft
ms.openlocfilehash: b65f4aa2d10b1bdf6c0d212a111a169bad23591a
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312884"
---
# <a name="whats-new-in-ras-gateway"></a>Neuerungen beim RAS-Gateway

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie mehr über die neuen Features für das RAS-Gateway, ein softwarebasierter, mehr Instanzen fähiger, Border Gateway Protocol (BGP)-fähiger Router in Windows Server 2016. Der mehrinstanzfähige RAS-BGP-Router ist für clouddienstanbieter (Cloud Service Providers, CSPs) und Unternehmen konzipiert, die mehrere virtuelle Mandanten Netzwerke mithilfe der Hyper-V-Netzwerkvirtualisierung  
  
> [!NOTE]  
> In Windows Server 2012 R2 hat das RAS-Gateway den Namen RRAS-Gateway. in System Center Virtual Machine Manager wird das RAS-Gateway als Windows Server-Gateway bezeichnet.  
  
Dieses Thema enthält folgende Abschnitte:  
  
-   [Optionen für die Standort-zu-Standort-Konnektivität](#bkmk_s2s)  
  
-   [Gatewaypools](#bkmk_pools)  
  
-   [Skalierbarkeit des gatewaypools](#bkmk_gps)  
  
-   [Mehr als die gatewaypoolpoolredundanz](#bkmk_m)  
  
-   [Routen Reflektor](#bkmk_rr)  
  
## <a name="site-to-site-connectivity-options"></a><a name="bkmk_s2s"></a>Optionen für die Standort-zu-Standort-Konnektivität  
Das RAS-Gateway unterstützt jetzt drei Arten von VPN-Standort-zu-Standort-Verbindungen: Internetschlüsselaustausch Version 2 (IKEv2) Site-to-Site-VPN-VPN-VPN-VPN-VPN-VPN-VPN-(Generic Routing Kapseln)-Tunnel.  
  
Weitere Informationen zu GRE finden Sie unter [GRE tunnelingin Windows Server 2016](../../../../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md).  
  
## <a name="gateway-pools"></a><a name="bkmk_pools"></a>Gatewaypools  
In Windows Server 2016 können Sie gatewaypools mit unterschiedlichen Typen erstellen. Gatewaypools enthalten viele Instanzen des RAS-Gateways und leiten Netzwerk Datenverkehr zwischen physischen und virtuellen Netzwerken weiter. Gatewaypools können alle einzelnen Gatewayfunktionen ausführen: Internetschlüsselaustausch Version 2 (IKEv2) Site-to-Site Virtual Private Networking (VPN), Layer 3 (L3)-VPN und generische Routing Kapselungs Tunnel (GRE), oder der Pool kann alle diese Vorgänge durchführen. fungiert als gemischter Pool und fungiert als gemischter Pool.  
  
Sie können gatewaypools mithilfe einer beliebigen Logik erstellen, die Sie basierend auf Ihren Infrastrukturanforderungen bevorzugen. Beispielsweise können Sie gatewaypools basierend auf den folgenden Merkmalen erstellen.  
  
-   Tunnel Typen (IKEv2-VPN, L3-VPN, GRE-VPN)  
  
-   Kapazität  
  
-   Redundanz Stufe (Zuverlässigkeit basierend auf Ihrem Abrechnungsplan für Mandanten)  
  
-   Angepasste Trennung für Kunden  
  
Weitere Informationen finden Sie unter [hohe Verfügbarkeit des RAS-Gateways](RAS-Gateway-High-Availability.md).  
  
## <a name="gateway-pool-scalability"></a><a name="bkmk_gps"></a>Skalierbarkeit des gatewaypools  
Sie können einen gatewaypool problemlos zentral hoch-oder herunterskalieren, indem Sie Gateway-VMS im Pool hinzufügen oder entfernen. Das Entfernen oder Hinzufügen von Gateways beeinträchtigt nicht die Dienste, die von einem Pool bereitgestellt werden. Sie können auch die gesamten Pools von Gateways hinzufügen und entfernen.  
  
Weitere Informationen finden Sie unter [hohe Verfügbarkeit des RAS-Gateways](RAS-Gateway-High-Availability.md).  
  
## <a name="mn-gateway-pool-redundancy"></a><a name="bkmk_m"></a>Mehr als die gatewaypoolpoolredundanz  
Jeder gatewaypool ist M + N redundant. Dies bedeutet, dass die Anzahl der aktiven Gateway-VMS (Virtual Gateway, VMS) durch eine "N"-Anzahl von virtuellen standbygatewaycomputern gesichert wird. Die Redundanz von M + N bietet Ihnen mehr Flexibilität bei der Ermittlung des Zuverlässigkeits Niveaus, das Sie bei der Bereitstellung des RAS-Gateways benötigen. Anstatt nur ein Standby-RAS-Gateway pro Active RAS-Gateway-VM zu verwenden, das die einzige Konfigurationsoption mit Windows Server 2012 R2 ist, können Sie nun beliebig viele Standby-VMS konfigurieren. Das Netzwerk Controller Gateway Service Manager Feature verwendet die VM-Kapazität des Standby-RAS-Gateways, um ein zuverlässiges Failover bereitzustellen, wenn ein aktiver RAS-Gateway-Computer ausfällt oder die Konnektivität verliert.  
  
Weitere Informationen finden Sie unter [hohe Verfügbarkeit des RAS-Gateways](RAS-Gateway-High-Availability.md).  
  
## <a name="route-reflector"></a><a name="bkmk_rr"></a>Routen Reflektor  
Der Border Gateway Protocol (BGP)-Routen Reflektor ist nun im RAS-Gateway enthalten und bietet eine Alternative zur vollständigen BGP-Mesh-Topologie, die für die Routen Synchronisierung zwischen Routern erforderlich ist. Bei der vollständigen Netzwerksynchronisierung müssen alle BGP-Router eine Verbindung mit allen anderen Routern in der Routing Topologie herstellen. Wenn Sie jedoch den Routen Reflektor verwenden, ist der Routen Reflektor der einzige Router, der mit allen anderen Routern verbunden ist, die als BGP-Clients bezeichnet werden. Dadurch wird die Routen Synchronisierung vereinfacht und der Netzwerk Datenverkehr reduziert. Der Routen Reflektor lernt alle Routen, berechnet die besten Routen und verteilt die besten Routen an seine BGP-Clients.  
  
Mit Windows Server 2016 können Sie die Remote Zugriffs Tunnel eines einzelnen Mandanten so konfigurieren, dass Sie auf mehr als einem virtuellen RAS-Gateway-Computer beendet werden. Dies bietet mehr Flexibilität für clouddienstanbieter, wenn eine RAS-Gateway-VM nicht alle Bandbreitenanforderungen der Mandanten Verbindungen erfüllen kann.  
  
Diese Funktion führt jedoch zu einer zusätzlichen Komplexität der Routen Verwaltung und effektiven Synchronisierungen von Routen zwischen den Remote Standorten des Mandanten und den zugehörigen virtuellen Ressourcen im cloudrechenzentrum. Wenn Mandanten Verbindungen mit mehreren RAS-Gateways bereitstellen, wird auch eine zusätzliche Komplexität der Konfiguration am Unternehmens Ende eingeführt, bei der jede Mandanten Site separate Routing Nachbarn hat.  
  
Ein BGP-Routen Reflektor in der Steuerungsebene löst diese Probleme und macht die interne CSP-Fabric-Bereitstellung für die Unternehmens Mandanten transparent. Im folgenden finden Sie einige wichtige Punkte zum BGP-Routen Reflektor, der im RAS-Gateway enthalten und in den Netzwerk Controller integriert ist.  
  
-   Ein Routen Reflektor in einer Software definierten Netzwerk Bereitstellung ist eine logische Entität, die sich auf der Steuerungsebene zwischen den RAS-Gateways und dem Netzwerk Controller befindet. Es ist jedoch nicht Teil des Routings auf Datenebene.  
  
-   Wenn Sie Ihrem Rechenzentrum einen neuen Mandanten hinzufügen, konfiguriert der Netzwerk Controller automatisch das erste Mandanten-RAS-Gateway als Routen Reflektor.  
  
-   Jeder Mandant verfügt über einen entsprechenden Routen Reflektor und befindet sich auf einem der RAS-Gateway-VMS, die diesem Mandanten zugeordnet sind.  
  
-   Ein mandantenweiterleitungs-Reflektor fungiert als Routen Reflektor für alle RAS-Gateway-VMS, die dem Mandanten zugeordnet sind. Andere Mandanten Gateways als der RAS-gatewayweiterleitungs-Reflektor sind die Routen Reflektor-Clients. Der Routen Reflektor führt die Routen Synchronisierung zwischen allen Routen reflektorclients aus, sodass das tatsächliche Routing des Daten Pfads erfolgen kann.  
  
-   Ein Routen Reflektor bietet keine Routen reflektordienste für das RAS-Gateway, auf dem es konfiguriert ist.  
  
-   Ein Routen Reflektor aktualisiert den Netzwerk Controller mit den Unternehmens Routen, die den Unternehmensstandorten des Mandanten entsprechen. Dadurch kann der Netzwerk Controller die erforderlichen Hyper-V-netzwerkvirtualisierungsrichtlinien im virtuellen Mandanten Netzwerk für den End-to-End-Datenpfad-Zugriff konfigurieren.  
  
-   Wenn Ihre Unternehmenskunden das BGP-Routing im Kunden Adressraum verwenden, ist der RAS-gatewayweiterleitungs-Reflektor der einzige externe BGP-Nachbar (EBGP) für alle Standorte des entsprechenden Mandanten. Dies gilt unabhängig von den Tunnel Beendigungs Punkten des Unternehmens. Anders ausgedrückt: unabhängig davon, welche RAS-Gateway-VM im CSP-Rechenzentrum den Standort-zu-Standort-VPN-Tunnel für eine Mandanten Site beendet, ist der EBGP-Peer für alle Mandanten Sites der Routen Reflektor.  
  
Weitere Informationen finden Sie unter [Bereitstellungs Architektur des RAS-Gateways](RAS-Gateway-Deployment-Architecture.md) und im IETF-Request (Internet Engineering Task Force) Request for Comments Topic [RFC 4456 BGP Route Reflection: eine Alternative zum vollständigen Mesh Internal BGP (IBGP)](https://tools.ietf.org/html/rfc4456).  
  

