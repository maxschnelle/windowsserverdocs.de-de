---
title: Konfigurieren von DNS und Firewall-Einstellungen
description: Dieses Thema enthält detaillierte Anweisungen zum Bereitstellen von Always On-VPN-unter Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: d8cf3bae-45bf-4ffa-9205-290d555c59da
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 06/11/2018
ms.openlocfilehash: 9cee39dbf240cac9701f926600d8efeffe99c214
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749492"
---
# <a name="step-5-configure-dns-and-firewall-settings"></a>Schritt 5 Konfigurieren von DNS und Firewall-Einstellungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorherige:** Schritt 4 Installieren und Konfigurieren des NPS-Servers](vpn-deploy-nps.md)
- [**nächster:** Schritt 6 Konfigurieren von Always On VPN-Verbindungen für den Windows 10-Client](vpn-deploy-client-vpn-connections.md)

In diesem Schritt konfigurieren Sie DNS und Firewall-Einstellungen für VPN-Konnektivität.

## <a name="configure-dns-name-resolution"></a>Konfigurieren von DNS-namensauflösung

Wenn remote-VPN-Clients verbunden sind, verwenden sie die gleichen DNS-Servern, die internen Clients verwenden, wodurch sie zum Auflösen von Namen auf die gleiche Weise wie der Rest von Ihren internen Arbeitsstationen.

Aus diesem Grund müssen Sie sicherstellen, dass der Computername, der externe Clients verwenden, um die Verbindung mit des VPN-Servers den alternativen Antragstellernamen in Zertifikaten für VPN-Server definierten übereinstimmt.

Um sicherzustellen, dass Remoteclients auf Ihrem VPN-Server eine Verbindung herstellen können, können Sie einen DNS-A (Host)-Eintrag in der externen DNS-Zone erstellen. Der A-Datensatz sollte den Zertifikat alternativen Antragstellernamen für das VPN-Server verwenden.

### <a name="to-add-a-host-a-or-aaaa-resource-record-to-a-zone"></a>Eine Zone einen Hostressourceneintrag (A oder AAAA) hinzu

1. Wählen Sie auf einem DNS-Server im Server-Manager **Tools**, und wählen Sie dann **DNS**. DNS-Manager wird geöffnet.
2. Wählen Sie in der Konsolenstruktur des DNS-Manager den Server, den Sie verwalten möchten.
3. Klicken Sie im Bereich "Details" im **Namen**, doppelklicken Sie auf **Forward-Lookupzonen** um die Ansicht zu erweitern.
4. In **Forward-Lookupzonen** Informationen mit der rechten Maustaste die forward-Lookupzone auf die Sie einen Eintrag, und wählen Sie dann möchten **neuer Host (A oder AAAA)** . Die **neuen Host** Dialogfeld wird geöffnet.
5. In **neuen Host**im **Namen**, geben Sie das Zertifikat alternativen Antragstellernamens für das VPN-Server.
6. Geben Sie IP-Adresse die IP-Adresse des VPN-Servers ein. Geben Sie die Adresse im IP-Version 4 (IPv4) Format einen Hostressourceneintrag (A) oder IP-Version 6 (IPv6) hinzufügen zu formatieren, um einen hostressourcendatensatz (AAAA) hinzuzufügen.
7. Wenn Sie eine reverse-Lookupzone für einen Bereich von IP-Adressen erstellt, einschließlich der IP-Adresse, die Sie, klicken Sie dann eingegeben auf die **verknüpften Zeigerressourceneinträge (PTR)-Eintrag erstellen** Kontrollkästchen.  Nach Auswahl dieser Option wird eine zusätzliche Zeigerressourceneinträge (PTR)-Ressourcendatensatz in einer reverse-Zone für diesen Host, auf Basis der Informationen, die Sie eingegeben, im haben erstellt **Namen** und **IP-Adresse**.
8. Wählen Sie **Host hinzufügen**.

## <a name="configure-the-edge-firewall"></a>Die Edge-Firewall konfigurieren

Der Edge-Firewall trennt den externen Umkreisnetzwerk über das öffentliche Internet. Eine visuelle Darstellung durch diese Trennung, finden Sie unter der Abbildung im Thema [immer auf VPN-Technologieübersicht](../always-on-vpn-technology-overview.md).

Der Edge-Firewall muss ermöglichen und bestimmte Ports bei der VPN-Server weiterleiten. Wenn Sie auf Ihrem Edge-Firewall (Network Address Translation, NAT) verwenden, müssen Sie möglicherweise die portweiterleitung für User Datagram Protocol (UDP) Ports: 500 und 4500 zu aktivieren. Weiterleiten Sie, diese Ports der IP-Adresse, die die externe Schnittstelle Ihres VPN-Servers zugewiesen ist.

Wenn das routing von Datenverkehr eingehend und Durchführen der NAT oder hinter dem VPN-Server, und klicken Sie dann, die Firewall-Regeln zum Zulassen von UDP öffnen Ports: 500 und 4500 eingehenden der externen IP-Adresse, die auf die öffentliche Schnittstelle auf dem VPN-Server angewendet.

In beiden Fällen sollten, wenn Ihre Firewall verschärfte paketinspektionen im entitätenkontext unterstützt, und Sie haben schwierigkeiten beim Herstellen von Verbindungen mit Clients Sie versuchen, entspannen Sie sich, oder deaktivieren eingehende paketuntersuchungen für IKE-Sitzungen.

Informationen zu diesen konfigurationsänderungen vornehmen finden Sie in Ihrer Firewalldokumentation.

## <a name="configure-the-internal-perimeter-network-firewall"></a>Konfigurieren der internen Umkreisnetzwerkfirewall

Die interne Umkreisnetzwerkfirewall trennt die Organisation/Unternehmensnetzwerk aus dem internen Netzwerk des Umkreisnetzwerks. Eine visuelle Darstellung durch diese Trennung, finden Sie unter der Abbildung im Thema [immer auf VPN-Technologieübersicht](../always-on-vpn-technology-overview.md).

In dieser Bereitstellung ist die Remote Access VPN-Server im Umkreisnetzwerk als RADIUS-Client konfiguriert.  Der VPN-Server sendet der RADIUS-Verkehr an den NPS mit dem Unternehmensnetzwerk verbunden und erhält auch aus den NPS RADIUS-Verkehr.

Konfigurieren Sie die Firewall so, dass RADIUS-Datenverkehr in beide Richtungen ermöglichen.

>[!NOTE]
>Der NPS-Server im Netzwerk der Organisation/Corporate (Unternehmen) fungiert als RADIUS-Server für die VPN-Server die RADIUS-Client ist. Weitere Informationen zu den RADIUS-Infrastruktur, finden Sie unter [(Network Policy Server, NPS)](../../../../../networking/technologies/nps/nps-top.md).

### <a name="radius-traffic-ports-on-the-vpn-server-and-nps-server"></a>RADIUS-Datenverkehr-Ports auf dem VPN-Server und NPS-Server

Standardmäßig überwachen NPS und VPN-RADIUS-Datenverkehr an Ports 1812, 1813, 1645 und 1646 für alle installierten Netzwerkadapter. Wenn Sie Windows-Firewall mit erweiterter Sicherheit bei der Installation von NPS aktivieren, werden Firewallausnahmen für diese Ports während des Installationsvorgangs für IPv6 und IPv4-Datenverkehr automatisch erstellt.

>[!IMPORTANT]
>Wenn Ihre Netzwerkzugriffsserver für das Senden von RADIUS-Verkehr über andere diese Standardwerte Ports konfiguriert sind, entfernen Sie die Ausnahmen, die in der Windows-Firewall mit erweiterter Sicherheit während der NPS-Installation erstellt, und erstellen Sie Ausnahmen für die Ports, denen Sie verwenden RADIUS-Verkehr.

### <a name="use-the-same-radius-ports-for-the-internal-perimeter-network-firewall-configuration"></a>Verwenden Sie die gleichen RADIUS-Ports für die interne Perimeter Firewall Netzwerkkonfiguration

Wenn Sie die Standardkonfiguration für RADIUS-Port auf dem VPN-Server und dem NPS-Server verwenden, stellen Sie sicher, dass Sie die folgenden Ports in der internen Umkreisnetzwerkfirewall öffnen:

- Ports UDP1812, UDP1813, UDP1645 und UDP1646

Wenn Sie nicht die Standard-RADIUS-Ports in der NPS-Bereitstellung verwenden, müssen Sie konfigurieren die Firewall für RADIUS-Datenverkehr an den Ports, die Sie verwenden. Weitere Informationen finden Sie unter [Konfigurieren von Firewalls für RADIUS-Verkehr](../../../../../networking/technologies/nps/nps-firewalls-configure.md).

## <a name="next-steps"></a>Nächste Schritte

[Schritt 6: Konfigurieren Sie Windows 10-Clientsysteme Always On-VPN-Verbindungen](vpn-deploy-client-vpn-connections.md): In diesem Schritt konfigurieren Sie die Windows 10-Clientcomputern für die Kommunikation mit dieser Infrastruktur mit einer VPN-Verbindung. Sie können mehrere Technologien verwenden, so konfigurieren Sie Windows 10-VPN-Clients, einschließlich Windows PowerShell, System Center Configuration Manager und Intune. Alle drei erfordern ein XML VPN-Profil so konfigurieren Sie die entsprechenden VPN-Einstellungen.