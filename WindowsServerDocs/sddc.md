---
title: Windows Server-Software-Defined Datacenter
Description: Übersicht über das Windows Server SDDC
ms.topic: get-started article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 06/04/2019
ms.localizationpriority: medium
ms.openlocfilehash: 632e08a6e560b9b9e4ab7010794eaf36d1873cac
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990613"
---
# <a name="windows-server-software-defined-datacenter"></a>Windows Server-Software-Defined Datacenter

>Gilt für: Windows Server 2019, Windows Server 2016

![Überschrift-Bild](media/sddc/heading.png)

## <a name="what-is-windows-server-software-defined-datacenter"></a>Was ist Windows Server-Software-Defined Datacenter?

Software-Defined Datacenter (SDDC) ist ein branchenüblicher Begriff, der ein Rechenzentrum beschreibt, dessen gesamte Infrastruktur virtualisiert ist. Virtualisierung ist der Schlüssel, und es bedeutet lediglich, dass die Hardware und Software im Datencenter über ein herkömmliches 1: 1-Verhältnis erweitert sind. Mit einem Software-Hypervisor, der Hardware emuliert, können Betriebssysteme und Anwendungen aus physischer Hardware herausgenommen und zum Erstellen elastischer Ressourcenpools von Prozessoren, Arbeitsspeichern, E/A und Netzwerken multipliziert werden.

Microsofts Implementierung der SDDC besteht aus Windows Server-Technologien, die in diesem Artikel beschrieben werden. Es beginnt mit dem Hyper-V-Hypervisor, der die Virtualisierungsplattform bereitstellt, auf der Netzwerk und Speicher aufgebaut werden. Sicherheitstechnologien, die für individuelle Herausforderungen der virtualisierten Infrastruktur entwickelt wurden, vermindern interne und externe Bedrohungen. Mit PowerShell in Windows Server und dem Hinzufügen von [System Center](/system-center/) und/oder [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview) können Sie die Bereitstellung, Konfiguration und Verwaltung programmieren und automatisieren.

Die in Windows Server und System Center integrierten Technologien sind die wichtigsten Bausteine der Windows Server-SDDC Erfahrung. Obwohl es sich um eine virtualisierte Plattform handelt, ist auch weiterhin die richtige Hardware darunter erforderlich. Microsoft-Partner, die an den Programmen **Windows Server Software-Defined (WSSD)-Lösung** und **Azure Stack HCI-Lösungen** teilnehmen, können Ihr Unternehmen dabei unterstützen, die richtige Hardware zu erwerben und vom ersten Tag an betriebsbereit zu sein.

![Video-Symbol](media/sddc/video.png)**[Video mit weiteren Informationen zu Microsoft SDDC](https://mva.microsoft.com/training-courses/whats-new-in-windows-server-2016-16457?l=YcsJR6sXC_1006218965)**

![Poster-Symbol](media/sddc/poster-ico.png)**[Große PDF-Datei von dieser Seite herunterladen](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/WindowsServerDocs/media/sddc/sddc_poster_0801417_ANSI-E.pdf)**

## <a name="azure-stack-hci-solutions"></a>Azure Stack HCI-Lösungen

Das Erstellen Ihres eigenen Windows Server Software-Defined Datacenters auf der richtigen Hardware-Infrastruktur ist entscheidend für Ihren Erfolg. Aus diesem Grund haben wir mit 15 Partnern zusammengearbeitet, um von Microsoft validierte SDDC-Designs und optimale Verfahren für die Bereitstellung zu erstellen.

Microsoft-Partner bieten eine Vielzahl von Lösungen an, die über das Azure Stack HCI-Programm mit Windows Server 2019 und über das WSSD-Programm (Windows Server Software-Defined) mit Windows Server 2016 zusammenarbeiten, um eine hyperkonvergente Speicher- und Netzwerkinfrastruktur mit hoher Leistung zur Verfügung zu stellen. Hyperkonvergente Lösung vereinen Computing, Speicher und Networking auf branchenüblichen Servern und Komponenten, um eine verbesserte Datacenter-Intelligence und -Kontrolle zu erreichen.

![Lernen-Symbol](media/sddc/learn.png)**[Weitere Informationen zu Azure Stack HCI-Lösungen](https://azure.microsoft.com/overview/azure-stack/hci)**

![Lernen-Symbol](media/sddc/learn.png)**[Weitere Informationen zu WSSD-Lösungen](https://www.microsoft.com/cloud-platform/software-defined-datacenter)**

## <a name="windows-server-virtualized-technologies"></a>Virtuelle Technologien in Windows Server ##

Der verbleibende Teil dieses Themas enthält die Windows Server-SDDC-Technologien und jeweilige Links zur Dokumentation. In der folgenden Tabelle werden diese Technologien aufgeführt:

![Verfügbare Windows Server SDDC-Technologien](media/sddc/table.png)

![Überschriftenleiste zum Virtualisieren beliebiger Elemente](media/sddc/virtualize.png)

### <a name="windows-server-hyper-converged"></a>Windows Server, hyperkonvergent

Windows Server-Virtualisierungstechnologien enthalten Updates für Hyper-V, Virtueller Hyper-V-Switch und Guarded Fabric und Shielded Virtual Machines (VMs), die die Sicherheit, Skalierbarkeit und Zuverlässigkeit verbessern. Updates für Failoverclustering, Networking und Speicher machen das Bereitstellen und Verwalten dieser Technologien mit Hyper-V noch einfacher.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Windows Server, hyperkonvergente Infrastruktur (Diagramm)](media/sddc/hyper-converged.png)

![Lernen-Symbol](media/sddc/learn.png)**[Erfahren Sie mehr über Windows Server, hyperkonvergent](./get-started/whats-new-in-windows-server-2016.md#compute)**

### <a name="hyper-v-hypervisor"></a>Hyper-V-Hypervisor

Hyper-V ist eine hypervisorbasierte Virtualisierungstechnologie für Windows. Der Hypervisor ist ein wesentlicher Bestandteil der Virtualisierung. Er ist die prozessorspezifische Virtualisierungsplattform, die es mehreren isolierten Betriebssystemen ermöglicht, sich eine einzige Hardwareplattform zu teilen.

![Hyper-V-Hypervisor (Diagramm)](media/sddc/spacer1.png)![Hyper](media/sddc/hypervisor.png)

![Lernen-Symbol](media/sddc/learn.png)**[Weitere Informationen zum Hyper-V-Hypervisor](https://www.microsoft.com/cloud-platform/server-virtualization)**

### <a name="guest-clustering-with-shared-vhdx"></a>Gastclustering mit VHDX-Freigaben

![Bild einer Zeile zu Abstandszwecken](media/sddc/virtualize-line.png)

VHDX-Freigaben sind flexibel und sicher und nicht an die zugrunde liegenden Speichertopologie gebunden, was die Präsenz eines zugrunde liegenden physischen Speichers auf dem Gastbetriebssystem nicht mehr erforderlich macht. Die neuen VHDX-Freigaben unterstützen die Größenänderung online.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Gastcluster und einer VHDX-Freigabe (Diagramm)](media/sddc/cluster.png)

- VHDX-Freigaben können sich auf einem freigegebenen Clustervolume (Cluster Shared Volume, CSV) im Blockspeicher oder auf SMB-dateibasiertem Speicher befinden.
- Geschützt: VHDX-Freigaben unterstützen Sicherung von Hyper-V-Replikaten und Sicherung auf Hostebene.

![Lernen-Symbol](media/sddc/learn.png)**[Erfahren Sie mehr über Gastclustering mit VHDX-Freigabe](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn281956(v=ws.11))**

### <a name="hyper-v-replica"></a>Hyper-V-Replikat

![Bild einer Zeile zu Abstandszwecken](media/sddc/virtualize-line.png)

Integrierte Software-basierte VM-Replikation im Netzwerk mit Zertifikaten. Ist nicht an Server, Netzwerk oder Speicher-Hardware an einem Standort gebunden.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Hyper-V-Replikat (Diagramm)](media/sddc/replica.png)

Benötigt keine andere -VM-Replikationstechnologien, was die Kosten reduziert.
- Übernimmt Livemigration automatisch.
- Einfache Konfiguration und Verwaltung – entweder durch Hyper-V-Manager, PowerShell oder mit Azure Site Recovery.

![Lernen-Symbol](media/sddc/learn.png)**[Weitere Informationen zum Hyper-V-Replikat](./virtualization/hyper-v/manage/set-up-hyper-v-replica.md)**

![Banner „Alles verbinden“](media/sddc/networking.png)

### <a name="network-controller"></a>Netzwerkcontroller

![Bild einer Zeile zu Abstandszwecken](media/sddc/networking-line.png)

Bietet die Möglichkeit einer zentralen, programmierbaren Automatisierung von Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Netzwerkcontroller (Diagramm)](media/sddc/netcontroller.png)

Ein Administrator verwendet ein Verwaltungstool, das direkt mit dem Netzwerkcontroller interagiert. Der Netzwerkcontroller übertragt Informationen über die Netzwerkinfrastruktur an das Verwaltungstool, einschließlich der virtuellen und physischen Infrastruktur.

![Lernen-Symbol](media/sddc/learn.png)**[Weitere Informationen zum Netzwerkcontroller](./networking/sdn/technologies/network-controller/network-controller.md)**

### <a name="datacenter-firewall"></a>Rechenzentrumsfirewall

![Bild einer Zeile zu Abstandszwecken](media/sddc/networking-line.png)

Wenn sie bereitgestellt ist und als Dienst angeboten wird, können Mandantenadministratoren Firewall-Richtlinien zum Schutz von virtuellen Netzwerken installieren und konfigurieren, um unerwünschten Datenverkehr aus dem Internet und Intranetnetzwerken fernzuhalten.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Rechenzentrumsfirewall (Diagramm)](media/sddc/firewall.png)

Der Internetanbieter-Administrator oder der Mandantenadministrator können die Rechenzentrumsfirewall-Richtlinien über den Netzwerkcontroller verwalten.

![Lernen-Symbol](media/sddc/learn.png)**[Hier erfahren Sie mehr über die Rechenzentrumsfirewall](./networking/sdn/technologies/network-function-virtualization/datacenter-firewall-overview.md)**

### <a name="switch-embedded-teaming"></a>Switch Embedded Teaming

![Bild einer Zeile zu Abstandszwecken](media/sddc/networking-line.png)

SET ist eine alternative Lösung zur NIC-Teamerstellung, die Sie in einer Umgebung verwenden können, die Hyper-V und den [Software Defined Networking (SDN)](./networking/sdn/software-defined-networking.md)-Stapel enthält.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Switch Embedded Teaming (Diagramm)](media/sddc/teaming.png)

![Lernen-Symbol](media/sddc/learn.png)**[Weitere Informationen zu Switch Embedded Teaming](./networking/sdn/technologies/set-for-sdn.md)**

### <a name="software-load-balancing"></a>Softwarelastenausgleich

![Bild einer Zeile zu Abstandszwecken](media/sddc/networking-line.png)

SLB ermöglicht es Ihnen, mehrere Server zum Hosten derselben Workload zu aktivieren, um hohe Verfügbarkeit und Skalierbarkeit bereitzustellen. Skalieren Sie Lastenausgleichsfunktionen mit SLB VMs auf den gleichen Hyper-V-Servern, die Sie für Ihre anderen VM-Arbeitslasten verwenden. SLB unterstützt die schnelle Erstellung und das Löschen von Lastenausgleich-Endpunkten für Cloud-Dienstanbieter-Vorgänge. SLB unterstützt Zehntausende Gigabyte pro Cluster, bietet ein einfaches Modell für den Bereitstellungsprozess und kann einfach erweitert und reduziert werden.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Softwarelastenausgleich (Diagramm)](media/sddc/balancer.png)

![Lernen-Symbol](media/sddc/learn.png)**[Weitere Informationen zum Lastenausgleich](./networking/sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)**

![Speicher (Diagramm)](media/sddc/storage.png)

### <a name="storage-spaces-direct"></a>Speicherplätze DAS

![Speicher, Bild einer Zeile zu Abstandszwecken](media/sddc/storage-line.png)

„Direkte Speicherplätze“ verwendet branchenübliche Server mit lokal angeschlossenen Laufwerken, um hoch verfügbare, hoch skalierbare softwaredefinierte Speicher zu einem Bruchteil der Kosten von herkömmlichen SAN- oder NAS-Arrays zu erstellen. Die Architektur vereinfacht radikal die Beschaffung und Bereitstellung.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Direkte Speicherplätze (S2D) (Diagramm)](media/sddc/ssd.png)

„Direkte Speicherplätze“ führt den neuen Softwarespeicherbus ein und nutzt viele Features von Windows Server, die Sie bereits kennen, z. B. Failoverclustering, CSV (Cluster Shared Volume, freigegebenes Clustervolume), SMB3 (Server Message Block) und natürlich „Speicherplätze“.

![Lernen-Symbol](media/sddc/learn.png)**[Weitere Informationen zu direkten Speicherplätzen](storage/storage-spaces/storage-spaces-direct-overview.md)**
### <a name="storage-quality-of-service"></a>Quality of Service für Speicher ###

![Zeile zu Abstandszwecken](media/sddc/storage-line.png)

Ermöglicht eine zentrale Überwachung und Verwaltung der Speicherleistung für virtuelle Computer unter Verwendung der Hyper-V-Rolle und der Rolle des Dateiservers mit horizontaler Skalierung und verbessert so die Speicherressourcen-Fairness zwischen mehreren virtuellen Computern.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Quality of Service (QoS) für Speicher (Diagramm)](media/sddc/qos.png)

Speicher-QoS ist in die softwaredefinierte Speicherlösung von Microsoft integriert, die mit dem Dateiserver mit horizontaler Skalierung und Hyper-V über das SMB3-Protokoll bereitgestellt wird. Ein neuer Richtlinien-Manager ermöglicht eine zentrale Überwachung der Speicherleistung.

![Lernen-Symbol](media/sddc/learn.png)**[Weitere Informationen zu Speicher-QoS](./storage/storage-qos/storage-qos-overview.md)**

### <a name="storage-replica"></a>Speicherreplikat

![Speicher, Bild einer Zeile zu Abstandszwecken](media/sddc/storage-line.png)

Notfallwiederherstellung und -Bereitschaft stellen sicher, dass keine Daten verloren gehen und bieten die Möglichkeit, Daten auf unterschiedlichen Racks, Etagen, Gebäuden, Campusgeländen, Standorten und Ländern durch eine effizientere Verwendung von mehreren Rechenzentren synchron zu schützen.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)
![Speicherreplikat (Diagramm)](media/sddc/storage-replica.png)

Synchrone Replikation

1. Anwendung schreibt Daten
2. Protokolldaten werden geschrieben, und die Daten werden am Remotestandort repliziert
3. Protokolldaten werden am Remotestandort geschrieben
4. Bestätigung durch den Remotestandort
5. Anwendungsschreibvorgang wird bestätigt

t & t1 : Daten werden auf das Volume geleert, Protokolle werden immer per Write-Through geschrieben

![Lernen-Symbol](media/sddc/learn.png)**[Weitere Informationen zum Speicherreplikat](./storage/storage-replica/storage-replica-overview.md)**

![Sicherheit (Diagramm)](media/sddc/security.png)

### <a name="guarded-fabric"></a>Guarded Fabric

![Sicherheit, Bild einer Zeile zu Abstandszwecken](media/sddc/security-line.png)

Als Cloud-Dienstanbieter oder privater Cloud-Administrator im Unternehmen können Sie ein geschütztes Fabric verwenden, um eine sicherere Umgebung für VMs bereitzustellen. Ein geschütztes Fabric besteht aus einem Host Guardian Service (Host-Überwachungsdienst) – in der Regel ein Cluster mit drei Knoten – sowie einem oder mehreren geschützten Hosts und einer Reihe von abgeschirmten virtuellen Computern (VMs).

![Geschütztes Fabric (Diagramm)](media/sddc/spacer1.png)![Geschütztes Fabric (Diagramm)](media/sddc/guarded-fabric.png)

![Lernen-Symbol](media/sddc/learn.png)**[Weitere Informationen zum geschützten Fabric](./security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md)**

### <a name="shielded-vms"></a>Abgeschirmte VMs

![Sicherheit, Bild einer Zeile zu Abstandszwecken](media/sddc/security-line.png)

Die Daten und der Status einer abgeschirmten VM sind geschützt gegen Überprüfung, Diebstahl und Manipulation, sowohl durch Schadsoftware als auch durch Rechenzentrums-Administratoren.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Abgeschirmte VMs (Diagramm)](media/sddc/shielded.png)

- Abgeschirmte VMs funktionieren nur in Fabrics, die als Besitzer des virtuellen Computers aufgeführt sind.
- Abgeschirmte VMs sind durch BitLocker oder auf andere Weise verschlüsselt, sodass nur die angegebenen Eigentümer sie ausführen können.
- Ausgeführte virtuelle Computer können in abgeschirmte Computer konvertiert werden.

![Lernen-Symbol](media/sddc/learn.png)**[Weitere Informationen zu abgeschirmten VMs](./security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md)**

### <a name="host-guardian-service"></a>Host-Überwachungsdienst

![Sicherheit, Bild einer Zeile zu Abstandszwecken](media/sddc/security-line.png)

Der Host-Überwachungsdienst stellt den Schlüssel zu legitimen Fabrics und zu verschlüsselten virtuellen Computern dar.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Host-Überwachungsdienst (Diagramm)](media/sddc/guardian.png)

![Lernen-Symbol](media/sddc/learn.png)**[Erfahren Sie mehr über den Host-Überwachungsdienst](./security/guarded-fabric-shielded-vm/guarded-fabric-manage-hgs.md)**

### <a name="device-health-attestation"></a>Integritätsnachweis für Geräte

![Sicherheit, Bild einer Zeile zu Abstandszwecken](media/sddc/security-line.png)

Der Integritätsnachweis ermöglicht Unternehmen, mit minimalem oder keinem Einfluss auf die Betriebskosten das Sicherheitsniveau ihrer Organisation auf hardwareüberwachte und -bescheinigte Sicherheit anzuheben.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Nachweis (Diagramm)](media/sddc/attestation.png)

Der vertrauenswürdige Modus für Hardware, wie oben angezeigt, bietet mit dem TPM v2.0-Hardware-Stamm-Vertrauensmodell und der Einhaltung der Codeintegritätsrichtlinien für die Schlüsselfreigabe die größtmögliche Sicherheit.

![Lernen-Symbol](media/sddc/learn.png)**[Weitere Informationen zum Integritätsnachweis für Geräte](./security/device-health-attestation.md)**

![Verwaltung (Diagramm)](media/sddc/management.png)

### <a name="powershell-desired-state-configuration"></a>PowerShell Desired State Configuration

![Verwaltung, Bild einer Zeile zu Abstandszwecken](media/sddc/management-line.png)

Windows PowerShell Desired State Configuration ist eine in Windows integrierte Plattform zur Konfigurationsverwaltung, die auf offenen Standards basiert. DSC ist flexibel genug, in jeder Phase des Bereitstellungslebenszyklus (Entwicklung, Test, Präproduktion, Produktion) sowie bei horizontaler Skalierung zuverlässig und konsistent zu funktionieren.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Desired State Configuration (DSC) (Diagramm)](media/sddc/dsc.png)

DSC unterstützt „Continuous Deployments“, damit Sie Konfigurationen wieder und wieder bereitstellen können, ohne etwas zu beschädigen.

-  DSC-Konfigurationen übernehmen nur die Einstellungen, die von der ursprünglichen auf die schnellere Bereitstellung geändert wurden.
-  DSC kann lokal, in einer öffentlichen oder in einer privaten Cloud-Umgebung verwendet werden.
-  Sie können DSC mit Microsoft oder mit jeder nicht von Microsoft stammenden Lösung integrieren, solange Sie ein PowerShell-Skript auf dem Zielsystem ausführen können.

![Lernen-Symbol](media/sddc/learn.png)**[Weitere Informationen zu PowerShell DSC](/powershell/dsc/overview)**

### <a name="system-center-vmm"></a>System Center VMM

![Verwaltung, Bild einer Zeile zu Abstandszwecken](media/sddc/management-line.png)

Virtual Machine Manager ist Teil der System Center-Suite, der zum Konfigurieren, Verwalten und Transformieren von herkömmlichen Rechenzentren verwendet wird, um eine einheitliche Verwaltung über lokale Dienstanbieter und Azure-Cloud anzubieten.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Virtual Machine Manager (Diagramm)](media/sddc/vmm.png)

- Datacenter: Konfigurieren und Verwalten von Datacenter-Komponenten als eine einzelne Fabric in VMM.
- Virtualisierungshosts: VMM kann Hyper-V und VMware-Virtualisierungshosts und Cluster hinzufügen, bereitstellen und verwalten.
- Netzwerk: VMM bietet die Netzwerkvirtualisierung, inklusive der Unterstützung für das Erstellen und Verwalten von virtuellen Netzwerken und Netzwerkgateways.
- Speicher: VMM kann lokale und Remotespeicher ermitteln, klassifizieren, bereitstellen und zuweisen.

![Lernen-Symbol](media/sddc/learn.png)**[Erfahren Sie mehr über System Center VMM](/system-center/vmm/)**

### <a name="windows-admin-center"></a>Windows Admin Center

![Verwaltung, Bild einer Zeile zu Abstandszwecken](media/sddc/management-line.png)

Windows Admin Center ist ein lokal bereitgestelltes, browserbasiertes Verwaltungs-Tool, welches die lokale Verwaltung von Windows-Servern unabhängig von Azure oder der Cloud ermöglicht. Windows Admin Center bietet IT-Administratoren Vollzugriff auf alle Aspekte ihrer Server-Infrastruktur und ist besonders nützlich für die Verwaltung in privaten Netzwerken, die nicht mit dem Internet verbunden sind.

![Bild nur zu Abstandszwecken](media/sddc/spacer1.png)![Architektur (Diagramm)](media/sddc/architecture.png)

Nach dem Veröffentlichen des Servers im DNS und dem Einrichten der Unternehmensfirewall können Sie über das Internet auf Windows Admin Center zugreifen und Ihre Server dann von jedem beliebigen Standort mit Microsoft Edge oder Google Chrome verwenden und verwalten.

![Lernen-Symbol](media/sddc/learn.png)**[Erfahren Sie mehr über Windows Admin Center](manage/windows-admin-center/overview.md)**