---
title: Hyper-V-Netzwerkvirtualisierung – Übersicht in WindowsServer 2016
description: Dieses Thema enthält eine Übersicht über Hyper-V-Netzwerkvirtualisierung in Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0115b7ad-d229-4c69-9d7e-a3f5fbaa3b2f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c7c20f9b2d81ac2d49ed0bbea5f3aca48dea0c50
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="hyper-v-network-virtualization-overview-in-windows-server-2016"></a>Hyper-V-Netzwerkvirtualisierung – Übersicht in WindowsServer 2016

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In Windows Server 2016 und Virtual Machine Manager bietet Microsoft eine End-to-End-Lösung für die Netzwerkvirtualisierung.  Es gibt fünf Hauptkomponenten, die von Microsoft-netzwerkvirtualisierungslösung:  
  
-   **Windows Azure Pack für Windows Server** bietet einen für Mandanten verfügbares Portal zum Erstellen von virtueller Netzwerken und eine administrative Portal zum Verwalten von virtueller Netzwerken.  
  
-   **Virtual Machine Manager** (VMM) ermöglicht die zentralisierte Verwaltung der Netzwerk-Fabric.  
  
-   **Microsoft-Netzwerkcontroller** bietet einen zentralen, programmierbaren Automatisierung zu verwalten, Konfiguration, Überwachung und Problembehandlung von virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum.  
  
-   **Hyper-V-Netzwerkvirtualisierung** stellt die Infrastruktur zum Virtualisieren des Netzwerkdatenverkehrs erforderlich.  
  
-   **Hyper-V-netzwerkvirtualisierungsgateways** Verbindungen zwischen virtuellen und physischen Netzwerken bereitstellen.  
  
In diesem Thema werden Konzepte vorgestellt und die wichtigsten Vorteile und Funktionen der Hyper-V-Netzwerkvirtualisierung (eines Bestandteils der gesamten Lösung für die Virtualisierung) in Windows Server 2016 erläutert. Es wird erläutert, wie die Netzwerkvirtualisierung sowohl für private Clouds für die Konsolidierung von unternehmensarbeitsauslastungen und public Cloud-Dienstanbieter-Infrastruktur als Service (IaaS) profitiert.  
  
Weitere technische Details zur Netzwerkvirtualisierung in Windows Server 2016 finden Sie [Hyper-V-Netzwerk Netzwerkvirtualisierung – technische Details in Windows Server 2016](../../../sdn/technologies/hyper-v-network-virtualization/hyperv-network-virtualization-technical-details-windows-server.md).  
  
**Meinten Sie**  
  
-   [Hyper-V-Netzwerkvirtualisierung – Übersicht](assetId:///bf1dba9d-1960-4dd2-a5e2-99466a02044b) (Windows Server 2012 R2)  
  
-   [Hyper-V (Übersicht)](assetId:///5aad349f-ef06-464a-b36f-366fbb040143)  
  
-   [Virtuelle Hyper-V-Switch (Übersicht)](assetId:///e6ec46af-6ef4-49b3-b1f1-5268dc03f05b)  
  
## <a name="BKMK_OVER"></a>Featurebeschreibung  
Hyper-V-Netzwerkvirtualisierung werden "virtuelle Netzwerke" (ein VM-Netzwerk bezeichnet) für virtuelle Maschinen vergleichbar mit der Servervirtualisierung (Hypervisor) "virtuelle Maschine" für das Betriebssystem bereitgestellt. Netzwerkvirtualisierung virtuelle Netzwerke von der physischen Netzwerkinfrastruktur entkoppelt und die Einschränkungen von VLAN und hierarchischer IP-Adresszuweisung von der Bereitstellung der virtuellen Maschine entfernt. Diese Flexibilität macht es für Kunden zum Wechsel zu IaaS-Clouds, einfach und effizient für gewährt Hostern und datencenteradministratoren, um ihre Infrastruktur zu verwalten, und gleichzeitig die erforderliche mehrinstanzenfähige Isolation und sicherheitsanforderungen erhalten, und unterstützende überlappende Virtual Machine-IP-Adressen.  
  
Kunden wünschen sich ihrer Datencenter in der Cloud nahtlos zu erweitern. Heute bestehen die technische Herausforderungen bei der Bereitstellung dieser nahtlose Hybrid Cloud-Architekturen. Eine der größten Hürden Kunden Fläche ist Wiederverwendung vorhandener Netzwerktopologien (Subnetze, IP-Adressen, Netzwerkdienste und So weiter.) in der Cloud und brückenschlag zwischen ihren lokalen Ressourcen und Cloud-Ressourcen.  Hyper-V-Netzwerkvirtualisierung umfasst das Konzept eines VM-Netzwerks, unabhängig von der zugrunde liegenden physischen Netzwerk ist. Bei diesem Konzept für VM-Netzwerke, bestehend aus einem oder mehreren virtuellen Subnetzen wird der exakte Speicherort im physischen Netzwerk mit einem virtuellen Netzwerk verbundenen virtuellen Maschinen von der Topologie des virtuellen Netzwerks entkoppelt. Daher können Kunden problemlos verschieben ihre virtuellen Subnetze in der Cloud und ihre bestehenden IP-Adressen und die Topologie in der Cloud beibehalten, sodass vorhandene Dienste weiterhin verwendet unabhängig von den physischen Speicherort der Subnetze. Dies bedeutet, dass Hyper-V-Netzwerkvirtualisierung eine nahtlose Hybrid-Cloud.  
  
Neben Hybrid-Clouds werden viele Organisationen die Konsolidierung ihrer Datencenter und erstellen private Clouds, um die Effizienz und Skalierbarkeit Vorteil von Cloud-Architekturen intern zu erhalten. Hyper-V-Netzwerkvirtualisierung ermöglicht eine höhere Flexibilität und Effizienz für private Clouds, indem einer Unternehmenseinheit Entkopplung Netzwerktopologie (durch Virtualisierung) von der tatsächlichen physischen Netzwerktopologie entkoppelt. Auf diese Weise können Geschäftseinheiten problemlos eine interne private Cloud Teilen, während Sie räumlich voneinander und bestehender Netzwerktopologien weiterhin. Das verantwortliche Team hat die Flexibilität, bereitstellen und Arbeitslasten an einer beliebigen Stelle des Datencenters ohne serverunterbrechungen höhere Betriebseffizienz und ein insgesamt effektiver Datencenter dynamisch zu verschieben.  
  
Für arbeitsauslastungsbesitzer ist der wichtigste Vorteil, dass sie ihre arbeitsauslastung "Topologien" jetzt in die Cloud verschieben können, ohne die IP-Adressen zu ändern oder ihre Anwendungen umschreiben. Z. B. die typische dreistufige LOB-Anwendung ein front-End-Ebene, einer Geschäftslogik-Ebene und einer Datenbank-Ebene besteht. Mithilfe von Richtlinien kann Hyper-V-Netzwerkvirtualisierung Kunden alle Onboarding oder Teile der drei Ebenen in der Cloud und gleichzeitig die Weiterleitungstopologie sowie die IP-Adressen der Dienste (d. h. virtuellen IP-Adressen), ohne dass die Anwendung geändert werden.  
  
Infrastrukturbesitzer erhalten ermöglicht die zusätzliche Flexibilität bei der Platzierung der virtuellen Maschine an einer beliebigen Stelle Arbeitslasten in den Datencentern verschieben, ohne die virtuellen Computer ändern oder die Netzwerke konfigurieren. Beispielsweise können Hyper-V-Netzwerkvirtualisierung subnetzübergreifende Livemigration, damit eine virtuelle Maschine an einer beliebigen Stelle im Datencenter ohne dienstunterbrechung eine Livemigration kann. Bisher waren livemigrationen begrenzte mit demselben Subnetz einschränken, in denen virtuelle Computer gefunden werden konnte. Bei der subnetzübergreifenden Livemigration kann Administratoren Arbeitslasten basierend auf dynamischen Ressourcenbedarfs Energieeffizienz konsolidieren und Infrastruktur Wartung kann auch ohne Unterbrechung der kundenarbeitsauslastung aufnehmen.  
  
## <a name="BKMK_APP"></a>In der Praxis  
Mit dem Erfolg virtualisierter Datencenter haben IT-Organisationen und Hostinganbieter (Anbieter anbieten Vermietung oder physischer Server bereitstellen) begonnen, flexiblere virtualisierte Infrastrukturen, die bei Bedarf Server-Instanzen für ihre Kunden anbieten zu vereinfachen. Diese neue Art von Dienst wird als Infrastructure-as-a-Service (IaaS) bezeichnet. Windows Server 2016 enthält alle erforderlichen Plattformfunktionen Unternehmenskunden private Clouds und Übergang an ein IT operative Modell erstellen aktivieren. Windows Server 2016 2016 können auch Hoster öffentliche Clouds erstellen und ihren Kunden IaaS-Lösungen anbieten. In Kombination mit Virtual Machine Manager und Windows Azure Pack zum Verwalten von Hyper-V-netzwerkvirtualisierungsrichtlinie stellt Microsoft eine leistungsstarke Cloudlösung bereit.  
  
Windows Server 2016 Hyper-V-Netzwerkvirtualisierung bietet richtlinienbasierte, softwaregesteuerte Netzwerkvirtualisierung, die die Verwaltung von Unternehmen Aufwand konfrontiert, wenn sie dedizierte IaaS-Clouds erweitern, und sie cloudhoster erhalten eine größere Flexibilität und Skalierbarkeit für die Verwaltung von virtuellen Computer bei der effizienteren ressourcenausnutzung reduziert.  
  
Ein IaaS-Szenario, die virtuellen Computer aus unterschiedlichen Organisationseinheiten (dedizierte Cloud) oder unterschiedliche Kunden (gehostete Cloud) verfügt über eine sichere Isolation notwendig. Die derzeitige Lösung virtuelle lokale Netzwerke (VLANs), kann in diesem Szenario Nachteile darstellen.  
  
**VLANs**  
  
VLANs sind derzeit den Mechanismus, den meisten Organisationen verwenden, um die Wiederverwendung von Adressräumen und zur instanzisolierung. In einem VLAN wird explizites tagging (VLAN-ID) in den Ethernet-Frame-Headers verwendet, und Ethernet-Switches Isolation zu erzwingen und den Datenverkehr auf Netzwerkknoten mit derselben VLAN-ID zu beschränken Die größten Nachteile mit VLANs lauten wie folgt:  
  
-   Erhöhtes Risiko einer unbeabsichtigten Ausfallzeit aufgrund der schwerfälligen Neukonfiguration der Produktions-switches, wenn der virtuelle Computer oder Isolationsgrenzen in das dynamische Datencenter verschoben.  
  
-   Begrenzte Skalierbarkeit, da es maximal 4094 VLANs sind und herkömmliche Switches höchstens 1000 VLAN-IDs unterstützen.  
  
-   In einem Subnetz, die die Anzahl der Knoten in einem einzelnen VLAN begrenzt und schränkt die Platzierung von virtuellen Maschinen basierend auf physischen Standorten eingeschränkt. Obwohl VLANs standortübergreifend erweitert werden können, muss das gesamte VLAN im gleichen Subnetz.  
  
**IP-Adresszuweisung**  
  
Zusätzlich zu den Nachteile, die von VLANs angezeigt werden, zeigt virtuellen IP-Adresszuweisung Probleme, z. b:  
  
-   Physischen Speicherorte in der datencenternetzwerkinfrastruktur bestimmen die IP-Adressen der virtuellen Maschine. Daher erfordert in der Regel der Wechsel zur Cloud IP-Adressen für die dienstarbeitsauslastungen zu ändern.  
  
-   Richtlinien sind für IP-Adressen, z. B. Firewallregeln, Ressourcen und Verzeichnisdienste usw. gebunden. Ändern der IP-Adressen erfordert Aktualisieren aller zugeordneten Richtlinien.  
  
-   Bereitstellung virtueller Computer und die datenverkehrisolierung sind abhängig von der Topologie.  
  
Wenn Datencenter-Netzwerkadministratoren die physische Form des Datencenters planen, müssen sie entscheiden, in denen Subnetze physisch platziert und weitergeleitet werden. Diese Entscheidungen basieren auf IP- und Ethernet-Technologie, die die potenziellen IP-Adressen auswirken, die für virtuelle Computer auf einem bestimmten Server oder einem Blade, die mit einem bestimmten Rack im Datencenter verbunden ist. Wenn eine virtuelle Maschine bereitgestellt und im Rechenzentrum platzierter, muss er diese Auswahloptionen und Einschränkungen in Bezug auf die IP-Adresse entsprechen. Daher ist die Regel führt dies dazu, dass die Datacenter-Administratoren den virtuellen Computern neue IP-Adressen zuweisen.  
  
Das Problem bei dieser Anforderung besteht, sondern eine Adresse semantische Informationen im Zusammenhang mit einer IP-Adresse vorhanden ist. Ein Subnetz kann beispielsweise bestimmte Dienste enthalten oder werden in einem dedizierten physischen Speicherort. Firewall-Regeln, Zugriffsrichtlinien und IPsec-sicherheitszuordnungen sind häufig IP-Adressen zugeordnet. Ändern der IP-Adressen erzwingt, dass der Besitzer des virtuellen Computers alle entsprechenden Richtlinien anpassen, die auf den ursprünglichen IP-Adresse basierten. Eine solche neunummerierung ist Aufwand hoch, dass sich viele Unternehmen dafür entscheiden, nur neue Dienste in der Cloud Anwendungen bereitstellen.  
  
Hyper-V-Netzwerkvirtualisierung wird ein virtuelles Netzwerk für virtuelle Computer der Kunden von der physischen Netzwerkinfrastruktur. Daher können sie virtuellen Computer der Kunden ihre ursprünglichen IP-Adressen, verwalten und zulassen, dass Administratoren im Rechenzentrum langfristig virtuellen Computer der Kunden an einer beliebigen Stelle im Datencenter bereitstellen, ohne dass eine Neukonfiguration der physischen IP-Adressen oder VLAN-IDs. Im nächste Abschnitt wird die eigentliche Funktionalität.  
  
## <a name="BKMK_NEW"></a>Wichtige Funktionen  
Im folgenden finden eine Liste der Hauptfunktionen, Vorteile und Funktionen der Hyper-V-Netzwerkvirtualisierung in Windows Server 2016:  
  
-   **Ermöglicht flexible arbeitsauslastungsplatzierung - Netzwerkisolation und IP-Adresse erneut verwenden, ohne VLANs**  
  
    Hyper-V-Netzwerkvirtualisierung virtuellen Netzwerke des Kunden, von der physischen Netzwerkinfrastruktur von der Hoster Platzierung der arbeitsauslastungen in den Datencentern. Platzierung der virtuellen Maschine Arbeitslast ist nicht mehr von der IP-adressenzuweisung oder VLAN-isolationsanforderungen des physischen Netzwerks beschränkt, da es in Hyper-V-Hosts basierend auf softwaredefinierten, mehrinstanzfähigen virtualisierungsrichtlinien erzwungen wird.  
  
    Virtuelle Computer anderer Kunden mit überlappenden IP-Adressen können nun auf demselben Hostserver bereitgestellt werden, ohne dass schwerfällige VLAN-Konfiguration oder eines Verstoßes gegen die IP-Adresse-Hierarchie. Dies erleichtert die Migration der kundenarbeitsauslastungen zu freigegebenen IaaS-Hostinganbietern, ermöglicht die entsprechenden arbeitsauslastungen ohne Änderungen, verschieben, d. h. auch die VM-IP-Adressen unverändert. Für den Hostinganbieter ist unterstützen zahlreiche Kunden, die ihren vorhandenen Netzwerk Adressraum auf den freigegebenen IaaS-Datencenter erweitern möchten, eine komplexe Aufgabe der Konfiguration und Wartung der isolierten VLANs für jeden Kunden, um die Koexistenz potenziell überlappender Adressräume zu gewährleisten. Mit Hyper-V-Netzwerkvirtualisierung Unterstützung von adressüberlappungen vereinfacht und erfordert weniger netzwerkneukonfiguration durch den Hostinganbieter.  
  
    Darüber hinaus können Wartung der physischen Infrastruktur und Upgrades ohne Ausfallzeiten im Hinblick auf kundenarbeitsauslastungen ausgeführt werden. Mit Hyper-V-Netzwerkvirtualisierung können virtuelle Maschinen auf einem bestimmten Host, Rack, Subnetz, VLAN oder gesamte Cluster migriert werden, ohne eine Änderung der physischen IP-Adresse oder wichtige Neukonfiguration.  
  
-   **Ermöglicht einer einfacheren Verschiebung von arbeitsauslastungen in einer freigegebenen IaaS-cloud**  
  
    Mit Hyper-V-Netzwerkvirtualisierung bleiben IP-Adressen und Konfigurationen virtueller Computer unverändert. Dadurch können IT-Organisationen einfacher arbeitsauslastungen aus ihren Datencentern verschieben, auf eine freigegebene IaaS-Hostinganbieter mit minimale Neukonfiguration der arbeitsauslastung oder der Infrastrukturtools und Richtlinien. In Fällen liegt der Konnektivität zwischen den beiden Datencentern, IT-Administratoren können weiterhin ihre Tools verwenden, ohne diese neu konfigurieren.  
  
-   **Ermöglicht die Livemigration in Subnetzen**  
  
    Livemigration von arbeitsauslastungen virtueller Computer traditionell auf der gleichen IP-Subnetz oder VLAN beschränkt da Gastbetriebssystem des virtuellen Computers, dessen IP-Adresse ändern subnetzübergreifenden benötigt werden. Diese Änderung unterbricht bestehende Kommunikation und unterbricht die Dienste auf dem virtuellen Computer ausgeführt wird. Bei der Hyper-V-Netzwerkvirtualisierung ist Arbeitslasten live von den Servern mit Windows Server 2016 in einem Subnetz auf Server mit Windows Server 2016 in einem anderen Subnetz ohne Änderung der Arbeitslast IP-Adressen. Hyper-V-Netzwerkvirtualisierung wird sichergestellt, dass virtuelle Maschine Standortwechsel aufgrund von live-Migration aktualisiert und auf Hosts, die laufende Kommunikation mit dem migrierten virtuellen Computer synchronisiert werden.  
  
-   **Ermöglicht eine einfachere Verwaltung des entkoppelten Servers und Netzwerks Verwaltung**  
  
    Server arbeitsauslastungsplatzierung wird vereinfacht, da die Migration und die Platzierung der arbeitsauslastungen unabhängig von der zugrunde liegenden physischen Netzwerkkonfigurationen sind. Serveradministratoren können sich auf die Verwaltung von Diensten und Servern konzentrieren, und Netzwerkadministratoren können sich auf allgemeine netzwerkverwaltung und die datenverkehrsverwaltung konzentrieren. Dies ermöglicht Datencenter-Serveradministratoren bereitstellen und Migrieren von virtuellen Maschinen ohne Änderung der IP-Adressen der virtuellen Computer. Mehraufwands, da Hyper-V-Netzwerkvirtualisierung ermöglicht die Platzierung der virtuellen Maschine auftreten, unabhängig von der Netzwerktopologie, mindert die Notwendigkeit für Netzwerkadministratoren mit Platzierungen einbezogen werden müssen, die die Isolationsgrenzen ändern kann.  
  
-   **Vereinfachung des Netzwerks und verbessert die Ressourcenverwendung für Server-Netzwerk**  
  
    Die Inflexibilität von VLANs und die Abhängigkeit der Platzierung der virtuellen Maschine auf einer physischen Netzwerkinfrastruktur führen zu einer überversorgung und unterauslastung führt. Aufteilen der Abhängigkeits, kann die gestiegene Flexibilität der Platzierung der virtuellen Maschine Arbeitslast vereinfacht die netzwerkverwaltung und Server und netzwerkressourcenauslastung verbessern. Beachten Sie, dass Hyper-V-Netzwerkvirtualisierung VLANs im Kontext physischer Datencenter unterstützt. Beispielsweise sollten ein Datencenter alle Hyper-V-Netzwerkvirtualisierung Datenverkehr in einem bestimmten VLAN sein.  
  
-   **Ist kompatibel mit der vorhandenen Infrastruktur und sich entwickelnder Technologie**  
  
    Hyper-V-Netzwerkvirtualisierung kann in heutigen Datencentern bereitgestellt werden, aber es ist kompatibel mit den kommenden Datacenter "flache Network" Technologien.  
  
    Unterstützt z. B. Hyper-v-in Windows Server 2016 VXLAN Kapselung Format und die öffnen-vSwitch Datenbank-Management-Protokoll (OVSDB) als die SouthBound Schnittstelle (SBI)...  
  
-   **Bietet für Interoperabilität und ökosystemvorbereitung**  
  
    Hyper-V-Netzwerkvirtualisierung werden mehrere Konfigurationen für die Kommunikation mit bestehenden Ressourcen wie z. B. plattformübergreifende übergreifende Konnektivität, Storage Area Network (SAN), nicht-virtualisierter Ressourcenzugriff usw. unterstützt. Microsoft arbeitet eng mit Partnern im Ökosystem zu unterstützen und Verbessern der Arbeitsmöglichkeiten von Hyper-V-Netzwerkvirtualisierung im Hinblick auf Leistung, Skalierbarkeit und verwaltbarkeit.  
  
-   **Richtlinienbasierte Konfiguration**  
  
    Virtualisierung Netzwerkrichtlinien in Windows Server 2016 werden über den Microsoft-Netzwerk-Controller konfiguriert. Netzwerkcontroller ist eine RESTful northbound-API und Windows PowerShell-Schnittstelle, um die Richtlinie zu konfigurieren. Weitere Informationen zu den Microsoft-Netzwerk-Controller, finden Sie unter [Netzwerkcontroller](../../../sdn/technologies/network-controller/../../../sdn/technologies/network-controller/Network-Controller.md).  
  
## <a name="BKMK_SOFT"></a>Anforderungen der Clientsoftware  
Hyper-V-Netzwerkvirtualisierung mit den Microsoft-Netzwerk-Controller erfordert Windows Server 2016 und Hyper-V-Rolle.  
  
## <a name="BKMK_LINKS"></a>Siehe auch  
Finden Sie weitere Informationen zu Hyper-V-Netzwerkvirtualisierung in Windows Server 2016 die folgenden Links:  
  
|Inhaltstyp|Verweise|  
|----------------|--------------|  
|**Community-Ressourcen**|-   [Architektur von Private Clouds-Blog](http://blogs.technet.com/b/privatecloud/archive/2012/03/19/cloud-datacenter-network-architecture-in-the-windows-server-8-era.aspx)<br />– Stellen Sie Fragen:[cloudnetfb@microsoft.com](mailto:%20cloudnetfb@microsoft.com)|  
|**RFC**|-VXLAN - [RFC 7348](http://www.rfc-editor.org/info/rfc7348)|  
|**Verwandte Technologien**|-   [Netzwerkcontroller](../../../sdn/technologies/network-controller/../../../sdn/technologies/network-controller/Network-Controller.md)<br />-   [Hyper-V-Netzwerkvirtualisierung – Übersicht](assetId:///bf1dba9d-1960-4dd2-a5e2-99466a02044b) (Windows Server 2012 R2)|  
  


