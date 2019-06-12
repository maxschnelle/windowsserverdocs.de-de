---
title: Schützen Sie Ihre Hyper-V-VMs mit Azure Site Recovery und Windows Admin Center
description: Verwenden Sie das Windows Admin Center (Projekt Honolulu), um Ihre virtuellen Hyper-V-Computer mit Azure Site Recovery schützen.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
ms.localizationpriority: low
ms.prod: windows-server-threshold
ms.openlocfilehash: 66e9b2e23a60d1e4725321e88fc1ac262b9c31fa
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445923"
---
# <a name="protect-your-hyper-v-virtual-machines-with-azure-site-recovery-and-windows-admin-center"></a>Schützen Sie Ihre Hyper-V-VMs mit Azure Site Recovery und Windows Admin Center

>Gilt für: Windows Admin Center Preview, Windows Admin Center

[Weitere Informationen zu Azure-Integration in Windows Admin Center.](../plan/azure-integration-options.md)

Das Windows Admin Center optimiert den Prozess der Replikation der virtuellen Computer auf Ihren Hyper-V-Servern oder Clustern, und vereinfacht so die Nutzung der Leistung von Azure von Ihrem eigenen Datencenter aus. Um den Setup zu automatisieren, können Sie das Windows Admin Center-Gateway verbinden

Verwenden Sie folgende Informationen zur Konfiguration der Replikationseinstellungen und der Erstellung eines Wiederherstellungsplans innerhalb des Azure-Portals, damit Windows Admin Center die VM-Replikation beginnen und so Ihre VMs schützen kann.

## <a name="what-is-azure-site-recovery-and-how-does-it-work-with-windows-admin-center"></a>Was ist Azure Site Recovery und wie funktioniert es mit Windows Admin Center? 

**Azure Site Recovery** ist ein Azure-Dienst, der Arbeitslasten auf VMs repliziert und so Ihre wichtige Geschäftsinfrastruktur in Notfällen schützt.  [Weitere Informationen zu Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)

Azure Site Recovery besteht aus zwei Komponenten: **Replikation** und **Failover**. Die Replikation schützt Ihre VMs in Notfällen, indem sie den VHD der Ziel-VM auf einem Azure-Speicherkonto repliziert. Sie können diese VMs in Notfällen auf Azure als Failover ausführen. Sie können ebenfalls einen Test-Failover durchführen, ohne die primären VMs zu beeinflussen, um den Wiederherstellungsprozess in Azure zu testen.

Das Durchführen des Setup für die Replikationskomponente reicht aus, um den VM im Notfall zu schützen. Sie können die VM allerdings nicht in Azure starten, bis die Failover-Komponente konfiguriert wurde. Sie können den Failover einrichten, wenn ein Failover auf einer Azure VM durchgeführt werden soll – dies ist nicht als Teil des Setups erforderlich. Wenn der Hostserver ausfällt, und Sie die Failoverkomponente noch nicht konfiguriert haben, können Sie sie zu diesem Zeitpunkt konfigurieren und auf die Arbeitslasten der geschützte VM zugreifen. Es ist jedoch besser, Failover-Einstellungen vor einem Notfall zu konfigurieren.
 

## <a name="prerequisites-and-planning"></a>Erforderliche Komponenten und Planung

- Die Zielserver der zu schützenden VMs benötigen Internetzugriff, um auf Azure repliziert zu werden.
- [Verbinden Sie das Windows Admin Center-Gateway mit Azure](azure-integration.md).
- [Überprüfen Sie das Kapazitätsplanungstool für die Anforderungen, um eine erfolgreiche Replikation und Failover durchzuführen](https://docs.microsoft.com/azure/site-recovery/hyper-v-site-walkthrough-capacity).

## <a name="step-1-set-up-vm-protection-on-your-target-host"></a>Schritt 1: Richten Sie einen virtuellen Computer auf dem Zielhost

> [!NOTE] 
> Sie müssen diesen Schritt einmal pro Hostserver oder Cluster ausführen, die VMs für den Schutz enthalten.

1. Navigieren Sie zum Server oder Cluster, der die virtuellen Computer hostet (entweder mit dem Server-Manager oder Hyper-Converged Cluster-Manager), die geschützt werden sollen.
2. Wechseln Sie zu **virtuelle Computer** > **Inventur**.
3. Wählen Sie eine beliebige VM (diese nicht auf dem virtuellen Computer werden zu schützenden erforderlich).
4. Wählen Sie **Weitere** > **VM Schutz einrichten** aus.
5. Melden Sie sich bei Ihrem Azure-Konto an.
6. Geben Sie die erforderlichen Informationen ein:

   - **Abonnement:** Das Azure-Abonnement, die, das Sie für die Replikation von virtuellen Maschinen auf diesem Host verwenden möchten.
   - **Pfad:** Der Azure-Region, in denen die ASR-Ressourcen erstellt werden soll.
   - **Speicherkonto:** Das Speicherkonto, in dem replizierten VM-Workloads auf diesem Host gespeichert werden.
   - **Tresor:** Wählen Sie einen Namen für den Azure Site Recovery-Tresor, für die geschützten virtuellen Maschinen auf diesem Host.

7. Wählen Sie **ASR einrichten** aus.
8. Warten Sie, bis die Benachrichtigung angezeigt wird: **Site Recovery festlegen "abgeschlossen"** .
 
Dies kann bis zu 10 Minuten dauern. Sie können den Fortschritt überwachen, indem Sie auf **Benachrichtigungen** klicken (das Glockensymbol oben rechts).

>[!NOTE]
> Dieser Schritt installiert automatisch den ASR-Agent auf den Zielserver oder Knoten (bei einer Cluster-Konfiguration), erstellt eine **Ressourcengruppe** mit dem **Speicherkonto** und **Tresor** in dem angegebenen **Speicherort**. Dies registriert auch den Zielhost mit dem ASR-Dienst und konfiguriert eine Standardrichtlinie für die Replikation.

## <a name="step-2-select-virtual-machines-to-protect"></a>Schritt 2: Wählen Sie virtuelle Computer schützen

1. Navigieren Sie zum Server oder Cluster, den Sie in Schritt 2 oben konfiguriert haben, und wechseln Sie zu **virtuelle Computer > Inventur**.
2. Wählen Sie die VM, die Sie schützen möchten.
3. Wählen Sie **Weiter** > **VM schützen**.
4. Überprüfen Sie die [Kapazitätsanforderungen, um den virtuellen Computer zu schützen](https://docs.microsoft.com/azure/site-recovery/site-recovery-capacity-planner).

    Wenn Sie ein Premium Speicherkonto verwenden möchten, [erstellen Sie eins im Azure-Portal](https://docs.microsoft.com/azure/storage/common/storage-premium-storage), das Sie verwenden möchten. Die Option **Neu erstellen** in der Windows Admin Center erstellt ein Standardspeicher-Konto.

5. Geben Sie den Namen des **Speicherkontos** an, das für die Replikation dieser VM verwendet werden soll und wählen Sie **VM schützen** aus. Dieser Schritt ermöglicht die Replikation für den ausgewählten virtuellen Computer. 

6. ASR startet die Replikation. Replikation abgeschlossen ist und die VM geschützt ist, wenn der Wert in der Spalte **geschützt** des Rasters **Virtual Machine Inventar** auf **Ja**ändert. Dieser Vorgang kann einige Minuten dauern.  

## <a name="step-3-configure-and-run-a-test-failover-in-the-azure-portal"></a>Schritt 3: Konfigurieren und Ausführen eines Testfailovers in Azure-portal

 Obwohl Sie diesen Schritt nicht beim Starten der VM-Replikation durchführen müssen (die VM ist bereits durch die Replikation geschützt), wird empfohlen, dass Sie beim Einrichten der Azure Site Recovery die Failovereinstellungen konfigurieren. Wenn Sie ein Failover auf einer Azure VM vorbereiten möchten, führen Sie die folgenden Schritte aus:

1. [Einrichten des Azure-Netzwerks](https://docs.microsoft.com/azure/site-recovery/hyper-v-site-walkthrough-prepare-azure), damit die Failover-VM an diesem VNET angefügt wird. Die anderen Schritte in der verknüpften Seite werden automatisch von Windows Admin Center abgeschlossen. Sie müssen nur das Azure-Netzwerk einrichten.

2. [Ausführen ein Failover-Tests](https://docs.microsoft.com/azure/site-recovery/hyper-v-site-walkthrough-test-failover).

## <a name="step-4-create-recovery-plans"></a>Schritt 4: Erstellen von Wiederherstellungsplänen

**Wiederherstellungsplan** ist eine Feature von Azure Site Recovery für das Failover und Wiederherstellen einer gesamte Anwendung, die eine Liste der VMs enthält. Es ist zwar möglich, geschützte VMs einzeln wiederherzustellen, indem Sie die virtuellen Computer und die Anwendung dem Wiederherstellungsplan hinzufügen, Sie können allerdings dem Failover die gesamte Anwendung über den Wiederherstellungsplan hinzufügen. Sie können auch die Failover-Testfunktion des Wiederherstellungsplans verwenden, um die Wiederherstellung der Anwendung zu testen. Mit dem Plan für die Wiederherstellung können Sie VMs gruppieren, die Sequenz der Reihenfolge festlegen, in der sie bei einem Failover geschaltet werden sollen und automatisieren, welche zusätzlichen Schritte im Rahmen der Wiederherstellung ausgeführt werden sollen. Nachdem Sie Ihre virtuellen Computer geschützt haben, können Sie zum Azure Site Recovery-Tresor im Azure-Portal wechseln und Recovery-Pläne für diese VMs erstellen. [Erfahren Sie mehr über Wiederherstellungspläne](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans).

## <a name="monitoring-replicated-vms-in-azure"></a>Überwachen der replizierten VMs in Azure ##

Wechseln Sie zum Bestätigen, dass keine Fehler in der Server-Registrierung auftreten auf das **Azure-Portal** > **Alle Ressourcen** > **Recovery Services Vault** (demjenigen, der in Schritt 2 angegeben ist) > **Aufträge** > **Site Recovery Jobs**.

Sie können VM-Replikation überwachen, durch das Aufrufen der **Wiederherstellung Services Vault** > **Elemente repliziert**.

Um herauszufinden, ob alle Server im Archiv registriert sind, wechseln Sie zu **Recovery Services Vault** > **Site Recovery Infrastructure** > **Hyper-V-Hosts** (im Abschnitt Websites Hyper-V).

## <a name="known-issue"></a>Bekanntes Problem ##

Wenn Sie ASR mit einem Cluster registrieren und wenn ein Knoten nicht ASR installiert oder den ASR-Dienst registriert, werden Ihre virtuellen Computer nicht geschützt. Stellen Sie sicher, dass alle Knoten im Cluster im Azure-Portal registriert sind, indem Sie auf **Recovery Services Vault** > **Aufträge** > **Site Recovery Jobs** wechseln.