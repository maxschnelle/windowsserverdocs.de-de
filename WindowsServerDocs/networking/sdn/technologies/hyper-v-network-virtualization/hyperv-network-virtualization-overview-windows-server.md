---
title: Hyper-V-Netzwerkvirtualisierung – Übersicht unter WindowsServer 2016
description: Dieses Thema enthält eine Übersicht über Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016
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
ms.openlocfilehash: d73b377a10842d32e224100e59d117fddc395ea2
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446281"
---
# <a name="hyper-v-network-virtualization-overview-in-windows-server-2016"></a>Hyper-V-Netzwerkvirtualisierung – Übersicht unter WindowsServer 2016

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In Windows Server 2016 und Virtual Machine Manager bietet Microsoft eine End-to-End-Lösung für die Netzwerkvirtualisierung.  Es gibt fünf wesentliche Komponenten, die netzwerkvirtualisierungslösung von Microsoft umfassen:  

-   **Windows Azure Pack für Windows Server** bietet einen für Mandanten verfügbares Portal zum Erstellen von virtueller Netzwerken und ein administratives Portal zum Verwalten virtueller Netzwerke.  

-   **Virtual Machine Manager-** (VMM) ermöglicht die zentralisierte Verwaltung des netzwerkfabric.  

-   **Microsoft-Netzwerkcontroller** stellt einen zentralen, programmierbaren Automatisierung von Verwaltung, konfigurieren, überwachen und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Datencenter bereit.  

-   Mit **Hyper-V-Netzwerkvirtualisierung** wird die zum Virtualisieren des Netzwerkdatenverkehrs benötigte Infrastruktur bereitgestellt.  

-   **Hyper-V-Netzwerkvirtualisierungs-Gateways** Verbindungen zwischen virtuellen und physischen Netzwerken zur Verfügung.  

In diesem Thema werden Konzepte vorgestellt und erläutert die wichtigsten Vorteile und Funktionen der Hyper-V-Netzwerkvirtualisierung (eines Bestandteils der gesamten Lösung für die Netzwerkvirtualisierung) in Windows Server 2016. Es wird erläutert, wie die Netzwerkvirtualisierung sowohl für private Clouds bei der Konsolidierung von Unternehmensarbeitsauslastungen sowie für Anbieter von IaaS-basierten (Infrastructure as a Service) öffentlichen Clouddiensten Vorteile bietet.  

Weitere technische Informationen zur Netzwerkvirtualisierung in Windows Server 2016 finden Sie unter [Hyper-V-Netzwerkvirtualisierung – technische Details unter Windows Server 2016](../../../sdn/technologies/hyper-v-network-virtualization/hyperv-network-virtualization-technical-details-windows-server.md).  

**Meinten Sie**  

-   [Hyper-V-Netzwerkvirtualisierung – Übersicht](assetId:///bf1dba9d-1960-4dd2-a5e2-99466a02044b) (Windows Server 2012 R2)  

-   [Hyper-V: Übersicht](assetId:///5aad349f-ef06-464a-b36f-366fbb040143)  

-   [Virtueller Hyper-V-Switch (Übersicht)](assetId:///e6ec46af-6ef4-49b3-b1f1-5268dc03f05b)  

## <a name="BKMK_OVER"></a>Featurebeschreibung  
Hyper-V-Netzwerkvirtualisierung werden "virtuelle Netzwerke" (ein VM-Netzwerk bezeichnet) für virtuelle Computer, die ähnlich wie der Servervirtualisierung (Hypervisor) "virtuelle Computer" für das Betriebssystem bereitstellt. Bei der Netzwerkvirtualisierung werden virtuelle Netzwerke von der physischen Netzwerkinfrastruktur entkoppelt und die Einschränkungen von VLAN und hierarchischer IP-Adressenzuweisung von der Bereitstellung virtueller Computer getrennt. Diese Flexibilität erleichtert es Kunden, zu IaaS-Clouds zu wechseln, und gewährt Hostern und Datencenteradministratoren Effizienz bei der Infrastrukturverwaltung. Gleichzeitig bleiben die erforderliche mehrinstanzenfähige Isolation und Sicherheitsanforderungen erhalten, und die IP-Adressen-Überlappung virtueller Computer wird unterstützt.  

Kunden wünschen sich eine Möglichkeit für eine nahtlose Ausweitung ihrer Datencenter in die Cloud. Heute bestehen die technischen Herausforderungen darin, nahtlose hybride Cloudarchitekturen zu erstellen. Eines der größten Hürden sehen Kunden ist die Wiederverwendung bestehender Netzwerktopologien (Subnetze, IP-Adressen, Netzwerkdienste und usw.) in der Cloud und für die Überbrückung zwischen ihren lokalen Ressourcen und Cloudressourcen.  Die Hyper-V-Netzwerkvirtualisierung umfasst das Konzept eines VM-Netzwerks, das unabhängig von dem zugrunde liegenden physischen Netzwerk ist. Bei diesem Konzept für VM-Netzwerke, die sich aus einem oder mehreren virtuellen Subnetzen zusammensetzen, wird der exakte Speicherort virtueller Computer im physischen Netzwerk von der Topologie des virtuellen Netzwerks entkoppelt. Dadurch können Kunden ihre virtuellen Subnetze auf einfache Weise in die Cloud verschieben und dabei gleichzeitig die bestehenden IP-Adressen und die Topologie in der Cloud beibehalten, sodass vorhandene Dienste weiterhin verwendet werden können, unabhängig von deren physischem Speicherort in den Subnetzen. Dies bedeutet, dass mit der Hyper-V-Netzwerkvirtualisierung eine nahtlose Hybrid-Cloud zur Verfügung steht.  

Neben Hybrid-Clouds konsolidieren zahlreiche Unternehmen ihre Datencenter und erstellen private Clouds, um die Effizienz und Skalierbarkeit von Cloud-Architekturen intern nutzen zu können. Hyper-V-Netzwerkvirtualisierung ermöglicht eine höhere Flexibilität und Effizienz für private Clouds, indem die Entkopplung von einer Geschäftseinheit die Netzwerktopologie (durch Virtualisierung) von der tatsächlichen physischen Netzwerktopologie. Auf diese Weise können Geschäftseinheiten trotz räumlicher Trennung gemeinsam eine interne private Cloud verwenden und vorhandene Netzwerktopologien beibehalten. Das für den Datencenterbetrieb verantwortliche Team hat die Flexibilität, Arbeitsauslastungen bereitzustellen und innerhalb des Datencenters ohne Serverunterbrechungen dynamisch zu verschieben, wodurch eine höhere Betriebseffizienz und ein Datencenter mit einer insgesamt höheren Effektivität ermöglicht wird.  

Für arbeitsauslastungsbesitzer ist der wichtigste Vorteil, dass sie ihre Workloads "Topologien" nun in die Cloud verschieben können, ohne die IP-Adressen zu ändern oder Umgestalten, ihre Anwendungen. So besteht beispielsweise eine typische dreistufige Branchenanwendungen aus einer Front-End-Ebene, einer Geschäftslogik-Ebene und einer Datenbank-Ebene. Mithilfe von Richtlinien kann der Kunde bei der Hyper-V-Netzwerkvirtualisierung alle Ebenen oder Teile der drei Ebenen in die Cloud integrieren und die Weiterleitungstopologie sowie die IP-Adressen der Dienste (d. h. die IP-Adressen der virtuellen Computer) beibehalten, ohne dass Änderungen an den Anwendungen vorgenommen werden müssen.  

Infrastrukturbesitzer erhalten dank der zusätzlichen Flexibilität bei der Platzierung virtueller Computer die Möglichkeit, Arbeitsauslastungen an beliebige Speicherorte in den Datencentern verschieben zu können, ohne die virtuellen Computer ändern oder die Netzwerke neu konfigurieren zu müssen. Die Hyper-V-Netzwerkvirtualisierung ermöglicht beispielsweise eine subnetzübergreifende Livemigration, sodass ein virtueller Computer an einem beliebigen Speicherort im Datencenter ohne Dienstunterbrechung eine Livemigration ausführen kann. Bisher waren Livemigrationen auf dasselbe Subnetz beschränkt und bedeuteten somit auch Einschränkungen im Hinblick darauf, wo sich die virtuellen Computer befinden können. Bei der subnetzübergreifenden Livemigration können Administratoren die Arbeitsauslastungen auf der Grundlage des dynamischen Ressourcenbedarfs und der Energieeffizienz konsolidieren und eine Infrastrukturwartung ohne Betriebszeitunterbrechung der Kundenarbeitsauslastung gewährleisten.  

## <a name="BKMK_APP"></a>Praktische Anwendungen  
Mit dem Erfolg virtualisierter Datencenter haben IT-Organisationen und Hostinganbieter (Anbieter, die eine Zusammenstellung oder Vermietung physischer Server bereitstellen) begonnen, flexiblere virtualisierte Infrastrukturen anzubieten, und das erleichtert die bedarfsorientierte Bereitstellung von Serverinstanzen für ihre Kunden. Diese neue Art von Dienst wird als %%amp;quot;Infrastructure as a Service (IaaS)%%amp;quot; bezeichnet. Windows Server 2016 bietet alle erforderlichen Plattformfunktionen Unternehmenskunden zum Erstellen von privaten Clouds und der Übergang zum IT as a Service-operational--Modell zu aktivieren. Windows Server 2016-2016 können auch die Hoster öffentliche Clouds erstellen und ihren Kunden IaaS-Lösungen anbieten. In Kombination mit Virtual Machine Manager und Windows Azure Pack zum Verwalten von Hyper-V-netzwerkvirtualisierungsrichtlinie stellt Microsoft eine leistungsstarke Cloudlösung bereit.  

Windows Server 2016 Hyper-V-Netzwerkvirtualisierung bietet richtlinienbasierten, das der Software unterliegt Netzwerkvirtualisierung, die reduziert den Verwaltungsaufwand Unternehmen gegenüberstehen, wenn sie dedizierte IaaS-Clouds erweitern, und bietet eine bessere Cloud-Hoster Flexibilität und Skalierbarkeit für die Verwaltung von virtuellen Computern, um höhere ressourcennutzung zu erreichen.  

Für ein IaaS-Szenario mit virtuellen Computern aus unterschiedlichen Organisationseinheiten (dedizierte Cloud) oder von unterschiedlichen Kunden (gehostete Cloud) ist eine sichere Isolation notwendig. Derzeitige Lösung, virtuelle lokale Netzwerke (VLANs), kann erhebliche Nachteile in diesem Szenario stellen.  

**VLANs**  

VLANs sind derzeit der Mechanismus, den meisten Organisationen verwenden, um die Wiederverwendung von Adressräumen und Isolation von Mandanten. In einem VLAN wird explizites Tagging (VLAN-ID) in den Ethernet-Frame-Headers verwendet, und Ethernet-Switches sind dafür verantwortlich, die Isolation zu erzwingen und den Datenverkehr auf Netzwerkknoten mit derselben VLAN-ID zu beschränken Dabei bestehen für VLANs die folgenden entscheidenden Nachteile:  

-   Erhöhtes Risiko einer unbeabsichtigten Ausfallzeit aufgrund der schwerfälligen Neukonfiguration der Produktions-Switches, wenn virtuelle Computer oder Isolationsgrenzen in das dynamische Datencenter verschoben werden.  

-   Begrenzte Skalierbarkeit, da von herkömmlichen Switches höchstens 1000 VLAN-IDs von maximal 4094 möglichen VLANs unterstützt werden.  

-   Beschränkt durch ein einzelnes IP-Subnetz, wodurch die Anzahl an Knoten in einem einzelnen VLAN begrenzt und die Platzierung virtueller Computer auf der Grundlage der physischen Speicherorte eingeschränkt ist. Zwar können VLANs standortübergreifend erweitert werden, das gesamte VLAN muss sich jedoch im selben Subnetz befinden.  

**IP-Adresszuweisung**  

Zusätzlich zu den Nachteilen, die durch VLANs angezeigt werden, stellt die IP-adressenzuweisung für virtuelle Maschine Probleme, z. b:  

-   Die physischen Speicherorte in der Datencenternetzwerkinfrastruktur bestimmen die IP-Adressen der virtuellen Computer. Im Ergebnis bedeutet dies, dass bei einer Verschiebung in die Cloud normalerweise eine Änderung der IP-Adressen für die Dienstarbeitsauslastungen erforderlich ist.  

-   Die Richtlinien wie Firewallregeln, Ressourcenerkennungs- und Verzeichnisdienste, sind an IP-Adressen gebunden. Eine Änderung der IP-Adressen bedeutet also auch eine erforderliche Aktualisierung aller zugeordneten Richtlinien.  

-   Die Bereitstellung virtueller Computer und die Datenverkehrisolierung sind von der Topologie abhängig.  

Wenn Datencenter-Netzwerkadministratoren die physische Form des Datencenters planen, müssen sie die physische Platzierung und Weiterleitung der Subnetze definieren. Die entsprechenden Entscheidungen erfolgen auf der Grundlage der IP- und Ethernet-Technologie, die sich auf die potenziellen IP-Adressen auswirken, die für virtuelle Computer, die auf einem bestimmten Server oder einem Blade, der sich in einem bestimmten Rack im Datencenter befindet, ausgeführt werden. Bei der Bereitstellung und Platzierung eines virtuellen Computers im Datencenter müssen diese Auswahloptionen und Einschränkungen in Bezug auf die IP-Adressen berücksichtigt werden. In der Regel führt dies dazu, dass die Datencenteradministratoren den virtuellen Computern neue IP-Adressen zuweisen.  

Das Problem bei dieser Anforderung besteht darin, dass eine IP-Adresse nicht nur einfach eine Adresse darstellt, sondern dass ihr semantische Informationen zugeordnet sind. Ein Subnetz kann beispielsweise bestimmte Dienste enthalten oder sich an einem dedizierten physischen Speicherort befinden. Firewallregeln, Zugriffssteuerungsregeln und IP-Sicherheitszuordnungen sind häufig mit IP-Adressen verknüpft. Bei einer Änderung der IP-Adressen muss der Besitzer des virtuellen Computers alle entsprechenden Richtlinien anpassen, die auf den ursprünglichen IP-Adressen basieren. Der Aufwand für eine solche Neunummerierung ist dermaßen hoch, dass sich viele Unternehmen dafür entscheiden, nur neue Dienste in der Cloud bereitzustellen und bereits vorhandene Anwendungen wie gehabt zu verwenden.  

Bei der Hyper-V-Netzwerkvirtualisierung werden die virtuellen Netzwerke für die virtuellen Computer der Kunden von der physischen Netzwerkinfrastruktur abgekoppelt. Dies bedeutet wiederum, dass die virtuellen Computer der Kunden ihre ursprünglichen IP-Adressen beibehalten können, während die virtuellen Computer der Kunden von den Datencenteradministratoren an einem beliebigen Speicherort im Datencenter bereitgestellt werden können, ohne dass eine Neukonfiguration der physischen IP-Adressen oder VLAN-IDs erforderlich ist. Im folgenden Abschnitt wird die eigentliche Funktionalität erläutert.  

## <a name="BKMK_NEW"></a>Wichtige Funktionen  
Im folgenden finden eine Übersicht der Hauptfunktionen, Vorteile und Funktionen der Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016:  

-   **Ermöglicht flexible arbeitsauslastungsplatzierung – von Netzwerkisolation und IP-Adresse erneut verwenden, ohne VLANs**  

    Hyper-V-Netzwerkvirtualisierung entkoppelt des Kunden virtuelle Netzwerke von der physischen Netzwerkinfrastruktur der Hoster, Workload Platzierungen innerhalb der Rechenzentren ermöglichen. Die Platzierung der Arbeitsauslastungen virtueller Computer ist damit nicht länger auf die IP-Adressenzuweisung oder VLAN-Isolationsanforderungen des physischen Netzwerks beschränkt, da die Platzierung nun innerhalb der Hyper-V-Hosts erzwungen wird, die auf softwaredefinierten, mehrinstanzfähigen Virtualisierungsrichtlinien basieren.  

    Virtuelle Computer anderer Kunden mit überlappenden IP-Adressen können nun auf demselben Hostserver bereitgestellt werden, ohne dass eine schwerfällige VLAN-Konfiguration oder eine Verletzung der IP-Adressenhierarchie erforderlich ist. Auf diese Weise kann die Migration der Kundenarbeitsauslastungen zu freigegebenen IaaS-Hostinganbietern vereinfacht werden: Kunden erhalten die Möglichkeit, die entsprechenden Arbeitsauslastungen ohne Änderungen zu verschieben, d. h. auch die IP-Adressen der virtuellen Computer können unverändert beibehalten werden. Für den Hostinganbieter, der zahlreiche Kunden unterstützt, die ihren derzeitigen Netzwerkadressraum in ein freigegebenes IaaS-Datencenter erweitern möchten, stellt dies eine komplexe Aufgabe im Hinblick auf die Konfiguration und Wartung der isolierten VLANs für die einzelnen Kunden dar, um die Koexistenz potenziell überlappender Adressräume zu gewährleisten. Mit der Hyper-V-Netzwerkvirtualisierung wurde die Unterstützung von Adressüberlappungen vereinfacht und es ist ein geringerer Anteil an Netzwerkneukonfiguration durch den Hostinganbieter erforderlich.  

    Außerdem können die Wartung der physischen Infrastruktur und Upgrades ohne Ausfallzeiten im Hinblick auf die Kundenarbeitsauslastungen ausgeführt werden. Mithilfe der Hyper-V-Netzwerkvirtualisierung können virtuelle Computer auf bzw. in einem bestimmten Host, Rack, Subnetz oder VLAN oder gesamte Cluster migriert werden, ohne dass eine Änderung der physischen IP-Adressen oder eine umfangreiche Neukonfiguration erforderlich ist.  

-   **Ermöglicht einer einfacheren Verschiebung von Workloads in einer freigegebenen IaaS-cloud**  

    Bei der Hyper-V-Netzwerkvirtualisierung bleiben IP-Adressen sowie die Konfiguration der virtuellen Computer unverändert. Dadurch ist es für IT-Organisationen deutlich einfacher, Arbeitsauslastungen aus ihren Datencentern zu einem freigegebenem IaaS-Hostinganbieter zu verschieben, da nur eine minimale Neukonfiguration der Arbeitsauslastung oder der Infrastrukturtools und -richtlinien erforderlich ist. Sofern eine Konnektivität zwischen den beiden Datencentern besteht, können IT-Administratoren weiterhin ihre Tools verwenden, ohne diese neu konfigurieren zu müssen.  

-   **Ermöglicht die Livemigration über Subnetze hinweg**  

    Livemigration von arbeitsauslastungen virtueller Computer wurde auf der gleichen IP-Subnetz oder VLAN beschränkt bisher da subnetzübergreifenden Gast-Betriebssystem so ändern Sie die IP-Adresse des virtuellen Computers erforderlich. Durch einen derartigen Adressenwechsel werden die bestehende Kommunikation und die auf dem virtuellen Computer ausgeführten Dienste unterbrochen. Bei der Hyper-V-Netzwerkvirtualisierung können arbeitsauslastungen live werden von Servern mit Windows Server 2016 in einem Subnetz auf Servern unter Windows Server 2016 in einem anderen Subnetz ohne Änderung der IP-Adressen für die arbeitsauslastung. Mit der Hyper-V-Netzwerkvirtualisierung wird sichergestellt, dass Änderungen am Speicherort des virtuellen Computers, die durch die Livemigration bedingt sind, zwischen den Hosts aktualisiert und synchronisiert werden, die kontinuierlich mit dem migrierten virtuellen Computer in Verbindung stehen.  

-   **Ermöglicht eine einfachere Verwaltung des entkoppelten Servers und Netzwerks-Verwaltung**  

    Die Platzierung der Serverarbeitsauslastung wurde vereinfacht, da die Migration und die Platzierung der Arbeitsauslastungen unabhängig von der zugrunde liegenden physischen Netzwerkkonfigurationen sind. Serveradministratoren können sich auf die Verwaltung von Diensten und Servern konzentrieren, Netzwerkadministratoren können sich hingegen vollständig auf die Netzwerkstruktur und die Datenverkehrsverwaltung konzentrieren. Dadurch erhalten Datencenter-Serveradministratoren die Möglichkeit, virtuelle Computer bereitzustellen und zu migrieren, ohne die IP-Adressen der virtuellen Computer ändern zu müssen. Dies führt zu einer deutlichen Reduzierung des Mehraufwands, da bei der Hyper-V-Netzwerkvirtualisierung die Platzierung der virtuellen Computer unabhängig von der Netzwerktopologie erfolgt. Daher werden auch weniger Netzwerkadministratoren benötigt, die bei der Platzierung die Isolationsgrenzen ändern müssen.  

-   **Vereinfachung des Netzwerks und verbessert die Server/netzwerkressourcenauslastung**  

    Die starren Vorgaben der VLANs und die Abhängigkeit der virtuellen Computer bei der Platzierung in einer physischen Netzwerkinfrastruktur führen zu einer Überversorgung und Unterauslastung. Die Aufhebung dieser Abhängigkeit ermöglicht die verbesserte Flexibilität im Hinblick auf die Platzierung der virtuellen Computer, vereinfacht die Netzwerkverwaltung und verbessert zugleich die Server-/Netzwerkressourcenauslastung. Beachten Sie, dass die Hyper-V-Netzwerkvirtualisierung VLANs im Kontext physischer Datencenter unterstützt. So kann beispielsweise der gesamte Hyper-V-Netzwerkvirtualisierungs-Datenverkehr für ein Datencenter in einem bestimmten VLAN erfolgen.  

-   **Ist kompatibel mit der vorhandenen Infrastruktur und sich entwickelnder Technologie**  

    Hyper-V-Netzwerkvirtualisierung kann in heutigen Datencentern bereitgestellt werden, aber es ist kompatibel mit neue Datacenter "flaches Netzwerk%"-Technologien.  

    Unterstützt z. B. HNV unter Windows Server 2016 paketkapselungsformat, das die VXLAN und Open vSwitches Datenbank Management Protocol (OVSDB) als die SouthBound Schnittstelle (SBI)...  

-   **Bietet für Interoperabilität und ökosystemvorbereitung**  

    Bei der Hyper-V-Netzwerkvirtualisierung werden verschiedene Konfigurationen für die Kommunikation mit bestehenden Ressourcen wie übergreifende Konnektivität vor Ort, SAN (Storage Area Network), nicht-virtualisierter Ressourcenzugriff usw. unterstützt. Microsoft hat sich zu einer Zusammenarbeit mit verschiedenen Ökosystempartnern verpflichtet, um die Benutzererfahrung für die Hyper-V-Netzwerkvirtualisierung im Hinblick auf Leistung, Skalierbarkeit und Verwaltbarkeit zu unterstützen und weiter zu optimieren.  

-   **Richtlinienbasierte Konfiguration**  

    Netzwerkvirtualisierungsrichtlinien in Windows Server 2016 werden über den Microsoft-Netzwerkcontroller konfiguriert. Die Netzwerkcontroller ist eine RESTful northbound-API und Windows PowerShell-Schnittstelle, um die Richtlinie zu konfigurieren. Weitere Informationen zu Microsoft-Netzwerkcontroller, finden Sie unter [Netzwerkcontroller](../../../sdn/technologies/network-controller/../../../sdn/technologies/network-controller/Network-Controller.md).  

## <a name="BKMK_SOFT"></a>Softwareanforderungen  
Hyper-V-Netzwerkvirtualisierung mit Microsoft-Netzwerkcontroller ist erforderlich, Windows Server 2016 und die Hyper-V-Rolle.  

## <a name="BKMK_LINKS"></a>Siehe auch  
Finden Sie weitere Informationen zu Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016 die folgenden Links:  


|       Inhaltstyp       |                                                                                                                                Verweise                                                                                                                                |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Community-Ressourcen**  |     -   [Architektur von Private Clouds-Blog](https://blogs.technet.com/b/privatecloud/archive/2012/03/19/cloud-datacenter-network-architecture-in-the-windows-server-8-era.aspx)<br />-Stellen Sie Fragen: [cloudnetfb@microsoft.com](mailto:%20cloudnetfb@microsoft.com)     |
|         **RFC**          |                                                                                                     -   VXLAN - [RFC 7348](https://www.rfc-editor.org/info/rfc7348)                                                                                                      |
| **Verwandte Technologien** | -   [Netzwerkcontroller](../../../sdn/technologies/network-controller/../../../sdn/technologies/network-controller/Network-Controller.md)<br />-   [Hyper-V-Netzwerkvirtualisierung – Übersicht](assetId:///bf1dba9d-1960-4dd2-a5e2-99466a02044b) (Windows Server 2012 R2) |

