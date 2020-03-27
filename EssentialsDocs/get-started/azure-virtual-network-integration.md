---
title: Azure Virtual Network-Integration
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7d38505-cff5-4f15-9fd5-ae6dba15ce88
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 92c8241d861e72d5f9f409a334e6edbeed5eae4c
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310577"
---
# <a name="azure-virtual-network-integration"></a>Azure Virtual Network-Integration

>Gilt für: Windows Server 2016 Essentials

Wenn Organisationen die Cloud Computing durchführen, werden Sie selten alle Ihre Ressourcen 100% zu einem Zeitpunkt verschieben, sondern stattdessen einen Ansatz treffen, bei dem sich einige Ressourcen in der Cloud befinden und einige weiterhin lokal sind. Dank dieses hybriden Ansatzes können Organisationen nicht nur einige Computerressourcen in die Cloud verlagern, sondern auch Ihre IT-Infrastruktur erweitern, ohne neue Hardware erwerben zu müssen.

Bei der Implementierung dieses hybriden Ansatzes für das Computing ist eine nahtlose Methode für Ressourcen an beiden Standorten erforderlich, um miteinander zu kommunizieren. Azure Virtual Network ist ein Azure-Dienst, mit dem Organisationen ein virtuelles privates Netzwerk (Punkt-zu-Punkt-(P2P) oder Site-to-Site-VPN (S2S) erstellen können, mit dem die in Azure (z. b. virtuelle Computer und Speicher) laufenden Ressourcen so aussehen, als wären Sie im lokalen Netzwerk für den nahtlosen Zugriff auf Anwendungen und Ressourcen.

Die Konfiguration eines virtuellen Azure-Netzwerks kann komplex sein. Mit Windows Server Essentials 2016 können Sie Ihr virtuelles Azure-Netzwerk problemlos über einen einfachen Assistenten konfigurieren, mit dem Sie die am besten geeigneten Standardeinstellungen für Ihre Netzwerkumgebung auswählen können. Wie im folgenden Screenshot gezeigt, wurde dem Abschnitt Microsoft Cloud Services des Windows Essentials-Dashboards eine neue Azure Virtual Network-Integrationsaufgabe hinzugefügt, um virtuelle Netzwerke in Azure einzuführen und einen schnellen Link zum Initiieren der Integration bereitzustellen. .

![Ein Screenshot mit der Registerkarte "Get Started" auf der Startseite des Windows Server Essentials-Dashboards. Auf der Registerkarte "Get Started" wurde der Abschnitt Dienste ausgewählt, und das Dashboard zeigt unter Microsoft Cloud Services-Integration an, dass das virtuelle Azure-Netzwerk zurzeit deaktiviert ist.](media/azure-virtual-network-1.PNG)

Wenn Sie im obigen Screenshot auf den Link **jetzt integrieren** für virtuelle Azure-Netzwerke klicken, wird ein Dialogfeld angezeigt, in dem Sie aufgefordert werden, sich bei Ihrem Microsoft Azure Konto anzumelden. Wenn Sie nicht über ein Microsoft Azure Konto verfügen, können Sie sich auf diesem Bildschirm für eine registrieren, die Sie zum Azure-Konto für die Anmeldung umleitet:

![Ein Screenshot, der die Seite anmelden bei Microsoft Azure des Assistenten zum Integrieren von virtuellen Azure-Netzwerken anzeigt](media/azure-virtual-network-2.PNG)

Nachdem Sie sich bei Azure angemeldet haben, haben Sie die Möglichkeit, das Abonnement auszuwählen, das dem virtuellen Azure-Netzwerkdienst zugeordnet werden soll:

![Ein Screenshot, der die Seite Mein Microsoft Azure Abonnement des Assistenten zum Integrieren von virtuellen Azure-Netzwerken anzeigt.](media/azure-virtual-network-3.PNG)

Nachdem Sie das Azure-Abonnement ausgewählt haben, das Sie für virtuelle Azure-Netzwerke verwenden möchten, erhalten Sie die Möglichkeit, ein neues virtuelles Azure-Netzwerk zu erstellen. Wenn bereits ein Abonnement unter diesem Abonnement eingerichtet wurde, wird im Dropdown Feld angezeigt, dass es verfügbar ist. Außerdem wählen Sie einen Namen für das lokale Netzwerk aus, mit dem das virtuelle Azure-Netzwerkressourcen in Ihrem lokalen Netzwerk identifizieren soll. Schließlich wählen Sie die Azure-Region aus, in der das virtuelle Azure-Netzwerk gehostet werden soll. Die Auswahl eines Orts, der sich physisch am nächsten an Ihrem lokalen Netzwerk befindet, eignet sich in der Regel zum Optimieren der Bandbreitengeschwindigkeit bei der Kommunikation mit Ressourcen, die Sie in ihren Azure-Diensten

![Ein Screenshot, der die Seite Virtuelles Azure-Netzwerk einrichten des Assistenten zum Integrieren von virtuellen Azure-Netzwerken anzeigt.](media/azure-virtual-network-4.PNG)

Der letzte Schritt des Integrationsprozesses ist das Einrichten des VPN-Geräts, das für die S2S-VPN-Verbindung verwendet wird. Da die meisten kleinen Unternehmen nur wenige Server in Ihrer Umgebung haben und das IT-Personal nicht für die ordnungsgemäße Konfiguration eines VPN-Routers zum Herstellen einer Verbindung mit Microsoft Azure, besteht die Standardauswahl darin, den Windows Server Essentials-Server als VPN-Server einzurichten, auf dem Ressourcen in Ihrem lokalen Netzwerk wird eine Verbindung mit hergestellt, um auf Ressourcen im virtuellen Azure-Netzwerk zuzugreifen. Wenn Sie jedoch lieber einen anderen Server in Ihrer Umgebung als den VPN-Server verwenden oder stattdessen einen VPN-Router verwenden möchten, können Sie diese Optionen auswählen.

Aufgrund der Variation von Routertypen und-Modellen wird von Windows Server Essentials nicht versucht, den VPN-Router automatisch zu konfigurieren. Wenn Sie den VPN-Router in diesem Integrations-Assistenten auswählen, wird nur das virtuelle Azure-Netzwerk des Gerätetyps benachrichtigt, damit für die Konnektivität geeignete Routing Konfigurationen in Azure erforderlich sind.

Nach dem Abschließen des Integrations-Assistenten wird im Windows Server Essentials-Dashboard für virtuelle Azure-Netzwerke eine neue Registerkarte angezeigt:

![Ein Screenshot, der die Azure-vnet-Seite des Windows Server Essentials-Dashboards anzeigt. Die Registerkarte Azure Virtual Network ist ausgewählt und zeigt den Status als Konfiguration an.](media/azure-virtual-network-5.PNG)

>! Beachten Sie, dass das Abschließen der Konfiguration eines virtuellen Azure-Netzwerks in der Cloud eine lange Zeit in Anspruch nehmen kann, bis zu 30 Minuten. Während dieser Zeit wird der Status der Konfiguration auf der Seite Status des virtuellen Azure-Netzwerks des Dashboards angezeigt.

Sobald die Konfiguration des virtuellen Azure-Netzwerks abgeschlossen ist, ändert sich der Status in verbunden und zeigt die Details Ihres virtuellen Azure-Netzwerks an, z. b. Daten in/out, Gateway-IP-Adresse, lokale IP-Adresse und Konto Details:

![Ein Screenshot, der die Azure-vnet-Seite des Windows Server Essentials-Dashboards anzeigt. Die Registerkarte Azure Virtual Network ist ausgewählt und zeigt den Status verbunden an. unter diesen Statusinformationen werden die Details des virtuellen Netzwerks angezeigt.](media/azure-virtual-network-6.PNG)

Im Bereich Tasks auf der rechten Seite des Dashboards finden Sie die verschiedenen Aufgaben, die Sie mit Ihrem virtuellen Azure-Netzwerk durchführen können.

-   Verbindung mit **Azure-vnet trennen** Das Einrichten eines virtuellen Azure-Netzwerks ist kostenlos, aber es fallen Kosten für das VPN-Gateway an, das eine Verbindung mit lokalen und anderen vnets in Azure herstellt. Durchtrennen der Verbindung mit dem Azure-vnet wird die gesamte Abrechnung beendet.

-   **Über VPN-Gerät wechseln** Wenn Sie von einem VPN-Server zu einem VPN-Router wechseln möchten, können Sie mit diesem Task den Switch festlegen und das Azure-vnet benachrichtigen.

-   **Azure-vnet konfigurieren** Mit dieser Aufgabe können Sie Erweiterte Konfigurationsoptionen für das Azure-vnet ändern, indem Sie Sie auf die Seite für die Azure-Portal Konfiguration für das Azure-vnet umleiten.

-   **Aktualisierungs Status** Aktualisiert die Seite Status und aktualisiert den Verbindungsstatus des Azure-vnets einschließlich der in/out-Daten.

-   **Deaktivieren von Azure-VNET-Integration** Trennt die Verbindung mit dem Azure-vnet und entfernt die Integration aus dem Windows Server Essentials-Dashboard. Beachten Sie, dass das Azure-vnet nicht gelöscht wird. die Einstellungen bleiben in Azure weiterhin erhalten, wenn Sie das Azure-vnet später erneut in das Dashboard integrieren möchten.

-   **Erfahren Sie mehr über Azure vnet** [https://azure.microsoft.com/services/virtual-network/](https://azure.microsoft.com/services/virtual-network/).

<a name="see-also"></a>Siehe auch
--------
[Erste Schritte in Windows Server Essentials](get-started.md)
