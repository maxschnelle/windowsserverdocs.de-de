---
title: Direkte Speicherplätze – Übersicht
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 03/26/2019
ms.assetid: 8bd0d09a-0421-40a4-b752-40ecb5350ffd
description: Eine Übersicht über "direkte Speicherplätze", ein Feature von Windows Server, die Sie in einer softwaredefinierten speicherlösung auf Cluster-Servern mit internem Speicher ermöglicht.
ms.localizationpriority: medium
ms.openlocfilehash: d71e4fc404f760102a2b22f71bbeec680868e9b8
ms.sourcegitcommit: e558dda2774345e9ad17ff04b759f68c59d88139
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2019
ms.locfileid: "9262783"
---
# Direkte Speicherplätze – Übersicht

>Gilt für: WindowsServer 2019, WindowsServer 2016

„Direkte Speicherplätze“ verwendet branchenübliche Server mit lokal angeschlossenen Laufwerken, um hoch verfügbare, hoch skalierbare softwaredefinierte Speicher zu einem Bruchteil der Kosten von herkömmlichen SAN- oder NAS-Arrays zu erstellen. Konvergente oder hyperkonvergente Architektur vereinfacht radikal die Beschaffung und Bereitstellung, während Features wie Zwischenspeicherung, Speicherebenen und Erasure coding zusammen mit den neuesten Hardwareinnovationen wie RDMA-Netzwerke und NVMe-Laufwerke, übermitteln unübertroffene Effizienz und Leistung.

"Direkte Speicherplätze" ist in Windows Server 2019 Datacenter, Windows Server 2016 Datacenter und [Windows Server Insider Preview-Builds](https://insider.windows.com/for-business-getting-started-server/)enthalten. 

Andere Anwendungen von Speicherplätzen, z. B. Cluster Shared SAS und eigenständige Server finden Sie unter ["Speicherplätze" (Übersicht)](overview.md). Wenn Sie Informationen zur Verwendung von Speicherplätzen auf einem Windows 10-PC suchen, finden Sie unter [Für Speicherplätze unter Windows 10](https://support.microsoft.com/help/12438/windows-10-storage-spaces).

<table>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>Grundlegende Informationen</a></strong>
            <ul>
              <li>Übersicht (Sie sind hier)</li>
              <li><a href="understand-the-cache.md">Grundlegendes zum Cache</a></li>
              <li><a href="storage-spaces-fault-tolerance.md">Fehlertoleranz und Speichereffizienz</a></li>
              <li><a href="drive-symmetry-considerations.md">Aspekte symmetrischer Laufwerke</a></li>
              <li><a href="understand-storage-resync.md">Grundlagen und Überwachung der Neusynchronisierung des Speichers</a></li>
              <li><a href="understand-quorum.md">Grundlegendes zu Cluster- und Pool-quorum</a></li>
              <li><a href="cluster-sets.md">Cluster-Gruppen</a></li>
            </ul>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>Plan</a></strong>
            <ul>
              <li><a href="storage-spaces-direct-hardware-requirements.md">Hardwareanforderungen</a></li>
              <li><a href="csv-cache.md">Mithilfe der CSV-speicherinterne Lesecache</li>
              <li><a href="choosing-drives.md">Auswählen von Laufwerken</a></li>
              <li><a href="plan-volumes.md">Planen von Volumes</a></li>
              <li><a href="storage-spaces-direct-in-vm.md">Verwendung von Gast-VM-Clustern</a></li>
              <li><a href="storage-spaces-direct-disaster-recovery.md">Notfallwiederherstellung</a></li>
            </ul>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>Bereitstellen</a></strong>
            <ul>
                    <li><a href="deploy-storage-spaces-direct.md">Bereitstellen von direkte Speicherplätze</a></li>
                    <li><a href="create-volumes.md">Erstellen von Volumes</a></li>
              <li><a href="nested-resiliency.md">Geschachtelte Ausfallsicherheit</a></li>
              <li><a href="../../failover-clustering/manage-cluster-quorum.md">Konfigurieren von Quorum</a></li>
              <li><a href="upgrade-storage-spaces-direct-to-windows-server-2019.md">Upgrade eines Storage Spaces Direct-Clusters auf Windows Server 2019</a></li>
            </ul>
        </td>        
        <td style="padding: 5px; border: 0;">
            <strong>Verwalten</a></strong>
            <ul>
              <li><a href="../../manage/windows-admin-center/use/manage-hyper-converged.md">Mit Windows Admin Center verwalten</a></li>
              <li><a href="add-nodes.md">Hinzufügen von Servern oder Laufwerken</a></li>
              <li><a href="maintain-servers.md">Server zu Wartungszwecken offline schalten</li>
              <li><a href="remove-servers.md">Server entfernen</a></li>
              <li><a href="resize-volumes.md">Erweitern von Volumes</a></li>
              <li><a href="../update-firmware.md">Aktualisieren der Laufwerkfirmware</a></li>
              <li><a href="performance-history.md">Leistungsverlauf</a></li>
              <li><a href="delimit-volume-allocation.md">Trennen der Zuweisung von Volumes</a></li>
              <li><a href="configure-azure-monitor.md">Verwenden von Azure-Monitor auf einem hyperkonvergenten cluster</a></li>
            </ul>
        </td>
    </tr>
    <tr style="border: 0;">
         <td style="padding: 5px; border: 0;">
            <strong>Problembehandlung</a></strong>
            <ul>
              <li><a href="storage-spaces-states.md">Problembehandlung bei Integrität- und Betriebsstatus</a></li>
              <li><a href="data-collection.md">Erfassen von Diagnosedaten mit "direkte Speicherplätze"</a></li>
            </ul>
         <td style="padding: 5px; border: 0;">
            <strong>Neue Blogbeiträge</a></strong>
            <ul>
              <li><a href="https://blogs.technet.microsoft.com/filecab/2018/10/30/windows-server-2019-and-intel-optane-dc-persistent-memory/">13,7 Million IOPS mit "direkte Speicherplätze": der neue Industry Datensatz für hyperkonvergente Infrastruktur</a></li>
              <li><a href="https://blogs.technet.microsoft.com/filecab/2018/10/02/hci-the-countdown-clock-starts-now/">Hyperkonvergente Infrastruktur in Windows Server 2019 - startet die Countdownuhr jetzt!</a></li>
              <li><a href="https://blogs.technet.microsoft.com/filecab/2018/06/27/windows-server-summit-recap/">Die Windows Server-Summit fünf große Ankündigungen</a></li>
              <li><a href="https://blogs.technet.microsoft.com/filecab/2018/03/27/storage-spaces-direct-momentum/">10.000 Storage Spaces Direct-Clustern und zählen …</a></li>
            </ul>
</table>

## Videos

**Kurzübersicht Video (5 Minuten)**

<iframe src="https://www.youtube-nocookie.com/embed/raeUiNtMk0E" width="560" height="315" allowfullscreen></iframe>

**"Direkte Speicherplätze" bei Microsoft Ignite 2018 (1 Stunde)**

[Bei YouTube ansehen](https://www.youtube.com/watch?v=5kaUiW3qo30)

**"Direkte Speicherplätze" bei Microsoft Ignite 2017 (1 Stunde)**

[Bei YouTube ansehen](https://www.youtube.com/watch?v=YDr2sqNB-3c)

**Starten Sie Ereignis at Microsoft Ignite 2016 (1 Stunde)**

[Bei YouTube ansehen](https://www.youtube.com/watch?v=-LK2ViRGbWs)

## Wichtigste Vorteile

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/simplicity-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>Einfachheit.</b> Wechseln Sie in weniger als 15 Minuten von branchenüblichen Servern unter Windows Server 2016 zu Ihrem ersten „Direkte Speicherplätze“-Cluster. Für System Center-Benutzer erfolgt die Bereitstellung über ein einziges Kontrollkästchen.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/performance-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>Unübertroffene Leistung.</b> Ganz gleich, ob All-Flash- oder Hybridspeicher, mit „Direkte Speicherplätze“ erreichen Sie mühelos über <a href="https://blogs.technet.microsoft.com/filecab/2016/07/26/storage-iops-update-with-storage-spaces-direct/">150.000 gemischte zufällige 4K-Random-IOPS (E/A-Vorgänge pro Sekunde) pro Server</a> mit konsistenter, geringer Latenz dank der in den Hypervisor eingebetteten Architektur, dem integrierten Lese-/Schreibcache und der Unterstützung für innovative, direkt auf dem PCIe-Bus montierte NVMe-Laufwerke.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/fault-tolerance-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>Fehlertoleranz. </b> Integrierte Resilienz verarbeitet Laufwerk-, Server- oder Komponentenausfälle bei fortlaufender Verfügbarkeit. Größere Bereitstellungen können auch für <a href="../../failover-clustering/fault-domains.md">Gehäuse- und Rack-Fehlertoleranz</a> konfiguriert werden. Bei Ausfall von Hardware brauchen Sie diese nur auszutauschen. Die Software setzt sich selbst und ohne komplizierte Verwaltungsschritte wieder instand.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/efficiency-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>Ressourceneffizienz.</b> Erasure Coding bietet bis zu 2,4 x höhere Speichereffizienz mit einzigartigen Innovationen wie Code für die lokale Wiederherstellung und ReFS-Ebenen in Echtzeit, um diese Effizienz auf Festplattenlaufwerke und gemischte Hot/Cold-Workloads auszudehnen, und das alles bei gleichzeitiger Minimierung der CPU-Auslastung, um Ressourcen dorthin zurückzugeben, wo sie am meisten benötigt werden: an die VMs.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/manageability-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>Verwaltbarkeit.</b> Verwenden Sie <a href="../storage-qos/storage-qos-overview.md">Storage QoS-Steuerelemente</a>, um zu gewährleisten, dass übermäßig ausgelastete VMs die Mindest- und Höchstgrenzen für IOPS pro-VM nicht unter- bzw. überschreiten. Der <a href="../../failover-clustering/health-service-overview.md">Integritätsdienst</a> bietet fortlaufende integrierte Überwachung und Warnung, und neue APIs erleichtern das Sammeln umfassender, clusterweiter Leistungs- und Kapazitätsmetriken.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/scalability-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>Skalierbarkeit.</b> Skalierung auf bis zu 16 Server und über 400 Laufwerke für bis zu 1 Petabyte (1.000 Terabyte) Speicher pro Cluster möglich. Zum horizontalen Skalieren fügen Sie einfach Laufwerke oder weitere Server hinzu. „Direkte Speicherplätze“ integriert und nutzt neue Laufwerke automatisch. Speichereffizienz und Leistung lassen sich berechenbar in großem Maßstab verbessern.
        </td>
    </tr>
</table>

## Bereitstellungsoptionen

„Direkte Speicherplätze“ wurde für zwei unterschiedliche Bereitstellungsoptionen entwickelt:

### Konvergente Bereitstellung

**Speicher und Compute in separaten Clustern.** Die Option der konvergenten Bereitstellung ordnet einen Dateiserver mit horizontaler Skalierung (Scale-out File Server, SoFS) in Ebenen über „Direkte Speicherplätze“ an, um NAS über SMB3-Dateifreigaben bereitzustellen. Dies ermöglicht die Skalierung von Compute/Workload unabhängig vom Speichercluster, was für Dienstanbieter und Unternehmen bei größeren Bereitstellungen wie Hyper-V-IaaS (Infrastruktur als Dienst) unerlässlich ist.

![„Direkte Speicherplätze“ stellt Speicher mit dem Feature „Dateiserver mit horizontaler Skalierung“ für Hyper-V-VMs in einem anderen Server oder Cluster bereit](media/storage-spaces-direct-in-windows-server-2016/converged-minimal.png)

### Hyperkonvergente Bereitstellung

**Ein einzelner Cluster für Compute und Speicher.** Die Option der hyperkonvergenten Bereitstellung führt virtuelle Hyper-V-Computer oder SQLServer-Datenbanken direkt auf den Servern aus, stellt den Speicher bereit und speichert die Dateien der virtuellen Computer auf den lokalen Volumes. Dadurch entfällt die Notwendigkeit, den Zugriff auf Dateiserver und die entsprechenden Berechtigungen zu konfigurieren, und die Hardwarekosten für kleine und mittelständische Unternehmen oder Installationen in Remotebüros/Filialen werden gesenkt. Finden Sie unter [Bereitstellen von direkte Speicherplätze](deploy-storage-spaces-direct.md).

![„Direkte Speicherplätze“ stellt Speicher für Hyper-V-VMs in demselben Cluster bereit](media/storage-spaces-direct-in-windows-server-2016/hyper-converged-minimal.png)

## Funktionsweise

„Direkte Speicherplätze“ ist die Weiterentwicklung von „Speicherplätze“, das mit Windows Server2012 eingeführt wurde. „Direkte Speicherplätze“ nutzt viele Features von Windows Server, die Sie bereits kennen, z. B. Failoverclustering, das CSV-Dateisystem (Cluster Shared Volume, freigegebenes Clustervolume), SMB3 (Server Message Block) und natürlich „Speicherplätze“. Außerdem werden neuen Technologie eingeführt, insbesondere der Softwarespeicherbus.

Hier finden Sie eine Übersicht über den „Direkte Speicherplätze“-Stapel:

![Stapel bei Verwendung von „Direkte Speicherplätze“](media/storage-spaces-direct-in-windows-server-2016/converged-full-stack.png)

**Netzwerkhardware.** „Direkte Speicherplätze“ verwendet für die Kommunikation zwischen Servern SMB3, einschließlich SMB Direct und SMB Multichannel über Ethernet. Es wird dringend empfohlen, mehr als 10GbE mit RDMA (Remote Direct Memory Access, Remotezugriff auf den direkten Speicher) zu verwenden, entweder iWARP oder RoCE.

**Speicherhardware.** Zwischen 2 und 16 Server mit lokal angeschlossenen SATA- SAS-, oder NVMe-Laufwerken. Jeder Server muss über mindestens 2 SSDs und mindestens 4 zusätzliche Laufwerke verfügen. Die SATA- und SAS-Geräte sollten sich hinter einem Hostbusadapter (HBA) und einer SAS-Erweiterung befinden. Wir empfehlen dringend die sorgfältig entwickelten und umfassend geprüften Plattformen unserer Partner (demnächst verfügbar).

**Failoverclustering.** Das integrierte Clusteringfeature von Windows Server wird verwendet, um den Server zu verbinden.

**Softwarespeicherbus.** Der Softwarespeicherbus ist neu in „Direkte Speicherplätze“. Er umfasst den Cluster und richtet ein softwaredefiniertes Speicherfabric ein, wodurch alle Server alle lokalen Laufwerke der jeweils anderen sehen können. Sie können es sich als Ersatz für die kostspielige und eingeschränkte Fibre Channel- oder Shared SAS-Verkabelung vorstellen.

**Cache der Speicherbusebene.** Der Softwarespeicherbus bindet dynamisch die schnellsten vorhandenen Laufwerke (z.B. SSD) an langsamere Laufwerke (z. B.HDDs), um das Zwischenspeichern von serverseitigem Lese-/Schreibzugriff zur Beschleunigung von E/A-Vorgängen und zur Steigerung des Durchsatzes zu ermöglichen.

**Speicherpool.** Die Sammlung der Laufwerke, die die Grundlage für „Speicherplätze“ darstellt, wird als Speicherpool bezeichnet. Der Speicherpool wird automatisch erstellt, und alle geeigneten Laufwerke werden automatisch ermittelt und hinzugefügt. Es wird dringend empfohlen, pro Cluster einen Pool mit den Standardeinstellungen zu verwenden. Weitere Informationen finden Sie in unserem [DeepDive-Artikel für den Speicherpool](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/).

**„Speicherplätze“.** „Speicherplätze“ bietet Fehlertoleranz für virtuelle „Festplatten“ mit [Spiegelung und/oder Erasure Coding](storage-spaces-fault-tolerance.md). Stellen Sie sich „Speicherplätze“ als verteiltes, softwaredefiniertes RAID mit den Laufwerken im Pool vor. In „Direkte Speicherplätze“ verfügen diese virtuellen Laufwerke in der Regel über Resilienz für zwei gleichzeitige Laufwerk- oder Serverausfälle (z. B. Drei-Wege-Spiegelung, wobei jede Datenkopie auf einem anderen Server gespeichert ist). Zusätzlich ist Gehäuse- und Rack-Fehlertoleranz verfügbar.

**Robustes Dateisystem (Resilient File System, ReFS).** ReFS ist das wichtigste, speziell für die Virtualisierung entwickelte Dateisystem. Es bietet erhebliche Beschleunigungen für VHDX-Dateivorgänge, wie Erstellung, Erweiterung und Prüfpunkt-Zusammenführung, sowie integrierte Prüfsummen zum Erkennen und Beheben von Bitfehlern. Außerdem werden Echtzeitebenen eingeführt, auf denen die Daten basierend auf ihrer Verwendung zwischen so genannten „Hot-“ und „Cold“-Speicherebenen in Echtzeit rotiert werden.

**Freigegebene Clustervolumes.** Das CSV-Dateisystem vereint alle ReFS-Volumes zu einem einzigen Namespace, auf den über jeden beliebigen Server zugegriffen werden kann, sodass alle Volumes für jeden Server aussehen und funktionieren, als ob sie lokal bereitgestellt worden wären.

**Dateiserver mit horizontaler Skalierung.** Diese letzte Ebene ist nur für konvergente Bereitstellungen erforderlich. Der Dateiserver mit horizontaler Skalierung bietet Clients, z. B. einem anderen Cluster mit Hyper-V, mithilfe des SMB3-Zugriffsprotokolls Remotezugriff auf Dateien über das Netzwerk, und wandelt „Direkte Speicherplätze“ dadurch effizient in NAS (Network Attached Storage) um.

## Kunden Geschichten

Es gibt [mehr als 10.000 Clustern](https://blogs.technet.microsoft.com/filecab/2018/03/27/storage-spaces-direct-momentum/) direkte weltweit ausgeführten "Speicherplätze" aus. Organisationen aller Größenordnungen, von Kleinunternehmen Bereitstellung nur zwei Knoten für große Unternehmen und Behörden Bereitstellen von Hunderten von Knoten, hängt "direkte Speicherplätze" für das wichtige Anwendung und die Infrastruktur.

Besuchen Sie [Microsoft.com/HCI](https://www.microsoft.com/hci) , um ihre Geschichten zu lesen:

[![GEntfernen Sie die Kunden Logos](media/storage-spaces-direct-in-windows-server-2016/customer-stories.png)](https://www.microsoft.com/hci)

## Verwaltungstools

Die folgenden Tools können zum Verwalten von und/oder überwachen "direkte Speicherplätze" verwendet werden:

| Name | Grafische oder Befehlszeilen? | Ausgezahlt oder enthalten? |
|-----------------|----------------------------|-------------------|
| [Windows Admin Center](../../manage/windows-admin-center/overview.md)     | Grafische    | Eingeschlossen |
| Server-Manager & Failovercluster-Manager                                 | Grafische    | Eingeschlossen |
| Windows PowerShell                                                        | Befehlszeile | Eingeschlossen |
| [System Center Virtual Machine Manager (SCVMM)](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-storage-spaces-direct-vmm) & [Operations Manager (SCOM)](https://www.microsoft.com/download/details.aspx?id=54700) | Grafische    | Kostenpflichtig     |

## Erste Schritte

Testen Sie Direkte Speicherplätze [in Microsoft Azure](https://blogs.technet.microsoft.com/filecab/2016/05/05/s2dazuretp5/), oder laden Sie eine für 180 Tage lizenzierte Evaluierungskopie von Windows Server von [Windows Server-Evaluierungsversionen](https://go.microsoft.com/fwlink/?linkid=842602) herunter.

## Weitere Informationen

-   [Fehlertoleranz und Speichereffizienz](storage-spaces-fault-tolerance.md)
-   [Speicherreplikat](../storage-replica/storage-replica-overview.md)
-   [Speicher zu Microsoft-blog](https://blogs.technet.microsoft.com/filecab/)
-   [Storage Spaces Direct throughput with iWARP](https://blogs.technet.microsoft.com/filecab/2017/03/13/storage-spaces-direct-throughput-with-iwarp) (Durchsatz von „Direkte Speicherplätze“ mit iWARP (TechNet-Blog)
-   [Neues beim Failoverclustering unter Windows Server](../../failover-clustering/whats-new-in-failover-clustering.md)  
-   [Quality of Service für Speicher](../storage-qos/storage-qos-overview.md)
-   [Windows IT Pro-Support](https://www.microsoft.com/itpro/windows/support)
