---
title: Integration mit Azure Site Recovery Services
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.openlocfilehash: 85e681cfc19241941773dd94f05ba59759aaf62a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
#<a name="azure-site-recovery-services-integration"></a>Integration mit Azure Site Recovery Services

>Gilt für: Windows Server2016 Essentials

[Azure Site Recovery Services](https://azure.microsoft.com/en-us/documentation/services/site-recovery/) ist ein Dienst angeboten von Microsoft Azure Aktivieren der Replikation der virtuellen Maschinen (VM) in Echtzeit auf einen sicherungstresor in Azure. Die Server- oder Standort aufgrund einer Hardware- oder einer anderen ausgefallen ist, Sie können mit Azure Failover, in denen die VM-Image in den sicherungstresor gespeichert als einen ausgeführten virtuellen Computer in Azure bereitgestellt wird. Kombiniert mit einem Azure virtuellen Netzwerk, im Falle eines Failovers in Azure, werden Client-PCs, die zuvor mit dem lokalen Server verbunden transparent auf den Server in Azure mit verbunden.

Integrieren von Azure Site Recovery Services in Windows Server Essentials startet auf die gleiche Weise wie das Konfigurieren [Azure virtuelle Netzwerke](azure-virtual-network-integration.md). Von der **Microsoft Cloud Services-Integration** im Dashboard auf, **Integration mit Azure Site Recovery Services** rechts neben dem Dashboard:

![Ein Bildschirmfoto die Registerkarte "Erste Schritte" auf der Startseite des Windows Server Essentials-Dashboards angezeigt. Auf der Registerkarte "Erste Schritte" im Abschnitt Dienste ausgewählt wurde, und das Dashboard gibt unter Microsoft Cloud Services-Integration, dass Azure Recovery derzeit deaktiviert ist.](media/azure-site-recovery-1.PNG)

Sie müssen wie bei der Integration von Azure virtuellen Netzwerk und Azure Backup-Integration, melden Sie sich Azure mit Sie vorhandenen Azure-Konto oder ein neues Konto erstellen:

![Screenshot mit der Anmeldung In zu Microsoft Azure-Seite des Assistenten für Replikation auf Azure zu aktivieren. Die Schaltfläche "Anmelden" wird angezeigt, da der Benutzer noch nicht in Microsoft Azure angemeldet hat.](media/azure-site-recovery-2.PNG)

Nach der erfolgreichen Anmeldung in Azure, sehen Sie einen Bildschirm mit der welches Abonnement wird zuordnen, den Azure Site Recovery-Dienst als auch die Azure-Region, in dem die virtuelle Maschine gespeichert und gehostet werden, sollen:

![Screenshot mit der Anmeldung In zu Microsoft Azure-Seite des Assistenten für Replikation auf Azure zu aktivieren. Da der Benutzer in Microsoft Azure angemeldet hat, werden auf dieser Seite Optionen zum Auswählen von einem Abonnement Speicherkonto und Region.](media/azure-site-recovery-3.PNG)

Nach dem Abonnement und die Auswahl der Region, erscheint eine neue Registerkarte der **Windows Server Essentials-Dashboard** aufgerufen **Azure Recovery**. Netzwerk-Überprüfung wird durchgeführt, um zu identifizieren und Aufzählen von unterstützten Hostserver (unter Windows Server Hyper-V 2012 R2 und höher) sowie die virtuellen Computer (Gäste) unter den einzelnen Hosts:

![Screenshot mit der Seite "Azure Recovery" des Windows Server Essentials-Dashboards. Zwei Hyper-V-Hosts werden zusammen mit den auf diesen Hosts ausgeführten virtuellen Computern angezeigt. Eine virtuelle Maschine mit dem Namen ramh157v01 auf Host-RAM-H1-7 ausgewählt wird, und die Replikation Azure ist momentan für diesen virtuellen Computer deaktiviert.](media/azure-site-recovery-4.PNG)

### <a name="enabling-guest-virtual-machines-for-protection"></a>Aktivieren von virtuellen Gastcomputern für den Schutz

Bei Auswahl eines virtuellen Computers im Azure-Wiederherstellung angezeigt wird, klicken Sie auf **Aktivieren der Replikation mit Azure** auf der rechten Seite des Dashboards zum Vorbereiten und kopieren Sie die virtuelle Maschine™ s Bild in Azure:

![Ein Bildschirmfoto, Anzeigen des Dialogfelds für die Replikation auf Azure zu aktivieren. Eine Statusleiste wird angezeigt, wenn ein Host hinzugefügt wird.](media/azure-site-recovery-5.PNG)

Während dieses Vorgangs ist der Azure Site Recovery-Dienst-Agent installiert auf dem Hostserver, einen sicherungstresor, in dem das Bild des Gastbetriebssystems VM gespeichert werden soll, wird erstellt, und Beginn der Replikation des Bilds in Azure. Abhängig von der Größe des virtuellen Computers, die repliziert werden soll kann es sich bei Abschluss der Replikation Stunden oder Tage dauern. Bis die gesamte VM-Image und die neuesten Deltas in Azure repliziert werden, Failover-Aufgaben sind nicht verfügbar, und der virtuelle Computer nicht geschützt ist. Sobald die Replikation abgeschlossen ist, ändert sich die Schutzstatus Spalte in das Fenster des Azure Recovery von **replizieren** auf **aktiviert**:

![Screenshot mit der Seite "Azure Recovery" des Windows Server Essentials-Dashboards. Zwei Hyper-V-Hosts werden zusammen mit den auf diesen Hosts ausgeführten virtuellen Computern angezeigt. Eine virtuelle Maschine mit dem Namen ramh12v02 auf Host-RAM-H1-2 ausgewählt wird, und die Replikation Azure ist momentan für diesen virtuellen Computer aktiviert.](media/azure-site-recovery-6.PNG)

### <a name="failover-of-a-guest-vm-to-azure"></a>Failover von einem Gast-VM mit Azure

![Screenshot mit VM-Failover zu Azure-Seite.](media/azure-site-recovery-7.PNG)

Wenn eine virtuelle Maschine, die geschützte ein Fehler auftritt, oder der Hostserver, die die geschützten virtuellen Computer ausgeführt wird, auf ein Fehler auftritt, einen Failover zu Azure ausgeführt werden können, um Geschäftskontinuität bis zu verwalten ist die auf lokalen virtuelle Maschine oder einen Host Server repariert und verfügbar. Wie in der Abbildung oben wird gezeigt gibt es drei Arten von Failover, die mit Azure Site Recovery Services unterstützt werden:

-   **Testfailover** ƒA guter Wiederherstellungsplan umfasst die Möglichkeit, einen Notfall, um sicherzustellen, dass Ausfälle bei einem echten Notfall zu simulieren. Ein Test-Failover wird der VM-Image, das auf Ihre Recovery-Tresor repliziert wurden, stellt es als einen ausgeführten virtuellen Computer in Azure und Herstellen einer Verbindung mit dem Server, um Szenarien zu testen, die für das Unternehmen gelten. Während eines Testfailovers weiterhin den lokalen virtuellen Computer ruckelfrei und nicht während der Tests der Disaster Recovery führen ausgeführt wird. Sobald das Failover testen abgeschlossen ist, beenden Sie den Test über das Azure-Portal die aufhebt der virtuellen Maschine und löscht die virtuelle Festplatte. Die VM-Image in den Recovery-Tresor weiterhin während des gesamten Testfailovers vom lokalen virtuellen Computer repliziert werden, als ob jemals nichts geschieht.

-   **Ungeplantes Failover** ƒAn ungeplantes Failover tritt auf, wenn ein Fehler durch eine tatsächliche mit dem geschützten Server oder virtueller Computer auf dem Hostserver. Das Failover entweder Windows Server Essentials-Dashboard manuell ausgelöst wird, oder wenn der ausgefallene Server selbst die Server, den Windows Server Essentials ausgeführt wird, kann ausgelöst werden, aus dem Azure-Portal direkt. In diesem Fall wird das ungeplante Failover der VM-Image, das auf Ihre Recovery-Tresor repliziert wurden, stellt es als einen ausgeführten virtuellen Computer in Azure und Herstellen einer Verbindung mit dem Server, um Szenarien zu testen, die für das Unternehmen gelten. Wenn Ihr Server lokal wiederhergestellt wird, kann ein Failback manuell aus dem Azure-Portal ausgelöst werden, die dann wieder auf dem lokalen Server auf das VM-Image kopiert werden.

-   **Geplantes Failover** ƒA Geplantes Failover ist eine Aktion, die durchgeführt werden kann, die geplante Aktivitäten, wie die Wartung von Hardware, stattfinden, müssen die der Server nach unten zu. Bei einem geplanten Failover erfolgt der gleiche Prozess im Hinblick auf die Bereitstellung des Abbilds replizierten virtuellen Computer in Azure. Allerdings wird vor der auf diese Weise der lokale Server heruntergefahren systematisch um sicherzustellen, dass alle Änderungen in Azure repliziert werden, bevor das Herunterfahren. Nachdem die geplante Wartung abgeschlossen ist, können Sie manuell ein Failback aus dem Windows Server Essentials-Dashboard oder im Azure-Portal die würde Schalten von den lokalen Server und den virtuellen Computer in Azure und löschen dann aufgehoben bereitstellen Auslösen der. VHD-Datei. Replikation vom lokalen virtuellen Computer in Azure würde dann weiterhin wieder normal auftreten.

In jeder der drei oben genannten Fälle wird Wenn ein virtueller Computer in Azure, Windows Server Essentials-Dashboard Failover ist die neue virtuelle Maschine in Azure ausgeführt wird, wie in der folgenden Abbildung angezeigt.

![Screenshot mit der Seite "Azure Recovery" des Windows Server Essentials-Dashboards. Azure-Replikation wurde für einen Host mit dem Namen Essentials und einer virtuellen Maschine benannten Essentials-Test in Azure ausgeführte weist darauf hin, dass der Host über Azure fehlgeschlagen ist aktiviert.](media/azure-site-recovery-8.PNG)

<a name="see-also"></a>Siehe auch
--------
[Erste Schrittemit Windows Server Essentials](get-started.md)
