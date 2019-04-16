---
title: Integration mit Azure virtuellen Netzwerk
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7d38505-cff5-4f15-9fd5-ae6dba15ce88
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 21057359967c73d8d9fc434694b8f203ad5c1f6a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
#<a name="azure-virtual-network-integration"></a>Integration mit Azure virtuellen Netzwerk

>Gilt für: Windows Server2016 Essentials

Wie Organisationen die Möglichkeit, das cloud-computing machen, werden nur selten sie verschieben Sie alle ihre Ressourcen auf einmal 100 %, sondern stattdessen nutzen einen Ansatz, in denen einige Ressourcen sind in der Cloud und einige noch im lokalen. Diese Herangehensweise ganz einfach für Unternehmen können Sie nicht nur einige computing-Ressourcen in die Cloud verschieben, aber auch ermöglicht es ihnen, ihre IT-Infrastruktur zu erweitern, ohne neue Hardware erwerben.

Bei der Implementierung dieser Herangehensweise Computing ist nahtlos für Ressourcen in beiden Speicherorten für die Kommunikation mit anderen erforderlich. Azure virtuelle Netzwerke ist ein Azure-Dienst, der Organisationen einen Punkt (P2P) erstellen oder die Standort-zu-Standort (S2S) VPN, die die Ressourcen, die in Azure (z. B. virtuelle Maschinen und Speicher) suchen ausgeführt werden macht, als ob sie für eine nahtlose Anwendung und Ressourcen im lokalen Netzwerk befinden.

Konfiguration von einem virtuellen Azure-Netzwerk kann sehr komplex sein. Mit Windows Server Essentials 2016 können Sie problemlos Azure virtuellen Netzwerk über einen einfachen Assistenten konfigurieren, die Sie auswählen, die am besten geeignete Standardwerte für die Netzwerk-Umgebung unterstützt. Wie im folgenden Screenshot gezeigt wird, wurde eine neue Azure virtuellen Netzwerk Integration Aufgabe mit dem Microsoft-Clouddienste Abschnitt Windows Essentials-Dashboard, um die Einführung von Azure virtuelle Netzwerke sowie einen Quicklink zum Initiieren der Integration hinzugefügt.

![Ein Bildschirmfoto die Registerkarte "Erste Schritte" auf der Startseite des Windows Server Essentials-Dashboards angezeigt. Auf der Registerkarte "Erste Schritte" im Abschnitt Dienste ausgewählt wurde, und das Dashboard gibt unter Microsoft Cloud Services-Integration, dass Azure virtuelles Netzwerk derzeit deaktiviert ist.](media/azure-virtual-network-1.PNG)

Beim Klicken auf die **integrieren jetzt** für Azure virtuelle Netzwerke aus dem Screenshot zu verknüpfen, ein Dialogfeld angezeigt wird, werden Sie aufgefordert, die mit Ihrem Microsoft Azure-Konto anmelden. Wenn Sie nicht über ein Microsoft Azure-Konto verfügen, müssen Sie die Option zum Registrieren für eine auf diesem Bildschirm, die Sie das Azure-Konto anmelden Portal umleitet:

![Screenshot der Anmeldung In zu Microsoft Azure Seite von der Integration mit Azure-Assistent.](media/azure-virtual-network-2.PNG)

Wenn – in Azure anmelden, wird angezeigt mit der Option zum auswählen, welches Abonnement sie Azure Virtual zuordnen möchten networking Service:

![Screenshot die Seite Mein Microsoft Azure-Abonnement die Integration mit virtuellen Azure-Assistent angezeigt.](media/azure-virtual-network-3.PNG)

Nachdem Sie entschieden haben, welche Azure-Abonnement für Azure-virtuelle Netzwerke verwenden möchten wird mit der Option zum Erstellen eines neuen Azure virtuelles Netzwerks angezeigt werden, oder eine bereits unter diesem Abonnement wurde, wird im Dropdown-Menü angezeigt, sofort verfügbar sind. Sie können auch einen Namen für das lokale Netzwerk auswählen, die im Azure virtuellen Netzwerk verwendet wird, um Ressourcen in Ihrem lokalen Netzwerk zu identifizieren. Wählen Sie zum Schluss die Azure-Region und ihre Azure Virtual Network gehostet werden soll. Wählen einen Speicherort, physisch am nächsten ist Ihrem lokalen Netzwerk empfiehlt sich in der Regel für die Optimierung der Bandbreite Geschwindigkeit für die Kommunikation mit Ressourcen, die in Azure-Dienste gehostet werden kann:

![Das Festlegen von Azure Virtual Network Seite von der Integration mit Azure-Assistent Screenshot.](media/azure-virtual-network-4.PNG)

Der letzte Schritt des Prozesses Integration ist das VPN-Gerät einrichten, das für die S2S-VPN-Verbindung verwendet werden. Da die meisten kleine Unternehmen nur wenige Server in ihrer Umgebung haben und verfügen nicht über die IT-Mitarbeiter, um einen Router-VPN-Verbindung mit Microsoft Azure ordnungsgemäß konfigurieren, werden die Standardauswahl auf den Windows Server Essentials-Server als VPN-Server einrichten, den Ressourcen in Ihrem lokalen Netzwerk für den Zugriff auf Ressourcen im Azure virtuellen Netzwerk zu verbinden. Wenn Sie einen anderen Server in Ihrer Umgebung würden Sie gerne verwenden, als der VPN-Server, oder verwenden Sie stattdessen ein VPN-Router, können Sie jedoch diese Optionen auswählen.

Aufgrund der unterschiedliche Arten von Router und Modelle versucht Windows Server Essentials nicht automatisch den VPN-Router konfigurieren. Auswählen der VPN-Router in diesem Assistenten Integration benachrichtigt nur Azure virtuelle Netzwerke, der Typ des Geräts für die entsprechenden routing Konfigurationen, die in Azure für die Konnektivität erforderlich.

Nach Abschluss der Integrations-Assistent, werden eine neue Registerkarte im Windows Server Essentials-Dashboard für Azure virtuelle Netzwerke angezeigt:

![Ein Screenshot die Seite Azure-VNet des Windows Server Essentials-Dashboards angezeigt. Registerkarte "Azure virtuellen Netzwerk" ausgewählt ist und zeigt den Status als konfigurieren.](media/azure-virtual-network-5.PNG)

>! Beachten Sie die Konfiguration für ein Azure-virtuelles Netzwerk in der Cloud kann sehr lange nach oben, um 30 Minuten dauern. Während dieser Zeit wird der Status der Konfigurieren von Azure Virtual Network Seite des Dashboards angezeigt.

Nach Abschluss die Konfiguration des virtuellen Azure wird der Status auf verbunden ändern und zeigt die Details Ihrer Azure virtuellen Netzwerk, z. B. Daten/ausblenden, Gateway-IP-Adresse, IP-Adresse und das Konto Informationen zum lokalen:

![Ein Screenshot die Seite Azure-VNet des Windows Server Essentials-Dashboards angezeigt. Registerkarte "Azure virtuellen Netzwerk" ausgewählt ist, und zeigt den Status als verbunden, und unter diese Statusinformationen werden die Details für das virtuelle Netzwerk angezeigt.](media/azure-virtual-network-6.PNG)

Klicken Sie im Aufgabenbereich auf der rechten Seite des Dashboards werden die verschiedenen Aufgaben, die Sie mit dem Azure virtuellen Netzwerk ausführen können.

-   **Trennen von Azure-VNET** Einrichten eines Azure virtuellen Netzwerks ist kostenlos, aber es gibt eine Gebühr für das VPN-Gateway, die mit lokalen und andere VNETs in Azure verbindet. Trennen die Azure-VNET beendet alle Abrechnung.

-   **Wechseln Sie über VPN-Gerät** den Fall, dass Sie über einen VPN-Server mit einem Router-VPN-ändern möchten, diese Aufgabe können Sie wechseln, und benachrichtigen die Azure-VNET.

-   **Konfigurieren von Azure-VNET** dieser Aufgabe können Sie erweiterte Konfigurationsoptionen von Azure-VNET zu ändern, indem sie auf der Seite Azure-Portal-Konfiguration für Azure-VNET umleiten.

-   **Aktualisiert den Status** aktualisiert die Statusseite, die den Verbindungsstatus der Azure-VNET, einschließlich der Daten in "/ out" aktualisieren.

-   **Deaktivieren der Integration von Azure-VNET** trennt den Azure-VNET und Integration über das Windows Server Essentials-Dashboard entfernt. Beachten Sie dabei die Azure-VNET löschen, die Einstellungen werden weiterhin in Azure beibehalten, wenn Sie Azure-VNET mit dem Dashboard später erneut integrieren möchten.

-   **Hier erfahren Sie mehr über Azure-VNET**[https://azure.microsoft.com/en-us/services/virtual-network/](https://azure.microsoft.com/en-us/services/virtual-network/).

<a name="see-also"></a>Siehe auch
--------
[Erste Schrittemit Windows Server Essentials](get-started.md)
