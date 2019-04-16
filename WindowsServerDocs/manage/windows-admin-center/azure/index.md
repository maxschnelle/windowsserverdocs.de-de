---
title: Verbinden von Windows Server mit Azure Hybrid-Diensten
description: Sie können lokale Bereitstellungen von Windows Server in der Cloud mithilfe von Azure Hybrid-Diensten erweitern.
ms.technology: manage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 04/12/2019
ms.openlocfilehash: 625bd4b79d277dfaa81767cd781c2ba1316d637e
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297025"
---
# Verbinden von Windows Server mit Azure Hybrid-Diensten

>Gilt für: WindowsServer 2019, WindowsServer 2016

Sie können lokale Bereitstellungen von Windows Server in der Cloud mithilfe von Azure Hybrid-Diensten erweitern. Diese Clouddienste bieten ein Array von Funktionen, einschließlich der folgenden:

- Schützen von virtuellen Computern und Cloud-basierte Backup und Notfall Recovery (hohe Verfügbarkeit/bietet) mit Azure Site Recovery. 
- Nachverfolgen Sie, was für Ihre Anwendungen, Netzwerk und Infrastruktur mit Hilfe der erweiterten Analysen und Machine learning-im Azure-Monitor passiert. 
- Netzwerkkonnektivität in Azure mit Azure-Netzwerkadapter zu vereinfachen.
- Halten Sie virtuelle Computer auf dem neuesten Stand mit Azure-Updateverwaltung.

Azure Hybrid Services zusammen mit Windows-Servern in den folgenden Konfigurationen:

- Eigenständige physischen Server und virtuellen Computern (VMs)
- Clustern, einschließlich von hyperkonvergenten Clustern zertifiziert vom [Azure Stack HCI](../../../azure-stack-hci/index.md)und [Windows_Server_Software-Defined (WSSD)](https://www.microsoft.com/en-us/cloud-platform/software-defined-datacenter) -Programme

Während Sie am Azure Hybrid-Dienste mithilfe des Azure-Portals und ein oder zwei einrichten können, sind viele direkt in Windows Admin Center, um eine vereinfachte Setup-Erfahrung und eine Server-orientierte Ansicht der Dienste bereitzustellen integriert.

## Azure Hybrid Services-Verwaltungstool

Das Azure Hybrid Services-Tool im [Windows Admin Center](../understand/windows-admin-center.md) konsolidiert alle integrierten Azure-Dienste in einen zentralen Hub, in denen Sie alle verfügbaren Azure Dienste, die den Wert Ihrer lokalen oder Hybriden erweitern leicht ermitteln können, Umgebung. 

![Screenshot der Windows Admin Center mit dem Azure Hybrid Services-tool](../media/azure-services/ahs-discover.png)

Wenn Sie mit einem Server mit Azure-Diensten bereits aktiviert verbinden, dient das Azure Hybrid Services-Tool als eine zentralen Konsole, um alle aktivierten Dienste auf diesem Server finden Sie unter. Sie einfach an das relevante Tool in Windows Admin Center erhalten, starten Azure-Portal für die tiefer Verwaltung von diesen Azure-Dienste oder Read Weitere Dokumentation zur Verfügung. 

![Screenshot von Windows Admin Center mit Azure-Dienste, die bereits auf dem Server installiert sind](../media/azure-services/ahs-dayN.png)

Im Tool Azure Hybrid-Dienste können Sie folgende Aktionen ausführen:
- Sichern Sie Ihre Windows-Server aus dem Windows Admin Center mit [Azure Backup](azure-backup.md)
- Schützen Sie Ihre virtuellen Hyper-V-Computer vor Windows Admin Center mit [Azure Site Recovery](azure-site-recovery.md)
- Synchronisieren Sie den Dateiserver mit der Cloud, die mit [Azure-Datei-Synchronisierung](azure-file-sync.md)
- Verwalten von Betriebssystemupdates für alle Ihre Windows-Server sowohl lokal oder in der Cloud, mit der [Azure-Updateverwaltung](azure-update-management.md)
- Überwachen von Servern, sowohl lokal oder in der Cloud und Konfigurieren von Warnungen mit [Azure-Monitor](azure-monitor.md)
- Schließen Sie die lokale Server auf einem virtuellen Azure-Netzwerk mit [Azure-Netzwerkadapter](https://aka.ms/WACNetworkAdapter)

## Dienste für eigenständigen Servern und VMs

Dies ist die vollständige Liste der Azure-Dienste, die Funktionalität zur eigenständigen Servern und VMs bereitstellen:

- **(Neu) Synchronisieren Sie den Dateiserver mit der Cloud mithilfe von [Azure-Datei-Synchronisierung](https://aka.ms/afs)**  
Synchronisieren von Dateien auf diesem Server mit Azure-Dateifreigaben. Alle Dateien lokale beibehalten, oder verwenden cloud tiering und Cache nur die am häufigsten verwendeten Dateien auf dem Server, tiering kalte Daten in der Cloud. Daten in der Cloud können gesichert werden, die lokale Server-Sicherung kümmern überflüssig. Darüber hinaus kann multi-Ort-Synchronisierung eine Reihe von Dateien über mehrere Server synchronisieren.

- **Fügen Sie eine Sicherheitsebene bei Windows Admin Center durch Hinzufügen von [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/) -Authentifizierung**  
Sie können eine zusätzliche Sicherheitsebene bei Windows Admin Center hinzufügen, indem Benutzer authentifizieren sich mit Azure Active Directory (Azure AD)-Identitäten auf das Gateway zugreifen. Azure AD-Authentifizierung können Sie die Azure AD-Sicherheitsfeatures wie bedingten Zugriff und Multi-Factor Authentication nutzen.  
Weitere Informationen finden Sie unter [Konfigurieren von Azure AD-Authentifizierung für Windows Admin Center.](../configure/user-access-control.md#azure-active-directory)  

- **Schützen Sie Ihr Hyper-V-VMs mit [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)**  
Sie können Arbeitslasten auf VMs, sodass Ihre wichtige Geschäftsinfrastruktur in Notfällen schützt ist replizieren. Windows Admin Center optimiert Setup und den Prozess der Replikation der virtuellen Computer auf Ihren Hyper-V-Servern oder Clustern, und vereinfacht so die Stabilität Ihrer Umgebung mit Azure Site Recovery Notfall Wiederherstellungsdienst erwerben.  
Weitere Informationen finden Sie in [Ihre virtuellen Computer mit Azure Site Recovery und Windows Admin Center schützen](azure-site-recovery.md).

- **Sichern Sie Ihre Windows-Server mit [Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview)**  
Sie können Ihren Windows-Servern in Azure, um Schutz vor unbeabsichtigte oder böswillige gelöschter, eine Beschädigung und Ransomware sichern.  
Weitere Informationen finden Sie unter [Sichern von Azure Backup-Servern](azure-backup.md).

- **Überwachen und Abrufen von e-Mail-Warnungen für alle Server in Ihrer Umgebung mit [Azure-Monitor für virtuelle Computer](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)**  
Können Sie Azure überwachen, auch bekannt als virtuelle Computer Einblicken, Überwachung von Serverstatus und Ereignisse, e-Mail-Warnungen zu erstellen, erhalten eine konsolidierte Sicht serverleistung in Ihrer Umgebung und Visualisieren Systeme,-apps und Dienste mit einer bestimmten Server.  
Weitere Informationen finden Sie unter [Verbinden Sie Ihre Server in Azure überwachen und Konfigurieren von e-Mail-Benachrichtigungen](azure-monitor.md).

- **Zentral verwalten Sie, Updates des Betriebssystems für alle Windows-Server mit [Azure-Updateverwaltung](https://docs.microsoft.com/azure/automation/automation-update-management)**  
Sie können Updates und Patches für mehrere Server und VMs aus einer einzigen Ort, anstatt auf pro Server verwalten. Mit Azure-Updateverwaltung können Sie schnell den Status der verfügbaren Updates zu bewerten, Planen der Updateinstallation erforderlich und überprüfen Bereitstellung Ergebnisse, um Updates zu überprüfen, die erfolgreich angewendet. Dies ist möglich, ob Ihre Server Azure-VMs, die von anderen Anbietern Cloud gehostet werden oder lokal.  
Weitere Informationen finden Sie unter [Konfigurieren von Servern für Azure-Updateverwaltung](azure-update-management.md).

- **Schließen Sie die lokale Server auf einem virtuellen Azure-Netzwerk mit einem [Azure-Netzwerkadapter](https://aka.ms/WACNetworkAdapter)**  
Sie können Ihre lokale Server, mit denen Sie den Server sicher mit einem virtuellen Azure-Netzwerk verbinden können ein Azure-Netzwerkadapter hinzufügen.  
Weitere Informationen finden Sie unter [Konfigurieren einer Punkt-zu-Standort-VPN-Verbindung zwischen einem lokalen Windows-Server und einem virtuellen Azure-Netzwerk](https://aka.ms/WACNetworkAdapter).

- **Verwalten von Azure IaaS virtuellen Computern mit [Windows Admin Center](manage-azure-vms.md)**  
Windows Admin Center können Sie um Ihre Azure-VMs sowie lokalen Computer zu verwalten. Konfigurieren das Windows Admin Center-Gateway mit einer Verbindung mit Ihrer Azure vnet angefügt wird, können Sie virtuelle Computer in Azure mithilfe der konsistente, vereinfachte Tools, die Windows Admin Center bietet verwalten. Weitere Informationen finden Sie unter [Konfigurieren von Windows Admin Center zum Verwalten von VMs in Azure](manage-azure-vms.md).

## Dienste für Cluster

Hierbei handelt es sich um die Azure-Dienste, die Funktionen zum Cluster als Ganzes bereitstellen (Dies sind nicht alle integriert in Windows Admin Center noch):

- [Überwachen von einem hyperkonvergenten Cluster mit Azure-Monitor](../../../storage/storage-spaces/configure-azure-monitor.md)
- [Schützen Sie Ihre virtuellen Computer mit Azure Site Recovery](azure-site-recovery.md)
- [Bereitstellen eines cloudzeugen cluster](../../../failover-clustering/deploy-cloud-witness.md)

## Weitere Informationen:

- [Verbinden von Windows Admin Center in Azure](azure-integration.md)
- [Bereitstellen von Windows Admin Center in Azure](deploy-wac-in-azure.md)