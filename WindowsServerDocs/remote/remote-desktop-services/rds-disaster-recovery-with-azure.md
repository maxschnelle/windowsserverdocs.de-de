---
title: Einrichten der notfallwiederherstellung für RDS mit Azure-Notfallwiederherstellung
description: Erfahren Sie, wie Sie mit Azure-Notfallwiederherstellung für die notfallwiederherstellung für eine RDS-Bereitstellung
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 06/12/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 561a515e23d12cc3397c40fd885550e735ed4d27
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878171"
---
# <a name="set-up-disaster-recovery-for-rds-using-azure-site-recovery"></a>Einrichten der notfallwiederherstellung für RDS mit Azure Site Recovery

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können Azure Site Recovery verwenden, um eine Lösung zur notfallwiederherstellung für die Remotedesktopdienste-Bereitstellung zu erstellen. 

[Azure Site Recovery](/azure/site-recovery/site-recovery-overview) ist ein Azure-basierten Dienst, der Disaster Recovery Funktionen bietet, durch Orchestrierung der Replikation, Failover und Wiederherstellung von virtuellen Computern. Azure Site Recovery unterstützt eine Reihe von Replikationstechnologien, um Sie konsistent zu replizieren, Schutz und nahtlos Failover für virtuelle Computer und Anwendungen in privaten/öffentlichen oder des Hosters-Clouds. 

Verwenden Sie die folgende Informationen zum Erstellen und überprüfen die Lösung für die notfallwiederherstellung.

## <a name="disaster-recovery-deployment-options"></a>Disaster Recovery-Bereitstellungsoptionen

Sie können RDS auf virtuelle Computer mit Hyper-V oder VMWare oder physischen Servern bereitstellen. Azure Site Recovery kann sowohl auf lokale und virtuelle Bereitstellungen entweder ein sekundärer Standort oder in Azure schützen. Die folgende Tabelle zeigt, dass die verschiedenen RDS-Bereitstellungen in Standort-zu-Standort und Standort-zu-Azure-notfallwiederherstellung Recvoery Szenarien unterstützt.

| Bereitstellungstyp                          | Hyper-V-Standort-zu-Standort | Hyper-V-Standort-zu-Azure | VMWare-Standort-zu-Azure | Physischer Standort-zu-Azure |
|------------------------------------------|----------------------|-----------------------|---------------------|----------------------|-----------------------|------------------------|
| In einem Pool zusammengefassten virtuellen Desktops, die (nicht verwaltet)       |Ja|Nein|Nein|Nein |
| Virtuelle Desktops eines Pools (verwaltet, ohne UPD) | Ja|Nein|Nein|Nein|
| RemoteApps und Desktop-Sitzungen (ohne UPD) | Ja|Ja|Ja|Ja  |

## <a name="prerequisites"></a>Vorraussetzungen

Bevor Sie Azure Site Recovery für die Bereitstellung konfigurieren können, stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:

- Erstellen Sie eine [lokalen RDS-Bereitstellung](rds-deploy-infrastructure.md).
- Hinzufügen [Azure Site Recovery Services-Tresor](/azure/site-recovery/site-recovery-vmm-to-azure#create-a-recovery-services-vault) mit Ihrem Microsoft Azure-Abonnement.
- Wenn Sie Azure als Wiederherstellungsstandort verwenden möchten, führen Sie die [Azure Virtual Machine Readiness Assessment-Tool](https://azure.microsoft.com/downloads/vm-readiness-assessment/) auf Ihren virtuellen Computern, um sicherzustellen, dass sie mit Azure-VMs und Azure Site Recovery Services kompatibel sind.
 
## <a name="implementation-checklist"></a>Checkliste für die Implementierung

Ich werde die verschiedenen Schritte zum Aktivieren von Azure Site Recovery Services für Ihre RDS-Bereitstellung im Detail, aber hier sind die Implementierungsschritte für die allgemeine.

| **Schritt 1: Konfigurieren von virtuellen Computern für die notfallwiederherstellung**                                                                                                                                                                                               |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Hyper-V - Download der Microsoft Azure Site Recovery-Anbieter. Installieren Sie es auf Ihrem VMM-Server oder Hyper-V-Host. Finden Sie unter [Voraussetzungen für die Replikation in Azure mithilfe von Azure Site Recovery](/azure/site-recovery/site-recovery-prereq) Informationen.                                                                                                                             |
| VMWare - Schutzserver, Konfigurationsserver und masterzielserver konfigurieren                                                                                                                                                      |
| **Schritt 2: Vorbereiten Ihrer Ressourcen**                                                                                                                                                                                                           |
| Hinzufügen einer [Azure Storage-Konto](/azure/storage/storage-create-storage-account).                                                                                                                                                                                                              |
| Hyper-V – Microsoft Azure Recovery Services-Agent herunterladen und installieren sie auf Hyper-V-Hostservern.                                                                                                                                     |
| VMWare - stellen Sie sicher, dass der Mobility Service auf allen virtuellen Computern installiert ist.                                                                                                                                                                           |
| [Aktivieren des Schutzes für virtuelle Computer in VMM-Cloud, Hyper-V-Websites oder VMWare-Standorten](rds-enable-dr-with-asr.md).                                                                                                                                                                    |
| **Schritt 3: Entwerfen von Ihren Wiederherstellungsplan.**                                                                                                                                                                                                        |
| Ordnen Sie Ihre Ressourcen - Zuordnung in lokalen Netzwerken und Azure-VNETs.                                                                                                                                                                              |
| [Erstellen des Wiederherstellungsplans](rds-disaster-recovery-plan.md). |
| Testen Sie den Wiederherstellungsplan, indem Sie ein Test-Failover erstellen. Stellen Sie sicher, dass alle virtuellen Computer die erforderliche Ressourcen wie Active Directory zugreifen können. Stellen Sie sicher, Netzwerk, die umleitungen konfiguriert sind und widmet RDS. Ausführliche Schritte zum Testen Ihres Plans finden Sie unter [Ausführen eines Testfailovers](/azure/site-recovery/site-recovery-test-failover-to-azure)|
| **Schritt 4: Ausführen ein notfallwiederherstellungsverfahrens.**                                                                                                                                                                                                     |
| Ausführen eines notfallwiederherstellungsverfahrens, die mithilfe von geplanten und ungeplanten Failover. Stellen Sie sicher, dass alle virtuellen Computer auf erforderliche Ressourcen, z. B. Active Directory zugreifen. Stellen Sie sicher, dass alle virtuellen Computer auf erforderliche Ressourcen, z. B. Active Directory zugreifen. Anleitung für Failover und führt einen Drilldown ausführen, finden Sie unter [-Failover in Site Recovery](/azure/site-recovery/site-recovery-failover).|


