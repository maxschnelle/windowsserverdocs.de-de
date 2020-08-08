---
title: Schützen Sie Ihre Hyper-V-Virtual Machines mit Azure Site Recovery und Windows Admin Center
description: Verwenden Sie das Windows Admin Center (Project Honolulu) zum Schutz von Hyper-V-VMS mit Azure Site Recovery.
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
ms.localizationpriority: low
ms.openlocfilehash: 265589789f2966e7b6140543876f41058aa5d705
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940081"
---
# <a name="protect-your-hyper-v-virtual-machines-with-azure-site-recovery-and-windows-admin-center"></a>Schützen Sie Ihre Hyper-V-Virtual Machines mit Azure Site Recovery und Windows Admin Center

>Gilt für: Windows Admin Center-Vorschau, Windows Admin Center

[Erfahren Sie mehr über die Azure-Integration in Windows Admin Center.](../plan/azure-integration-options.md)

Windows Admin Center optimiert den Prozess der Replikation ihrer virtuellen Computer auf Ihren Hyper-V-Servern oder-Clustern, sodass Sie die Leistungsfähigkeit von Azure aus Ihrem eigenen Daten Center leichter nutzen können. Zum Automatisieren des Setups können Sie das Windows Admin Center-Gateway mit Azure verbinden.

Verwenden Sie die folgenden Informationen, um die Replikationseinstellungen zu konfigurieren und einen Wiederherstellungs Plan innerhalb des Azure-Portal zu erstellen, damit Windows Admin Center die VM-Replikation starten und ihre VMs schützen kann.

## <a name="what-is-azure-site-recovery-and-how-does-it-work-with-windows-admin-center"></a>Was ist Azure Site Recovery und wie funktioniert es mit dem Windows Admin Center?

**Azure Site Recovery** ist ein Azure-Dienst, der Workloads auf virtuellen Computern repliziert, damit Ihre unternehmenskritische Infrastruktur im Notfall geschützt wird.  [Erfahren Sie mehr über Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview).

Azure Site Recovery besteht aus zwei Komponenten: **Replikation** und **Failover**. Der Replikations Teil schützt Ihre VMS im Notfall, indem die VHD des virtuellen Ziel Computers in einem Azure-Speicherkonto repliziert wird. Sie können dann ein Failover für diese VMS ausführen und Sie im Falle eines Notfalls in Azure ausführen. Sie können auch ein Test Failover ausführen, ohne dass sich dies auf Ihre primären VMS auswirkt, um den Wiederherstellungsprozess in Azure zu testen.

Das Abschließen des Setups für die Replikations Komponente ist ausreichend, um Ihre VM im Notfall zu schützen. Sie können den virtuellen Computer jedoch erst in Azure starten, wenn Sie den failoverteil konfiguriert haben. Sie können den failoverbereich einrichten, wenn Sie ein Failover auf eine Azure-VM durchsetzen möchten. Dies ist im Rahmen der anfänglichen Installation nicht erforderlich. Wenn der Host Server ausfällt und Sie die failoverkomponente noch nicht konfiguriert haben, können Sie Sie zu diesem Zeitpunkt konfigurieren und auf die Arbeits Auslastungen der geschützten VM zugreifen. Es empfiehlt sich jedoch, die failoverbezogenen Einstellungen vor einem Notfall zu konfigurieren.


## <a name="prerequisites-and-planning"></a>Voraussetzungen und Planung

- Die Zielserver, auf denen die virtuellen Computer gehostet werden, die Sie schützen möchten, müssen über Internet Zugang verfügen, um die Replikation
- [Verbinden Sie Ihr Windows Admin Center-Gateway mit Azure](azure-integration.md).
- [Überprüfen Sie das Tool Capacity Planning, um die Anforderungen für eine erfolgreiche Replikation und ein Failover auszuwerten](https://docs.microsoft.com/azure/site-recovery/hyper-v-site-walkthrough-capacity).

## <a name="step-1-set-up-vm-protection-on-your-target-host"></a>Schritt 1: Einrichten des VM-Schutzes auf dem Zielhost

> [!NOTE]
> Sie müssen diesen Schritt einmal pro Host Server oder Cluster mit virtuellen Computern durchführen, die für den Schutz vorgesehen sind.

1. Navigieren Sie zu dem Server oder dem Cluster, der virtuelle Computer, die Sie schützen möchten (entweder mit Server-Manager oder dem hyperkonvergierten Cluster-Manager).
2. Wechseln Sie zu **Virtual Machines**  >  **Inventory**.
3. Wählen Sie einen beliebigen virtuellen Computer aus (Dies muss nicht der virtuelle Computer sein, den Sie schützen möchten).
4. Wählen Sie **Weitere**  >  **Einrichten von VM-Schutz**aus.
5. Melden Sie sich bei Ihrem Azure-Konto an.
6. Geben Sie die erforderlichen Informationen ein:

   - **Abonnement:** Das Azure-Abonnement, das Sie für die Replikation von VMS auf diesem Host verwenden möchten.
   - **Speicherort:** Die Azure-Region, in der die ASR-Ressourcen erstellt werden sollen.
   - **Speicherkonto:** Das Speicherkonto, in dem die replizierten VM-Arbeits Auslastungen auf diesem Host gespeichert werden.
   - Tresor **:** Wählen Sie einen Namen für den Azure Site Recovery Tresor für geschützte VMS auf diesem Host aus.

7. Wählen Sie **Setup ASR**aus.
8. Warten Sie, bis die folgende Benachrichtigung angezeigt wird: **Site Recovery-Einstellung wurde abgeschlossen**.

Diese kann bis zu 10 Minuten dauern. Sie können den Fortschritt verfolgen, indem Sie zu **Benachrichtigungen** (das Glocken Symbol oben rechts) wechseln.

>[!NOTE]
> Bei diesem Schritt wird der **ASR-Agent** automatisch auf dem Zielserver oder den Knoten installiert (bei der Konfiguration auf einem Cluster), und es wird eine **Ressourcengruppe** mit **dem angegebenen** **Speicherkonto** und Tresor erstellt. Dadurch wird auch der Zielhost für den ASR-Dienst registriert und eine Standard Replikations Richtlinie konfiguriert.

## <a name="step-2-select-virtual-machines-to-protect"></a>Schritt 2: Auswählen der zu schützenden virtuellen Computer

1. Navigieren Sie zurück zum Server oder Cluster, den Sie in Schritt 2 oben konfiguriert haben, und wechseln Sie zu **Virtual Machines > Inventory**.
2. Wählen Sie den virtuellen Computer aus, den Sie schützen möchten.
3. Wählen Sie **Weitere**  >  **Schutz-VM**aus.
4. Überprüfen Sie die [Kapazitätsanforderungen für den Schutz der VM](https://docs.microsoft.com/azure/site-recovery/site-recovery-capacity-planner).

    Wenn Sie ein Storage Premium-Konto verwenden möchten, erstellen Sie ein Storage Premium-Konto [in der Azure-Portal](https://docs.microsoft.com/azure/storage/common/storage-premium-storage). Die Option **neu erstellen** im Bereich Windows Admin Center erstellt ein Standard Speicherkonto.

5. Geben Sie den Namen des **Speicher Kontos** ein, das für die Replikation dieser VM verwendet werden soll, und wählen Sie **VM schützen**aus. Mit diesem Schritt wird die Replikation für den ausgewählten virtuellen Computer aktiviert.

6. ASR startet die Replikation. Die Replikation ist abgeschlossen, und der virtuelle Computer wird geschützt, wenn der Wert in der **geschützten** Spalte des Inventur Rasters der **virtuellen Maschine** in **Ja**geändert wird. Dies kann einige Minuten dauern.

## <a name="step-3-configure-and-run-a-test-failover-in-the-azure-portal"></a>Schritt 3: Konfigurieren und Ausführen eines Testfailovers im Azure-Portal

 Obwohl Sie diesen Schritt beim Starten der VM-Replikation nicht ausführen müssen (der virtuelle Computer wird bereits durch die Replikation geschützt), empfiehlt es sich, beim Einrichten von Azure Site Recovery Failovereinstellungen zu konfigurieren. Wenn Sie ein Failover auf eine Azure-VM vorbereiten möchten, führen Sie die folgenden Schritte aus:

1. [Richten Sie ein Azure-Netzwerk ein](https://docs.microsoft.com/azure/site-recovery/hyper-v-site-walkthrough-prepare-azure) , das durch einen virtuellen Computer mit Failover an dieses vnet angefügt wird. Beachten Sie, dass die anderen auf der verknüpften Seite aufgeführten Schritte automatisch vom Windows Admin Center abgeschlossen werden.  Sie müssen das Azure-Netzwerk nur einrichten.

2. [Führen Sie ein Test Failover](https://docs.microsoft.com/azure/site-recovery/hyper-v-site-walkthrough-test-failover)aus.

## <a name="step-4-create-recovery-plans"></a>Schritt 4: Erstellen von Wiederherstellungs Plänen

Der **Wiederherstellungs Plan** ist eine Funktion in Azure Site Recovery, mit der Sie ein Failover und eine vollständige Anwendung mit einer Sammlung von virtuellen Computern durch ein Failover durch Obwohl es möglich ist, geschützte VMS einzeln wiederherzustellen, indem Sie die virtuellen Computer, die eine Anwendung enthalten, einem Wiederherstellungs Plan hinzufügen, können Sie ein Failover für die gesamte Anwendung über den Wiederherstellungs Plan ausführen. Sie können auch das Feature Test Failover des Wiederherstellungs Plans verwenden, um die Wiederherstellung der Anwendung zu testen. Mit dem Wiederherstellungs Plan können Sie virtuelle Computer gruppieren, die Reihenfolge, in der Sie während eines Failovers hochgefahren werden sollten, sequenzieren und zusätzliche Schritte automatisieren, die im Rahmen des Wiederherstellungs Vorgangs ausgeführt werden sollen. Nachdem Sie Ihre virtuellen Computer geschützt haben, können Sie in der Azure-Portal zum Azure Site Recovery Tresor wechseln und Wiederherstellungs Pläne für diese VMS erstellen. [Erfahren Sie mehr über Wiederherstellungs Pläne](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans).

## <a name="monitoring-replicated-vms-in-azure"></a>Überwachen von replizierten VMs in Azure ##

Um sicherzustellen, dass bei der Server Registrierung keine Fehler auftreten, wechseln Sie zum **Azure-Portal**  >  **alle Ressourcen**  >  **Recovery Services** Tresor (der in Schritt 2 angegeben ist) > **Aufträge**  >  **Site Recovery Aufträge**.

Sie können die VM-Replikation überwachen **Recovery Services Vault**, indem Sie die  >  **replizierten Elemente**Recovery Services-Tresors

Wenn Sie alle Server anzeigen möchten, die beim Tresor registriert sind, wechseln Sie zu **Recovery Services**Tresor  >  **Site Recovery-Infrastruktur**  >  **Hyper-V-Hosts** (im Abschnitt "Hyper-v-Standorte").

## <a name="known-issue"></a>Bekanntes Problem ##

Wenn bei der Registrierung von ASR bei einem Cluster ein Knoten die ASR-Installation nicht durchführt oder beim ASR-Dienst registriert wird, sind die VMs möglicherweise nicht geschützt. Überprüfen Sie, ob alle Knoten im Cluster in der Azure-Portal registriert sind, indem **Recovery Services vault**Sie die Aufträge  >  **Jobs**  >  **Site Recovery Aufträge**des Recovery Services-Tresors aufrufen.