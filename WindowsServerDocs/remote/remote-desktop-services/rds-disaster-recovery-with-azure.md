---
title: Einrichten von Notfallwiederherstellung für RDS mithilfe von Azure Disaster Recovery
description: Erfahren Sie, wie Sie Azure Disaster Recovery zur Notfallwiederherstellung für eine RDS-Bereitstellung verwenden
ms.author: elizapo
ms.date: 06/12/2017
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 6c0e9b97a436f51babf679d6ce0aa67c09bcfe26
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936905"
---
# <a name="set-up-disaster-recovery-for-rds-using-azure-site-recovery"></a>Einrichten von Notfallwiederherstellung für RDS mithilfe von Azure Site Recovery

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Sie können Azure Site Recovery verwenden, um eine Lösung zur Notfallwiederherstellung für Ihre Remotedesktopdienste-Bereitstellung zu erstellen.

[Azure Site Recovery](/azure/site-recovery/site-recovery-overview) ist ein Azure-basierter Dienst, der Funktionen zur Notfallwiederherstellung bietet, indem er Replikation, Failover und Wiederherstellung von virtuellen Computern orchestriert. Azure Site Recovery unterstützt eine Reihe von Replikationstechnologien, um konsistente Replikation, Schutz und nahtloses Failover von virtuellen Computern und Anwendungen in private/öffentliche oder von Hostanbietern betriebene Clouds zu ermöglichen.

Verwenden Sie die folgenden Informationen zum Erstellen und Überprüfen der Lösung zur Notfallwiederherstellung.

## <a name="disaster-recovery-deployment-options"></a>Bereitstellungsoptionen für Notfallwiederherstellung

Sie können RDS wahlweise auf physischen Servern oder auf virtuellen Computern bereitstellen, die Hyper-V oder VMWare ausführen. Azure Site Recovery kann sowohl lokale als auch virtuelle Bereitstellungen mit entweder einem zweiten Standort oder auf Azure schützen. Die folgende Tabelle zeigt die verschiedenen unterstützten RDS-Bereitstellungen in Szenarien für die Notfallwiederherstellung von Standort zu Standort oder von Standort zu Azure.

| Bereitstellungstyp                          | Hyper-V-Standort-zu-Standort | Hyper-V-Standort-zu-Azure | VMWare-Standort-zu-Azure | Physischer Standort-zu-Azure |
|------------------------------------------|----------------------|-----------------------|---------------------|----------------------|-----------------------|------------------------|
| Gepoolter virtueller Desktop (nicht verwaltet)       |Ja|Nein|Nein|Nein |
| Gepoolter virtueller Desktop (verwaltet, ohne UPD) | Ja|Nein|Nein|Nein|
| RemoteApps und Desktopsitzungen (ohne UPD) | Ja|Ja|Ja|Ja  |

## <a name="prerequisites"></a>Voraussetzungen

Bevor Sie Azure Site Recovery für Ihre Bereitstellung konfigurieren können, achten Sie darauf, dass die folgenden Anforderungen erfüllt sind:

- Erstellen Sie eine [lokale RDS-Bereitstellung](rds-deploy-infrastructure.md).
- Fügen Sie Ihrem Microsoft Azure-Abonnement den [Azure Site Recovery Services-Tresor](/azure/site-recovery/site-recovery-vmm-to-azure#create-a-recovery-services-vault) hinzu.
- Wenn Sie Azure als Ihren Wiederherstellungsstandort verwenden, führen Sie das [Azure Virtual Machine Readiness Assessment-Tool](https://azure.microsoft.com/downloads/vm-readiness-assessment/) auf Ihren VMs aus, um sicherzustellen, dass sie mit Azure-VMs und Azure Site Recovery-Diensten kompatibel sind.

## <a name="implementation-checklist"></a>Checkliste für die Implementierung

Wir behandeln die verschiedenen Schritte zum Aktivieren der Azure Site Recovery-Dienste für Ihre RDS-Bereitstellung noch ausführlicher, dies sind zunächst mal die allgemeinen Implementierungsschritte.

| **Schritt 1: Konfigurieren von virtuellen Computern für die Notfallwiederherstellung**                                                                                                                                                                                               |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Hyper-V: Laden Sie den Microsoft Azure Site Recovery-Anbieter herunter. Installieren Sie ihn auf Ihrem VMM-Server oder Hyper-V-Host. Weitere Informationen finden Sie unter [Prerequisites for replication to Azure by using Azure Site Recovery](/azure/site-recovery/site-recovery-prereq) (Voraussetzungen für die Replikation in Azure mithilfe von Azure Site Recovery).                                                                                                                             |
| VMWare: Konfigurieren Sie den Schutzserver, den Konfigurationsserver und die Masterzielserver                                                                                                                                                      |
| **Schritt 2: Vorbereiten Ihrer Ressourcen**                                                                                                                                                                                                           |
| Fügen Sie ein [Azure Storage-Konto](/azure/storage/storage-create-storage-account) hinzu.                                                                                                                                                                                                              |
| Hyper-V: Laden Sie den Microsoft Azure Recovery Services-Agent herunter, und installieren Sie ihn auf den Hyper-V-Hostservern.                                                                                                                                     |
| VMWare: Stellen Sie sicher, dass der Mobilitätsdienst auf allen VMs installiert ist.                                                                                                                                                                           |
| [Aktivieren Sie Schutz für VMs in der VMM-Cloud, auf Hyper-V-Sites oder auf VMWare-Sites](rds-enable-dr-with-asr.md).                                                                                                                                                                    |
| **Schritt 3: Entwerfen Ihres Wiederherstellungsplans.**                                                                                                                                                                                                        |
| Zuordnen Ihrer Ressourcen: Ordnen Sie lokale Netzwerke Azure VNETs zu.                                                                                                                                                                              |
| [Erstellen Sie den Wiederherstellungsplan](rds-disaster-recovery-plan.md). |
| Testen Sie den Wiederherstellungsplan, indem Sie ein Testfailover erstellen. Stellen Sie sicher, dass alle VMs auf die erforderlichen Ressourcen wie Active Directory zugreifen können. Achten Sie darauf, dass Netzwerkumleitungen für RDS konfiguriert sind und funktionieren. Detaillierte Schritte zum Testen Ihres Wiederherstellungsplans finden Sie unter [Ausführen eines Testfailovers](/azure/site-recovery/site-recovery-test-failover-to-azure)|
| **Schritt 4: Ausführen einer Notfallwiederherstellungsübung.**                                                                                                                                                                                                     |
| Führen Sie eine Notfallwiederherstellungsübung durch, und verwenden Sie dazu geplante und ungeplante Failover. Achten Sie darauf, dass alle VMs Zugriff auf die erforderlichen Ressourcen wie Active Directory haben. Achten Sie darauf, dass alle VMs Zugriff auf die erforderlichen Ressourcen wie Active Directory haben. Detaillierte Schritte zu Failovern und dem Durchführen von Übungen finden Sie unter [Failover in Site Recovery](/azure/site-recovery/site-recovery-failover).|


