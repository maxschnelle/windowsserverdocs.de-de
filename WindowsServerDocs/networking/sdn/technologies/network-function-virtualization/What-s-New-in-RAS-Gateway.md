---
title: Neuerungen beim RAS-Gateway
description: Sie können in diesem Thema verwenden, sich zu neuen Features für RAS-Gateway, ein softwarebasierter ist, mehrinstanzenfähiger, Border Gateway Protocol (BGP)-fähiger Router in Windows Server 2016.
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
ms.openlocfilehash: 5cc7d8bab3f2783750dbd723da745b1df3c2e462
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863021"
---
# <a name="whats-new-in-ras-gateway"></a>Neuerungen beim RAS-Gateway

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, sich zu neuen Features für RAS-Gateway, ein softwarebasierter ist, mehrinstanzenfähiger, Border Gateway Protocol (BGP)-fähiger Router in Windows Server 2016. Der RAS-Gateway mehrinstanzenfähige BGP-Router dient für Clouddienstanbieter (CSPs) und Unternehmen, die mehrinstanzenfähige virtuelle Netzwerke mithilfe der Hyper-V-Netzwerkvirtualisierung hosten.  
  
> [!NOTE]  
> RAS-Gateway ist in Windows Server 2012 R2 RRAS-Gateway benannt werden. und in System Center Virtual Machine Manager-RAS-Gateway ist mit dem Namen Windows Server-Gateway.  
  
Dieses Thema enthält die folgenden Abschnitte:  
  
-   [Konnektivitätsoptionen für die Standort-zu-Standort](#bkmk_s2s)  
  
-   [Gatewaypools](#bkmk_pools)  
  
-   [Gateway-Pool-Skalierbarkeit](#bkmk_gps)  
  
-   [Gateway-Pool-Redundanz M + N](#bkmk_m)  
  
-   [Route-Reflector](#bkmk_rr)  
  
## <a name="bkmk_s2s"></a>Konnektivitätsoptionen für die Standort-zu-Standort  
RAS-Gateway unterstützt jetzt drei Arten von VPN-Standort-zu-Standort-Verbindungen:  Internet Key Exchange Version 2 (IKEv2) Generic Routing Encapsulation (GRE), Standort-zu-Standort für virtuelle private Netzwerke (VPN) und Layer-3 (L3) VPN-Tunnel.  
  
Weitere Informationen zu GRE, finden Sie unter [GRE Tunneling in Windows Server 2016](../../../../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md).  
  
## <a name="bkmk_pools"></a>Gatewaypools  
In Windows Server 2016 können Sie gatewaypools verschiedener Typen erstellen. Gatewaypools enthalten viele Instanzen des RAS-Gateway und Weiterleiten von Netzwerkdatenverkehr zwischen physischen und virtuellen Netzwerken. Die einzelne Gateway-Funktionen – Internet Key Exchange Version 2 (IKEv2) ausführen, gatewaypools können Standort-zu-Standort für virtuelle private Netzwerke (VPN), Generic Routing Encapsulation (GRE) und Layer-3 (L3) VPN-Tunnel - oder des Pools kann alle diese ausführen Funktionen und Act als gemischte Pool.  
  
Sie können die Logik, die Sie bevorzugen, basierend auf der infrastrukturanforderungen gatewaypools erstellen. Beispielsweise können Sie die gatewaypools, die basierend auf einem der folgenden Eigenschaften erstellen.  
  
-   Tunneltypen (L3-VPN IKEv2-VPN GRE VPN)  
  
-   Kapazität  
  
-   Redundanzebene (Zuverlässigkeit basierend auf Ihrem Abrechnungsplan für Mandanten)  
  
-   Benutzerdefinierte Trennung für Kunden  
  
Weitere Informationen finden Sie unter [RAS-Gateway: hohe Verfügbarkeit](RAS-Gateway-High-Availability.md).  
  
## <a name="bkmk_gps"></a>Gateway-Pool-Skalierbarkeit  
Sie können ganz einfach einen gatewaypool nach oben oder unten skalieren durch Hinzufügen oder Entfernen der Gateway-VMs im Pool. Entfernen oder Hinzufügen des Gateways ist nicht die Dienste unterbrochen werden, die von einem Pool bereitgestellt werden. Sie können auch hinzufügen und entfernen die gesamte Pools von Gateways.  
  
Weitere Informationen finden Sie unter [RAS-Gateway: hohe Verfügbarkeit](RAS-Gateway-High-Availability.md).  
  
## <a name="bkmk_m"></a>Gateway-Pool-Redundanz M + N  
Jede gatewaypool ist M + N ist redundant. Dies bedeutet, dass ein bin "Anzahl der aktiven Gateway-VMs (VMs) werden" n "die Anzahl der standby-Gateway-VMs gesichert. M + N-Redundanz bietet mehr Flexibilität bei der Bestimmung der Grad an Zuverlässigkeit, die beim Bereitstellen des RAS-Gateways erforderlich sind. Anstatt nur eine standby-RAS-Gateway pro aktiven RAS-Gateway-VM – was bedeutet die einzige Konfigurationsoption mit Windows Server 2012 R2 – können Sie jetzt so viele standby VMs wie gewünscht konfigurieren. Das Network Controller Gateway Service Manager-Feature verwendet die standby-RAS-Gateway-VM-Kapazität effizient zuverlässige Failover bereitstellen, wenn ein aktiver RAS-Gateway-VM ein Fehler auftritt oder die Netzwerkverbindung unterbrochen.  
  
Weitere Informationen finden Sie unter [RAS-Gateway: hohe Verfügbarkeit](RAS-Gateway-High-Availability.md).  
  
## <a name="bkmk_rr"></a>Route-Reflector  
Die Route-Reflector Border Gateway Protocol (BGP) ist jetzt mit der RAS-Gateway enthalten und stellt eine Alternative zur BGP-full-Mesh-Topologie, die für die Route Synchronisierung zwischen Routern erforderlich ist. Bei der Synchronisierung vollständig vermaschte müssen alle BGP-Router mit allen anderen Routern in die Routingtopologie verbinden. Bei Verwendung von Route-Reflector ist die Route-Reflector jedoch der einzige Router, der mit allen anderen Routern, BGP-Clients, um so Route Synchronisierung zu vereinfachen und Reduzierung des Netzwerkverkehrs wird aufgerufen, eine Verbindung herstellt. Die Route-Reflector lernt alle Routen, berechnet der beste Routen und die beste Routen zu den BGP-Clients verteilt.  
  
Mit Windows Server 2016 können Sie einen einzelnen Mandanten RAS-Tunnel zum Beenden auf mehr als eine RAS-Gateway-VM konfigurieren. Dies bietet mehr Flexibilität für Cloud Service Providers bei Fällen, in denen kann nicht einem RAS-Gateway-VM erfüllen aller Anforderungen an die Netzwerkbandbreite der Mandanten-Verbindungen.  
  
Diese Funktion führt jedoch die zusätzliche Komplexität der Verwaltung der Route und effektive Synchronisierung von Routen zwischen den Remotestandorten Mandanten und deren virtuellen Ressourcen in der Cloud-Datencenter. Bereitstellen von Mandanten mit Verbindungen für mehrere RAS-Gateways führt auch zusätzliche Komplexität in der Konfiguration am Ende Unternehmen, in dem jeder mandantenstandort separate routing Nachbarn hat.  
  
Eine BGP-Route-Reflector Steuerungsebene behandelt diese Probleme, und es werden die CSP-internen Fabric-Bereitstellung für den Enterprise-Mandanten. Es folgen einige wichtige Punkte hinsichtlich der BGP-Route-Reflector, die in der RAS-Gateway enthalten und in den Netzwerkcontroller integriert.  
  
-   Eine Route-Reflector in einer Software Defined Networking-Bereitstellung ist eine logische Entität, die auf der Steuerungsebene zwischen den RAS-Gateways und dem Netzwerkcontroller befindet. Er wird jedoch nicht der Fall, in die Daten auf Datenebene routing berücksichtigt.  
  
-   Wenn Sie einen neuen Mandanten in Ihrem Rechenzentrum hinzufügen, konfiguriert den Netzwerkcontroller automatisch den ersten Mandanten RAS-Gateway als eine Route-Reflector.  
  
-   Jeder Mandant verfügt über eine entsprechende Route-Reflector, und es befindet sich auf einen der RAS-Gateway-VMs, die diesem Mandanten zugeordnet sind.  
  
-   Ein Route-Reflector-Mandanten fungiert als die Route-Reflector für alle RAS-Gateway-VMs, die dem Mandanten zugeordnet sind. Als der RAS-Gateway-Route-Reflector-Mandanten-computergateways sind die Route-Reflector-Clients. Die Route-Reflector führt die Route-Synchronisierung zwischen allen Clients der Route-Reflector so, dass die tatsächlichen Daten Path routing auftreten kann.  
  
-   Eine Route-Reflector bietet keine Route-Reflector-Dienste für das RAS-Gateway auf dem es konfiguriert ist.  
  
-   Eine Route-Reflector aktualisiert Netzwerkcontroller mit den Enterprise-Routen, die entsprechen, für Unternehmensstandorte des Mandanten. Dadurch können den Netzwerkcontroller für die erforderlichen Hyper-V-Netzwerkvirtualisierungs-Richtlinien auf das virtuelle Netzwerk des Mandanten für den Datenpfad für End-to-End-Zugriff konfigurieren.  
  
-   Wenn Ihre Enterprise-Kunden BGP-Routing in der Customer-Adressraum verwenden, ist die RAS-Gateway-Route-Reflector nur externe BGP (eBGP)-Nachbarn für alle Websites der entsprechenden Mandanten an. Dies gilt unabhängig von der Enterprise-Mandanten Tunnel Beendigung Punkte. Das heißt, unabhängig davon, welche RAS-Gateway-VM im CSP-Datencenter beendet die Standort-zu-Standort-VPN-Tunnel für eine mandantenwebsite, die eBGP-Peers für alle mandantenwebsites ist die Route-Reflector.  
  
Weitere Informationen finden Sie unter [RAS-Gateway: Bereitstellungsarchitektur](RAS-Gateway-Deployment-Architecture.md) und der Internet Engineering Task Force (IETF)-Anforderung für Kommentare Thema [RFC 4456 BGP-Route-Reflektion: Eine Alternative zur vollständigen Mesh internes BGP (IBGP)](https://tools.ietf.org/html/rfc4456).  
  

