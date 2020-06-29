---
title: Verbinden von Windows Server mit Azure Hybriddiensten
description: Du kannst lokale Bereitstellungen von Windows Server mithilfe von Azure-Hybriddiensten auf die Cloud erweitern.
ms.technology: manage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 05/31/2019
ms.openlocfilehash: ec01431b320c710eddedc2f9c5e174bea1355b1c
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475697"
---
# <a name="connecting-windows-server-to-azure-hybrid-services"></a>Verbinden von Windows Server mit Azure Hybriddiensten

Du kannst lokale Bereitstellungen von Windows Server mithilfe von Azure-Hybriddiensten auf die Cloud erweitern. Diese Clouddienste bieten eine Reihe nützlicher Funktionen, sowohl für die Erweiterung lokaler Bereitstellungen in Azure als auch für die zentrale Verwaltung aus Azure.

![Diagramm, das den Pfeil von einem lokalen Standort in die Cloud – für die Erweiterung des lokalen Standorts in Azure – sowie einen Pfeil von der Cloud zum lokalen Standort –für die zentrale Verwaltung mit Azure – zeigt](../media/azure-services/hybrid-framing.png)

Die Verwendung von hybriden Azure-Diensten im Windows Admin Center bietet dir folgende Möglichkeiten:

- [Schützen von virtuellen Computern und Verwenden von cloudbasierter Sicherung und Notfallwiederherstellung (HA/DR)](#back-up-and-protect-your-on-premises-servers-and-vms).
- [Erweitern der lokalen Kapazität mit Speicher und Compute in Azure und Vereinfachen der Netzwerkkonnektivität mit Azure](#extend-on-premises-capacity-with-azure).
- [Übergreifende Zentralisierung von Überwachung, Governance, Konfiguration und Sicherheit für deine sämtlichen Anwendungen, das Netzwerk und die gesamte Infrastruktur mithilfe intelligenter Azure-Verwaltungsdienste in der Cloud](#centrally-manage-your-hybrid-environment-from-azure).

Zwar können die meisten hybriden Azure-Dienste durch Herunterladen einer App und etwas manuelle Konfiguration eingerichtet werden, doch sind viele direkt in das Windows Admin Center integriert, um ein verbessertes Setupverhalten und eine serverorientierte Ansicht der Dienste zu bieten. Im Windows Admin Center stehen außerdem komfortable intelligente Hyperlinks zum Azure-Portal zur Verfügung, um die verbundenen Azure-Ressourcen sowie eine zentralisierte Ansicht deiner Hybridumgebung anzuzeigen.

## <a name="discover-integrated-services-in-the-azure-hybrid-services-tool"></a>Entdecken der integrierten Dienste im Azure-Hybriddienstetool

Das Azure-Hybriddienstetool in [Windows Admin Center](../overview.md) konsolidiert alle integrierten Azure-Dienste in einem zentralen Hub, in dem du mühelos alle verfügbaren Azure-Dienste erkennen kannst, die einen Mehrwert für Ihre lokale oder hybride Umgebung bieten.

![Screenshot von Windows Admin Center mit dem Azure-Hybriddienstetool](../media/azure-services/ahs-discover.png)

Wenn du eine Verbindung mit einem Server herstellst, auf dem bereits Azure-Dienste aktiviert sind, dient das Azure-Hybriddienstetool als zentrale Benutzeroberfläche zur Anzeige aller aktivierten Dienste auf diesem Server. Du kannst mühelos zum entsprechenden Tool in Windows Admin Center gelangen, das Azure-Portal für eine bessere Verwaltung dieser Azure-Dienste aufrufen oder über die immer verfügbare Dokumentation mehr erfahren.

![Screenshot von Windows Admin Center mit Azure-Diensten, die bereits auf dem Server installiert sind](../media/azure-services/ahs-dayN.png)

Über das Azure-Hybriddienstetool hast du folgende Möglichkeiten:

- Sichern des Windows-Servers über Windows Admin Center mit [Azure Backup](azure-backup.md)
- [Schützen der virtuellen Hyper-V-Computer mit Azure Site Recovery in Windows Admin Center](azure-site-recovery.md)
- Synchronisierung des Dateiservers mit der Cloud per [Azure-Dateisynchronisierung](azure-file-sync.md)
- Verwalten von Betriebssystemupdates für alle deine Windows-Server – lokal oder in der Cloud – mit [Azure-Updateverwaltung](azure-update-management.md)
- Überwachen von Servern, sowohl lokal als auch in der Cloud, und Konfigurieren von Warnungen mit [Azure Monitor](azure-monitor.md)
- Anwenden von Governancerichtlinien auf deine lokalen Server durch Azure-Richtlinien mithilfe von [Azure Arc für Server](https://docs.microsoft.com/azure/azure-arc/servers/overview)
- Schutz deiner Server und Erwerb von erweitertem Schutz vor Bedrohungen mit [Azure Security Center](https://docs.microsoft.com/azure/security-center/windows-admin-center-integration)
- Verbinden der lokalen Server mit einem virtuellen Azure-Netzwerk mithilfe von [Azure-Netzwerkadapter](https://aka.ms/WACNetworkAdapter)
- Transparentes Einbinden von Azure-VMs in das lokale Netzwerk mit [Azure Extended Network](https://go.microsoft.com/fwlink/?linkid=2109517&clcid=0x409)

## <a name="back-up-and-protect-your-on-premises-servers-and-vms"></a>Sichern und Schützen deiner lokalen Server und VMs

- **Sichern der Windows-Server mit [Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview)** Sie können Ihre Windows-Server bei Azure sichern und so dazu beitragen, sie vor versehentlichem oder böswilligem Löschen, Beschädigung und Ransomware zu schützen.
Weitere Informationen findest du unter [Back up your servers with Azure Backup](azure-backup.md) (Sichern der Server mit Azure Backup).

- **Schützen der virtuellen Hyper-V-Computer mit [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)** Sie können Arbeitslasten auf virtuellen Computern replizieren und so Ihre wichtige unternehmenskritische Infrastruktur in Notfällen schützen. Windows Admin Center optimiert die Einrichtung und den Prozess der Replikation der virtuellen Computer auf deinen Hyper-V-Servern oder -Clustern und macht es einfacher, die Ausfallsicherheit der Umgebung mit dem Notfallwiederherstellungsdienst von Azure Site Recovery zu erhöhen.
Weitere Informationen findest du unter [Schützen Sie Ihre Hyper-V-VMs mit Azure Site Recovery und Windows Admin Center](azure-site-recovery.md).

- **Verwenden der synchronen oder asynchronen blockbasierten Replikation in einer VM in Azure mithilfe von [Speicherreplikaten](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-overview)** Mithilfe eines Speicherreplikats können Sie blockbasierte oder volumebasierte Replikation auf Server-zu-Server-Ebene auf einem sekundären Server oder in einer VM konfigurieren. Im Windows Admin Center kannst du eine Azure VM speziell für dein Replikationsziel erstellen, was dich beim richtigen Dimensionieren und ordnungsgemäßen Konfigurieren des Speichers in einer neuen Azure VM unterstützt.
Weitere Informationen findest du unter [Server-to-server replication with Storage Replica](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-ui) (Server-zu-Server-Replikation mit einem Speicherreplikat).

## <a name="extend-on-premises-capacity-with-azure"></a>Erweitern der lokalen Kapazität mit Azure

### <a name="extend-storage-capacity"></a>Erweitern der Speicherkapazität

- **Synchronisierung des Dateiservers mit der Cloud per [Azure-Dateisynchronisierung](https://aka.ms/afs)** Synchronisieren Sie Dateien auf diesem Server mit Azure-Dateifreigaben. Behalte alle deine Dateien lokal, oder verwende Cloudtiering, um Platz freizugeben, sodass nur die am häufigsten verwendeten Dateien auf dem Server zwischengespeichert und kalte Daten in die Cloud übertragen werden. Daten in der Cloud können gesichert werden, sodass keine lokale Serversicherung erforderlich ist. Darüber hinaus kann mit Multisite-Synchronisierung eine Gruppe von Dateien auf mehreren Servern synchronisiert werden.
Weitere Informationen findest du unter [Synchronisierung des Dateiservers mit der Cloud per Azure-Dateisynchronisierung](azure-file-sync.md).

- **Migrieren von Speicher zu einem virtuellen Computer in Azure mithilfe des [Speichermigrationsdiensts](https://docs.microsoft.com/windows-server/storage/storage-migration-service/overview)** Verwenden Sie dieses Schritt-für-Schritt-Tool, um den Datenbestand auf Windows- und Linux-Servern zu erfassen und die Daten anschließend in eine neue Azure VM zu übertragen. Windows Admin Center kann eine neue Azure VM für die Aufgabe erstellen, die richtig dimensioniert und ordnungsgemäß konfiguriert ist, um die Daten von deinem Quellserver entgegenzunehmen.
Weitere Informationen findest du unter [Verwenden des Speichermigrationsdiensts zum Migrieren eines Servers](https://docs.microsoft.com/windows-server/storage/storage-migration-service/migrate-data).

### <a name="extend-compute-capacity"></a>Erweitern der Computekapazität

- **Erstellen eines neuen virtuellen Azure-Computers, ohne Windows Admin Center zu verlassen** Wechseln Sie im Windows Admin Center von der Seite *Alle Verbindungen* zu **Hinzufügen**, und wählen Sie dann unter **Azure VM** die Option **Neu erstellen** aus. Dieses Schritt-für-Schritt-Tool zur Erstellung ermöglicht sogar den Beitritt der Azure VM zu einer Domäne und die Konfiguration des Speichers.

- **Nutzen von Azure zum Erreichen eines Quorums auf Ihrem Failovercluster mithilfe eines [Cloudzeugen](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness)** Statt in zusätzliche Hardware zu investieren, um auf einem Cluster aus zwei Knoten Quorum zu erreichen, können Sie ein Azure-Speicherkonto verwenden, das als Clusterzeuge für Ihren Azure Stack HCI-Cluster oder sonstigen Failovercluster fungiert.
Weitere Informationen finden Sei unter [Deploy a cloud witness for a Failover Cluster (Bereitstellen eines Cloudzeugen für einen Failovercluster)](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness).

### <a name="simplify-network-connectivity-between-your-on-premises-and-azure-networks"></a>Vereinfachen der Netzwerkkonnektivität zwischen deinem lokalen und deinem Azure-Netzwerk

- **Verbinden der lokalen Server mit einem virtuellen Azure-Netzwerk mithilfe von [Azure-Netzwerkadapter](https://aka.ms/WACNetworkAdapter)** Lassen Sie sich im Windows Admin Center beim Einrichten eines Punkt-zu-Standort-VPNs von einem lokalen Server in ein virtuelles Azure-Netzwerk helfen.

- **Transparentes Einbinden von Azure-VMs in das lokale Netzwerk mit [Azure Extended Network](https://go.microsoft.com/fwlink/?linkid=2109517&clcid=0x409)** Im Windows Admin Center kann ein Standort-zu-Standort-VPN eingerichtet werden, mit dem sich Ihre lokalen IP-Adressen in das Azure vNet erweitern lassen, sodass Workloads komfortabler nach Azure verschoben werden können, ohne Abhängigkeiten bei den IP-Adressen zu beschädigen.

## <a name="centrally-manage-your-hybrid-environment-from-azure"></a>Zentrale Verwaltung deiner Hybridumgebung aus Azure

- **Überwachen und Erhalten von E-Mail-Benachrichtigungen für alle Server in der Umgebung mit [Azure Monitor für virtuelle Computer](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)** Mit Azure Monitor, auch bekannt als „Virtual Machines Insights“, können Sie die Integrität und die Ereignisse des Servers überwachen, E-Mail-Benachrichtigungen erstellen, eine konsolidierte Ansicht der Serverleistung in der Umgebung erhalten und Anwendungen, Systeme und Dienste visualisieren, die mit einem bestimmten Server verbunden sind. Im Windows Admin Center können ferner standardmäßige E-Mail-Benachrichtigungen für Ereignisse bei der Serverintegrität und der Clusterintegrität eingerichtet werden.
Weitere Informationen findest du unter [Connect your servers to Azure Monitor and configure email notifications](azure-monitor.md) (Verbinden der Server mit Azure Monitor und Konfigurieren von E-Mail-Benachrichtigungen).

- **Zentrales Verwalten von Betriebssystemupdates für alle Ihre Windows Server-Instanzen mit [Azure-Updateverwaltung](https://docs.microsoft.com/azure/automation/automation-update-management)** Sie können Updates und Patches für mehrere Server und virtuelle Computer über eine einzige Stelle anstatt auf Serverebene verwalten. Mit Azure-Updateverwaltung kannst du den Status verfügbarer Updates schnell bewerten, die Installation der erforderlichen Updates planen und die Ergebnisse der Bereitstellung überprüfen, um sicherzustellen, dass Updates erfolgreich angewendet werden. Dies ist unabhängig davon möglich, ob es sich bei den Servern um virtuelle Azure-Computer handelt, die von anderen Cloudanbietern gehostet werden, oder um lokale Computer.
Weitere Informationen findest du unter [Verwenden von Windows Admin Center zum Verwalten von Betriebssystem-Updates mit der Azure-Updateverwaltung](azure-update-management.md).

- **Verbessern des Sicherheitsstatus und Erwerb von erweitertem Schutz vor Bedrohungen mit [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro)** Azure Security Center ist ein Sicherheitsmanagementsystem für vereinheitlichte Infrastruktur, das den Sicherheitsstatus Ihrer Rechenzentren stärkt und übergreifend für alle Ihre hybriden Workloads in der Cloud – ob in Azure oder nicht – oder lokal erweiterten Schutz vor Bedrohungen bietet. Mit Windows Admin Center kannst du deine Server komfortabel einrichten und sie mit dem Azure Security Center verbinden.
Weitere Informationen findest du unter [Integrieren von Azure Security Center in Windows Admin Center (Vorschau)](https://docs.microsoft.com/azure/security-center/windows-admin-center-integration).

- **Anwenden von Richtlinien und Sicherstellen der Compliance in der gesamten hybriden Umgebung mit [Azure Arc für Server ](https://docs.microsoft.com/azure/azure-arc/servers/overview) und [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview)** Erfassen, Ordnen und Verwalten lokaler Server in Azure. Du kannst Server mithilfe von Azure-Richtlinien verwalten, den Zugriff mithilfe von RBAC steuern und weitere Verwaltungsdienste in Azure aktivieren.

## <a name="clusters-versus-stand-alone-servers-and-vms"></a>Cluster im Vergleich mit eigenständigen Servern und VMs

Azure-Hybriddienste funktionieren mit Windows-Servern in den folgenden Konfigurationen:

- Eigenständige physische Server und virtuelle Computer (VMs)
- Cluster, einschließlich der hyperkonvergenten Clustern, die durch die Programme [Azure Stack HCI](../../../azure-stack-hci/index.md) und [Windows Server Software-Defined (WSSD)](https://www.microsoft.com/cloud-platform/software-defined-datacenter) zertifiziert sind

### <a name="services-for-stand-alone-servers-and-vms"></a>Dienste für eigenständige Server und virtuelle Computer

Dies ist die vollständige Liste der Azure-Dienste, die Funktionen für eigenständige Server und virtuelle Computer bereitstellen:

- Sichern des Windows-Servers über Windows Admin Center mit [Azure Backup](azure-backup.md)
- [Schützen der virtuellen Hyper-V-Computer mit Azure Site Recovery in Windows Admin Center](azure-site-recovery.md)
- Synchronisierung des Dateiservers mit der Cloud per [Azure-Dateisynchronisierung](azure-file-sync.md)
- Verwalten von Betriebssystemupdates für alle deine Windows-Server – lokal oder in der Cloud – mit [Azure-Updateverwaltung](azure-update-management.md)
- Überwachen von Servern, sowohl lokal als auch in der Cloud, und Konfigurieren von Warnungen mit [Azure Monitor](azure-monitor.md)
- Anwenden von Governancerichtlinien auf deine lokalen Server durch Azure-Richtlinien mithilfe von [Azure Arc für Server](https://docs.microsoft.com/azure/azure-arc/servers/overview)
- Schutz deiner Server und Erwerb von erweitertem Schutz vor Bedrohungen mit [Azure Security Center](https://docs.microsoft.com/azure/security-center/windows-admin-center-integration)
- Verbinden der lokalen Server mit einem virtuellen Azure-Netzwerk mithilfe von [Azure-Netzwerkadapter](https://aka.ms/WACNetworkAdapter)
- Transparentes Einbinden von Azure-VMs in das lokale Netzwerk mit [Azure Extended Network](https://go.microsoft.com/fwlink/?linkid=2109517&clcid=0x409)

### <a name="services-for-clusters"></a>Dienste für Cluster

Dies sind die Azure-Dienste, die für die Bereitstellung der allgemeinen Funktionalität für Cluster zuständig sind:

- [Überwachen eines hyperkonvergenten Clusters mit Azure Monitor](../../../storage/storage-spaces/configure-azure-monitor.md)
- [Schützen von virtuellen Computern mit Azure Site Recovery](azure-site-recovery.md)
- [Bereitstellen eines Cluster-Cloudzeugen](../../../failover-clustering/deploy-cloud-witness.md)

## <a name="other-azure-integrated-abilities-of-windows-admin-center"></a>Andere in Azure integrierte Funktionen von Windows Admin Center

- **[Hinzufügen von Azure VM-Verbindungen](manage-azure-vms.md) in Windows Admin Center** Mit Windows Admin Center können Sie Ihre virtuellen Azure-Computer und lokalen Computer verwalten. Durch die Konfiguration des Windows Admin Center-Gateways für die Verbindung mit deinem Azure VNET kannst du virtuelle Computer in Azure mit den konsistenten, vereinfachten Tools von Windows Admin Center verwalten.
Weitere Informationen findest du unter [Verwalten von virtuellen Azure IaaS-Computern mit Windows Admin Center](manage-azure-vms.md).

- **Hinzufügen einer Sicherheitsschicht zu Windows Admin Center durch Hinzufügen von [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/)-Authentifizierung** Sie können eine zusätzliche Sicherheitsschicht zum Windows Admin Center hinzufügen, indem Sie von den Benutzern verlangen, sich über Azure Active Directory (Azure AD)-Identitäten für den Zugriff auf das Gateway zu authentifizieren. Mit der Azure AD-Authentifizierung kannst du auch die Sicherheitsfunktionen von Azure AD wie bedingten Zugriff und mehrstufige Authentifizierung nutzen.
Weitere Informationen findest du unter [Konfigurieren der Azure Active Directory-Authentifizierung für Windows Admin Center](../configure/user-access-control.md#azure-active-directory).

- **Direktes Verwalten von Azure-Ressourcen mithilfe der in Windows Admin Center eingebetteten [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview)** Nutzen Sie Azure Cloud Shell zum Abrufen einer Bash- oder PowerShell-Benutzeroberfläche in Windows Admin Center für den einfachen Zugriff auf Azure-Verwaltungsaufgaben.
Weitere Informationen findest du unter [Übersicht zu Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).


## <a name="additional-references"></a>Weitere Verweise

- [Verbinden von Windows Admin Center mit Azure](azure-integration.md)
- [Bereitstellen von Windows Admin Center in Azure](deploy-wac-in-azure.md)
