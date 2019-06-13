---
title: Verbinden von Windows Server mit Azure Hybrid-Diensten
description: Sie können bei lokalen Bereitstellungen von Windows Server in die Cloud erweitern, mithilfe von Azure Hybrid-Diensten.
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
# <a name="connecting-windows-server-to-azure-hybrid-services"></a>Verbinden von Windows Server mit Azure Hybrid-Diensten

>Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal)

Sie können bei lokalen Bereitstellungen von Windows Server in die Cloud erweitern, mithilfe von Azure Hybrid-Diensten. Diese Cloud-Dienste bieten ein Array von nützlichen Funktionen, einschließlich der folgenden:

- Schützen Sie virtueller Computer und verwenden Sie Cloud-basierten Backup und Disaster Recovery (HA/DR) mit Azure Site Recovery. 
- Verfolgen Sie, was in Anwendungen, Netzwerk und Infrastruktur mithilfe von erweiterten Analysen und Machine learning in Azure Monitor geht. 
- Vereinfachen Sie die Netzwerkkonnektivität mit Azure mit Azure-Netzwerkadapter.
- Halten Sie virtuelle Computer auf dem neuesten Stand mit der Azure-Updateverwaltung.

Azure Hybrid Services funktionieren mit Windows-Servern in der folgenden Konfiguration:

- Eigenständige physischen Servern und virtuellen Computern (VMs)
- Cluster, einschließlich der hyperkonvergenten Cluster zertifiziert den [Azure Stack HCI](https://docs.microsoft.com/azure-stack/operator/azure-stack-hci-overview), und [Windows Server Software-Defined (WSSD)](https://www.microsoft.com/en-us/cloud-platform/software-defined-datacenter) Programme

Während Sie die meisten Azure hybriddienste, die mithilfe von Azure-Portal und ein Download oder zwei einrichten können, sind viele direkt in Windows Admin Center ein vereinfachtes Setup-Benutzeroberfläche und eine serverorientierten Ansicht der Dienste integriert.

## <a name="azure-hybrid-services-tool"></a>Azure Hybrid-Services-Konfigurationstool

Die hybriddienste Azure-tool in [Windows Admin Center](../understand/windows-admin-center.md) konsolidiert alle integrierten Azure-Dienste in einer zentralen Hub, in dem Sie alle verfügbaren Azure-Dienste, die Wert für Ihre lokalen bietet mühelos ermitteln können, oder Hybrid-Umgebung. 

![Screenshot der Windows Admin Center zeigt das Tool Azure Hybrid Services](../media/azure-services/ahs-discover.png)

Wenn Sie mit Azure-Diensten geschehen auf einem Server verbunden sind, dient das Azure Hybrid-Services-Konfigurationstool, als eine zentrale Konsole auf alle aktivierten Dienste auf dem Server finden Sie unter. Sie können problemlos lernen Sie die relevanten Tool in Windows Admin Center, starten Sie zum Azure-Portal für detailliertere Verwaltung von dieser Azure-Dienste, oder erfahren Sie mehr mit der Dokumentation zur Hand. 

![Screenshot der Windows Admin Center mit der Azure-Dienste, die bereits auf dem Server installiert sind](../media/azure-services/ahs-dayN.png)

Aus dem Azure Hybrid-Services-Tool können Sie folgende Aktionen ausführen:
- Sichern des Windows-Servers von Windows Admin Center mit [Azure-Sicherung](azure-backup.md)
- Schützen Sie Ihre Hyper-V-VMs aus Windows Admin Center mit [Azure Site Recovery](azure-site-recovery.md)
- Synchronisieren Sie Ihre Dateiserver mit der Cloud mit [Azure File Sync](azure-file-sync.md)
- Verwalten von Betriebssystem-Updates für alle Ihre Windows Server lokal oder in der Cloud mit [Updateverwaltung für Azure](azure-update-management.md)
- Überwachen von Servern, sowohl lokal oder in der Cloud, und Konfigurieren von Warnungen mit [Azure Monitor](azure-monitor.md)
- Verbinden Sie Ihre lokalen Server, auf einem virtuellen Azure-Netzwerk mit [Azure-Netzwerkadapter](https://aka.ms/WACNetworkAdapter)

## <a name="services-for-stand-alone-servers-and-vms"></a>Dienste für die eigenständigen Servern und VMs

Dies ist die vollständige Liste der Azure-Dienste, die Funktionen auf eigenständigen Servern und virtuellen Computern bereitstellen:

- **(Neu) Synchronisieren Sie den Dateiserver mit der Cloud mithilfe [Azure File Sync](https://aka.ms/afs)**  
Synchronisieren von Dateien auf diesem Server mit Azure-Dateifreigaben. Alle Dateien lokal beibehalten, oder Verwenden von cloud-tiering und Cache nur die am häufigsten verwendeten Dateien auf dem Server, die kalte Daten in die Cloud-tiering aus. Daten in der Cloud können gesichert werden und Sie müssen auf lokale Server-Sicherung kümmern. Darüber hinaus kann multi-site-Synchronisierung einen Satz von Dateien auf mehreren Servern synchronisieren.

- **Windows Admin Center eine Sicherheitsschicht hinzugefügt, durch Hinzufügen von [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/) Authentifizierung**  
Sie können Windows Admin Center eine zusätzliche Sicherheitsebene hinzufügen, indem Sie Benutzer für die Authentifizierung mit Azure Active Directory (Azure AD)-Identitäten auf dem Gateway. Azure AD-Authentifizierung können Sie die Azure AD Sicherheitsfunktionen wie bedingten Zugriff und Multi-Factor Authentication nutzen.  
Weitere Informationen finden Sie unter [Konfigurieren von Azure AD-Authentifizierung für Windows Admin Center.](../configure/user-access-control.md#azure-active-directory)  

- **Schützen Sie Ihre Hyper-V-VMs mit [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)**  
Sie können Workloads replizieren, die auf virtuellen Computern ausgeführt werden, sodass Ihre unternehmenskritischen Infrastruktur bei einem Notfall geschützt ist. Windows Admin Center optimiert Setup- und der Prozess der Replikation Ihrer virtuellen Computer am Hyper-V-Server oder Cluster, erleichtert Ihnen die resilienz Ihrer Umgebung mit Azure Site Recovery, Disaster Recovery-Dienst zu untermauern.  
Weitere Informationen finden Sie unter [Schützen von virtuellen Computern mit Azure Site Recovery und Windows Admin Center](azure-site-recovery.md).

- **Sichern Sie Ihre Windows-Server mit [Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview)**  
Sie können Ihre Windows-Server in Azure und zum Schutz vor versehentlichem oder böswilligem löschen, Ransomware und Beschädigungen sichern.  
Weitere Informationen finden Sie unter [sichern Sie Ihre Server mit Azure Backup](azure-backup.md).

- **Überwachen und erhalten Sie e-Mail-Benachrichtigungen für alle Server in Ihrer Umgebung mit [Azure Monitor für virtuelle Computer](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)**  
Können Sie Azure Monitor, auch bekannt als virtuelle Computer Einblicke, Serverzustand und Ereignisse überwachen, e-Mail-Warnungen erstellen, erhalten eine konsolidierte Ansicht der Leistung in Ihrer gesamten Umgebung und Visualisieren von Systemen, Anwendungen und von verbundenen Diensten zu einer bestimmten Server.  
Weitere Informationen finden Sie unter [verbinden Ihrer Server mit Azure Monitor, und Konfigurieren von e-Mail-Benachrichtigungen](azure-monitor.md).

- **Aktualisieren des Betriebssystems zentral zu verwalten, für alle Windows-Server mit [Azure-Updateverwaltung](https://docs.microsoft.com/azure/automation/automation-update-management)**  
Sie können Updates und Patches für mehrere Server und VMs an einem zentralen Ort, und nicht auf eine einzelne Server verwalten. Mit der Azure-Updateverwaltung können Sie schnell den Status verfügbarer Updates bewerten, Installation von erforderlichen Updates planen und Bereitstellungsergebnisse überprüfen um sicherzustellen, dass Updates, die erfolgreich angewendet. Dies ist möglich, ob Ihre Server auf virtuellen Azure-Computern, die von anderen cloudanbietern gehostet sind oder lokal.  
Weitere Informationen finden Sie unter [Konfigurieren von Servern für die Verwaltung von Azure](azure-update-management.md).

- **Verbinden Sie Ihre lokalen Server, auf einem virtuellen Azure-Netzwerk mit einem [Azure-Netzwerkadapter](https://aka.ms/WACNetworkAdapter)**  
Sie können ein Azure-Netzwerkadapter hinzufügen, mit Ihren lokalen Servern können Sie den Server mit einem Azure Virtual Network sicher zu verbinden.  
Weitere Informationen finden Sie unter [konfigurieren eine Punkt-zu-Standort-VPN-Verbindung zwischen einem lokalen Windows-Server und einem Azure Virtual Network](https://aka.ms/WACNetworkAdapter).

- **Verwalten von Azure-IaaS-VMs mit [Windows Admin Center](manage-azure-vms.md)**  
Sie können Windows Admin Center verwenden, zum Verwalten Ihrer virtuellen Azure-Computern sowie auf lokalen Computern. Konfigurieren Sie Ihr Windows Admin Center-Gateway eine Verbindung mit Ihrem Azure-VNet herstellen, können Sie virtuelle Computer in Azure mithilfe der konsistente, vereinfachte Tools Windows Admin Center verwalten. Weitere Informationen finden Sie unter [konfigurieren Windows Admin Center zum Verwalten von virtuellen Computern in Azure](manage-azure-vms.md).

## <a name="services-for-clusters"></a>Dienste für Cluster

Hierbei handelt es sich um die Azure-Dienste, die Funktionalität für Cluster als Ganzes bereitstellen (diese werden nicht alle integriert Windows Admin Center noch):

- [Überwachen eines hyperkonvergenten Clusters mit Azure Monitor](../../../storage/storage-spaces/configure-azure-monitor.md)
- [Schützen von virtuellen Computern mit Azure Site Recovery](azure-site-recovery.md)
- [Bereitstellen eines cloudzeugen für den cluster](../../../failover-clustering/deploy-cloud-witness.md)

## <a name="see-also"></a>Weitere Informationen

- [Verbinden von Windows Admin Center in Azure](azure-integration.md)
- [Bereitstellen von Windows Admin Center in Azure](deploy-wac-in-azure.md)