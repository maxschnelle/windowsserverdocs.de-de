---
title: Übersicht über die Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016
description: Dieses Thema bietet einen Überblick über die Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0115b7ad-d229-4c69-9d7e-a3f5fbaa3b2f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0eda30b0980f2080f1603eb906fd308440316248
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405951"
---
# <a name="hyper-v-network-virtualization-overview-in-windows-server-2016"></a>Übersicht über die Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In Windows Server 2016 und Virtual Machine Manager bietet Microsoft eine End-to-End-Lösung für die Netzwerkvirtualisierung.  Es gibt fünf Hauptkomponenten, die die netzwerkvirtualisierungslösung von Microsoft umfasst:  

-   **Windows Azure Pack für Windows Server** stellt ein Mandanten Portal zum Erstellen virtueller Netzwerke und ein Verwaltungs Portal zum Verwalten virtueller Netzwerke bereit.  

-   Mit **Virtual Machine Manager** (VMM) wird die zentrale Verwaltung der netzwerkfabric ermöglicht.  

-   **Microsoft Network Controller** bietet einen zentralisierten, programmierbaren Automatisierungs Punkt für die Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Daten Center.  

-   Mit **Hyper-V-Netzwerkvirtualisierung** wird die zum Virtualisieren des Netzwerkdatenverkehrs benötigte Infrastruktur bereitgestellt.  

-   Mit **Hyper-V-netzwerkvirtualisierungsgateways** werden Verbindungen zwischen virtuellen und physischen Netzwerken bereitgestellt.  

In diesem Thema werden Konzepte vorgestellt und die wichtigsten Vorteile und Funktionen der Hyper-V-Netzwerkvirtualisierung (ein Teil der gesamten Lösung für die Netzwerkvirtualisierung) in Windows Server 2016 erläutert. Es wird erläutert, wie die Netzwerkvirtualisierung sowohl für private Clouds bei der Konsolidierung von Unternehmensarbeitsauslastungen sowie für Anbieter von IaaS-basierten (Infrastructure as a Service) öffentlichen Clouddiensten Vorteile bietet.  

Weitere technische Details zur Netzwerkvirtualisierung in Windows Server 2016 finden Sie unter [Technische Details zur Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016](../../../sdn/technologies/hyper-v-network-virtualization/hyperv-network-virtualization-technical-details-windows-server.md).  

**Meinten Sie**  

-   [Übersicht über die Hyper-V-Netzwerkvirtualisierung](assetId:///bf1dba9d-1960-4dd2-a5e2-99466a02044b) (Windows Server 2012 R2)  

-   [Übersicht über Hyper-V](assetId:///5aad349f-ef06-464a-b36f-366fbb040143)  

-   [Virtueller Hyper-V-Switch (Übersicht)](assetId:///e6ec46af-6ef4-49b3-b1f1-5268dc03f05b)  

## <a name="BKMK_OVER"></a>Funktionsbeschreibung  
Bei der Hyper-V-Netzwerkvirtualisierung werden "virtuelle Netzwerke" (VM-Netzwerk) virtuellen Computern ähnlich wie bei der Servervirtualisierung (Hypervisor) für das Betriebssystem bereitgestellt. Bei der Netzwerkvirtualisierung werden virtuelle Netzwerke von der physischen Netzwerkinfrastruktur entkoppelt und die Einschränkungen von VLAN und hierarchischer IP-Adressenzuweisung von der Bereitstellung virtueller Computer getrennt. Diese Flexibilität erleichtert es Kunden, zu IaaS-Clouds zu wechseln, und gewährt Hostern und Datencenteradministratoren Effizienz bei der Infrastrukturverwaltung. Gleichzeitig bleiben die erforderliche mehrinstanzenfähige Isolation und Sicherheitsanforderungen erhalten, und die IP-Adressen-Überlappung virtueller Computer wird unterstützt.  

Kunden wünschen sich eine Möglichkeit für eine nahtlose Ausweitung ihrer Datencenter in die Cloud. Heute bestehen die technischen Herausforderungen darin, nahtlose hybride Cloudarchitekturen zu erstellen. Eine der größten Hürden, denen Kunden begegnen, ist die Wiederverwendung Ihrer vorhandenen Netzwerktopologien (Subnetze, IP-Adressen, Netzwerkdienste usw.) in der Cloud und die Überbrückung zwischen Ihren lokalen Ressourcen und ihren cloudressourcen.  Die Hyper-V-Netzwerkvirtualisierung umfasst das Konzept eines VM-Netzwerks, das unabhängig von dem zugrunde liegenden physischen Netzwerk ist. Bei diesem Konzept für VM-Netzwerke, die sich aus einem oder mehreren virtuellen Subnetzen zusammensetzen, wird der exakte Speicherort virtueller Computer im physischen Netzwerk von der Topologie des virtuellen Netzwerks entkoppelt. Dadurch können Kunden ihre virtuellen Subnetze auf einfache Weise in die Cloud verschieben und dabei gleichzeitig die bestehenden IP-Adressen und die Topologie in der Cloud beibehalten, sodass vorhandene Dienste weiterhin verwendet werden können, unabhängig von deren physischem Speicherort in den Subnetzen. Dies bedeutet, dass mit der Hyper-V-Netzwerkvirtualisierung eine nahtlose Hybrid-Cloud zur Verfügung steht.  

Neben Hybrid-Clouds konsolidieren zahlreiche Unternehmen ihre Datencenter und erstellen private Clouds, um die Effizienz und Skalierbarkeit von Cloud-Architekturen intern nutzen zu können. Die Hyper-V-Netzwerkvirtualisierung ermöglicht eine bessere Flexibilität und Effizienz für Private Clouds, indem die Netzwerktopologie einer Geschäftseinheit von der eigentlichen physischen Netzwerktopologie entkoppelt wird. Auf diese Weise können Geschäftseinheiten trotz räumlicher Trennung gemeinsam eine interne private Cloud verwenden und vorhandene Netzwerktopologien beibehalten. Das für den Datencenterbetrieb verantwortliche Team hat die Flexibilität, Arbeitsauslastungen bereitzustellen und innerhalb des Datencenters ohne Serverunterbrechungen dynamisch zu verschieben, wodurch eine höhere Betriebseffizienz und ein Datencenter mit einer insgesamt höheren Effektivität ermöglicht wird.  

Der Hauptvorteil von workloadbesitzern besteht darin, dass Sie jetzt Ihre Workloads "Topologien" in die Cloud verschieben können, ohne Ihre IP-Adressen ändern oder Ihre Anwendungen umschreiben zu müssen. So besteht beispielsweise eine typische dreistufige Branchenanwendungen aus einer Front-End-Ebene, einer Geschäftslogik-Ebene und einer Datenbank-Ebene. Mithilfe von Richtlinien kann der Kunde bei der Hyper-V-Netzwerkvirtualisierung alle Ebenen oder Teile der drei Ebenen in die Cloud integrieren und die Weiterleitungstopologie sowie die IP-Adressen der Dienste (d. h. die IP-Adressen der virtuellen Computer) beibehalten, ohne dass Änderungen an den Anwendungen vorgenommen werden müssen.  

Infrastrukturbesitzer erhalten dank der zusätzlichen Flexibilität bei der Platzierung virtueller Computer die Möglichkeit, Arbeitsauslastungen an beliebige Speicherorte in den Datencentern verschieben zu können, ohne die virtuellen Computer ändern oder die Netzwerke neu konfigurieren zu müssen. Die Hyper-V-Netzwerkvirtualisierung ermöglicht beispielsweise eine subnetzübergreifende Livemigration, sodass ein virtueller Computer an einem beliebigen Speicherort im Datencenter ohne Dienstunterbrechung eine Livemigration ausführen kann. Bisher waren Livemigrationen auf dasselbe Subnetz beschränkt und bedeuteten somit auch Einschränkungen im Hinblick darauf, wo sich die virtuellen Computer befinden können. Bei der subnetzübergreifenden Livemigration können Administratoren die Arbeitsauslastungen auf der Grundlage des dynamischen Ressourcenbedarfs und der Energieeffizienz konsolidieren und eine Infrastrukturwartung ohne Betriebszeitunterbrechung der Kundenarbeitsauslastung gewährleisten.  

## <a name="BKMK_APP"></a>Praktische Anwendungen  
Mit dem Erfolg virtualisierter Datencenter haben IT-Organisationen und Hostinganbieter (Anbieter, die eine Zusammenstellung oder Vermietung physischer Server bereitstellen) begonnen, flexiblere virtualisierte Infrastrukturen anzubieten, und das erleichtert die bedarfsorientierte Bereitstellung von Serverinstanzen für ihre Kunden. Diese neue Art von Dienst wird als %%amp;quot;Infrastructure as a Service (IaaS)%%amp;quot; bezeichnet. Windows Server 2016 bietet alle erforderlichen Plattformfunktionen, damit Unternehmenskunden Private Clouds erstellen und zu einem IT-as-a-Service-Betriebsmodell wechseln können. Windows Server 2016 2016 ermöglicht Hostern auch, öffentliche Clouds zu erstellen und ihren Kunden IaaS-Lösungen anzubieten. In Kombination mit Virtual Machine Manager und Windows Azure Pack zur Verwaltung der Hyper-V-netzwerkvirtualisierungsrichtlinie stellt Microsoft eine leistungsstarke cloudlösung bereit.  

Die Hyper-V-Netzwerkvirtualisierung von Windows Server 2016 bietet eine Richtlinien basierte, softwaregesteuerte Netzwerkvirtualisierung, die den Verwaltungsaufwand reduziert, der von Unternehmen bei der Erweiterung dedizierter IaaS-Clouds festgestellt wird, und cloudhoster verbessern. Flexibilität und Skalierbarkeit für die Verwaltung virtueller Computer, um eine höhere Ressourcennutzung zu erzielen.  

Für ein IaaS-Szenario mit virtuellen Computern aus unterschiedlichen Organisationseinheiten (dedizierte Cloud) oder von unterschiedlichen Kunden (gehostete Cloud) ist eine sichere Isolation notwendig. Die heutige Lösung, virtuelle lokale Netzwerke (Virtual Local Area Networks, VLANs), kann in diesem Szenario erhebliche Nachteile darstellen.  

**VLANs**  

Derzeit sind VLANs der Mechanismus, den die meisten Organisationen verwenden, um die Wiederverwendung von Adressräumen und die Mandanten Isolation zu unterstützen. In einem VLAN wird explizites Tagging (VLAN-ID) in den Ethernet-Frame-Headers verwendet, und Ethernet-Switches sind dafür verantwortlich, die Isolation zu erzwingen und den Datenverkehr auf Netzwerkknoten mit derselben VLAN-ID zu beschränken Dabei bestehen für VLANs die folgenden entscheidenden Nachteile:  

-   Erhöhtes Risiko einer unbeabsichtigten Ausfallzeit aufgrund der schwerfälligen Neukonfiguration der Produktions-Switches, wenn virtuelle Computer oder Isolationsgrenzen in das dynamische Datencenter verschoben werden.  

-   Begrenzte Skalierbarkeit, da von herkömmlichen Switches höchstens 1000 VLAN-IDs von maximal 4094 möglichen VLANs unterstützt werden.  

-   Beschränkt durch ein einzelnes IP-Subnetz, wodurch die Anzahl an Knoten in einem einzelnen VLAN begrenzt und die Platzierung virtueller Computer auf der Grundlage der physischen Speicherorte eingeschränkt ist. Zwar können VLANs standortübergreifend erweitert werden, das gesamte VLAN muss sich jedoch im selben Subnetz befinden.  

**IP-Adresszuweisung**  

Zusätzlich zu den von VLANs dargestellten Nachteilen werden bei der Zuweisung von IP-Adressen für virtuelle Computerprobleme angezeigt. Hierzu gehören:  

-   Die physischen Speicherorte in der Datencenternetzwerkinfrastruktur bestimmen die IP-Adressen der virtuellen Computer. Im Ergebnis bedeutet dies, dass bei einer Verschiebung in die Cloud normalerweise eine Änderung der IP-Adressen für die Dienstarbeitsauslastungen erforderlich ist.  

-   Die Richtlinien wie Firewallregeln, Ressourcenerkennungs- und Verzeichnisdienste, sind an IP-Adressen gebunden. Eine Änderung der IP-Adressen bedeutet also auch eine erforderliche Aktualisierung aller zugeordneten Richtlinien.  

-   Die Bereitstellung virtueller Computer und die Datenverkehrisolierung sind von der Topologie abhängig.  

Wenn Datencenter-Netzwerkadministratoren die physische Form des Datencenters planen, müssen sie die physische Platzierung und Weiterleitung der Subnetze definieren. Die entsprechenden Entscheidungen erfolgen auf der Grundlage der IP- und Ethernet-Technologie, die sich auf die potenziellen IP-Adressen auswirken, die für virtuelle Computer, die auf einem bestimmten Server oder einem Blade, der sich in einem bestimmten Rack im Datencenter befindet, ausgeführt werden. Bei der Bereitstellung und Platzierung eines virtuellen Computers im Datencenter müssen diese Auswahloptionen und Einschränkungen in Bezug auf die IP-Adressen berücksichtigt werden. In der Regel führt dies dazu, dass die Datencenteradministratoren den virtuellen Computern neue IP-Adressen zuweisen.  

Das Problem bei dieser Anforderung besteht darin, dass eine IP-Adresse nicht nur einfach eine Adresse darstellt, sondern dass ihr semantische Informationen zugeordnet sind. Ein Subnetz kann beispielsweise bestimmte Dienste enthalten oder sich an einem dedizierten physischen Speicherort befinden. Firewallregeln, Zugriffssteuerungsregeln und IP-Sicherheitszuordnungen sind häufig mit IP-Adressen verknüpft. Bei einer Änderung der IP-Adressen muss der Besitzer des virtuellen Computers alle entsprechenden Richtlinien anpassen, die auf den ursprünglichen IP-Adressen basieren. Der Aufwand für eine solche Neunummerierung ist dermaßen hoch, dass sich viele Unternehmen dafür entscheiden, nur neue Dienste in der Cloud bereitzustellen und bereits vorhandene Anwendungen wie gehabt zu verwenden.  

Bei der Hyper-V-Netzwerkvirtualisierung werden die virtuellen Netzwerke für die virtuellen Computer der Kunden von der physischen Netzwerkinfrastruktur abgekoppelt. Dies bedeutet wiederum, dass die virtuellen Computer der Kunden ihre ursprünglichen IP-Adressen beibehalten können, während die virtuellen Computer der Kunden von den Datencenteradministratoren an einem beliebigen Speicherort im Datencenter bereitgestellt werden können, ohne dass eine Neukonfiguration der physischen IP-Adressen oder VLAN-IDs erforderlich ist. Im folgenden Abschnitt wird die eigentliche Funktionalität erläutert.  

## <a name="BKMK_NEW"></a>Wichtige Funktionen  
Im folgenden finden Sie eine Liste der wichtigsten Funktionen, Vorteile und Funktionen der Hyper-V-Netzwerkvirtualisierung in Windows Server 2016:  

-   **Ermöglicht flexible Arbeits Auslastungs Platzierung: Netzwerk Isolation und Wiederverwendung von IP-Adressen ohne VLANs**  

    Bei der Hyper-V-Netzwerkvirtualisierung werden die virtuellen Netzwerke des Kunden von der physischen Netzwerkinfrastruktur der Hoster abgekoppelt, sodass in den Rechenzentren die Kosten für die Arbeits Auslastungs Platzierung gewährleistet sind. Die Platzierung der Arbeitsauslastungen virtueller Computer ist damit nicht länger auf die IP-Adressenzuweisung oder VLAN-Isolationsanforderungen des physischen Netzwerks beschränkt, da die Platzierung nun innerhalb der Hyper-V-Hosts erzwungen wird, die auf softwaredefinierten, mehrinstanzfähigen Virtualisierungsrichtlinien basieren.  

    Virtuelle Computer anderer Kunden mit überlappenden IP-Adressen können nun auf demselben Hostserver bereitgestellt werden, ohne dass eine schwerfällige VLAN-Konfiguration oder eine Verletzung der IP-Adressenhierarchie erforderlich ist. Auf diese Weise kann die Migration der Kundenarbeitsauslastungen zu freigegebenen IaaS-Hostinganbietern vereinfacht werden: Kunden erhalten die Möglichkeit, die entsprechenden Arbeitsauslastungen ohne Änderungen zu verschieben, d. h. auch die IP-Adressen der virtuellen Computer können unverändert beibehalten werden. Für den Hostinganbieter, der zahlreiche Kunden unterstützt, die ihren derzeitigen Netzwerkadressraum in ein freigegebenes IaaS-Datencenter erweitern möchten, stellt dies eine komplexe Aufgabe im Hinblick auf die Konfiguration und Wartung der isolierten VLANs für die einzelnen Kunden dar, um die Koexistenz potenziell überlappender Adressräume zu gewährleisten. Mit der Hyper-V-Netzwerkvirtualisierung wurde die Unterstützung von Adressüberlappungen vereinfacht und es ist ein geringerer Anteil an Netzwerkneukonfiguration durch den Hostinganbieter erforderlich.  

    Außerdem können die Wartung der physischen Infrastruktur und Upgrades ohne Ausfallzeiten im Hinblick auf die Kundenarbeitsauslastungen ausgeführt werden. Mithilfe der Hyper-V-Netzwerkvirtualisierung können virtuelle Computer auf bzw. in einem bestimmten Host, Rack, Subnetz oder VLAN oder gesamte Cluster migriert werden, ohne dass eine Änderung der physischen IP-Adressen oder eine umfangreiche Neukonfiguration erforderlich ist.  

-   **Ermöglicht einfachere Verschiebungen für Workloads in eine freigegebene IaaS-Cloud.**  

    Bei der Hyper-V-Netzwerkvirtualisierung bleiben IP-Adressen sowie die Konfiguration der virtuellen Computer unverändert. Dadurch ist es für IT-Organisationen deutlich einfacher, Arbeitsauslastungen aus ihren Datencentern zu einem freigegebenem IaaS-Hostinganbieter zu verschieben, da nur eine minimale Neukonfiguration der Arbeitsauslastung oder der Infrastrukturtools und -richtlinien erforderlich ist. Sofern eine Konnektivität zwischen den beiden Datencentern besteht, können IT-Administratoren weiterhin ihre Tools verwenden, ohne diese neu konfigurieren zu müssen.  

-   **Ermöglicht die Live Migration zwischen Subnetzen.**  

    Die Live Migration von Arbeits Auslastungen virtueller Computer wurde traditionell auf dasselbe IP-Subnetz oder VLAN beschränkt, da das Gast Betriebssystem des virtuellen Computers die IP-Adresse des virtuellen Computers ändern muss. Durch einen derartigen Adressenwechsel werden die bestehende Kommunikation und die auf dem virtuellen Computer ausgeführten Dienste unterbrochen. Bei der Hyper-V-Netzwerkvirtualisierung können Arbeits Auslastungen von Servern mit Windows Server 2016 in einem Subnetz auf Server mit Windows Server 2016 in einem anderen Subnetz migriert werden, ohne dass die IP-Adressen der Arbeitsauslastung geändert werden. Mit der Hyper-V-Netzwerkvirtualisierung wird sichergestellt, dass Änderungen am Speicherort des virtuellen Computers, die durch die Livemigration bedingt sind, zwischen den Hosts aktualisiert und synchronisiert werden, die kontinuierlich mit dem migrierten virtuellen Computer in Verbindung stehen.  

-   **Ermöglicht eine einfachere Verwaltung der entkoppelten Server-und Netzwerkverwaltung**  

    Die Platzierung der Serverarbeitsauslastung wurde vereinfacht, da die Migration und die Platzierung der Arbeitsauslastungen unabhängig von der zugrunde liegenden physischen Netzwerkkonfigurationen sind. Serveradministratoren können sich auf die Verwaltung von Diensten und Servern konzentrieren, Netzwerkadministratoren können sich hingegen vollständig auf die Netzwerkstruktur und die Datenverkehrsverwaltung konzentrieren. Dadurch erhalten Datencenter-Serveradministratoren die Möglichkeit, virtuelle Computer bereitzustellen und zu migrieren, ohne die IP-Adressen der virtuellen Computer ändern zu müssen. Dies führt zu einer deutlichen Reduzierung des Mehraufwands, da bei der Hyper-V-Netzwerkvirtualisierung die Platzierung der virtuellen Computer unabhängig von der Netzwerktopologie erfolgt. Daher werden auch weniger Netzwerkadministratoren benötigt, die bei der Platzierung die Isolationsgrenzen ändern müssen.  

-   **Vereinfachung des Netzwerks und Verbesserung der Server-/netzwerkressourcenverwendung**  

    Die starren Vorgaben der VLANs und die Abhängigkeit der virtuellen Computer bei der Platzierung in einer physischen Netzwerkinfrastruktur führen zu einer Überversorgung und Unterauslastung. Die Aufhebung dieser Abhängigkeit ermöglicht die verbesserte Flexibilität im Hinblick auf die Platzierung der virtuellen Computer, vereinfacht die Netzwerkverwaltung und verbessert zugleich die Server-/Netzwerkressourcenauslastung. Beachten Sie, dass die Hyper-V-Netzwerkvirtualisierung VLANs im Kontext physischer Datencenter unterstützt. So kann beispielsweise der gesamte Hyper-V-Netzwerkvirtualisierungs-Datenverkehr für ein Datencenter in einem bestimmten VLAN erfolgen.  

-   **Ist kompatibel mit vorhandener Infrastruktur und neuer Technologie**  

    Die Hyper-V-Netzwerkvirtualisierung kann im heutigen Rechenzentrum bereitgestellt werden, aber Sie ist mit den Technologien des neuen Rechenzentrums "Flat Network" kompatibel.  

    Beispielsweise unterstützt HNV in Windows Server 2016 das vxlan-Kapselungs Format und das Open Vswitch Database Management Protocol (ovsdb) als Southbound Interface (SBI).  

-   **Bietet Interoperabilität und Ökosystem Bereitschaft**  

    Bei der Hyper-V-Netzwerkvirtualisierung werden verschiedene Konfigurationen für die Kommunikation mit bestehenden Ressourcen wie übergreifende Konnektivität vor Ort, SAN (Storage Area Network), nicht-virtualisierter Ressourcenzugriff usw. unterstützt. Microsoft hat sich zu einer Zusammenarbeit mit verschiedenen Ökosystempartnern verpflichtet, um die Benutzererfahrung für die Hyper-V-Netzwerkvirtualisierung im Hinblick auf Leistung, Skalierbarkeit und Verwaltbarkeit zu unterstützen und weiter zu optimieren.  

-   **Richtlinien basierte Konfiguration**  

    Netzwerkvirtualisierungsrichtlinien in Windows Server 2016 werden über den Microsoft-Netzwerk Controller konfiguriert. Der Netzwerk Controller verfügt über eine Rest-Northbound-API und eine Windows PowerShell-Schnittstelle zum Konfigurieren der Richtlinie. Weitere Informationen zum Microsoft-Netzwerk Controller finden Sie unter [Netzwerk Controller](../../../sdn/technologies/network-controller/../../../sdn/technologies/network-controller/Network-Controller.md).  

## <a name="BKMK_SOFT"></a>Software Anforderungen  
Die Hyper-v-Netzwerkvirtualisierung unter Verwendung des Microsoft-Netzwerk Controllers erfordert Windows Server 2016 und die Hyper-v-Rolle.  

## <a name="BKMK_LINKS"></a>Siehe auch  
Weitere Informationen zur Hyper-V-Netzwerkvirtualisierung unter Windows Server 2016 finden Sie unter den folgenden Links:  


|       Inhaltstyp       |                                                                                                                                Verweise                                                                                                                                |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Communityressourcen**  |     Blog zur -   [Private Cloud-Architektur](https://blogs.technet.com/b/privatecloud/archive/2012/03/19/cloud-datacenter-network-architecture-in-the-windows-server-8-era.aspx)<br />-Stellen Sie Fragen: [cloudnetfb@microsoft.com](mailto:%20cloudnetfb@microsoft.com)     |
|         **RFC**          |                                                                                                     -Vxlan: [RFC 7348](https://www.rfc-editor.org/info/rfc7348)                                                                                                      |
| **Verwandte Technologien** | [Netzwerk Controller](../../../sdn/technologies/network-controller/../../../sdn/technologies/network-controller/Network-Controller.md) -   <br />-   [Übersicht über die Hyper-V-Netzwerkvirtualisierung](assetId:///bf1dba9d-1960-4dd2-a5e2-99466a02044b) (Windows Server 2012 R2) |

