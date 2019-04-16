---
title: Planen der Always On VPN-Bereitstellung
description: Dieses Thema enthält Anweisungen für die Bereitstellung von Always On VPN in Windows Server 2016 Planung.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 3c9de3ec-4bbd-4db0-b47a-03507a315383
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 11/05/2018
ms.openlocfilehash: d629f04abda0ce22deb75e487f5b485f50a60a53
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067324"
---
# Schritt 1. Planen der Always On VPN-Bereitstellung

>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10


& #171;  [ **Vorherige:** erfahren Sie mehr über den Workflow für die Bereitstellung von Always On VPN](always-on-vpn-deploy-deployment.md)<br>
& #187;  [ **Weiter:** Schritt 2. Konfigurieren der Serverinfrastruktur](vpn-deploy-server-infrastructure.md)

In diesem Schritt starten Sie zum Planen und Vorbereiten der Always On VPN-Bereitstellung. Bevor Sie die RAS-Server-Rolle auf dem Computer, die Sie, zur Verwendung als VPN-Server beabsichtigen installieren, führen Sie die folgenden Aufgaben. Nach dem ordnungsgemäßen Planen können Sie Always On VPN bereitstellen und optional den bedingten Zugriff für VPN-Konnektivität mit Azure AD konfigurieren. 

[!INCLUDE [always-on-vpn-standard-config-considerations-include](../../../includes/always-on-vpn-standard-config-considerations-include.md)]


## Vorbereiten des RAS-Servers

Sie müssen auf dem Computer als VPN-Server verwendet die folgenden Schritte ausführen: 

- **Stellen Sie sicher, dass die VPN-Server-Software und Hardware-Konfiguration richtig ist**. Installieren Sie Windows Server 2016 auf dem Computer, den Sie als Remote Access VPN-Server verwenden möchten. Diese Server muss zwei physischen Netzwerkadapter installiert, eine Verbindung mit dem externen Umkreisnetzwerk und eine Verbindung mit dem internen Umkreisnetzwerk verfügen.

- **Ermitteln, welcher Netzwerkadapter verbindet auf das Internet und stellt eine Verbindung her welcher Netzwerkadapter auf Ihrem privaten Netzwerk**. Konfigurieren des Netzwerkadapters mit einer öffentliche IP-Adresse im Internet gerichtet, während der Adapter Intranet gerichteten eine IP-Adresse aus dem lokalen Netzwerk verwenden kann.

    >[!TIP]
    >Wenn Sie nicht auf das Umkreisnetzwerk eine öffentliche IP-Adresse verwenden lieber, können Sie der Edge-Firewall mit eine öffentliche IP-Adresse konfigurieren, und klicken Sie dann die Firewall zum Weiterleiten von VPN-Verbindungsanfragen an den VPN-Server konfigurieren.

- **Der VPN-Server mit dem Netzwerk verbinden**. Installieren des VPN-Servers auf einem Umkreisnetzwerk, zwischen der Edgefirewall und der Perimeterfirewall.

## Planen von Authentifizierungsmethoden

IKEv2 ist ein VPN-Tunneling-Protokoll im [Internet Engineering Task Force Request for Comments7296](https://datatracker.ietf.org/doc/rfc7296/)beschrieben. Der wichtigste Vorteil von IKEv2 ist, dass es Unterbrechung der zugrunde liegenden Netzwerkverbindung verträglich. Z. B. wenn einen vorübergehenden Ausfall in Verbindung oder wenn ein Benutzer ein Clientcomputers über verschiebt ein Netzwerk zu einem anderen, wenn die Netzwerkschnittstelle IKEv2 wiederherstellen die VPN-Verbindung automatisch wiederhergestellt – ohne Eingreifen des Benutzers.

>[!TIP]
>Sie können den Remote Access VPN-Server zur Unterstützung von IKEv2 Verbindungen beim auch deaktivieren nicht verwendete Protokolle konfigurieren, der der Server Security Speicherbedarf verringert. 

## Planen der IP-Adressen für Remoteclients

Sie können den VPN-Server zum Zuweisen von Adressen VPN-Clients von einer statischen Adresspool, den Sie konfigurieren oder IP-Adressen von einem DHCP-Server konfigurieren. 

## Vorbereiten der Umgebung

- **Stellen Sie sicher, dass Sie Berechtigungen zum Konfigurieren der externen Firewalls haben und dass Sie eine gültige öffentliche IP-Adresse verfügen**. Offene Ports auf der Firewall IKEv2-VPN-Verbindung zu unterstützen. Außerdem benötigen Sie eine öffentliche IP-Adresse, um Verbindungen von externen Clients zu akzeptieren.

- **Wählen Sie einen Bereich von statische IP-Adressen für VPN-Clients**. Bestimmen Sie die maximale Anzahl gleichzeitig aktiver VPN-Clients, die Sie unterstützen möchten. Planen Sie auch, einen Bereich von statischen IP-Adressen im internen Umkreisnetzwerk erfüllen diese Anforderung, nämlich der *statischen Adresse Speicherpool*. Wenn Sie DHCP zum Bereitstellen von IP-Adressen auf der internen DMZ verwenden, müssen Sie auch einen Ausschluss für die statischen IP-Adressen in DHCP erstellen.

- **Stellen Sie sicher, dass Sie Ihre öffentliche DNS-Zone bearbeiten können**. Fügen Sie DNS-Einträge an Ihre öffentlichen DNS-Domäne und Unterstützung für die VPN-Infrastruktur. 

- **Stellen Sie sicher, dass alle VPN-Benutzer Benutzerkonten in Active Directory-Benutzer \(AD DS\) haben**. Bevor Benutzer über VPN-Verbindungen mit dem Netzwerk verbinden können, müssen sie Benutzerkonten in ADDS haben.

## Vorbereiten der Routing und Firewall 

Den VPN-Server in das Umkreisnetzwerk, das das Umkreisnetzwerk in internen und externen Umkreisnetzwerke Partitionen zu installieren. Abhängig von Ihrer Netzwerkumgebung müssen Sie möglicherweise mehrere routing Änderungen vornehmen.

- **Portweiterleitung für \(Optional\) konfigurieren.** Die Edgefirewall die Ports und Protokolle IDs zugeordnet IKEv2-VPN öffnen und diese an den VPN-Server weiterleiten. In den meisten Umgebungen hierfür muss portweiterleitung konfigurieren. Universal Datagram Protocol (UDP) Ports 500 und 4500 in der VPN-Server umgeleitet.

- **Routing konfigurieren, damit die DNS-Server und VPN-Server mit dem Internet verbunden**. Diese Bereitstellung verwendet IKEv2 und Network Address Translation \(NAT\). Stellen Sie sicher, dass der VPN-Server alle erforderlichen internen Netzwerken und Netzwerkressourcen zugreifen kann. Die Netzwerk- oder eine Ressource aus der VPN-Server nicht erreichbar ist auch über VPN-Verbindungen von Remotestandorten nicht erreichbar.

Passen Sie in den meisten Umgebungen um das neue interne Umkreisnetzwerk zu erreichen, statische Routen auf der Edgefirewall und der VPN-Server ein. In komplexeren Umgebungen allerdings müssen Sie internen Routern statische Routen hinzufügen oder internen Firewall-Regeln für die VPN-Server und den Block von VPN-Clients zugeordneten IP-Adressen anpassen.

## Nächster Schritt
[Schritt 2. Konfigurieren der Server-Infrastruktur](vpn-deploy-server-infrastructure.md): In diesem Schritt installieren und Konfigurieren der serverseitigen Komponenten erforderlich, um die VPN-Unterstützung. Die serverseitige Komponenten umfassen konfigurieren PKI, um die vom Benutzer, der VPN-Server und dem Netzwerkrichtlinienserver verwendeten Zertifikate zu verteilen. 

---