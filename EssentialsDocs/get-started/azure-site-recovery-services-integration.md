---
title: Azure Site Recovery Services-Integration
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/01/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 262701a6-8a97-4c4e-bfbf-9f8007c308d6
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e9dabc1b986fd86b5ee3efc6022023b331046250
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433950"
---
# <a name="azure-site-recovery-services-integration"></a>Azure Site Recovery Services-Integration

>Gilt für: Windows Server 2016 Essentials

[Azure Site Recovery Services](https://docs.microsoft.com/azure/site-recovery/) einem sicherungstresor in Azure einen Dienst von Microsoft Azure Aktivieren der Replikation Ihrer virtuellen Computer (VM) in Echtzeit angeboten werden. Die den Server oder die Website aufgrund einer Hardware- oder andere Fehler nicht ausgeführt wird, Sie können in Azure Failover, in dem das VM-Image in den backup-Tresor gespeichert als eine ausgeführte VM in Azure bereitgestellt wird. In Kombination mit einem virtuellen Azure-Netzwerk im Falle eines Failovers in Azure werden-Client-PCs, die zuvor mit dem lokalen Server verbunden transparent an den Server in Azure ausgeführte verbunden.

Die Integration von Azure Site Recovery Services mit Windows Server Essentials startet in die gleiche Weise wie das Konfigurieren von [Azure Virtual Networking](azure-virtual-network-integration.md). Von der **Microsoft Cloud Services-Integration** auf der Seite Dashboard, klicken Sie auf **Integration in Azure Site Recovery Services** auf der rechten Seite des Dashboards:

![Dieser Screenshot zeigt die Registerkarte "Erste Schritte" auf der Homepage des Windows Server Essentials-Dashboards. Klicken Sie auf der Registerkarte "Erste Schritte" Dienstabschnitt ausgewählt wurde, und im Dashboard unter Microsoft Cloud Services-Integration angegeben ist, dass Azure Recovery derzeit deaktiviert ist.](media/azure-site-recovery-1.PNG)

Sie müssen wie bei Azure Virtual Network-Integration und Azure Backup-Integration, melden Sie sich bei Azure mit der Sie vorhandene Azure-Konto oder ein neues Konto erstellen:

![Dieser Screenshot zeigt die Anmeldung bei Microsoft Azure-Seite des Assistenten zum Aktivieren der Replikation in Azure. Die Schaltfläche "Anmelden" wird angezeigt, da der Benutzer in Microsoft Azure noch nicht angemeldet hat.](media/azure-site-recovery-2.PNG)

Nach der erfolgreichen Anmeldung in Azure, sehen Sie einen Bildschirm, der das Abonnement aufgefordert wird, ordnen Sie den Azure Site Recovery-Dienst als auch der Azure-Region, in dem Ihr virtueller Computer gespeichert und gehostet werden, sollen:

![Dieser Screenshot zeigt die Anmeldung bei Microsoft Azure-Seite des Assistenten zum Aktivieren der Replikation in Azure. Da der Benutzer in Microsoft Azure angemeldet hat, werden auf dieser Seite Optionen zur Auswahl von einem Abonnement, Speicherkonto und Region.](media/azure-site-recovery-3.PNG)

Nach dem Abonnement und die Auswahl der Region, erscheint eine neue Registerkarte der **Windows Server Essentials-Dashboard** namens **Azure Recovery**. Netzwerke Überprüfung erfolgt, um zu identifizieren und Auflisten von unterstützte Host-Servern (mit Windows Server Hyper-V 2012 R2 und höher) sowie die virtuellen Computer (Gäste) unter den einzelnen Hosts:

![Dieser Screenshot zeigt die Seite "Azure Recovery" des Windows Server Essentials-Dashboards. Zwei Hyper-V-Hosts werden zusammen mit die virtuellen Computer ausgeführt wird, auf diesen Hosts angezeigt. Ein virtueller Computer namens ramh157v01 auf dem Host, die RAM-H1-7 aktiviert ist und die Replikation in Azure ist für diesen virtuellen Computer derzeit deaktiviert.](media/azure-site-recovery-4.PNG)

### <a name="enabling-guest-virtual-machines-for-protection"></a>Gast-VMs für den Schutz aktivieren

Klicken Sie auf die Auswahl eines virtuellen Computers im Azure Recovery angezeigt, **Aktivieren der Replikation in Azure** auf der rechten Seite des Dashboards zum Vorbereiten und kopieren Sie die virtuelle Maschine™ s-Image in Azure:

![Dieser Screenshot zeigt das Dialogfeld "Aktivieren der Replikation zu Azure". Eine Statusanzeige wird angezeigt, wie ein Host hinzugefügt wird.](media/azure-site-recovery-5.PNG)

Während dieses Vorgangs ist der Azure Site Recovery-Dienst-Agent auf dem Host, einen sicherungstresor installiert, in dem das Image des Gastbetriebssystems, die zu virtuellen Computer speichernden wird erstellt und Replikation des Abbilds in Azure beginnt. Abhängig von der Größe des virtuellen Computers, die repliziert werden soll kann es sich bei Abschluss des Replikationsvorgangs Stunden oder Tage dauern. Bis der gesamte VM-Image und die neuesten Deltas zu Azure repliziert werden, Failover Aufgaben sind nicht verfügbar, und der virtuelle Computer ist nicht geschützt. Sobald die Replikation abgeschlossen ist, ändert die Protection-Status-Spalte im Fenster des Azure Recovery von **Replikation** zu **aktiviert**:

![Dieser Screenshot zeigt die Seite "Azure Recovery" des Windows Server Essentials-Dashboards. Zwei Hyper-V-Hosts werden zusammen mit die virtuellen Computer ausgeführt wird, auf diesen Hosts angezeigt. Ein virtueller Computer namens ramh12v02 auf dem Host, die RAM-H1-2 ausgewählt ist und die Replikation in Azure ist zurzeit für diesen virtuellen Computer aktiviert.](media/azure-site-recovery-6.PNG)

### <a name="failover-of-a-guest-vm-to-azure"></a>Failover von einem Gast-VM in Azure

![Screenshot der Failover-VM zur Azure-Seite.](media/azure-site-recovery-7.PNG)

Wenn ein virtueller Computer, die geschützte ein Fehler auftritt oder der Hostserver, die die geschützten virtuellen Computer ausgeführt wird, tritt ein Fehler auf, ein Failover auf Azure ausgeführt werden können, um die Aufrechterhaltung der Geschäftskontinuität bis ist die lokalen virtuelle Computer oder Hosts Server repariert und verfügbar. Wie die Abbildung oben zeigt gibt es drei Arten des Failovers, die mit Azure Site Recovery Services unterstützt werden:

-   **Test-Failover** ƒA guten Notfallwiederherstellungsplan umfasst die Möglichkeit zum Simulieren eines Notfalls, um eine minimale Ausfallzeit bei einem echten Notfall sicherzustellen. Eine Test-Failover wird die VM-Images, die in Ihrem Recovery-Tresor repliziert wurde, wird als einen ausgeführten virtuellen Computer in Azure bereitgestellt und ermöglicht es Ihnen, eine Verbindung mit dem Server, um Szenarios zu testen, die für das Unternehmen gelten. Während eines Testfailovers wird dem lokalen virtuellen Computer weiterhin mit keine Unterbrechungen, die nicht während des Disaster-Recovery-Tests führen ausgeführt. Nachdem der Test-Failover abgeschlossen ist, müssen Sie den Test über das Azure-Portal beenden hebt die Bereitstellung von den virtuellen Computer und löscht die virtuelle Festplatte. Die VM-Images in Ihrem Recovery-Tresor weiterhin während des gesamten Test-Failovers auf dem lokalen virtuellen Computer repliziert werden, als ob nichts je geschehen.

-   **Ungeplantes Failover** ƒAn ungeplantes Failover tritt auf, wenn es ein tatsächlichen Fehler mit dem geschützten Host-Server oder den virtuellen Computer, auf dem Hostserver ausgeführt wird. Das Failover manuell ausgelöst wird, entweder Windows Server Essentials-Dashboard, oder wenn der ausgefallenen Server selbst der Server ist, die, den Windows Server Essentials ausgeführt wird, kann ausgelöst werden, aus dem Azure-Portal direkt. In diesem Fall nimmt das ungeplante Failover der VM-Images, die in Ihrem Recovery-Tresor repliziert wurde, wird als einen ausgeführten virtuellen Computer in Azure bereitgestellt und ermöglicht es Ihnen, eine Verbindung mit dem Server, um Szenarios zu testen, die für das Unternehmen gelten. Wenn Ihr Server lokal wiederhergestellt wird, kann ein manuelles Failback über das Azure-Portal ausgelöst werden, die Sie dann das VM-Image wieder auf dem lokalen Server kopiert.

-   **Geplantes Failover** ƒA Geplantes Failover ist eine Aktion, die ausgeführt werden kann, wenn die geplante Aktivitäten, z. B. Wartung von Hardware, die durchgeführt werden müssen, der den Server, nach unten dauern würde. Bei einem geplanten Failover erfolgt der gleiche Prozess im Hinblick auf die Bereitstellung von Ihrem replizierten VM-Image in Azure. Allerdings wird vor dem auf diese Weise der lokale Server heruntergefahren in strukturierter Weise sicherstellen, dass alle Änderungen vor dem Herunterfahren in Azure repliziert werden. Sobald die geplante Wartung abgeschlossen ist, können Sie ein Failback aus dem Windows Server Essentials-Dashboard oder im Azure-Portal die würde bringen von dem lokalen Server und klicken Sie dann den virtuellen Computer in Azure "und" Delete Aufheben der Bereitstellung manuell Auslösen der. VHD-Datei. Replikation auf dem lokalen virtuellen Computer in Azure würde dann weiter wieder normal ausgeführt.

In keinem der oben genannten drei Fälle wird bei ein virtuellen Computer in Azure, das Windows Server Essentials-Dashboard Failover ausgeführt wird den neuen virtuelle Computer in Azure ausgeführt wird, wie in der folgenden Abbildung angezeigt.

![Dieser Screenshot zeigt die Seite "Azure Recovery" des Windows Server Essentials-Dashboards. Replikation in Azure wurde für einen Host mit dem Namen Essentials und eines virtuellen Computers benannte Essentials-Test-Ausführung in Azure gibt an, dass der Host ein Failover nach Azure durchgeführt wurde aktiviert.](media/azure-site-recovery-8.PNG)

<a name="see-also"></a>Siehe auch
--------
[Erste Schritte in Windows Server Essentials](get-started.md)
