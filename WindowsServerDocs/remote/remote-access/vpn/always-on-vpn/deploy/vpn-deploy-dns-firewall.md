---
title: Konfigurieren von DNS und Firewall-Einstellungen
description: Dieses Thema enthält ausführliche Anweisungen für die Bereitstellung von Always On VPN in Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: d8cf3bae-45bf-4ffa-9205-290d555c59da
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 06/11/2018
ms.openlocfilehash: f57bfa005ef1af2556e4bd1cbb90ef8d3cfd22e3
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067319"
---
# Schritt 5. Konfigurieren von DNS- und Firewall-Einstellungen

>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **Vorherigen:** Schritt 4. Installieren und Konfigurieren von NPS-Servers](vpn-deploy-nps.md)<br>
& #187;  [ **Weiter:** Schritt 6 fort. Konfigurieren von Windows 10-Client immer auf VPN-Verbindungen](vpn-deploy-client-vpn-connections.md)

In diesem Schritt konfigurieren Sie DNS und Firewall-Einstellungen für VPN-Konnektivität.

## Konfigurieren der DNS-namensauflösung

Wenn remote-VPN-Clients zu verbinden, verwenden sie die gleichen DNS-Server, die Ihre interne Clients verwenden, können sie zur Auflösung von Namen auf die gleiche Weise wie der Rest der Ihre internen Arbeitsstationen. 

Aus diesem Grund müssen Sie sicherstellen, dass der Computername, die externe Clients verwenden, um die Verbindung mit dem VPN-Server den alternativen Antragstellernamen in der VPN-Server ausgestellten Zertifikate definierten entspricht.

Um sicherzustellen, dass Remoteclients Ihrer VPN-Server herstellen können, können Sie einen DNS A (Host)-Eintrag in Ihre externe DNS-Zone erstellen. A-Eintrag sollte das Zertifikat alternative Antragstellernamen für die VPN-Server verwenden.


### Um einen Host hinzufügen \ (A oder AAAA\) Ressourceneintrag für eine Zone

1. Klicken Sie auf einem DNS-Server im Server-Manager auf **Extras**, und klicken Sie dann auf **DNS**. DNS-Manager wird geöffnet.
2. Klicken Sie in der Konsolenstruktur DNS-Manager auf dem Server, den Sie verwalten möchten.
3. Klicken Sie im Detailbereich im **Namen**, Double\ Mausklick **Forward-Lookupzonen** , um die Ansicht zu erweitern.
4. In den **Forward-Lookupzonen** -Details, Right\ Klick forward-Lookupzone, fügen Sie einen Datensatz, und klicken Sie auf werden sollen **Neuer Host \(A or AAAA\)**. Das Dialogfeld **Neuer Host** wird geöffnet.
5. Geben Sie im **Neuen Host**im **Namen**den Zertifikat Alternativer Antragstellername des VPN-Servers.
6. Geben Sie die IP-Adresse für den VPN-Server, IP-Adresse. Geben Sie die Adresse im IP-Version 4 (IPv4) Format zum Hinzufügen eines Hostressourceneintrags \(A\) oder IP-Version 6 \(IPv6\) Format zum Hinzufügen eines Hostressourceneintrags \(AAAA\).
7. Wenn Sie eine reverse-Lookupzone für einen Bereich von IP-Adressen erstellt, einschließlich IP-Adresse, die Sie eingegeben haben, wählen Sie dann das Kontrollkästchen **verknüpften Zeiger (PTR)-Eintrag erstellen** .  Diese Option erstellt einen zusätzliche Zeiger \(PTR\) Ressourceneintrag in einer reverse-Zone für diesen Host, basierend auf den Informationen, die, den Sie im **Namen** und **IP-Adresse**eingegeben haben.
8. Klicken Sie auf **Host hinzufügen**.

## Konfigurieren der Edgefirewall

Die Edge-Firewall trennt externe Umkreisnetzwerk vom öffentlichen Internet. Eine visuelle Darstellung der diese Trennung finden Sie in der Abbildung im Thema [Always On VPN-Technologie Overview](../always-on-vpn-technology-overview.md).

Der Edge-Firewall muss ermöglichen und bestimmte Ports zu Ihrer VPN-Server weitergeleitet. Wenn Sie in der Edgefirewall Network Address Translation \(NAT\) verwenden, müssen Sie möglicherweise portweiterleitung User Datagram Protocol \(UDP\) ports500 und 4500 aktivieren. Weiterleiten von diese Ports zur IP-Adresse, die die externe Schnittstelle des VPN-Server zugewiesen wird.

Wenn Sie Datenverkehr weiterleiten können eingehende und NAT an oder hinter der VPN-Server ausführen, müssen Sie Ihre Firewall-Regeln, um UDP-ports500 ermöglichen öffnen und 4500 eingehende auf die externe IP-Adresse für die öffentliche Schnittstelle auf dem VPN-Server angewendet.

In beiden Fällen sollten, wenn Ihre Firewall tiefgehende unterstützt und Sie haben Probleme bei der Herstellung Clientverbindungen, Sie versuchen, lockern oder deep-Packet Überprüfung bei IKE-Sitzungen zu deaktivieren.

Informationen zur Verwendung dieser konfigurationsänderungen vornehmen finden Sie unter der Firewall-Dokumentation.

## Konfigurieren Sie die interne Perimeter Netzwerk-Firewall

Die interne Perimeter Netzwerk-Firewall trennt die Organisation /-Unternehmensnetzwerk von internen Umkreisnetzwerk. Eine visuelle Darstellung der diese Trennung finden Sie in der Abbildung im Thema [Always On VPN-Technologie Overview](../always-on-vpn-technology-overview.md).

In dieser Bereitstellung ist der Remote Access VPN-Server auf das Umkreisnetzwerk als RADIUS-Clients konfiguriert.  Der VPN-Server sendet den RADIUS-Datenverkehr an den NPS im Unternehmensnetzwerk und auch von der NPS RADIUS-Datenverkehr empfängt.

Konfigurieren des Firewalls RADIUS-Datenverkehr in beide Richtungen zulassen.


>[!NOTE]
>Die NPS-Servers für die Organisation/Corporate Netzwerkfunktionen als RADIUS-Server für den VPN-Server, der RADIUS-Client ist. Weitere Informationen zu den RADIUS-Infrastruktur finden Sie unter [(Network Policy Server, NPS)](../../../../../networking/technologies/nps/nps-top.md).

### RADIUS-Datenverkehr Ports auf dem VPN-Server und NPS-Servers

Standardmäßig überwachen NPS und VPN-RADIUS-Datenverkehr auf Ports 1812, 1813, 1645 und 1646 auf alle installierten Netzwerkadapter. Wenn Sie Windows-Firewall mit erweiterter Sicherheit beim Installieren von NPS aktivieren, erhalten Firewallausnahmen für diese Ports während des Installationsprozesses für IPv4- und IPv6-Datenverkehr automatisch erstellt.

>[!IMPORTANT]
>Wenn Server für den Netzwerkzugriff zum Senden von RADIUS-Datenverkehr über Ports als diese Standardwerte konfiguriert sind, entfernen Sie die Ausnahmen in Windows-Firewall mit erweiterter Sicherheit während der Installation von NPS erstellt haben, und erstellen Sie Ausnahmen für die Ports, denen Sie verwenden RADIUS-Datenverkehr.

### Verwenden Sie dieselben RADIUS-Ports für die interne Perimeter Netzwerk-Firewall-Konfiguration

Wenn Sie die Standardkonfiguration für RADIUS-Port auf dem VPN-Server und dem Netzwerkrichtlinienserver verwenden, stellen Sie sicher, dass Sie die folgenden Ports auf dem internen Perimeter Netzwerk-Firewall öffnen:

- Ports UDP1812, UDP1813, UDP1645 und UDP1646

Wenn Sie nicht die standardmäßigen RADIUS-Ports in der NPS-Bereitstellung verwenden, müssen Sie konfigurieren den Firewall für RADIUS-Datenverkehr über die Ports, die Sie verwenden. Weitere Informationen finden Sie unter [Konfigurieren von Firewalls für RADIUS-Datenverkehr](../../../../../networking/technologies/nps/nps-firewalls-configure.md).

## Nächster Schritt
[Schritt 6 fort. Konfigurieren von Windows 10-Client immer auf VPN-Verbindungen](vpn-deploy-client-vpn-connections.md): In diesem Schritt konfigurieren Sie die Windows 10-Clientcomputern für die Kommunikation mit dieser Infrastruktur mit einer VPN-Verbindung. Sie können verschiedene Technologien zum Konfigurieren von Windows 10-VPN-Clients, einschließlich Windows PowerShell, System Center Configuration Manager und Intune verwenden. Alle drei erfordern eine XML-VPN-Profil so konfigurieren Sie die entsprechenden VPN-Einstellungen. 

---
