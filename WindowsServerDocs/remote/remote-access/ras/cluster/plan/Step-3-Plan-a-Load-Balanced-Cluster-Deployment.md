---
title: 'Schritt 3: Planen einer Cluster Bereitstellung mit Lastenausgleich'
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs in einem Cluster unter Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7540c17b-81de-47de-a04f-3247afa26f70
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1a195be9c00ef35f80a7e1975b52128681fca1f0
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308210"
---
# <a name="step-3-plan-a-load-balanced-cluster-deployment"></a>Schritt 3: Planen einer Cluster Bereitstellung mit Lastenausgleich

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Der nächste Schritt besteht darin, die Lasten Ausgleichs Konfiguration und die Cluster Bereitstellung zu planen.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|3,1 Planen des Lasten Ausgleichs|Entscheiden Sie, ob Sie den Windows-Netzwerk Lastenausgleich (Network Load Balancing, NLB) oder einen externen Lastenausgleich (ELB) verwenden möchten.|  
|3,2 planen IP-HTTPS|Wenn kein selbst signiertes Zertifikat verwendet wird, benötigt der RAS-Server ein SSL-Zertifikat auf jedem Server im Cluster, um IP-HTTPS-Verbindungen zu authentifizieren.|  
|3,3 Planen von VPN-Clientverbindungen|Beachten Sie die Anforderungen für VPN-Clientverbindungen.|  
|3,4 Planen des Netzwerkadressen Servers|Wenn die Netzwerkadressen Server-Website auf dem Remote Zugriffs Server gehostet wird und kein selbst signiertes Zertifikat verwendet wird, stellen Sie sicher, dass jeder Server im Cluster über ein Serverzertifikat verfügt, um die Verbindung mit der Website zu authentifizieren.|  
  
## <a name="31-plan-load-balancing"></a><a name="bkmk_2_1_Plan_LB"></a>3,1 Planen des Lasten Ausgleichs  
Der Remote Zugriff kann auf einem einzelnen Server oder auf einem Cluster von Remote Zugriffs Servern bereitgestellt werden. Für den Datenverkehr an den Cluster kann ein Lastenausgleich ausgeführt werden, um für DirectAccess-Clients Hochverfügbarkeit und Skalierbarkeit zu bieten. Es gibt zwei Optionen für den Lastenausgleich:  
  
-   **Windows NLB**-Windows NLB ist eine Windows Server-Funktion. Um es zu verwenden, benötigen Sie keine zusätzliche Hardware, da alle Server im Cluster für die Verwaltung der Datenverkehrs Auslastung verantwortlich sind. Windows-NLB unterstützt maximal acht Server in einem Remote Zugriffs Cluster.  
  
-   **Externer Lastenausgleich**: bei Verwendung eines externen Lasten Ausgleichs ist externe Hardware erforderlich, um die Auslastung des Datenverkehrs zwischen den Remote Zugriffs-Cluster Servern zu verwalten. Außerdem unterstützt die Verwendung eines externen Load Balancers maximal 32 RAS-Server in einem Cluster. Beim Konfigurieren des externen Lasten Ausgleichs sollten folgende Punkte berücksichtigt werden:  
  
    -   Der Administrator muss sicherstellen, dass die über den RAS-Assistenten für den Remote Zugriff konfigurierten virtuellen IP-Adressen auf dem externen Lasten Ausgleichs Modul (z. b. F5 BIG-IP local Traffic Manager System) verwendet werden. Wenn externer Lastenausgleich aktiviert ist, werden die IP-Adressen der externen und der internen Schnittstelle zu virtuellen IP-Adressen herauf gestuft und müssen auf den Lasten Ausgleichs Modulen gecabt werden. Dies geschieht, damit der Administrator den DNS-Eintrag für den öffentlichen Namen der Cluster Bereitstellung nicht ändern muss. Außerdem werden die IPSec-Tunnel Endpunkte von den Server-IPS abgeleitet. Wenn der Administrator separate virtuelle IPS bereitstellt, kann der Client keine Verbindung mit dem Server herstellen. Ein Beispiel für die Konfiguration von DirectAccess mit externem Lastenausgleich finden Sie unter Beispiel für externe Load Balancer Konfiguration von 3.1.1.  
  
    -   Viele externe Lasten Ausgleichs Module (einschließlich F5) unterstützen keinen Lastenausgleich von IPv6 zu 4 und ISATAP. Wenn es sich bei dem RAS-Server um einen ISATAP-Router handelt, sollte die ISATAP-Funktion auf einen anderen Computer verschoben werden. Wenn sich die ISATAP-Funktion auf einem anderen Computer befindet, müssen die DirectAccess-Server außerdem über eine systemeigene IPv6-Konnektivität mit dem ISATAP-Router verfügen. Beachten Sie, dass diese Konnektivität vorhanden sein sollte, bevor Sie DirectAccess konfigurieren.  
  
    -   Wenn Teredo verwendet werden muss, müssen für den externen Lastenausgleich alle Remote Zugriffs Server über zwei aufeinander folgende öffentliche IPv4-Adressen als dedizierte IP-Adressen verfügen. Die virtuellen IP-Adressen des Clusters müssen auch über zwei aufeinander folgende öffentliche IPv4-Adressen verfügen. Dies gilt nicht für Windows NLB, bei dem nur die virtuellen IPS des Clusters über zwei aufeinander folgende öffentliche IPv4-Adressen verfügen müssen. Wenn Teredo nicht verwendet wird, sind zwei aufeinander folgende IP-Adressen nicht erforderlich.  
  
    -   Der Administrator kann von der Windows-Netzwerk lastenverwaltung zum externen Load Balancer wechseln und umgekehrt. Beachten Sie, dass der Administrator nicht von einem externen Lasten Ausgleichs Modul zu Windows NLB wechseln kann, wenn er mehr als acht Server in der externen Load Balancer-Bereitstellung aufweist.  
  
### <a name="311-external-load-balancer-configuration-example"></a><a name="ELBConfigEx"></a>3.1.1 externe Load Balancer Konfigurationsbeispiel  
In diesem Abschnitt werden die Konfigurationsschritte zum Aktivieren eines externen Load Balancers für eine neue Remote Zugriffs Bereitstellung beschrieben. Wenn Sie einen externen Load Balancer verwenden, könnte der Remote Zugriffs Cluster wie in der folgenden Abbildung aussehen, wobei die RAS-Server über einen Load Balancer im internen Netzwerk und das Internet über einen Load Balancer mit dem Unternehmensnetzwerk verbunden sind. Verbindung mit dem externen Netzwerk:  
  
![Beispiel für eine externe Load Balancer Konfiguration](../../../../media/Step-3-Plan-a-Load-Balanced-Cluster-Deployment/ELBDiagram-URA_Enterprise_NLB-.png)  
  
##### <a name="planning-information"></a>Informationen zur Planung  
  
1.  Externe VIPs (IPS, die der Client für die Verbindung mit dem Remote Zugriff verwendet) wurden als 131.107.0.102, 131.107.0.103  
  
2.  Load Balancer in externen Netzwerk-Self-IPS-131.107.0.245 (Internet), 131.107.1.245  
  
    Das Umkreis Netzwerk (auch als demilitarisierte Zone und DMZ bezeichnet) liegt zwischen dem Load Balancer im externen Netzwerk und dem RAS-Server.  
  
3.  IP-Adressen für den RAS-Server im Umkreis Netzwerk 131.107.1.102, 131.107.1.103  
  
4.  IP-Adressen für den RAS-Server im ELB-Netzwerk (d. h. zwischen dem RAS-Server und dem Load Balancer im internen Netzwerk)-30.11.1.101, 2006:2005:11:1::101  
  
5.  Load Balancer on Internal Network Self-IPS-30.11.1.245 2006:2005:11:1::245 (ELB), 30.1.1.245 2006:2005:1:1::245 (Corpnet)  
  
6.  Interne VIPs (IP-Adressen, die für den Clientweb Test verwendet werden, und für den Netzwerkadressen Server, wenn Sie auf den RAS-Servern installiert sind), werden als 30.1.1.10, 2006:2005:1:1::10  
  
##### <a name="steps"></a>Schritte  
  
1.  Konfigurieren Sie den externen Netzwerkadapter des RAS-Servers, der mit dem Umkreis Netzwerk verbunden ist, mit den Adressen 131.107.0.102, 131.107.0.103. Dieser Schritt ist erforderlich, damit die DirectAccess-Konfiguration die richtigen IPSec-Tunnel Endpunkte erkennt.  
  
2.  Konfigurieren Sie den internen Netzwerkadapter des RAS-Servers (der mit dem ELB-Netzwerk verbunden ist) mit den IP-Adressen des Webtests/Netzwerkadressen Servers (30.1.1.10, 2006:2005:1:1::10). Dieser Schritt ist erforderlich, um Clients den Zugriff auf die Webtest-IP zu gestatten, sodass der netzwerkkonnektivitätsproxy den Verbindungsstatus für DirectAccess ordnungsgemäß angibt. Dieser Schritt ermöglicht auch den Zugriff auf den Netzwerkadressen Server, wenn er auf dem DirectAccess-Server konfiguriert ist.  
  
    > [!NOTE]  
    > Stellen Sie sicher, dass der Domänen Controller vom RAS-Server aus mit dieser Konfiguration erreichbar ist.  
  
3.  Konfigurieren Sie den DirectAccess-Einzel Server auf dem Remote Zugriffs Server.  
  
4.  Aktivieren Sie den externen Lastenausgleich in der DirectAccess-Konfiguration. Verwenden Sie 131.107.1.102 als externe dedizierte IP-Adresse (DIP) (131.107.1.103 wird automatisch ausgewählt), verwenden Sie 30.11.1.101, 2006:2005:11:1::101 als interne Dips.  
  
5.  Konfigurieren Sie die externen virtuellen IPS (VIP) auf dem externen Lasten Ausgleichs Modul mit den Adressen 131.107.0.102 und 131.107.0.103. Konfigurieren Sie außerdem die internen VIPs auf dem externen Load Balancer mit den Adressen 30.1.1.10 und 2006:2005:1:1::10.  
  
6.  Der Remote Zugriffs Server wird nun mit den geplanten IP-Adressen konfiguriert, und die externen und internen IP-Adressen für den Cluster werden gemäß den geplanten IP-Adressen konfiguriert.  
  
## <a name="32-plan-ip-https"></a><a name="bkmk_2_2_NLB"></a>3,2 planen IP-HTTPS  
  
1.  **Zertifikat Anforderungen**: während der Bereitstellung des einzelnen RAS-Servers haben Sie die Verwendung eines IP-HTTPS-Zertifikats ausgewählt, das von einer öffentlichen oder internen Zertifizierungsstelle (Certification Authority, ca) ausgestellt wurde, oder ein selbst signiertes Zertifikat. Für die Cluster Bereitstellung müssen Sie für jedes Mitglied des Remote Zugriffs Clusters denselben Zertifikattyp verwenden. Wenn Sie also ein von einer öffentlichen Zertifizierungsstelle ausgestelltes Zertifikat verwendet haben (empfohlen), müssen Sie ein von einer öffentlichen Zertifizierungsstelle ausgestelltes Zertifikat auf jedem Mitglied des Clusters installieren. Der Antragsteller Name des neuen Zertifikats muss mit dem Antragsteller Namen des IP-HTTPS-Zertifikats identisch sein, das zurzeit in der Bereitstellung verwendet wird. Beachten Sie Folgendes: Wenn Sie selbst signierte Zertifikate verwenden, werden diese bei der Cluster Bereitstellung automatisch auf jedem Server konfiguriert.  
  
2.  **Präfix Anforderungen**: der Remote Zugriff ermöglicht den Lastenausgleich für SSL-basierten Datenverkehr und DirectAccess-Datenverkehr. Für den Lastenausgleich für den gesamten IPv6-basierten DirectAccess-Datenverkehr muss der Remote Zugriff das IPv4-Tunnelingverfahren für alle Übergangs Technologien untersuchen. Da der IP-HTTPS-Datenverkehr verschlüsselt ist, ist die Untersuchung des Inhalts des IPv4-Tunnels nicht möglich. Um den IP-HTTPS-Datenverkehr für den Lastenausgleich zu aktivieren, müssen Sie ein breit genug IPv6-Präfix zuordnen, damit jedem Cluster Mitglied ein anderes IPv6/64-Präfix zugewiesen werden kann. Sie können maximal 32 Server in einem Cluster mit Lastenausgleich konfigurieren. Daher müssen Sie ein Präfix/59 angeben. Dieses Präfix muss an die interne IPv6-Adresse des Remote Zugriffs Clusters Routing fähig sein und ist im Setup-Assistenten für den Remote Zugriffs Server konfiguriert.  
  
    > [!NOTE]  
    > Die Präfix Anforderungen sind nur in einem IPv6-fähigen internen Netzwerk (nur IPv6 oder IPv4 + IPv6) relevant. In einem reinen IPv4-Unternehmensnetzwerk wird das Client Präfix automatisch konfiguriert und kann vom Administrator nicht geändert werden.  
  
## <a name="33-plan-for-vpn-client-connections"></a><a name="BKMK_3.3"></a>3,3 Planen von VPN-Clientverbindungen  
Es gibt eine Reihe von Überlegungen zu VPN-Clientverbindungen:  
  
-   Der Lastenausgleich für den VPN-Client Verkehr ist nicht möglich, wenn VPN-Client Adressen mithilfe von DHCP zugeordnet werden Ein statischer Adresspool ist erforderlich.  
  
-   RRAS kann auf einem Cluster mit Lastenausgleich aktiviert werden, der nur für DirectAccess bereitgestellt wurde, indem **VPN** auf der Taskbereich der Remote Zugriffs-Verwaltungskonsole aktiviert ist.  
  
-   Alle VPN-Änderungen, die in der Routing-und RAS-Verwaltungskonsole (rrasmgmt. msc) abgeschlossen wurden, müssen manuell auf allen RAS-Servern im Cluster repliziert werden.  
  
-   Um den Lastenausgleich für den VPN-IPv6-Client Datenverkehr zu ermöglichen, müssen Sie ein IPv6-Präfix von 59 Bit angeben.  
  
## <a name="34-plan-the-network-location-server"></a><a name="BKMK_nls"></a>3,4 Planen des Netzwerkadressen Servers  
Wenn Sie die Netzwerkadressen Server-Website auf dem einzelnen RAS-Server ausführen, haben Sie während der Bereitstellung die Verwendung eines von einer internen Zertifizierungsstelle (Certification Authority, ca) ausgestellten Zertifikats oder eines selbst signierten Zertifikats ausgewählt.  Beachten Sie Folgendes:  
  
1.  Jedes Mitglied des Remote Zugriffs Clusters muss über ein Zertifikat für den Netzwerkadressen Server verfügen, das dem DNS-Eintrag für die Netzwerkadressen Server-Website entspricht.  
  
2.  Das Zertifikat für die einzelnen Cluster Server muss auf die gleiche Weise ausgestellt werden wie das Zertifikat auf dem aktuellen Netzwerkadressen Serverzertifikat des Remote Zugriffs Servers. Wenn Sie z. b. ein von einer internen Zertifizierungsstelle ausgestelltes Zertifikat verwendet haben, müssen Sie für jedes Mitglied des Clusters ein von der internen Zertifizierungsstelle ausgestelltes Zertifikat installieren.  
  
3.  Wenn Sie ein selbst signiertes Zertifikat verwendet haben, wird bei der Cluster Bereitstellung automatisch ein selbst signiertes Zertifikat für jeden Server konfiguriert.  
  
4.  Der Antragsteller Name des Zertifikats darf nicht mit dem Namen eines beliebigen Servers in der Remote Zugriffs Bereitstellung identisch sein.  
