---
title: Azure Virtual Network-integration
description: Beschreibt, wie Windows Server Essentials
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
ms.openlocfilehash: 673cb5a2292bab113aefb1de37f80bf4d880b467
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433906"
---
# <a name="azure-virtual-network-integration"></a>Azure Virtual Network-integration

>Gilt für: Windows Server 2016 Essentials

Wenn Unternehmen ihren Weg in die cloud computing vornehmen, werden nur selten sie verschieben Sie alle ihre Ressourcen gleichzeitig zu 100 %, aber stattdessen dauern einen Ansatz, in dem einige Ressourcen sind in der Cloud und einige sind weiterhin lokal. Dieser kombinierte Ansatz erleichtert es für Unternehmen nicht nur einige Compute-Ressourcen in die Cloud verschieben, aber auch können sie ihre IT-Infrastruktur zu erweitern, ohne neue Hardware erwerben.

Bei der Implementierung dieser kombinierte Ansatz beim computing ist ein nahtloses Verfahren für Ressourcen in beiden Speicherorten für die Kommunikation mit anderen erforderlich. Azure Virtual Networking ist ein Azure-Dienste, die es ermöglicht Organisationen einen Punkt (P2P) zu erstellen oder Standort-zu-Standort (S2S) virtuelles privates Netzwerk, mit der die Ressourcen, die in Azure (z. B. virtuelle Maschinen und Speicher) suchen ausgeführt werden, als wären sie sind im lokalen Netzwerk für den Zugriff für nahtlose und Ressourcen.

Konfiguration von einem virtuellen Azure-Netzwerk kann komplex sein. Mit Windows Server Essentials 2016 können Sie problemlos Ihrem virtuellen Azure-Netzwerk über einen einfachen Assistenten konfigurieren, mit dem Sie die am besten geeignete Standardwerte für Ihre vernetzten Umgebung auswählen können. Wie im folgenden Screenshot gezeigt, wurde eine neue Azure Virtual Network Integration Aufgabe hinzugefügt, um die Microsoft Cloud Services-Abschnitt des Windows-Essentials-Dashboards zum Einführen von virtuellen Azure-Netzwerk sowie einen direkter Link zum Initiieren der integration .

![Dieser Screenshot zeigt die Registerkarte "Erste Schritte" auf der Homepage des Windows Server Essentials-Dashboards. Klicken Sie auf der Registerkarte "Erste Schritte" Dienstabschnitt ausgewählt wurde, und im Dashboard unter Microsoft Cloud Services-Integration angegeben ist, dass Azure Virtual Network ist derzeit deaktiviert.](media/azure-virtual-network-1.PNG)

Beim Klicken auf die **integrieren jetzt** für virtuelle Azure-Netzwerke im Screenshot oben, verknüpfen Sie aufgefordert werden, melden Sie sich mit Ihrem Microsoft Azure-Konto ein Dialogfeld angezeigt. Wenn Sie nicht über ein Microsoft Azure-Konto verfügen, müssen Sie die Option zur Registrierung für eine auf diesem Bildschirm die Sie an das anmeldungsportal für Azure-Konto umleitet:

![Dieser Screenshot zeigt die Anmeldung bei Microsoft Azure-Seite des Assistenten für die Integration mit virtuellen Azure-Netzwerk.](media/azure-virtual-network-2.PNG)

Sobald in Azure sich anmelden, wird Ihnen angezeigt mit der Option, welches Abonnement wählen sie die virtuellen Azure-zuordnen möchten networking Dienst:

![Dieser Screenshot zeigt die Seite Meine Microsoft Azure-Abonnement von der Integration in Azure Virtual Network-Assistenten.](media/azure-virtual-network-3.PNG)

Nachdem Sie ausgewählt haben, welches Azure-Abonnement für virtuelle Azure-Netzwerken verwenden möchten Sie die Option zum Erstellen eines neuen virtuellen Azure-Netzwerks angezeigt werden oder wenn eine Installation unter diesem Abonnement bereits stattgefunden hat, zeigt die Dropdown-Feld, dass sie verfügbar ist. Sie werden auch einen Namen für das lokale Netzwerk auswählen, die im virtuellen Azure-Netzwerk zum Identifizieren von Ressourcen in Ihrem lokalen Netzwerk verwenden. Schließlich werden Sie die Azure-Region auswählen, in dem ihre virtuellen Azure-Netzwerk gehostet werden soll. Auswählen eines Speicherorts, die physisch am ehesten entsprechen Ihrem lokalen Netzwerk empfiehlt sich in der Regel zur Optimierung der Geschwindigkeit der Bandbreite für die Kommunikation mit Ressourcen, die Sie in ihrer Azure-Dienste hosten können:

![Dieser Screenshot zeigt die legen Sie virtuelle Azure-Netzwerk-Seite des Assistenten für die Integration mit virtuellen Azure-Netzwerk.](media/azure-virtual-network-4.PNG)

Der letzte Schritt des Integrationsprozesses ist das VPN-Gerät einrichten, das für die S2S-VPN-Verbindung verwendet werden. Da die meisten kleine Unternehmen nur einige Server in ihrer Umgebung haben und nicht über die IT-Mitarbeiter, um ein VPN-Router für Microsoft Azure die Verbindung ordnungsgemäß zu konfigurieren, wird die Standardauswahl werden auf dem Windows Server Essentials-Server als dem VPN-Server richten Sie diese Ressourcen in Ihrem lokale Netzwerk werden mit verbunden, um den Zugriff auf Ressourcen im virtuellen Azure-Netzwerk. Wenn Sie eher einen anderen Server in Ihrer Umgebung, wie der VPN-Server verwenden würden, oder Sie stattdessen ein VPN-Router verwenden, können Sie jedoch, diese Optionen auswählen.

Aufgrund der Variante in Routertypen und Modelle versucht Windows Server Essentials nicht automatisch den VPN-Router konfigurieren. Auswählen der VPN-Router in diesem Assistenten Integration benachrichtigt nur virtuelle Azure-Netzwerk des Gerätetyps für die entsprechenden routing-Konfigurationen in Azure für Verbindungen erforderlich.

Nach Abschluss des Assistenten für Integration, werden eine neue Registerkarte angezeigt, auf dem Windows Server Essentials-Dashboard für virtuelle Azure-Netzwerke:

![Dieser Screenshot zeigt die Azure-VNet-Seite des Windows Server Essentials-Dashboards. Die Registerkarte "virtuelle Azure-Netzwerk" ausgewählt ist, und es wird der Status als konfigurieren.](media/azure-virtual-network-5.PNG)

>! Beachten Sie die Konfiguration für einen virtuellen Azure-Netzwerk in der Cloud kann viel Zeit nach oben, um 30 Minuten dauern. Während dieser Zeit werden der Status der Konfigurieren von in die Azure Virtual Network-Statusseite des Dashboards vorhanden.

Nach Abschluss die Konfiguration des virtuellen Azure-Netzwerks der Status ändert, verbunden und die Details Ihres virtuellen Azure-Netzwerks wie z. B. Daten in/Out "," Gateway-IP-Adresse "," lokale IP-Adresse und den Kontonamen Details anzeigen:

![Dieser Screenshot zeigt die Azure-VNet-Seite des Windows Server Essentials-Dashboards. Die Registerkarte "virtuelle Azure-Netzwerk" ausgewählt ist, und zeigt den Status als verbunden, und die Details des virtuellen Netzwerks werden unter diese Statusinformationen angezeigt.](media/azure-virtual-network-6.PNG)

Im Bereich Tasks auf der rechten Seite des Dashboards sind die verschiedenen Aufgaben, die Sie mit Ihrem virtuellen Azure-Netzwerk ausführen können.

-   **Trennen von Azure-VNET** zum Einrichten eines Azure Virtual Network ist kostenlos, aber eine Gebühr für das VPN-Gateway, die eine Verbindung mit lokalen und anderen VNETs in Azure. Trennen der Verbindung aus dem Azure VNET beendet abgerechnet.

-   **Wechseln Sie über VPN-Gerät** den Fall, dass Sie über einen VPN-Server mit einem VPN-Router ändern möchten, diese Aufgabe können Sie wechseln, und benachrichtigen das Azure-VNET.

-   **Konfigurieren von Azure-VNET** mit diesem Task können Sie erweiterte Konfigurationsoptionen des Azure-VNETS zu ändern, indem sie auf der Seite "Azure-Portal-Konfiguration" für Azure-VNET umleiten.

-   **Aktualisierungsstatus** die Statusseite, aktualisieren den Status der Verbindung des Azure-VNETS, einschließlich der Daten in/out-aktualisiert.

-   **Azure-VNET-Integration deaktivieren** trennt die Verbindung im Azure-VNET und die Integration über das Windows Server Essentials-Dashboard entfernt. Beachten Sie dies nicht das Azure-VNET gelöscht, die Einstellungen werden in Azure weiterhin beibehalten, wenn Sie Azure-VNET mit dem Dashboard später erneut integrieren möchten.

-   **Erfahren Sie mehr über Azure-VNET** [ https://azure.microsoft.com/services/virtual-network/ ](https://azure.microsoft.com/services/virtual-network/).

<a name="see-also"></a>Siehe auch
--------
[Erste Schritte in Windows Server Essentials](get-started.md)
