---
title: Windows Server-Software-Defined Datacenter
description: Übersicht über das Windows Server SDDC
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: SDDC
ms.tgt_pltfrm: na
ms.topic: get-started article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c8c530568d7f336ae2bd4981c02093fe580d9b7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880811"
---
# <a name="windows-server-software-defined-datacenter"></a>Windows Server-Software-Defined Datacenter

>Gilt für: Windows Server 2016

![](media/sddc/heading.png)

## <a name="what-is-windows-server-software-defined-datacenter"></a>Was ist Windows Server-Software-Defined Datacenter? ##

Software-Defined Datacenter (SDDC) ist ein branchenüblicher Begriff, der ein Datencenter beschreibt, auf dem die gesamte Infrastruktur virtualisiert ist. Virtualisierung ist der Schlüssel, und es bedeutet lediglich, dass die Hardware und Software im Datencenter über ein herkömmliches 1: 1-Verhältnis erweitert sind. Mit einem Software-Hypervisor, der Hardware emuliert, können Betriebssysteme und Anwendungen aus physischer Hardware herausgenommen und zum Erstellen elastischer Ressourcenpools von Prozessoren, Arbeitsspeichern, E/A und Netzwerken multipliziert werden.
 
Microsofts Implementierung der SDDC besteht aus Windows Server-Technologien, die in diesem Artikel beschrieben werden. Es beginnt mit dem Hyper-V-Hypervisor, der die Virtualisierungsplattform bereitstellt, auf dem Netzwerk und Speicher aufgebaut werden. Sicherheitstechnologien, die für individuelle Herausforderungen der virtualisierten Infrastruktur entwickelt wurden, vermindern interne und externe Bedrohungen. Mit PowerShell in Windows Server und dem Hinzufügen von [System Center](https://docs.microsoft.com/system-center/) und/oder [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) können Sie die Bereitstellung, Konfiguration und Verwaltung programmieren und automatisieren.

Die in Windows Server und System Center integrierten Technologien sind die wichtigsten Bausteine der Windows Server-SDDC Erfahrung. Obwohl es sich um eine virtualisierte Plattform handelt, ist auch weiterhin die richtige Hardware darunter erforderlich. Microsoft-Partner, die am Programm **Windows Server Software-Defined (WSSD)-Lösung** teilnehmen, können Ihr Unternehmen dabei unterstützen, die richtige Hardware zu erwerben und vom ersten Tag an betriebsbereit zu sein.

![](media/sddc/video.png)**[Sehen Sie sich ein Video an, um weitere Informationen zu Microsoft die SDDC](https://mva.microsoft.com/en-US/training-courses/whats-new-in-windows-server-2016-16457?l=YcsJR6sXC_1006218965)**

![](media/sddc/poster-ico.png)**[Poster Größe PDF-Datei von dieser Seite herunterladen](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/WindowsServerDocs/media/sddc/sddc_poster_0801417_ANSI-E.pdf)**


![](media/sddc/spacer1.png)<a href="https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/WindowsServerDocs//media/sddc/sddc_poster_0801417_ANSI-E.pdf"><img src="media/sddc/poster.png"></a>


## <a name="windows-server-software-defined-wssd-solutions"></a>Windows Server-Software-Defined (WSSD)-Lösung ##
Das Erstellen Ihres eigenen Windows Server Software-Defined Datencenters auf der richtigen Hardware-Infrastruktur ist entscheidend für Ihren Erfolg. Daher sind wir eine Partnerschaft mit **DataON**, **Fujitsu**, **Lenovo**, **QCT**, **SuperMicro**, **Hewlett Packard Enterprise** und **Dell EMC** eingegangen, um Microsoft überprüfte SDDC-Designs und bewährte Methoden für die Bereitstellung zu erstellen. Microsoft-Partner bieten eine Vielzahl an Windows Server Software-Defined (WSSD)-Lösungen an, die mit Windows Server 2016 funktionieren, um eine Speicher- und Netzwerkinfrastruktur mit hoher Leistung und zusammengeführt anzubieten. Zusammengeführte Lösung vereinen Computing, Speicher und Networking auf branchenüblichen Servern und Komponenten für eine verbesserte Datacenter-Intelligence und -Kontrolle.



![](media/sddc/learn.png)**[Weitere Informationen zu WSSD-Lösungen](https://www.microsoft.com/en-us/cloud-platform/software-defined-datacenter)**

## <a name="windows-server-virtualized-technologies"></a>Virtuelle Technologien in Windows Server ##

Der verbleibende Teil dieses Themas enthält die Windows Server-SDDC-Technologien und jeweilige Links zur Dokumentation. In der folgenden Tabelle werden diese Technologien aufgeführt:

![](media/sddc/table.png)

![](media/sddc/virtualize.png)

### <a name="windows-server-hyper-converged"></a>Windows Server, zusammengeführt ###

Windows Server-Virtualisierungstechnologien enthalten Updates für Hyper-V, Virtueller Hyper-V-Switch und Guarded Fabric und Shielded Virtual Machines (VMs), die die Sicherheit, Skalierbarkeit und Zuverlässigkeit verbessern. Updates für Failoverclustering, Networking und Speicher machen das Bereitstellen und Verwalten dieser Technologien mit Hyper-V noch einfacher.

![](media/sddc/spacer1.png)![](media/sddc/hyper-converged.png)

![](media/sddc/learn.png)**[Erfahren Sie mehr über Windows Server, Hyper-konvergiert](https://docs.microsoft.com/windows-server/get-started/what-s-new-in-windows-server-2016#computevirtualizationvirtualizationmd)**
 
### <a name="hyper-v-hypervisor"></a>Hyper-V-Hypervisor ###

Hyper-V ist eine hypervisorbasierte Virtualisierungstechnologie für Windows. Der Hypervisor ist ein wesentlicher Bestandteil der Virtualisierung. Er ist die prozessorspezifische Virtualisierungsplattform, die es mehreren isolierten Betriebssystemen ermöglicht, sich eine einzige Hardwareplattform zu teilen.

![](media/sddc/spacer1.png)![](media/sddc/hypervisor.png)

![](media/sddc/learn.png)**[Erfahren Sie mehr über Hyper-V-Hypervisor](https://www.microsoft.com/en-us/cloud-platform/server-virtualization)**

### <a name="guest-clustering-with-shared-vhdx"></a>Gastclustering mit VHDX-Freigaben ###

![](media/sddc/virtualize-line.png)

VHDX-Freigaben sind flexibel und sicher und nicht an die zugrunde liegenden Speichertopologie gebunden, was die Präsenz eines zugrunde liegenden physischen Speichers auf dem Gastbetriebssystem nicht mehr erforderlich macht. Die neuen VHDX-Freigaben unterstützen die Größenänderung online.

![](media/sddc/spacer1.png)![](media/sddc/cluster.png)

- VHDX-Freigaben können sich auf einem Volumes mit freigegebener Unterstützung (Cluster Shared Volume, CSV) im Blockspeicher oder auf SMB-dateibasiertem Speicher befinden.
- Geschützt: Freigegebener VHDX unterstützt Hyper-V Replica und Hostebene sichern.

![](media/sddc/learn.png)**[Erfahren Sie mehr über die Gastcluster mit freigegebenen VHDX](https://technet.microsoft.com/library/dn281956(v=ws.11).aspx)**

### <a name="hyper-v-replica"></a>Hyper-V-Replikat ###

![](media/sddc/virtualize-line.png)

Integrierte Software-basierte VM-Replikation im Netzwerk mit Zertifikaten. Ist nicht an Server, Netzwerk oder Speicher-Hardware an einem Standort gebunden.

![](media/sddc/spacer1.png)![](media/sddc/replica.png)

Benötigt keine andere -VM-Replikationstechnologien, was die Kosten reduziert.
- Übernimmt Livemigration automatisch.
- Einfache Konfiguration und Verwaltung – entweder durch Hyper-V-Manager, PowerShell oder mit Azure Site Recovery.

![](media/sddc/learn.png)**[Erfahren Sie mehr über Hyper-V-Replikat](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/set-up-hyper-v-replica)**

![](media/sddc/networking.png)

### <a name="network-controller"></a>Netzwerkcontroller ###

![](media/sddc/networking-line.png)

Bietet die Möglichkeit einer zentralen, programmierbaren Automatisierung von Verwaltung, Konfiguration, Überwachung und Problembehandlung der virtuellen und physischen Netzwerkinfrastruktur in Ihrem Rechenzentrum.

![](media/sddc/spacer1.png)![](media/sddc/netcontroller.png)

Ein Administrator verwendet ein Verwaltungstool, das direkt mit Netzwerkcontroller interagiert. Der Netzwerkcontroller übertragt Informationen über die Netzwerkinfrastruktur an das Verwaltungstool, einschließlich der virtuellen und physischen Infrastruktur.

![](media/sddc/learn.png)**[Erfahren Sie mehr über den Netzwerkcontroller](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-controller/network-controller)**

### <a name="datacenter-firewall"></a>Rechenzentrumsfirewall ###

![](media/sddc/networking-line.png)

Wenn es bereitgestellt und als ein Dienst angeboten wird, können Mandantenadministratoren Firewall-Richtlinien zum Schutz von virtuellen Netzwerken installieren und konfigurieren, um unerwünschten Datenverkehr aus dem Internet und Intranetnetzwerken fernzuhalten.

![](media/sddc/spacer1.png)![](media/sddc/firewall.png)

Der Internetanbieter-Administrator oder der Mandantenadministrator können die Rechenzentrumsfirewall-Richtlinien über den Netzwerkcontroller verwalten.

![](media/sddc/learn.png)**[Erfahren Sie mehr über die Rechenzentrumsfirewall](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-function-virtualization/datacenter-firewall-overview)**

### <a name="switch-embedded-teaming"></a>Switch Embedded Teaming ###

![](media/sddc/networking-line.png)

SET ist eine alternative NIC-Teaming-Lösung, die Sie in einer Umgebung verwenden können, die Hyper-V und [Software Defined Networking (SDN)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)-Stapel enthält.

![](media/sddc/spacer1.png)![](media/sddc/teaming.png)

![](media/sddc/learn.png)**[Weitere Informationen zu Switch Embedded Teaming](https://docs.microsoft.com/windows-server/networking/sdn/technologies/set-for-sdn)**

### <a name="software-load-balancing"></a>Softwarelastenausgleich ###

![](media/sddc/networking-line.png)

SLB ermöglicht es Ihnen, mehrere Server zum Hosten derselben Workload zu aktivieren, um hohe Verfügbarkeit und Skalierbarkeit bereitzustellen. Skalieren Sie Lastenausgleichsfunktionen mit SLB VMs auf den gleichen Hyper-V-Servern, die Sie für Ihre anderen VM-Arbeitslasten verwenden. SLB unterstützt die schnelle Erstellung und das Löschen von Lastenausgleich-Endpunkten für Cloud-Dienstanbieter-Vorgänge. SLB unterstützt Zehntausende von Gigabyte pro Cluster, bietet ein einfaches Modell für den Bereitstellungsprozess und kann einfach erweitert und zu reduziert werden.

![](media/sddc/spacer1.png)![](media/sddc/balancer.png)

![](media/sddc/learn.png)**[Erfahren Sie mehr über den Softwarelastenausgleich](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn)**


![](media/sddc/storage.png)

### <a name="storage-spaces-direct"></a>Direkte Speicherplätze ###

![](media/sddc/storage-line.png)

„Direkte Speicherplätze“ verwendet branchenübliche Server mit lokal angeschlossenen Laufwerken, um hoch verfügbare, hoch skalierbare softwaredefinierte Speicher zu einem Bruchteil der Kosten von herkömmlichen SAN- oder NAS-Arrays zu erstellen. Die Architektur vereinfacht radikal die Beschaffung und Bereitstellung.

![Jeder Knoten verfügt über Laufwerke, die von "direkte Speicherplätze" Zugriff auf die dann vom virtuellen Computer über freigegebene Clustervolumes in einem Pool zusammengefasst, auf der Clusterebene lokal verbunden.](media/sddc/spacer1.png)![](media/sddc/ssd.png)

„Direkte Speicherplätze“ führt den neuen Softwarespeicherbus ein und nutzt viele Features von Windows Server, die Sie bereits kennen, z. B. Failoverclustering, CSV (Cluster Shared Volume, freigegebenes Clustervolume), SMB3 (Server Message Block) und natürlich „Speicherplätze“.

![](media/sddc/learn.png)**[Erfahren Sie mehr über "direkte Speicherplätze"](storage/storage-spaces/storage-spaces-direct-overview.md)**
### <a name="storage-quality-of-service"></a>Quality of Service für Speicher ###


![](media/sddc/storage-line.png)

Ermöglicht eine zentrale Überwachung und Verwaltung der Speicherleistung für virtuelle Computer unter Verwendung der Hyper-V-Rolle und der Rolle des Dateiservers mit horizontaler Skalierung und verbessert so die Speicherressourcen-Fairness zwischen mehreren virtuellen Computern.

![](media/sddc/spacer1.png)![](media/sddc/qos.png)

Speicher-QoS ist in die softwaredefinierte Speicherlösung von Microsoft integriert, die mit dem Dateiserver mit horizontaler Skalierung und Hyper-V über das SMB3-Protokoll bereitgestellt wird. Ein neuer Richtlinien-Manager ermöglicht eine zentrale Überwachung der Speicherleistung.

![](media/sddc/learn.png)**[Weitere Informationen zu QoS für Speicher](https://docs.microsoft.com/windows-server/storage/storage-qos/storage-qos-overview)**

### <a name="storage-replica"></a>Speicherreplikat ###


![](media/sddc/storage-line.png)

Notfallwiederherstellung und -Bereitschaft stellen sicher, dass keine Daten verloren gehen und bieten die Möglichkeit, Daten auf unterschiedlichen Racks, Etagen, Gebäuden, Campusgeländen, Standorten und Ländern durch eine effizientere Verwendung von mehreren Rechenzentren synchron zu schützen.

![](media/sddc/spacer1.png)
![](media/sddc/storage-replica.png)

Synchrone Replikation

1. Anwendung schreibt Daten
2. Protokolldaten werden geschrieben, und die Daten werden am Remotestandort repliziert
3. Protokolldaten werden am Remotestandort geschrieben
4. Bestätigung durch den Remotestandort
5. Anwendungsschreibvorgang wird bestätigt

t & t1: Daten, die auf das Volume geleert Protokolle werden immer geschrieben


![](media/sddc/learn.png)**[Erfahren Sie mehr über die Funktion "Speicherreplikat"](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-overview)**


![](media/sddc/security.png)


### <a name="guarded-fabric"></a>Geschütztes Fabric ###


![](media/sddc/security-line.png)

Als Cloud-Dienstanbieter oder privater Cloud-Administrator in Unternehmen können Sie eine geschützte Fabric verwenden, um eine sicherere Umgebung für VMs bereitzustellen. Ein geschütztes Fabric besteht aus einem Host Guardian Service (Host-Überwachungsdienst) – in der Regel ein Cluster mit drei Knoten – sowie einem oder mehreren geschützten Hosts und einer Reihe von abgeschirmten virtuellen Computern (VMs).

![](media/sddc/spacer1.png)![](media/sddc/guarded-fabric.png)

![](media/sddc/learn.png)**[Erfahren Sie mehr über geschütztes fabric](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)**

### <a name="shielded-vms"></a>Abgeschirmte VMs ###

![](media/sddc/security-line.png)

Die Daten und der Status eines abgeschirmten VM sind geschützt gegen Überprüfung, Diebstahl und Manipulation durch Schadsoftware und Datacenter-Administratoren.

![](media/sddc/spacer1.png)![](media/sddc/shielded.png)

- Abgeschirmte VMs funktionieren nur in Fabrics, die als Besitzer des virtuellen Computers aufgeführt sind.
- Abgeschirmte VMs sind durch BitLocker oder auf andere Weise verschlüsselt, sodass nur die angegebenen Eigentümer sie ausführen können.
- Ausgeführte virtuelle Computer können in abgeschirmte Computer konvertiert werden.

![](media/sddc/learn.png)**[Erfahren Sie mehr über die abgeschirmte VMs](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)**

### <a name="host-guardian-service"></a>Host-Überwachungsdienst ###

![](media/sddc/security-line.png)

Host-Überwachungsdienst sind die Schlüssel zu legitimen Fabrics und zu verschlüsselten virtuellen Computern.

![](media/sddc/spacer1.png)![](media/sddc/guardian.png)

![](media/sddc/learn.png)**[Erfahren Sie mehr über die Host-Überwachungsdienst](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-manage-hgs)**

### <a name="device-health-attestation"></a>Integritätsnachweis für Geräte ###

![](media/sddc/security-line.png)

Der Integritätsnachweis ermöglicht Unternehmen, mit minimalem oder keinem Einfluss auf die Betriebskosten das Sicherheitsniveau ihrer Organisation auf hardwareüberwachte und -bescheinigte Sicherheit anzuheben.


![](media/sddc/spacer1.png)![](media/sddc/attestation.png)


Der vertrauenswürdige Modus für Hardware, wie oben angezeigt, bietet mit dem TPM v2. 0-Hardware-Stamm-Vertrauensmodell und der Einhaltung der Codeintegritätsrichtlinien für Schlüssel-Version die größtmögliche Sicherheit.


![](media/sddc/learn.png)**[Erfahren Sie mehr über Integritätsnachweis für Geräte](https://docs.microsoft.com/windows-server/security/device-health-attestation)**

![](media/sddc/management.png)

### <a name="powershell-dsc"></a>PowerShell-DSC ###

![](media/sddc/management-line.png)

Windows PowerShell Desired State Configuration ist eine in Windows integrierte Konfigurationsverwaltungsplattform, die auf offenen Standards basiert. DSC ist flexibel genug, in jeder Phase des Bereitstellungslebenszyklus (Entwicklung, Test, Präproduktion, Produktion) sowie bei horizontaler Skalierung zuverlässig und konsistent zu funktionieren.

![](media/sddc/spacer1.png)![](media/sddc/dsc.png)

DSC unterstützt die "fortlaufende Bereitstellungen", damit Sie Konfigurationen wiederholt bereitstellen können, ohne etwas zu beschädigen.

-  DSC-Konfigurationen übernehmen nur die Einstellungen, die von der ursprünglichen auf die schnellere Bereitstellung geändert wurden.
-  DSC kann lokal, in einer öffentlichen oder in einer privaten Cloud-Umgebung verwendet werden.
-  Sie können DSC mit Microsoft oder mit jeder nicht von Microsoft stammenden Lösung integrieren, solange Sie ein PowerShell-Skript auf dem Zielsystem ausführen können.

![](media/sddc/learn.png)**[Erfahren Sie mehr über die PowerShell DSC](https://docs.microsoft.com/powershell/dsc/overview)**


### <a name="system-center-vmm"></a>System Center VMM ###

![](media/sddc/management-line.png)

Virtual Machine Manager ist Teil der System Center-Suite, der zum Konfigurieren, Verwalten und Transformieren von herkömmlichen Datencentern verwendet wird, um eine einheitliche Verwaltung über lokale Dienstanbieter und Azure-Cloud anzubieten.

![](media/sddc/spacer1.png)![](media/sddc/vmm.png)

- Rechenzentrum: Konfigurieren und Verwalten von Datacenter-Komponenten als ein einziges Fabric in VMM. 
- Virtualisierungshosts: VMM hinzufügen, bereitstellen und Verwalten von Hyper-V und VMware-Virtualisierungshosts und -Clustern.
- Netzwerke: VMM bietet Netzwerkvirtualisierung, einschließlich Unterstützung für das Erstellen und Verwalten von virtuellen Netzwerken und Netzwerkgateways. 
- Speicher: VMM zu ermitteln, klassifizieren, bereitstellen, reservieren und Zuweisen von lokalen und Remotespeicher.

![](media/sddc/learn.png)**[Erfahren Sie mehr über System Center VMM](https://docs.microsoft.com/system-center/vmm/)**

### <a name="windows-admin-center"></a>Windows Admin Center ###

![](media/sddc/management-line.png)

Windows Admin Center ist ein lokal bereitgestelltes, browserbasiertes Verwaltungs-Tool, welches die lokale Verwaltung von Windows-Servern unabhängig von Azure oder der Cloud ermöglicht. Windows Admin Center bietet IT-Administratoren Vollzugriff auf alle Aspekte ihrer Server-Infrastruktur und ist besonders nützlich für die Verwaltung in privaten Netzwerken, die nicht mit dem Internet verbunden sind.

![](media/sddc/spacer1.png)![](media/sddc/architecture.png)

Nach dem Veröffentlichen des Servers im DNS und dem Einrichten der Unternehmensfirewall können Sie über das Internet auf Windows Admin Center zugreifen und Ihre Server dann von jedem beliebigen Standort mit Microsoft Edge oder Google Chrome verwenden und verwalten.

![](media/sddc/learn.png)**[Erfahren Sie mehr über Microsoft Project Windows Admin Center](manage/windows-admin-center/overview.md)**

