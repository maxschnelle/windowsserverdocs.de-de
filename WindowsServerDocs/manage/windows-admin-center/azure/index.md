---
title: Verbinden von Windows Server mit Azure Hybriddiensten
description: Du kannst lokale Bereitstellungen von Windows Server mithilfe von Azure-Hybriddiensten auf die Cloud erweitern.
ms.technology: manage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 05/31/2019
ms.openlocfilehash: 460399a57bc229b44d37a9fdd1e4938bf9e7d6ac
ms.sourcegitcommit: fe621b72d45d0259bac1d5b9031deed3dcbed29d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2019
ms.locfileid: "66455361"
---
# <a name="connecting-windows-server-to-azure-hybrid-services"></a>Verbinden von Windows Server mit Azure Hybriddiensten

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal)

Du kannst lokale Bereitstellungen von Windows Server mithilfe von Azure-Hybriddiensten auf die Cloud erweitern. Diese Clouddienste bieten eine Reihe nützlicher Funktionen, darunter die folgenden:

- Schützen von virtuellen Computern und Verwenden von cloudbasierter Sicherung und Notfallwiederherstellung (HA/DR) mit Azure Site Recovery 
- Nachverfolgen von Anwendungen, Netzwerk und Infrastruktur mithilfe von erweiterten Analysefunktionen und maschinellem Lernen in Azure Monitor 
- Vereinfachen der Netzwerkverbindung zu Azure mit dem Azure Netzwerkadapter
- Virtuelle Computer mit der Azure-Updateverwaltung auf dem neuesten Stand halten

Azure-Hybriddienste funktionieren mit Windows-Servern in den folgenden Konfigurationen:

- Eigenständige physische Server und virtuelle Computer (VMs)
- Cluster, einschließlich der hyperkonvergenten Clustern, die durch die Programme [Azure Stack HCI](https://docs.microsoft.com/azure-stack/operator/azure-stack-hci-overview) und [Windows Server Software-Defined (WSSD)](https://www.microsoft.com/en-us/cloud-platform/software-defined-datacenter) zertifiziert sind

Während du die meisten Azure-Hybriddienste über das Azure-Portal und ein oder zwei Downloads einrichten kannst, sind viele davon direkt in Windows Admin Center integriert, um eine vereinfachte Einrichtung und eine serverorientierte Ansicht der Dienste zu ermöglichen.

## <a name="azure-hybrid-services-tool"></a>Azure-Hybriddienstetool

Das Azure-Hybriddienstetool in [Windows Admin Center](../understand/windows-admin-center.md) konsolidiert alle integrierten Azure-Dienste in einem zentralen Hub, in dem du mühelos alle verfügbaren Azure-Dienste erkennen kannst, die einen Mehrwert für Ihre lokale oder hybride Umgebung bieten. 

![Screenshot von Windows Admin Center mit dem Azure-Hybriddienstetool](../media/azure-services/ahs-discover.png)

Wenn du eine Verbindung mit einem Server herstellst, auf dem bereits Azure-Dienste aktiviert sind, dient das Azure-Hybriddienstetool als zentrale Benutzeroberfläche zur Anzeige aller aktivierten Dienste auf diesem Server. Du kannst mühelos zum entsprechenden Tool in Windows Admin Center gelangen, das Azure-Portal für eine bessere Verwaltung dieser Azure-Dienste aufrufen oder über die immer verfügbare Dokumentation mehr erfahren. 

![Screenshot von Windows Admin Center mit Azure-Diensten, die bereits auf dem Server installiert sind](../media/azure-services/ahs-dayN.png)

Über das Azure-Hybriddienstetool hast du folgende Möglichkeiten:
- Sichern des Windows-Servers über Windows Admin Center mit [Azure Backup](azure-backup.md)
- [Schützen der virtuellen Hyper-V-Computer mit Azure Site Recovery in Windows Admin Center](azure-site-recovery.md)
- Synchronisierung des Dateiservers mit der Cloud per [Azure-Dateisynchronisierung](azure-file-sync.md)
- Verwalten von Betriebssystemupdates für alle deine Windows-Server – lokal oder in der Cloud – mit [Azure-Updateverwaltung](azure-update-management.md)
- Überwachen von Servern, sowohl lokal als auch in der Cloud, und Konfigurieren von Warnungen mit [Azure Monitor](azure-monitor.md)
- Verbinden der lokalen Server mit einem virtuellen Azure-Netzwerk mithilfe von [Azure-Netzwerkadapter](https://aka.ms/WACNetworkAdapter)

## <a name="services-for-stand-alone-servers-and-vms"></a>Dienste für eigenständige Server und virtuelle Computer

Dies ist die vollständige Liste der Azure-Dienste, die Funktionen für eigenständige Server und virtuelle Computer bereitstellen:

- **Synchronisierung des Dateiservers mit der Cloud per [Azure-Dateisynchronisierung](https://aka.ms/afs)**  
Synchronisiere Dateien auf diesem Server mit Azure-Dateifreigaben. Behalte alle deine Dateien lokal, oder verwende Cloudtiering, um nur die am häufigsten verwendeten Dateien auf dem Server zwischenzuspeichern und kalte Daten in die Cloud zu übertragen. Daten in der Cloud können gesichert werden, sodass keine lokale Serversicherung erforderlich ist. Darüber hinaus kann mit Multisite-Synchronisierung eine Gruppe von Dateien auf mehreren Servern synchronisiert werden.

- **Hinzufügen einer Sicherheitsschicht zu Windows Admin Center durch Hinzufügen von [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/)-Authentifizierung**  
Du kannst Windows Admin Center eine zusätzliche Sicherheitsschicht hinzufügen, indem du von den Benutzern verlangst, sich über Azure Active Directory (Azure AD)-Identitäten für den Zugriff auf das Gateway zu authentifizieren. Mit der Azure AD-Authentifizierung kannst du auch die Sicherheitsfunktionen von Azure AD wie bedingten Zugriff und mehrstufige Authentifizierung nutzen.  
Weitere Informationen findest du unter [Konfigurieren der Azure Active Directory-Authentifizierung für Windows Admin Center (Vorschau)](../configure/user-access-control.md#azure-active-directory).  

- **Schützen der virtuellen Hyper-V-Computer mit [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)**  
Du kannst Arbeitslasten auf virtuellen Computern replizieren und so deine wichtige Geschäftsinfrastruktur in Notfällen schützen. Windows Admin Center optimiert die Einrichtung und den Prozess der Replikation der virtuellen Computer auf deinen Hyper-V-Servern oder -Clustern und macht es einfacher, die Ausfallsicherheit der Umgebung mit dem Notfallwiederherstellungsdienst von Azure Site Recovery zu erhöhen.  
Weitere Informationen findest du unter [Schützen Sie Ihre Hyper-V-VMs mit Azure Site Recovery und Windows Admin Center](azure-site-recovery.md).

- **Sichern der Windows-Server mit [Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview)**  
Du kannst deine Windows-Server bei Azure sichern und so dazu beitragen, sie vor versehentlichem oder böswilligem Löschen, Beschädigung und Ransomware zu schützen.  
Weitere Informationen findest du unter [Back up your servers with Azure Backup](azure-backup.md) (Sichern der Server mit Azure Backup).

- **Überwachen und Erhalten von E-Mail-Benachrichtigungen für alle Server in der Umgebung mit [Azure Monitor für virtuelle Computer](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)**  
Mit Azure Monitor, auch bekannt als „Virtual Machines Insights“, kannst du die Integrität und die Ereignisse des Servers überwachen, E-Mail-Benachrichtigungen erstellen, eine konsolidierte Ansicht der Serverleistung in der Umgebung erhalten und Anwendungen, Systeme und Dienste visualisieren, die mit einem bestimmten Server verbunden sind.  
Weitere Informationen findest du unter [Connect your servers to Azure Monitor and configure email notifications](azure-monitor.md) (Verbinden der Server mit Azure Monitor und Konfigurieren von E-Mail-Benachrichtigungen).

- **Zentrales Verwalten von Betriebssystemupdates für alle deine Windows-Server mit [Azure-Updateverwaltung](https://docs.microsoft.com/azure/automation/automation-update-management)**  
Du kannst Updates und Patches für mehrere Server und virtuelle Computer über eine einzige Stelle anstatt auf Serverebene verwalten. Mit Azure-Updateverwaltung kannst du den Status verfügbarer Updates schnell bewerten, die Installation der erforderlichen Updates planen und die Ergebnisse der Bereitstellung überprüfen, um sicherzustellen, dass Updates erfolgreich angewendet werden. Dies ist unabhängig davon möglich, ob es sich bei den Servern um virtuelle Azure-Computer handelt, die von anderen Cloudanbietern gehostet werden, oder um lokale Computer.  
Weitere Informationen findest du unter [Verwenden von Windows Admin Center zum Verwalten von Betriebssystem-Updates mit der Azure-Updateverwaltung](azure-update-management.md).

- **Verbinden der lokalen Server mit einem virtuellen Azure-Netzwerk mithilfe eines [Azure-Netzwerkadapters](https://aka.ms/WACNetworkAdapter)**  
Du kannst deinen lokalen Servern einen Azure-Netzwerkadapter hinzufügen, um den Server sicher mit einem virtuellen Azure-Netzwerk zu verbinden.  
Weitere Informationen findest du unter [Configure a point-to-site VPN connection between an on-premises Windows Server and an Azure Virtual Network](https://aka.ms/WACNetworkAdapter) (Konfigurieren einer Punkt-zu-Standort-VPN-Verbindung zwischen einem lokalen Windows-Server und einem virtuellen Azure-Netzwerk).

- **Verwalten von virtuellen Azure IaaS-Computern mit [Windows Admin Center](manage-azure-vms.md)**  
Mit Windows Admin Center kannst du deine virtuellen Azure-Computer und lokalen Computer verwalten. Durch die Konfiguration des Windows Admin Center-Gateways für die Verbindung mit deinem Azure VNET kannst du virtuelle Computer in Azure mit den konsistenten, vereinfachten Tools von Windows Admin Center verwalten. Weitere Informationen findest du unter [Verwalten von virtuellen Azure IaaS-Computern mit Windows Admin Center](manage-azure-vms.md).

## <a name="services-for-clusters"></a>Dienste für Cluster

Dies sind die Azure-Dienste, die Funktionen für Cluster als Ganzes bereitstellen (diese sind noch nicht alle in Windows Admin Center integriert):

- [Überwachen eines hyperkonvergenten Clusters mit Azure Monitor](../../../storage/storage-spaces/configure-azure-monitor.md)
- [Schützen von virtuellen Computern mit Azure Site Recovery](azure-site-recovery.md)
- [Bereitstellen eines Cluster-Cloudzeugen](../../../failover-clustering/deploy-cloud-witness.md)

## <a name="see-also"></a>Weitere Informationen

- [Verbinden von Windows Admin Center mit Azure](azure-integration.md)
- [Bereitstellen von Windows Admin Center in Azure](deploy-wac-in-azure.md)