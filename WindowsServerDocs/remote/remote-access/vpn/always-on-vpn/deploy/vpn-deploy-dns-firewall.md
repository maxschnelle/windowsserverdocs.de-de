---
title: Konfigurieren von DNS und Firewall-Einstellungen
description: Dieses Thema enthält ausführliche Anweisungen zum Bereitstellen von Always on-VPN in Windows Server 2016.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: d8cf3bae-45bf-4ffa-9205-290d555c59da
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 06/11/2018
ms.openlocfilehash: aa7658587b8434bfbaa6874498215a6b2c9213be
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822663"
---
# <a name="step-5-configure-dns-and-firewall-settings"></a>Schritt 5 Konfigurieren von DNS-und Firewalleinstellungen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorheriges:** Schritt 4: Installieren und Konfigurieren des NPS-Servers](vpn-deploy-nps.md)
- [**Weiter:** Schritt 6: Konfigurieren von Windows 10-Client Always on-VPN-Verbindungen](vpn-deploy-client-vpn-connections.md)

In diesem Schritt konfigurieren Sie DNS-und Firewalleinstellungen für VPN-Konnektivität.

## <a name="configure-dns-name-resolution"></a>Konfigurieren der DNS-Namensauflösung

Wenn Remote-VPN-Clients eine Verbindung herstellen, verwenden Sie die gleichen DNS-Server, die von den internen Clients verwendet werden. auf diese Weise können Namen auf die gleiche Weise wie die übrigen internen Arbeitsstationen aufgelöst werden.

Aus diesem Grund müssen Sie sicherstellen, dass der Computername, den externe Clients zum Herstellen einer Verbindung mit dem VPN-Server verwenden, dem alternativen Antragsteller Namen entspricht, der in für den VPN-Server ausgestellten Zertifikaten definiert ist.

Um sicherzustellen, dass Remote Clients eine Verbindung mit dem VPN-Server herstellen können, können Sie einen DNS a-Datensatz (Host) in der externen DNS-Zone erstellen. Der A-Datensatz sollte den alternativen Antragsteller Namen des Zertifikats für den VPN-Server verwenden.

### <a name="to-add-a-host-a-or-aaaa-resource-record-to-a-zone"></a>So fügen Sie einer Zone einen Host Ressourcen Daten Satz (a oder AAAA) hinzu

1. Wählen Sie auf einem DNS-Server in Server-Manager Extras aus, und **Wählen Sie dann** **DNS**aus. Der DNS-Manager wird geöffnet.
2. Wählen Sie in der Konsolen Struktur des DNS-Managers den Server aus, den Sie verwalten möchten.
3. Doppelklicken Sie im Detailbereich unter **Name**auf Forward- **Lookupzonen** , um die Ansicht zu erweitern.
4. Klicken Sie in Details der **Forward-Lookupzonen** mit der rechten Maustaste auf die Forward-Lookupzone, der Sie einen Datensatz hinzufügen möchten, und wählen Sie dann **neuer Host (a oder AAAA)** aus. Das Dialogfeld **neuer Host** wird geöffnet.
5. Geben Sie im Feld **neuer Host**unter **Name**den alternativen Antragsteller Namen des Zertifikats für den VPN-Server ein.
6. Geben Sie unter IP-Adresse die IP-Adresse für den VPN-Server ein. Sie können die Adresse im IPv4-Format (IP Version 4) eingeben, um einen Host-(a) Ressourcen Daten Satz oder ein IPv6-Format (IP Version 6) zum Hinzufügen eines Host Ressourceneinsatzes (AAAA) hinzuzufügen.
7. Wenn Sie für einen Bereich von IP-Adressen eine Reverse-Lookupzone erstellt haben, einschließlich der eingegebenen IP-Adresse, aktivieren Sie das Kontrollkästchen **zugeordneten Zeiger erstellen (PTR-Datensatz)** .  Wenn Sie diese Option auswählen, wird ein zusätzlicher Zeiger (PTR)-Ressourcen Daten Satz in einer umgekehrten Zone für diesen Host erstellt, basierend auf den Informationen, die Sie unter **Name** und **IP-Adresse**eingegeben haben.
8. Wählen Sie **Host hinzufügen**aus.

## <a name="configure-the-edge-firewall"></a>Konfigurieren der Edge-Firewall

Die Edge-Firewall trennt das externe Umkreis Netzwerk vom öffentlichen Internet. Eine visuelle Darstellung dieser Trennung finden Sie in der Abbildung im Thema [Always on VPN-Technologie Übersicht](../always-on-vpn-technology-overview.md).

Ihre Edge-Firewall muss bestimmte Ports an Ihren VPN-Server zulassen und weiterleiten. Wenn Sie die Netzwerk Adressübersetzung (Network Address Translation, NAT) in ihrer Edge-Firewall verwenden, müssen Sie möglicherweise die Port Weiterleitung für UDP (User Datagram Protocol)-Ports 500 und 4500 aktivieren. Leiten Sie diese Ports an die IP-Adresse weiter, die der externen Schnittstelle des VPN-Servers zugewiesen ist.

Wenn Sie eingehenden Datenverkehr weiterleiten und NAT auf dem VPN-Server ausführen, müssen Sie die Firewallregeln öffnen, damit die UDP-Ports 500 und 4500 in der externen IP-Adresse eingehenden können, die auf die öffentliche Schnittstelle auf dem VPN-Server angewendet wird.

Wenn Ihre Firewall eine umfassende Paket Untersuchung unterstützt und Probleme beim Einrichten von Clientverbindungen auftreten, sollten Sie versuchen, die umfassende Paketüberprüfung für IKE-Sitzungen zu lockern oder zu deaktivieren.

Informationen dazu, wie Sie diese Konfigurationsänderungen vornehmen, finden Sie in der Firewalldokumentation.

## <a name="configure-the-internal-perimeter-network-firewall"></a>Konfigurieren der Firewall für das interne Umkreis Netzwerk

Die interne Umkreis Netzwerk Firewall trennt die Organisation/das Unternehmensnetzwerk vom internen Umkreis Netzwerk. Eine visuelle Darstellung dieser Trennung finden Sie in der Abbildung im Thema [Always on VPN-Technologie Übersicht](../always-on-vpn-technology-overview.md).

In dieser Bereitstellung wird der RAS-VPN-Server im Umkreis Netzwerk als RADIUS-Client konfiguriert.  Der VPN-Server sendet RADIUS-Datenverkehr an den NPS im Unternehmensnetzwerk und empfängt RADIUS-Datenverkehr aus dem NPS.

Konfigurieren Sie die Firewall so, dass RADIUS-Datenverkehr in beide Richtungen fließen kann.

>[!NOTE]
>Der NPS-Server im Organisations-/Unternehmensnetzwerk fungiert als RADIUS-Server für den VPN-Server, bei dem es sich um einen RADIUS-Client handelt. Weitere Informationen zur RADIUS-Infrastruktur finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](../../../../../networking/technologies/nps/nps-top.md).

### <a name="radius-traffic-ports-on-the-vpn-server-and-nps-server"></a>RADIUS-datenverkehrsports auf dem VPN-Server und dem NPS-Server

Standardmäßig lauschen NPS und VPN auf den Ports 1812, 1813, 1645 und 1646 auf den RADIUS-Datenverkehr auf allen installierten Netzwerkadaptern. Wenn Sie die Windows-Firewall mit erweiterter Sicherheit bei der Installation von NPS aktivieren, werden Firewallausnahmen für diese Ports während des Installationsvorgangs für IPv6-und IPv4-Datenverkehr automatisch erstellt.

>[!IMPORTANT]
>Wenn Ihre Netzwerk Zugriffs Server für das Senden von RADIUS-Datenverkehr über andere Ports als diese Standardeinstellungen konfiguriert sind, entfernen Sie die Ausnahmen, die bei der NPS-Installation unter Windows-Firewall mit erweiterter Sicherheit erstellt wurden, und erstellen Sie Ausnahmen für die Ports, die Sie für RADIUS-Datenverkehr.

### <a name="use-the-same-radius-ports-for-the-internal-perimeter-network-firewall-configuration"></a>Verwenden Sie die gleichen RADIUS-Ports für die Firewallkonfiguration des internen Umkreis Netzwerks.

Wenn Sie die Standardkonfiguration des RADIUS-Ports auf dem VPN-Server und dem NPS-Server verwenden, stellen Sie sicher, dass Sie die folgenden Ports in der internen Umkreis Netzwerk Firewall öffnen:

- Ports UDP1812, UDP1813, UDP1645 und UDP1646

Wenn Sie nicht die Standardradius-Ports in der NPS-Bereitstellung verwenden, müssen Sie die Firewall so konfigurieren, dass RADIUS-Datenverkehr für die von Ihnen verwendeten Ports zugelassen wird. Weitere Informationen finden Sie unter [Konfigurieren von Firewalls für RADIUS-Datenverkehr](../../../../../networking/technologies/nps/nps-firewalls-configure.md).

## <a name="next-steps"></a>Nächste Schritte

[Schritt 6: Konfigurieren von Windows 10-Client-Always on-VPN-Verbindungen](vpn-deploy-client-vpn-connections.md): in diesem Schritt konfigurieren Sie die Windows 10-Client Computer für die Kommunikation mit dieser Infrastruktur über eine VPN-Verbindung. Sie können verschiedene Technologien zum Konfigurieren von Windows 10-VPN-Clients verwenden, einschließlich Windows PowerShell, Microsoft Endpoint Configuration Manager und InTune. Alle drei erfordern ein XML-VPN-Profil, um die entsprechenden VPN-Einstellungen zu konfigurieren.