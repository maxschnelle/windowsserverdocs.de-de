---
title: 'Azure Stack HCI: Übersicht'
description: Azure Stack HCI ist ein hyperkonvergenter Windows Server 2019-Cluster, bei dem überprüfte Hardware beispielsweise zum lokalen Ausführen von virtualisierten Workloads, optionalen Herstellen einer Verbindung mit Azure-Diensten für cloudbasierte Sicherungen und Durchführen der Standortwiederherstellung genutzt wird. Für Azure Stack HCI-Lösungen wird mit von Microsoft überprüfter Hardware die optimale Leistung und Zuverlässigkeit sichergestellt, und Technologiekomponenten wie NVMe-Laufwerke, beständiger Speicher und RDMA-Netzwerke (Remote Direct Memory Access, Remotezugriff auf den direkten Speicher) werden unterstützt.
ms.technology: storage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 05/22/2019
ms.openlocfilehash: 92d600eeb833cd70bd714702b1fd950c4fe2cd87
ms.sourcegitcommit: b190fac4bfa5599751a60d3fc3b4c4a64dd9afd7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/22/2019
ms.locfileid: "66008978"
---
# <a name="azure-stack-hci-overview"></a>Azure Stack HCI: Übersicht

>Gilt für: Windows Server 2019

Azure Stack HCI ist ein hyperkonvergenter Windows Server 2019-Cluster, bei dem überprüfte Hardware beispielsweise zum lokalen Ausführen von virtualisierten Workloads, optionalen Herstellen einer Verbindung mit Azure-Diensten für cloudbasierte Sicherungen und Durchführen der Standortwiederherstellung genutzt wird. Für Azure Stack HCI-Lösungen wird mit von Microsoft überprüfter Hardware die optimale Leistung und Zuverlässigkeit sichergestellt, und Technologiekomponenten wie NVMe-Laufwerke, beständiger Speicher und RDMA-Netzwerke (Remote Direct Memory Access, Remotezugriff auf den direkten Speicher) werden unterstützt.

Azure Stack HCI ist eine Lösung, in der mehrere Produkte vereint sind:

- Hardware von einem OEM-Partner

- Windows Server 2019 Datacenter Edition

- Windows Admin Center

- Azure-Dienste (optional)

![Azure Stack HCI ist eine hyperkonvergente Lösung von Microsoft, die bei vielen Hardwarepartnern erhältlich ist.](media/AS_HCI_solution.png)

Azure Stack HCI ist eine hyperkonvergente Lösung von Microsoft, die bei vielen Hardwarepartnern erhältlich ist. Sehen Sie sich die folgenden Szenarien für eine hyperkonvergente Lösung an, damit Sie ermitteln können, ob Azure Stack HCI die für Sie am besten geeignete Lösung ist:

- **Aktualisieren von veralteter Hardware**: Tauschen Sie ältere Server und Speicherinfrastruktur aus, und führen Sie virtuelle Windows- und Linux-Computer lokal und im Edgebereich mit vorhandenen IT-Funktionen und Tools aus.

- **Konsolidieren von virtualisierten Workloads**: Fassen Sie Legacy-Apps in einer effizienten hyperkonvergenten Infrastruktur zusammen. Nutzen Sie die gleichen Arten von effizienten Cloudfunktionen, die für die Ausführung von Datencentern mit Hyperskalierung, z. B. Microsoft Azure, verwendet werden.

- **Herstellen einer Verbindung mit Azure für Hybrid Cloud-Dienste**: Optimieren Sie den Zugriff auf Dienste für die Cloudverwaltung und Sicherheit in Azure, z. B. externe Sicherung, Standortwiederherstellung, cloudbasierte Überwachung und mehr.

## <a name="the-azure-stack-family"></a>Azure Stack-Familie

Azure Stack HCI ist Teil der Azure- und Azure Stack-Familie, und es werden die gleichen softwaredefinierten Compute-, Speicher- und Netzwerkkomponenten wie für Azure Stack verwendet. Hier ist eine kurze Übersicht über die verschiedenen Lösungen angegeben:

- [Azure](https://azure.microsoft.com): Nutzen von öffentlichen Clouddiensten
- [Azure Stack](https://azure.microsoft.com/overview/azure-stack): Lokales Betreiben von Clouddiensten
- [Azure Stack HCI](https://azure.microsoft.com/overview/azure-stack/hci): Lokales Ausführen von virtualisierten Apps mit optionalen Verbindungen mit Azure

![Für Azure und Azure Stack werden Clouddienste ausgeführt, während für Azure Stack HCI lokal virtualisierte Anwendungen ausgeführt werden.](media/azure_family.png)

|Azure: Nutzen von öffentlichen Clouddiensten|Azure Stack: Lokales Betreiben von Clouddiensten|Azure Stack HCI: Lokales Ausführen von virtualisierten Apps|
|-----------------|-----------------|-----------------|
|Für bedarfsgesteuerte Self-Service-Computeressourcen zum Migrieren und Modernisieren von vorhandenen Apps und Erstellen von neuen cloudnativen Apps.|Entwickeln und Ausführen von Cloudanwendungen im Edgebereich (bei getrennter Verbindung) oder Erfüllen von rechtlichen Bestimmungen mit einheitlichen lokalen Azure-Diensten.| Lokales Ausführen von virtualisierten Anwendungen, Austauschen und Konsolidieren von veralteter Serverinfrastruktur und Herstellen einer Verbindung mit Azure für Clouddienste.|
|Mehr als 100 verfügbare Dienste in 54 Regionen weltweit|Azure-VMs für Windows und Linux, Azure-Web-Apps und Functions, Azure Key Vault, Azure Resource Manager, Azure Marketplace, Container, Azure IoT und Event Hubs, Verwaltungstools (Pläne, Angebote, RBAC)|Überprüfte HCI-Lösungen auf Grundlage von Hyper-V und „Direkte Speicherplätze“ mit Windows Server 2019 und Windows Admin Center für die Verwaltung und integrierten Zugriff auf Azure-Dienste.|

Weitere Informationen:

- Erfahren Sie mehr auf der Website mit den [Azure Stack HCI](https://azure.microsoft.com/overview/azure-stack/hci)-Lösungen.
- Verfolgen Sie, wie die Microsoft-Experten Jeff Woolsey und Vijay Tewari [über die neuen Azure Stack HCI-Lösungen diskutieren](https://aka.ms/AzureStackOverviewVideo).

## <a name="hyperconverged-efficiencies"></a>Effizienz durch hyperkonvergente Lösungen

Mit Azure Stack HCI-Lösungen werden stark virtualisierte Compute-, Speicher- und Netzwerkfunktionen auf branchenüblichen x86-Servern und -Komponenten zusammengefasst. Die Kombination von Ressourcen in demselben Cluster erleichtert Ihnen die Bereitstellung, Verwaltung und Skalierung. Wählen Sie für die Verwaltung Ihre bevorzugte Befehlszeilenautomatisierung oder Windows Admin Center aus.

Erzielen Sie mit Hyper-V, der grundlegenden Hypervisor-Technologie der Microsoft-Cloud, und der Technologie „Direkte Speicherplätze“ mit integrierter NVMe-Unterstützung, beständigem Speicher und RDMA-Netzwerkfunktionen (Remote-Direct Memory Access) die branchenweit beste VM-Leistung für Ihre Serveranwendungen.

Sorgen Sie für den Schutz von Apps und Daten, indem Sie abgeschirmte virtuelle Computer, Mikrosegmentierung für Netzwerke und native Verschlüsselung für Daten im Ruhezustand und während der Übertragung nutzen.

## <a name="hybrid-capabilities"></a>Hybridfunktionen

Sie können die Vorteile des Zusammenspiels von Cloud- und lokalen Ressourcen und einer hyperkonvergenten Infrastrukturplattform in der öffentlichen Cloud nutzen. Ihr Team kann damit beginnen, Fertigkeiten für die Cloud zu erwerben – bei gleichzeitiger Integration in die Verwaltungsdienste für die Azure-Infrastruktur:

- Azure Site Recovery für Hochverfügbarkeit und „Disaster Recovery-as-a-Service“ (DRaaS, Notfallwiederherstellung als Dienst).

- Azure Monitor, ein zentraler Hub zum Nachverfolgen von Anwendungen, Netzwerk und Infrastruktur – mit erweiterten Analysefunktionen auf Grundlage von KI.

- Cloudzeuge zur Verwendung von Azure als einfache Lösung für das Clusterquorum.

- Azure Backup für den Schutz von Daten an anderen Standorten und als Schutz vor Ransomware.

- Azure-Updateverwaltung für Bewertungen und Bereitstellungen von Updates für Windows-VMs, die in Azure und lokal ausgeführt werden.

- Azure-Netzwerkadapter zum lokalen Verbinden von Ressourcen mit Ihren VMs in Azure per Point-to-Site-VPN.

- Synchronisierung Ihres Dateiservers mit der Cloud per Azure-Dateisynchronisierung.

Weitere Informationen finden Sie unter [Connecting Windows Server to Azure hybrid services](..\manage\windows-admin-center\azure\index.md) (Herstellen einer Verbindung für Windows Server mit Azure-Hybriddiensten).

## <a name="management-tools-and-system-center"></a>Verwaltungstools und System Center

Für Azure Stack HCI wird die gleiche Virtualisierung und Software für softwaredefinierten Speicher und Netzwerke wie für Azure Stack verwendet. Mit Azure Stack HCI verfügen Sie über vollständige Administratorrechte für den Cluster: Sie können [Windows Admin Center](..\manage\windows-admin-center\overview.md), [System Center](https://www.microsoft.com/cloud-platform/system-center) und alle Features von [Hyper-V](../virtualization/hyper-v/hyper-v-on-windows-server.md), [Direkte Speicherplätze](..\storage\storage-spaces\storage-spaces-direct-overview.md), PowerShell und Drittanbietertools, z. B. 5Nine Manager, nutzen.

Microsoft Azure wird auf der gleichen Windows Server- und Hyper-V-Plattform ausgeführt, die auch in Windows Server enthalten ist. Windows Server und System Center enthalten Verbesserungen und bewährte Methoden, die aus den Erfahrungen von Microsoft mit dem Betrieb von globalen Datencenternetzwerken wie Microsoft Azure stammen. Auf diese Weise können Sie bei Verwendung von Software-Defined Networking-Technologien die gleichen Technologien für die Bereiche Flexibilität, Automatisierung und Kontrolle bereitstellen.

Führen Sie Bereitstellung und Verwaltung der Infrastruktur mit System Center Virtual Machine Management (VMM) und System Center Operations Manager durch. Mit VMM können Sie die Ressourcen bereitstellen und verwalten, die zum Erstellen und Bereitstellen von virtuellen Computern und Diensten für private Clouds erforderlich sind. Mit Operations Manager überwachen Sie Dienste, Geräte und Vorgänge in Ihrem gesamten Unternehmen, um ermitteln zu können, für welche Probleme sofortige Maßnahmen ergriffen werden müssen.

## <a name="hardware-partners"></a>Hardwarepartner

Sie können überprüfte Azure Stack HCI-Lösungen, für die Windows Server 2019 ausgeführt wird, von 15 Partnern erwerben. Ihr bevorzugter Microsoft-Partner richtet ohne langwierige Entwurfs- und Builddauern alles für Sie ein und dient als zentraler Ansprechpartner für die Implementierung und für Supportleistungen.

Besuchen Sie die [Azure Stack HCI-Website](https://azure.microsoft.com/overview/azure-stack/hci), um sich über unsere mehr als 70 Azure Stack HCI-Lösungen zu informieren, die derzeit von diesen Microsoft-Partnern erhältlich sind: ASUS, Axellio, bluechip, DataON, Dell EMC, Fujitsu, HPE, Hitachi, Huawei, Lenovo, NEC, primeLine Solutions, QCT, SecureGUARD und Supermicro.

## <a name="faq"></a>Häufig gestellte Fragen

### <a name="what-do-azure-stack-and-azure-stack-hci-solutions-have-in-common"></a>Was haben Azure Stack- und Azure Stack HCI-Lösungen gemeinsam?

Azure Stack HCI-Lösungen verfügen über die gleiche Hyper-V-basierte softwaredefinierte Compute-, Speicher- und Netzwerktechnologie wie Azure Stack. Für beide Angebote werden strenge Test- und Prüfkriterien erfüllt, um sicherzustellen, dass die Zuverlässigkeit und die Kompatibilität mit der zugrunde liegenden Hardwareplattform gewährleistet ist.

### <a name="how-are-they-different"></a>Welche Unterschiede gibt es?

Mit Azure Stack führen Sie Clouddienste lokal aus. Sie können Azure-Dienste vom Typ IaaS und PaaS lokal ausführen, um auf einheitliche Weise an beliebigen Orten Cloudanwendungen zu erstellen und auszuführen, die mit dem Azure-Portal lokal verwaltet werden.

Mit Azure Stack HCI führen Sie virtualisierte Workloads lokal aus, die mit Windows Admin Center und vertrauten Windows Server-Tools verwaltet werden. Sie können optional auch eine Verbindung mit Azure für Hybridszenarien herstellen, z. B. cloudbasierte Standortwiederherstellung, Überwachung und andere.

### <a name="why-is-microsoft-bringing-its-hci-offering-to-the-azure-stack-family"></a>Warum bindet Microsoft sein HCI-Angebot in die Azure Stack-Familie ein?

Die Hyperkonvergenztechnologie von Microsoft stellt bereits die Grundlage von Azure Stack dar.

Viele Microsoft-Kunden verfügen über komplexe IT-Umgebungen, und unser Ziel ist die Bereitstellung von Lösungen, die genau zum Entwicklungsstand passen und jeweils die richtige Technologie für die jeweilige Geschäftsanforderung umfassen. Azure Stack HCI ist eine Weiterentwicklung der Windows Server 2016-basierten WSSD-Lösungen (Windows Server Software-Defined), die bisher bei unseren Hardwarepartnern erhältlich waren. Wir haben uns für die Integration in die Azure Stack-Familie entschieden, weil wir neue Optionen zur nahtlosen Verbindung mit Azure für Infrastrukturverwaltungsdienste anbieten.

### <a name="does-azure-stack-hci-need-to-be-connected-to-azure"></a>Muss für Azure Stack HCI eine Verbindung mit Azure hergestellt werden?

Nein. Dies ist absolut optional. Sie können die Integration in Azure für Hybridszenarien nutzen, z. B. externe Sicherungen und Notfallwiederherstellung, cloudbasierte Überwachung und Updateverwaltung, aber dies sind optionale Szenarien. Wir haben vollstes Verständnis und unterstützen Sie, falls Sie die Ausführung ohne Verbindung bevorzugen bzw. benötigen.

### <a name="how-does-azure-stack-hci-relate-to-windows-server"></a>Welche Beziehung besteht zwischen Azure Stack HCI und Windows Server?

Windows Server 2019 ist die Grundlage von nahezu jedem Azure-Produkt. Alle Features, die für Sie wichtig sind, werden weiterhin bereitgestellt und in Windows Server unterstützt. Azure Stack HCI ist die empfohlene Lösung zur lokalen Bereitstellung von HCI, indem von Microsoft überprüfte Hardware von unseren Partnern genutzt wird.

### <a name="will-i-be-able-to-upgrade-from-azure-stack-hci-to-azure-stack"></a>Kann ich ein Upgrade von Azure Stack HCI auf Azure Stack durchführen? 

Nein. Kunden können ihre Workloads aber von Azure Stack HCI zu Azure Stack oder Azure migrieren.

### <a name="what-azure-services-can-i-connect-to-azure-stack-hci"></a>Für welche Azure-Dienste kann ich eine Verbindung mit Azure Stack HCI herstellen?

Eine aktualisierte Liste mit den Azure-Diensten, für die Sie eine Verbindung mit Azure Stack HCI herstellen können, finden Sie unter [Connecting Windows Server to Azure hybrid services](../azure-hybrid-services/index.md) (Herstellen einer Verbindung für Windows Server mit Azure-Hybriddiensten).

### <a name="how-does-the-cost-of-azure-stack-hci-compare-to-azure-stack"></a>Wie verhalten sich die Kosten für Azure Stack HCI gegenüber den Kosten für Azure Stack? 

Azure Stack wird als vollständig integriertes System mit Diensten und Support angeboten. Sie können Azure Stack als System erwerben, das Sie selbst verwalten, oder als vollständig verwalteten Dienst von unseren Partnern. Zusätzlich zum Basissystem werden die Azure-Dienste, die unter Azure Stack oder Azure ausgeführt werden, mit „Nutzungsbasierter Bezahlung“ angeboten.

Für Azure Stack HCI-Lösungen gilt das herkömmliche Verkaufsmodell. Sie können überprüfte Hardware von Azure Stack HCI-Partnern und Software (Windows Server 2019 Datacenter Edition mit softwaredefinierten Datencenterfunktionen und Windows Admin Center) über unterschiedliche Kanäle erwerben. Für Azure-Dienste, die Sie mit Windows Admin Center verwenden können, bezahlen Sie per Azure-Abonnement.

### <a name="how-do-i-buy-azure-stack-hci-solutions"></a>Wie kann ich Azure Stack HCI-Lösungen kaufen?

Folgen Sie diesen Schritten:

1. Erwerben Sie bei Ihrem bevorzugten Hardwarepartner ein von Microsoft überprüftes Hardwaresystem.
1. Installieren Sie die Windows Server 2019 Datacenter Edition und Windows Admin Center, um die Verwaltung durchführen und eine Verbindung mit Azure für Clouddienste herstellen zu können.
1. Nutzen Sie optional Ihr Azure-Konto, um cloudbasierte Verwaltungs- und Sicherheitsdienste an Ihre Workloads anzufügen.

![Wählen Sie zum Erwerben von Azure Stack HCI-Lösungen den besten Hardwarepartner bzw. die beste Konfiguration für Ihre Anforderungen.](media/howbuy_ashci.png)

## <a name="compare-azure-stack-and-azure-stack-hci"></a>Vergleich: Azure Stack und Azure Stack HCI

Während der digitalen Transformation Ihrer Organisation kommen Sie unter Umständen zu dem Schluss, dass Sie schneller vorankommen, indem Sie öffentliche Clouddienste für die Entwicklung auf moderner Architektur und die Aktualisierung von Legacy-Apps verwenden. Aufgrund von technologischen und regulatorischen Hindernissen müssen viele Workloads weiterhin lokal angeordnet sein. Anhand der folgenden Tabelle können Sie ermitteln, mit welcher Microsoft Hybrid Cloud-Strategie Sie die richtigen Werkzeuge am richten Ort erhalten und innovative Cloudlösungen für Workloads unabhängig vom Standort bereitstellen können.

|Azure Stack|Azure Stack HCI|
|--------|-------|
|Neue Fertigkeiten, innovative Prozesse|Dieselben Fertigkeiten, vertraute Prozesse|
|Azure-Dienste in Ihrem Datencenter|Verbindung Ihres Datencenters mit Azure-Diensten|

### <a name="when-to-use-azure-stack"></a>Verwendung von Azure Stack

|Azure Stack|Azure Stack HCI|
|--------|-------|
|Verwenden Sie Azure Stack für Self-Service-IaaS (Infrastructure-as-a-Service) mit strenger Isolation und präziser Nutzungsnachverfolgung und Rückbelastung für mehrere zusammengestellte Mandanten. Ideal geeignet für Dienstanbieter und private Clouds von Unternehmen. Vorlagen aus Azure Marketplace.|Für Azure Stack HCI wird die Mehrinstanzenfähigkeit nicht nativ erzwungen oder bereitgestellt.|
|Nutzen Sie Azure Stack zum Entwickeln und Ausführen von Apps, für die PaaS-Dienste (Platform-as-a-Service) verwendet werden, z. B. Web-Apps, Functions oder Event Hubs (lokal). Diese Dienste werden unter Azure Stack genauso wie in Azure ausgeführt und sorgen für eine einheitliche Entwicklungs- und Laufzeit-Hybridumgebung.|Für Azure Stack HCI werden keine PaaS-Dienste lokal ausgeführt.
|Verwenden Sie Azure Stack zum Modernisieren von App-Bereitstellung und -Betrieb mit DevOps-Methoden, z. B. „Infrastructure as Code“, Continuous Integration und Continuous Deployment (CI/CD) sowie nützlichen Features wie einheitlichen Azure-VM-Erweiterungen. Ideal geeignet für Entwicklungs- und DevOps-Teams.|In Azure Stack HCI sind nativ keine DevOps-Tools enthalten.

### <a name="when-to-use-azure-stack-hci"></a>Verwendung von Azure Stack HCI

|Azure Stack|Azure Stack HCI|
|---------------|---------------|
|Für Azure Stack sind mindestens vier Knoten und eigene Netzwerkswitches erforderlich.|Verwenden Sie Azure Stack HCI, um für entfernte bzw. Zweigniederlassungen (Remote-Office/Branch-Office, ROBO) den Aufwand möglichst gering zu halten. Beginnen Sie mit nur zwei Serverknoten und kaskadierenden Netzwerken ohne Switches, um für Einfachheit und Kostengünstigkeit zu sorgen. Die Hardwareangebote beginnen für vier Laufwerke und 64 GB Arbeitsspeicher bei deutlich unter 10.000 USD pro Knoten.
|Azure Stack verfügt über Hyper-V-Konfigurierbarkeit und einen Featuresatz für die Konsistenz mit Azure.|Verwenden Sie Azure Stack HCI für die einfache Hyper-V-Virtualisierung für klassische Unternehmens-Apps, z. B. Exchange, SharePoint und SQL Server, und zum Virtualisieren von Windows Server-Rollen wie Dateiserver, DNS, DHCP, IIS und AD. Es besteht uneingeschränkter Zugriff auf alle Hyper-V-Features, z. B. abgeschirmte VMs.|
|Von Azure Stack wird diese Infrastrukturtechnologie nicht verfügbar gemacht.|Verwenden Sie Azure Stack HCI, um softwaredefinierte Infrastruktur anstelle von veralteten Speicherarrays oder Netzwerkgeräten einzusetzen, ohne dass größere Änderungen an der Architektur erforderlich sind. Die integrierten Features „Direkte Speicherplätze“ und „Softwaredefinierte Netzwerke“ (Software-Defined Networking, SDN) ermöglichen die reibungslose Integration in Hyper-V-Umgebungen.|