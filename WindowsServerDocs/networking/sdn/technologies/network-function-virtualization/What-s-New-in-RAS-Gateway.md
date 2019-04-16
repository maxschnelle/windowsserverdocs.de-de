---
title: Neuerungen beim RAS-Gateway
description: Sie können in diesem Thema erfahren Sie über die neuen Features für RAS-Gateway, ein softwarebasierter ist, mehrinstanzenfähiger, Border Gateway Protocol (BGP)-fähigen Router in Windows Server 2016 verwenden.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 709cb192-313a-47b5-954e-eb5f6fee51a7
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1a9ac762f6cd80d3889cf72478b7a7f8ce9e5cb7
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-ras-gateway"></a>Neuerungen beim RAS-Gateway

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema erfahren Sie über die neuen Features für RAS-Gateway, ein softwarebasierter ist, mehrinstanzenfähiger, Border Gateway Protocol (BGP)-fähigen Router in Windows Server 2016 verwenden. Der RAS-Gateway mehrinstanzenfähige BGP-Router dient für Clouddienstanbieter (CSPs) und Unternehmen, die mehrere Mandanten virtuelle Netzwerke mithilfe von Hyper-V-Netzwerkvirtualisierung hosten.  
  
> [!NOTE]  
> In Windows Server 2012 R2 wird der RAS-Gateway-RRAS-Gateway benannt. und in System Center Virtual Machine Manager und RAS-Gateway ist mit dem Namen Windows Server-Gateway.  
  
Dieses Thema enthält die folgenden Abschnitte.  
  
-   [Optionen für die Standort-zu-Standort-Netzwerkkonnektivität](#bkmk_s2s)  
  
-   [Gateway-Pools](#bkmk_pools)  
  
-   [Gateway-Pool Skalierbarkeit](#bkmk_gps)  
  
-   [M + N Gateway-Pool-Redundanz](#bkmk_m)  
  
-   [Route-Reflector](#bkmk_rr)  
  
## <a name="bkmk_s2s"></a>Optionen für die Standort-zu-Standort-Netzwerkkonnektivität  
RAS-Gateway unterstützt jetzt drei Arten von VPN-Standort-zu-Standort-Verbindungen: Internet Key Exchange Version 2 (IKEv2) Tunnel Standort-zu-Standort virtuelles privates Netzwerk (VPN), VPN-Layer 3 (L3) und Generic Routing Encapsulation (GRE).  
  
Weitere Informationen zu GRE, finden Sie unter [GRE-Tunneling in Windows Server 2016](../../../../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md).  
  
## <a name="bkmk_pools"></a>Gateway-Pools  
In Windows Server 2016 können Sie das Gateway Pools verschiedener Typen erstellen. Gateway-Pools enthalten viele Instanzen des RAS-Gateway und Weiterleiten von Netzwerkdatenverkehr zwischen physischen und virtuellen Netzwerken. Gateway-Pools können führen Sie die Funktionen der einzelnen Gateway - Internet Key Exchange Version 2 (IKEv2) Standort-zu-Standort virtuelles privates Netzwerk (VPN), VPN-Layer 3 (L3) und Generic Routing Encapsulation (GRE) Tunnel - oder Pool führen Sie alle diese Funktionen und als eine gemischte Pool fungieren kann.  
  
Sie können die Logik, den Sie bevorzugen basierend auf Ihrer infrastrukturanforderungen Gateway-Pools erstellen. Beispielsweise können Sie das Gateway-Adresspools basierend auf eine der folgenden Eigenschaften erstellen.  
  
-   Tunneltypen (IKEv2-VPN-L3-VPN GRE VPN)  
  
-   Kapazität  
  
-   Redundanzebene (Zuverlässigkeit auf der Grundlage Ihrer Abrechnung Plans für Mandanten)  
  
-   Benutzerdefinierte Trennung für Kunden  
  
Weitere Informationen finden Sie unter [RAS-Gateway: hohe Verfügbarkeit](RAS-Gateway-High-Availability.md).  
  
## <a name="bkmk_gps"></a>Gateway-Pool Skalierbarkeit  
Sie können ganz einfach einen Gateway-Pool nach oben oder unten skalieren durch Hinzufügen oder Entfernen der Gateway-VMs im Pool. Zum Entfernen oder Hinzufügen eines Gateways wird nicht die Dienste unterbrochen werden, die von einem Pool bereitgestellt werden. Sie können auch hinzufügen und entfernen ganze Pools von Gateways.  
  
Weitere Informationen finden Sie unter [RAS-Gateway: hohe Verfügbarkeit](RAS-Gateway-High-Availability.md).  
  
## <a name="bkmk_m"></a>M + N Gateway-Pool-Redundanz  
Alle Gateway-Pool ist M + N redundant. Dies bedeutet, dass eine bin "Anzahl der aktiven Gateway-VMs (virtuelle Computer)" n "die Anzahl der standby-Gateway-VMs gesichert werden. M + N Redundanz bietet Ihnen mehr Flexibilität bei der Bestimmung der Maß an Zuverlässigkeit, die Sie benötigen, wenn Sie RAS-Gateway bereitstellen. Anstatt nur eine pro active RAS-Gateway-VM - der Konfiguration mit Windows Server 2012 R2 kann nur - standby RAS-Gateway können Sie jetzt beliebig viele standby VMs wie nötig konfigurieren. Das Netzwerk Controller Remotedesktopgateway-Dienst-Manager-Feature verwendet die standby-RAS-Gateway-VM-Kapazität effizient zuverlässiges Failover bereitstellen, wenn ein aktiver RAS-Gateway-VM ausfällt oder die Verbindung unterbrochen.  
  
Weitere Informationen finden Sie unter [RAS-Gateway: hohe Verfügbarkeit](RAS-Gateway-High-Availability.md).  
  
## <a name="bkmk_rr"></a>Route-Reflector  
Das Border Gateway Protocol (BGP) Route-Reflector ist jetzt mit RAS-Gateway enthalten und stellt eine Alternative zu BGP-full-Mesh-Topologie, die für die Route Synchronisierung zwischen Routern erforderlich ist. Mit full-Mesh-Synchronisierung müssen alle BGP-Router mit allen Routern in die Weiterleitungstopologie verbinden. Bei Verwendung der Route-Reflector ist die Route-Reflector jedoch nur Routers, der mit allen anderen Routern, BGP-Clients, dadurch vereinfacht Route Synchronisierung und Reduzierung des Netzwerkverkehrs bezeichnet eine Verbindung herstellt. Die Route-Reflector lernt alle Routen, berechnet der beste Routen und die besten Routen zu den BGP-Clients verteilt.  
  
Mit Windows Server 2016 können Sie eines einzelnen Mandanten RAS-Tunnel zum Beenden auf mehrere RAS-Gateway-VM konfigurieren. Dies bietet mehr Flexibilität für Cloud-Dienstanbieter bei Situationen, in denen ein RAS-Gateway-VM erfüllen kann nicht alle der Anforderungen an Netzwerkbandbreite, die Mandanten-Verbindungen.  
  
Diese Funktion wird jedoch der zusätzliche Komplexität der Route Management und effektive Synchronisierung von Routen zwischen der Mandanten-remote-Standorte und Ihre eigenen virtuellen Ressourcen in der Cloud-Datencenter eingeführt. Bereitstellen von Mandanten mit Verbindungen für mehrere RAS-Gateways Komplexität auch in Konfiguration am Ende Unternehmen, in jeder mandantenstandort separate routing Nachbarn haben wird.  
  
Eine BGP-Route-Reflector in der Steuerelement-Ebene löst diese Probleme und macht die CSP-interne Fabric-Bereitstellung für den Enterprise-Mandanten transparent. Im folgenden werden einige wichtige Punkte zu den BGP-Route-Reflector, die RAS-Gateway enthaltenen und mit dem Netzwerkcontroller integriert ist.  
  
-   Eine Route-Reflector in einer Software Defined Networking-Bereitstellung ist eine logische Entität, die sich auf der Steuerelement-Ebene zwischen den RAS-Gateways und Netzwerkcontroller befindet. Er wird jedoch nicht, Daten Ebene Routing berücksichtigt.  
  
-   Wenn Sie einen neuen Mandanten in Ihrem Datencenter hinzufügen, konfiguriert Netzwerkcontroller automatisch die ersten Mandanten RAS-Gateway als eine Route-Reflector.  
  
-   Jeder Mandant hat eine entsprechende Route-Reflector, und es befindet sich auf einen der RAS-Gateway-VMs, die die Mandanten zugeordnet sind.  
  
-   Ein Mandant Route-Reflector fungiert als Route-Reflector für alle RAS-Gateway-VMs, die Mandanten zugeordnet sind. Mandanten-computergateways als RAS-Gateway-Route-Reflector sind die Route-Reflector-Clients. Die Route-Reflector führt Route Synchronisierung zwischen allen Route-Reflector-Clients, damit die tatsächlichen Daten Path routing auftreten kann.  
  
-   Eine Route-Reflector bietet keine Route-Reflector-Dienste für das RAS-Gateway auf dem es konfiguriert ist.  
  
-   Eine Route-Reflector aktualisiert Netzwerkcontroller mit der auf dem Mandanten Unternehmensstandorte entsprechen unternehmensrouten. Dadurch können Netzwerkcontroller zum Konfigurieren der erforderlichen Hyper-V-Netzwerkvirtualisierung Richtlinien auf das virtuelle Netzwerk des Mandanten für Datenpfad für End-to-End-Zugriff.  
  
-   Wenn Ihre Enterprise-Kunden BGP-Routing in der Kunden-Adressbereich verwenden, wird der RAS-Gateway-Route-Reflector nur externe BGP (eBGP) Nachbarn für alle Sites des entsprechenden Mandanten. Dies gilt unabhängig von der Enterprise-Mandanten-Tunnel-Endpunkte. Anders ausgedrückt, unabhängig davon, welche RAS-Gateway-VM im CSP Datacenter beendet die Standort-zu-Standort-VPN-Tunnel für einen Standort des Mandanten, die eBGP Peer für alle Standorte der Mandanten ist die Route-Reflector.  
  
Weitere Informationen finden Sie unter [RAS-Gateway: Bereitstellungsarchitektur](RAS-Gateway-Deployment-Architecture.md) und der Internet Engineering Task Force (IETF) Request für Kommentare Thema [RFC 4456 BGP Route Reflektion: eine Alternative zum vollständigen Mesh internes BGP (IBGP)](https://tools.ietf.org/html/rfc4456).  
  

