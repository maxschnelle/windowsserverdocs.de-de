---
title: Schritt 3 planen eine Clusterbereitstellung mit Lastenausgleich
description: Dieses Thema ist Teil des Leitfadens Bereitstellen des Remotezugriffs in einem Cluster unter Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7540c17b-81de-47de-a04f-3247afa26f70
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8efeb29bf07b572d5e2faef677349690d4282b4d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281185"
---
# <a name="step-3-plan-a-load-balanced-cluster-deployment"></a>Schritt 3 planen eine Clusterbereitstellung mit Lastenausgleich

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Der nächste Schritt ist die Konfiguration des Lastenausgleichs und die Bereitstellung des Clusters zu planen.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|3.1 Planen des Lastenausgleichs|Entscheiden Sie, ob Windows-Netzwerklastenausgleich (NLB) oder einem externen Lastenausgleich (ELB) verwenden.|  
|3.2 Planen der IP-HTTPS|Wenn ein selbst signiertes Zertifikat nicht verwendet wird, benötigt der RAS-Server ein SSL-Zertifikat auf jedem Server im Cluster, um die IP-HTTPS-Verbindungen zu authentifizieren.|  
|3.3-Plan für die VPN-Clientverbindungen|Beachten Sie die Anforderungen für VPN-Clientverbindungen.|  
|3.4 Planen des Netzwerkadressenservers|Wenn die Netzwerkadressenserver-Website auf dem RAS-Server gehostet wird, und ein selbstsigniertes Zertifikat wird nicht verwendet, stellen Sie sicher, dass jeder Server im Cluster ein Serverzertifikat zur Authentifizierung der Verbindung an die Website verfügt.|  
  
## <a name="bkmk_2_1_Plan_LB"></a>3.1 Planen des Lastenausgleichs  
Remotezugriff kann auf einem einzelnen Server oder auf einem RAS-Server-Cluster bereitgestellt werden. Den Datenverkehr zum Cluster möglich Lastenausgleich ausgeführt werden, um hohe Verfügbarkeit und Skalierbarkeit für DirectAccess-Clients bereitzustellen. Es gibt zwei Lastenausgleich Ladeoptionen aus:  
  
-   **Windows-NLB**-Windows-Netzwerklastenausgleich ist eine Funktion von Windows Server. Um es zu verwenden, erfordern keine zusätzlichen Hardware, da alle Server im Cluster für die Verwaltung der Datenverkehrslast verantwortlich sind. Windows-NLB unterstützt maximal acht Server in einem Cluster den Remotezugriff.  
  
-   **Externer Lastenausgleich**-Verwenden eines externen Lastenausgleichs erfordert externen Hardware, um die Datenverkehrslast zwischen RAS-Server-Cluster zu verwalten. Darüber hinaus unterstützt die Verwendung eines externen Lastenausgleichs maximal 32 RAS-Server in einem Cluster. Sind einige Punkte zu bedenken, wenn der externe Lastenausgleich konfigurieren:  
  
    -   Der Administrator muss stellen Sie sicher, dass die virtuelle IP-Adressen über den RAS-Assistenten zum Laden Lastenausgleich konfiguriert werden auf die externen Load balancer (z. B. F5 Big-Ip Local Traffic Manager-System) verwendet. Wenn der externe Lastenausgleich aktiviert ist, wird die IP-Adressen für die externen und internen Schnittstellen werden höher gestuft werden, um virtuelle IP-Adressen und auf den lastenausgleichsmodulen angewandten werden müssen. Dies erfolgt, damit der Administrator nicht verfügt, um den DNS-Eintrag für den öffentlichen Namen der Bereitstellung des Clusters zu ändern. Darüber hinaus werden die IPSec-Tunnel-Endpunkte auf dem Server-IP-Adressen abgeleitet. Wenn der Administrator den separaten virtuellen IP-Adressen bereitstellt, wird der Client nicht für die Verbindung mit dem Server sein. Siehe Beispiel für die Konfiguration von DirectAccess mit externen Lastenausgleich in 3.1.1 Konfigurationsbeispiel für den externen Lastenausgleich.  
  
    -   Lastenausgleich von 6to4- und ISATAP unterstützt viele externe Load balancer (einschließlich F5) nicht. Wenn der RAS-Server als ISATAP-Router ist, sollten die ISATAP-Funktion auf einem anderen Computer verschoben werden. Auch wenn sich ISATAP-Funktion auf einem anderen Computer befindet, benötigen die DirectAccess-Server systemeigenen IPv6-Konnektivität mit ISATAP-Routers. Beachten Sie, dass die Verbindung vor dem Konfigurieren von DirectAccess vorhanden sein soll.  
  
    -   Für den externen Lastenausgleich Wenn Teredo verwendet werden wurde, benötigen der RAS-Server zwei aufeinander folgende öffentliche IPv4-Adressen als dedizierte IP-Adressen. Die virtuelle IP-Adressen des Clusters muss auch zwei aufeinander folgende öffentliche IPv4-Adressen verfügen. Dies gilt nicht für den Windows-Netzwerklastenausgleich, in dem nur die virtuelle IP-Adressen des Clusters zwei aufeinander folgende öffentliche IPv4-Adressen benötigen. Falls Sie Teredo nicht verwendet wird, sind zwei aufeinander folgende IP-Adressen nicht erforderlich.  
  
    -   Der Administrator kann vom Windows-Netzwerklastenausgleich in externen Load Balancer und umgekehrt wechseln. Beachten Sie, dass der Administrator aus dem externen Load Balancer Windows NLB wechseln kann, wenn er mehr als 8-Server in der externen Load Balancer-Bereitstellung verfügt.  
  
### <a name="ELBConfigEx"></a>3.1.1 externen Load Balancer-Konfigurationsbeispiel  
Dieser Abschnitt beschreibt die Konfigurationsschritte zum Aktivieren von eines externen Lastenausgleichs auf einer neuen Bereitstellung von Remotezugriff. Wenn Sie einen Load Balancer verwenden, kann remotezugriffsclusters wie in der folgenden Abbildung aussehen, in denen RAS-Server mit dem Unternehmensnetzwerk über einen Lastenausgleich im internen Netzwerk und über einen Load Balancer mit dem Internet verbunden sind mit dem externen Netzwerk verbunden ist:  
  
![Externe Load Balancer-Konfigurationsbeispiel](../../../../media/Step-3-Plan-a-Load-Balanced-Cluster-Deployment/ELBDiagram-URA_Enterprise_NLB-.png)  
  
##### <a name="planning-information"></a>Informationen zur Planung  
  
1.  Externen VIPs (IP-Adressen, die der Client verwendet, Herstellen einer Verbindung mit Remote) wurden möchte 131.107.0.102, werden 131.107.0.103  
  
2.  Lastenausgleich auf dem externen Netzwerk Self-IP-Adressen - 131.107.0.245 (Internet), 131.107.1.245  
  
    Umkreisnetzwerk (auch bekannt als demilitarisierte Zone und DMZ) wird zwischen dem Load Balancer im externen Netzwerk und RAS-Servers.  
  
3.  IP-Adressen für RAS-Server im Umkreisnetzwerk - 131.107.1.102, 131.107.1.103  
  
4.  IP-Adressen für RAS-Servers im Netzwerk ELB (d. h. zwischen RAS-Servers und den Lastenausgleich im internen Netzwerk) - 30.11.1.101, 2006:2005:11:1::101  
  
5.  Lastenausgleich auf dem internen Netzwerk Self-IP-Adressen - 30.11.1.245 2006:2005:11:1::245 (ELB), 30.1.1.245 2006:2005:1:1::245 (Corpnet)  
  
6.  Internen VIPs (IP-Adressen für den Webtest-Client und für den Netzwerkadressenserver verwendet, wenn auf dem RAS-Server installiert) wurden für die 30.1.1.10, 2006:2005:1:1::10 werden möchte  
  
##### <a name="steps"></a>Schritte  
  
1.  Konfigurieren Sie die RAS-Server externen Netzwerkadapter (die mit dem Umkreisnetzwerk verbunden ist), mit Adressen 131.107.0.102, 131.107.0.103. Dieser Schritt ist erforderlich, damit der DirectAccess-Konfiguration, um die korrekten Endpunkte des IPsec-Tunnel zu erkennen.  
  
2.  Konfigurieren Sie die RAS-Servers internen Netzwerkadapter (die mit dem ELB-Netzwerk verbunden ist), mit der Web-Test/Network Location Server IP-Adressen (30.1.1.10, 2006:2005:1:1::10). Dieser Schritt ist erforderlich, für das Zulassen von Clients auf die Webtest IP-Adresse zugreifen, damit der Netzwerkkonnektivitäts-Assistent den Status der Verbindung zu DirectAccess vollkommen richtig an. Dieser Schritt ermöglicht auch Zugriff auf den Netzwerkadressenserver, wenn es auf dem DirectAccess-Server konfiguriert ist.  
  
    > [!NOTE]  
    > Stellen Sie sicher, dass der Domänencontroller vom RAS-Servers mit dieser Konfiguration aus erreichbar ist.  
  
3.  Konfigurieren Sie einzelne DirectAccess-Servers, auf dem RAS-Server.  
  
4.  Externen Lastenausgleich, die in der DirectAccess-Konfiguration zu aktivieren. Verwenden Sie die externen dedizierte IP-Adresse (DIP) 131.107.1.102 (131.107.1.103 wird automatisch ausgewählt), 30.11.1.101, 2006:2005:11:1::101 als der internen DIPs verwenden.  
  
5.  Konfigurieren Sie die externen virtuellen IP-Adressen (VIP), auf den externen Lastenausgleich mit den Adressen 131.107.0.102 und 131.107.0.103. Konfigurieren Sie außerdem den internen VIPs für den externen Lastenausgleich mit Adressen 30.1.1.10 und 2006:2005:1:1::10.  
  
6.  RAS-Servers wird jetzt mit der geplanten IP-Adressen konfiguriert, und die externen und internen IP-Adressen für den Cluster werden entsprechend der geplanten IP-Adressen konfiguriert sein.  
  
## <a name="bkmk_2_2_NLB"></a>3.2 Planen der IP-HTTPS  
  
1.  **Zertifikatanforderungen**-während der Bereitstellung der RAS-Servers, das Sie ausgewählt haben, entweder eine IP-HTTPS-Zertifikat von einer öffentlichen oder internen Zertifizierungsstelle (CA) ausgegeben oder ein selbstsigniertes Zertifikat verwenden. Für die Bereitstellung des Clusters müssen Sie denselben Typ des Zertifikats für jedes Element des remotezugriffsclusters verwenden. D.h., wenn Sie ein Zertifikat von einer öffentlichen Zertifizierungsstelle (empfohlen) verwendet, müssen Sie ein Zertifikat von einer öffentlichen Zertifizierungsstelle auf jedes Mitglied des Clusters installieren. Der Antragstellername des neuen Zertifikats sollte mit dem Antragstellernamen des IP-HTTPS-Zertifikats, das derzeit in Ihrer Bereitstellung verwendeten identisch sein. Beachten Sie, dass wenn Sie selbstsignierte Zertifikate verwenden, werden diese automatisch auf jedem Server während der Clusterbereitstellung konfiguriert werden.  
  
2.  **Präfix Anforderungen**-Remote-Zugriff ermöglicht den Lastenausgleich, SSL-basierten Datenverkehr und DirectAccess-Datenverkehr. Für den Lastenausgleich alle IPv6-basierten DirectAccess-Datenverkehr, Remote-Zugriff müssen die IPv4-tunneling für alle übergangstechnologien untersuchen. Da IP-HTTPS-Datenverkehr verschlüsselt ist, ist den Inhalt der IPv4-Tunnel untersuchen nicht möglich. Um IP-HTTPS-Datenverkehr für den Lastenausgleich zu aktivieren, müssen Sie die breit genug ist, IPv6-Präfix zuweisen, damit ein anderes Präfix für die IPv6-/64 jedes Clustermitglied zugewiesen werden kann. Sie können maximal 32 Servern in einem Auslastungstest mit Lastenausgleich-Cluster konfigurieren. aus diesem Grund müssen Sie angeben, ein nur in/59 Präfix. Dieses Präfix muss auf die interne IPv6-Adresse des remotezugriffsclusters geroutet werden, und in der RAS-Server-Setup-Assistent konfiguriert ist.  
  
    > [!NOTE]  
    > Die Präfix-Anforderungen sind nur in einem internen Netzwerk mit aktiviertem IPv6 Bedeutung (reine IPv6-, oder IPV4 und IPv6). In einem IPv4-Netzwerk nur Unternehmen das clientpräfix wird automatisch konfiguriert, und der Administrator nicht ändern.  
  
## <a name="BKMK_3.3"></a>3.3-Plan für die VPN-Clientverbindungen  
Es gibt einige Aspekte für VPN-Client-Verbindungen:  
  
-   VPN-Client-Datenverkehr nicht möglich, wenn VPN-Client-Adressen zugeordnet sind, mithilfe von DHCP-Lastenausgleich. Ein statischer Adresspool ist erforderlich.  
  
-   RRAS kann aktiviert werden, in einem Cluster mit Lastenausgleich, die nur für DirectAccess bereitgestellt wurde mit **Aktivieren von VPN-** Aufgaben im Bereich der Remotezugriffs-Verwaltungskonsole.  
  
-   VPN-Änderungen abgeschlossen werden, in der Routing- und Remotezugriffs-Verwaltungskonsole (rrasmgmt.msc) müssen manuell für alle RAS-Server im Cluster repliziert werden.  
  
-   Um VPN-IPv6-Client-Datenverkehr für den Lastenausgleich zu aktivieren, müssen Sie ein 59 Bit-IPv6-Präfix angeben.  
  
## <a name="BKMK_nls"></a>3.4 Planen des Netzwerkadressenservers  
Wenn Sie die Netzwerkadressenserver-Website auf dem RAS-Servers ausführen, während der Bereitstellung haben Sie ausgewählt, entweder ein von einer internen Zertifizierungsstelle (CA) ausgestelltes Zertifikat oder ein selbstsigniertes Zertifikat verwenden.  Beachten Sie Folgendes:  
  
1.  Jedes Mitglied des RAS-Clusters muss es sich um ein Zertifikat für den Netzwerkadressenserver verfügen, die den DNS-Eintrag für die Netzwerkadressenserver-Website entspricht.  
  
2.  Das Zertifikat für jeden Clusterserver muss auf die gleiche Weise wie das Zertifikat auf den einzelnen RAS-Server aktuelle Netzwerkadressenserver-Zertifikat ausgestellt werden. Wenn Sie ein von einer internen Zertifizierungsstelle ausgestelltes Zertifikat verwendet haben, müssen Sie z. B. ein Zertifikat von der internen Zertifizierungsstelle auf jedem Mitglied des Clusters installieren.  
  
3.  Wenn Sie ein selbstsigniertes Zertifikat verwendet, wird ein selbst signiertes Zertifikat während der Clusterbereitstellung automatisch für jeden Server konfiguriert.  
  
4.  Der Antragstellername des Zertifikats muss nicht auf den Namen aller Server in der remotezugriffsbereitstellung identisch sein.  
