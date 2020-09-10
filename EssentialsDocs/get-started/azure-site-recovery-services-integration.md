---
title: Azure Site Recovery Services-Integration
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/01/2016
ms.topic: article
ms.assetid: 262701a6-8a97-4c4e-bfbf-9f8007c308d6
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: aa84ae8f3d11631b76d2e85e6a50f309eb83dd74
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622583"
---
# <a name="azure-site-recovery-services-integration"></a>Azure Site Recovery Services-Integration

>Gilt für: Windows Server 2016 Essentials

[Azure Site Recovery Services](/azure/site-recovery/) ist ein Dienst, der durch Microsoft Azure die Echt Zeit Replikation ihrer virtuellen Computer (VM) in einem Sicherungs Tresor in Azure ermöglicht. Wenn Ihr Server oder Standort aufgrund eines Hardwarefehlers oder eines anderen Fehlers ausfällt, können Sie ein Failover zu Azure ausführen, wobei das in Ihrem Sicherungs Tresor gespeicherte VM-Image als laufender virtueller Computer in Azure bereitgestellt wird. In Kombination mit einem virtuellen Azure-Netzwerk stellen Client-PCs, die zuvor mit dem lokalen Server verbunden waren, eine transparente Verbindung mit dem Server her, der in Azure ausgeführt wird.

Die Integration von Azure Site Recovery Services in Windows Server Essentials beginnt auf die gleiche Weise wie das Konfigurieren von [virtuellen Azure-Netzwerken](azure-virtual-network-integration.md). Klicken Sie im Dashboard auf der **Microsoft Cloud Dienste-Integrations** Seite auf in **Azure Site Recovery Dienste integrieren** rechts neben dem Dashboard:

![Ein Screenshot mit der Registerkarte "Get Started" auf der Startseite des Windows Server Essentials-Dashboards. Auf der Registerkarte "Get Started" wurde der Abschnitt Dienste ausgewählt, und im Dashboard wird unter Microsoft Cloud Services-Integration angezeigt, dass die Azure-Wiederherstellung zurzeit deaktiviert ist.](media/azure-site-recovery-1.PNG)

Wie bei der Integration von Azure Virtual Network und Azure Backup Integration müssen Sie sich entweder mit Ihrem vorhandenen Azure-Konto bei Azure anmelden oder ein neues Konto erstellen:

![Ein Screenshot, der die Seite anmelden bei Microsoft Azure des Assistenten zum Aktivieren der Replikation in Azure anzeigt Die Schaltfläche Anmelden wird angezeigt, da der Benutzer noch nicht bei Microsoft Azure angemeldet ist.](media/azure-site-recovery-2.PNG)

Nachdem Sie sich erfolgreich bei Azure angemeldet haben, wird ein Bildschirm angezeigt, auf dem Sie gefragt werden, welches Abonnement Sie dem Azure Site Recovery-Dienst zuordnen möchten, sowie die Azure-Region, in der Ihre VM gespeichert und gehostet wird:

![Ein Screenshot, der die Seite anmelden bei Microsoft Azure des Assistenten zum Aktivieren der Replikation in Azure anzeigt Da sich der Benutzer bei Microsoft Azure angemeldet hat, bietet diese Seite Optionen zum Auswählen eines Abonnements, eines Speicher Kontos und einer Region.](media/azure-site-recovery-3.PNG)

Nachdem Sie die Abonnement-und Regions Auswahl ausgewählt haben, wird im **Windows Server Essentials-Dashboard** eine neue Registerkarte mit dem Namen **Azure Recovery**angezeigt. Die Netzwerk Überprüfung dient zum Identifizieren und auflisten unterstützter Host Server (auf denen Windows Server Hyper-V 2012 R2 und höher ausgeführt wird) sowie der virtuellen Computer (Gäste) unter den einzelnen Hosts:

![Ein Screenshot, der die Azure-Wiederherstellungs Seite des Windows Server Essentials-Dashboards anzeigt. Zwei Hyper-V-Hosts werden zusammen mit den virtuellen Maschinen angezeigt, die auf diesen Hosts ausgeführt werden. Eine virtuelle Maschine mit dem Namen ramh157v01 auf Host RAM-H1-7 ist ausgewählt, und die Replikation in Azure ist für diesen virtuellen Computer zurzeit deaktiviert.](media/azure-site-recovery-4.PNG)

### <a name="enabling-guest-virtual-machines-for-protection"></a>Aktivieren von virtuellen Gast Computern für den Schutz

Wenn Sie einen virtuellen Computer im Azure-Wiederherstellungs Fenster ausgewählt haben, können Sie auf der rechten Seite des Dashboards auf **Replikation in Azure aktivieren** klicken, um das Image des virtuellen Computers auf Azure vorzubereiten und &trade; zu kopieren:

![Screenshot, der das Dialogfeld "Replikation in Azure aktivieren" anzeigt. Eine Statusanzeige wird angezeigt, wenn ein Host hinzugefügt wird.](media/azure-site-recovery-5.PNG)

Während dieses Vorgangs wird der Azure Site Recovery-Dienst-Agent auf dem Host Server installiert, ein Sicherungs Tresor, in dem das Abbild der Gast-VM gespeichert wird, und die Replikation des Images in Azure. Abhängig von der Größe des virtuellen Computers, der repliziert wird, kann der Abschluss des Replikations Vorgangs Stunden oder Tage dauern. Bis das gesamte VM-Image und die neuesten Delta-Daten in Azure repliziert werden, sind keine failovertasks verfügbar, und der virtuelle Computer ist nicht geschützt. Nachdem die Replikation abgeschlossen ist, ändert sich die Spalte Schutz Status im Fenster Azure-Wiederherstellung von **Replizierung** in **aktiviert**:

![Ein Screenshot, der die Azure-Wiederherstellungs Seite des Windows Server Essentials-Dashboards anzeigt. Zwei Hyper-V-Hosts werden zusammen mit den virtuellen Maschinen angezeigt, die auf diesen Hosts ausgeführt werden. Eine virtuelle Maschine mit dem Namen ramh12v02 auf Host RAM-H1-2 ist ausgewählt, und die Replikation in Azure ist für diesen virtuellen Computer zurzeit aktiviert.](media/azure-site-recovery-6.PNG)

### <a name="failover-of-a-guest-vm-to-azure"></a>Failover einer Gast-VM zu Azure

![Screenshot der Seite "Failover-VM zu Azure"](media/azure-site-recovery-7.PNG)

Wenn bei einem geschützten virtuellen Computer ein Fehler auftritt oder der Host Server, auf dem der geschützte virtuelle Computer ausgeführt wird, ausfällt, kann ein Failover zu Azure durchgeführt werden, um die Geschäftskontinuität aufrechtzuerhalten, bis der lokale virtuelle Computer oder der lokale Host Server repariert und verfügbar ist. Wie die obige Abbildung zeigt, gibt es drei failovertypen, die mit Azure Site Recovery-Diensten unterstützt werden:

-   **Test Failover** ƒA ein guter Notfall Wiederherstellungs Plan bietet die Möglichkeit, einen Notfall zu simulieren, um im Falle eines echten notfalls minimale Ausfallzeiten sicherzustellen. Bei einem Test Failover wird das VM-Image, das in den Wiederherstellungs Tresor repliziert wurde, als laufender virtueller Computer in Azure bereitgestellt, und Sie können eine Verbindung mit dem Server herstellen, um Szenarios zu testen, die für das Unternehmen gelten. Während eines Test Failovers wird der lokale virtuelle Computer weiterhin ohne Unterbrechungen ausgeführt, da das Geschäft während des Notfall Wiederherstellungs Tests nicht unterbrochen werden kann. Nachdem das Test Failover durchgeführt wurde, beenden Sie den Test über das Azure-Portal, wodurch die Bereitstellung des virtuellen Computers aufgehoben wird und die virtuelle Festplatte gelöscht wird. Während des gesamten Test Failovers wird das VM-Image in Ihrem Wiederherstellungs Tresor weiterhin von der virtuellen Maschine auf dem Standort repliziert, als wäre nichts passiert.

-   **Ungeplantes Failover** ƒAn ein ungeplantes Failover tritt auf, wenn ein tatsächlicher Fehler mit dem geschützten Host Server oder dem virtuellen Computer auf dem Host Server vorliegt. Das Failover wird manuell aus dem Windows Server Essentials-Dashboard ausgelöst, oder wenn es sich bei dem fehlerhaften Server selbst um den Server handelt, auf dem Windows Server Essentials ausgeführt wird, kann direkt über das Azure-Portal ausgelöst werden. In diesem Fall nimmt das ungeplante Failover das VM-Image an, das in den Wiederherstellungs Tresor repliziert wurde, stellt es als laufenden virtuellen Computer in Azure bereit und ermöglicht es Ihnen, eine Verbindung mit dem Server herzustellen, um Szenarios zu testen, die für das Unternehmen gelten. Wenn Ihr Server lokal wieder hergestellt wird, kann im Azure-Portal ein manuelles Failback ausgelöst werden, das dann das VM-Image wieder auf den lokalen Server kopiert.

-   **Geplantes Failover** ƒA das geplante Failover ist eine Aktion, die ausgeführt werden kann, wenn geplante Aktivitäten, wie z. b. die HW-Wartung, ausgeführt werden müssen, wodurch der Server heruntergefahren wird. Im Fall eines geplanten Failovers findet der gleiche Prozess in Bezug auf die Bereitstellung Ihres replizierten VM-Images in Azure statt. Bevor Sie dies tun, wird der lokale Server jedoch ordnungsgemäß heruntergefahren, um sicherzustellen, dass alle Änderungen vor dem Herunterfahren in Azure repliziert werden. Nachdem die geplante Wartung abgeschlossen ist, können Sie manuell ein Failback aus dem Windows Server Essentials-Dashboard oder dem Azure-Portal durchführen, um den lokalen Server zu starten und die Bereitstellung des virtuellen Computers in Azure aufzuheben und das zu löschen. VHD-Datei. Die Replikation von der lokalen VM zu Azure wird dann weiterhin wie gewohnt ausgeführt.

In den drei oben genannten Fällen zeigt das Windows Server Essentials-Dashboard den neuen virtuellen Computer in Azure an, wenn ein Failover für einen virtuellen Computer zu Azure ausgeführt wird, wie in der folgenden Abbildung dargestellt.

![Ein Screenshot, der die Azure-Wiederherstellungs Seite des Windows Server Essentials-Dashboards anzeigt. Die Replikation in Azure wurde für einen Host mit dem Namen Essentials aktiviert, und ein virtueller Computer namens Essentials-Test wird in Azure ausgeführt und zeigt an, dass für den Host ein Failover zu Azure ausgeführt wurde.](media/azure-site-recovery-8.PNG)

<a name="see-also"></a>Weitere Informationen
--------
[Erste Schritte in Windows Server Essentials](get-started.md)