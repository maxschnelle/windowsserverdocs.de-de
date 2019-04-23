---
title: Planen der Always On VPN-Bereitstellung
description: Dieses Thema enthält die Planung Anweisungen zum Bereitstellen von Always On-VPN-unter Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 3c9de3ec-4bbd-4db0-b47a-03507a315383
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 11/05/2018
ms.openlocfilehash: d629f04abda0ce22deb75e487f5b485f50a60a53
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881911"
---
# <a name="step-1-plan-the-always-on-vpn-deployment"></a>Schritt 1 Planen der Always On-VPN-Bereitstellung

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10


&#171;  [**Vorherige:** Erfahren Sie mehr über den Workflow für die Always On-VPN-Bereitstellung](always-on-vpn-deploy-deployment.md)<br>
&#187;  [**Next:** Schritt 2 Konfigurieren der Serverinfrastruktur](vpn-deploy-server-infrastructure.md)

In diesem Schritt starten Sie zum Planen und Vorbereiten der Always On-VPN-Bereitstellung. Bevor Sie die Remotezugriffs-Serverrolle auf dem Computer, die Sie zur Verwendung als VPN-Server planen installieren, werden führen Sie die folgenden Aufgaben aus. Nach dem ordnungsgemäßen Planen können Sie Always On VPN bereitstellen und optional den bedingten Zugriff für VPN-Konnektivität mit Azure AD konfigurieren. 

[!INCLUDE [always-on-vpn-standard-config-considerations-include](../../../includes/always-on-vpn-standard-config-considerations-include.md)]


## <a name="prepare-the-remote-access-server"></a>RAS-Server Vorbereiten

Sie müssen auf dem Computer, die als VPN-Server verwendet die folgenden Schritte ausführen: 

- **Stellen Sie sicher, dass die VPN-Server-Software und Hardware-Konfiguration korrekt ist**. Installieren Sie Windows Server 2016, auf dem Computer, den Sie einen Remote Access VPN-Server verwenden möchten. Dieser Server muss über zwei physische Netzwerkadapter installiert, eine Verbindung mit dem externen Umkreisnetzwerk, und eine für die Verbindung mit dem internen Umkreisnetzwerk verfügen.

- **Identifizieren der Netzwerkadapter mit dem Internet eine Verbindung herstellt, und der Netzwerkadapter mit dem privaten Netzwerk verbindet**. Konfigurieren Sie den Netzwerkadapter mit Internetzugriff mit einer öffentlichen IP-Adresse über das Internet, obwohl der Adapter mit dem Intranet eine IP-Adresse aus dem lokalen Netzwerk verwenden kann.

    >[!TIP]
    >Wenn Sie keine öffentliche IP-Adresse in Ihrem Umkreisnetzwerk verwenden möchten, können Sie der Edge-Firewall mit einer öffentlichen IP-Adresse konfigurieren und dann konfigurieren Sie die Firewall zum Weiterleiten von Anforderungen von VPN-Verbindung mit dem VPN-Server.

- **Den VPN-Server mit dem Netzwerk verbinden**. Installieren des VPN-Servers in einem Umkreisnetzwerk, zwischen der Edgefirewall und der Umkreisfirewall an.

## <a name="plan-authentication-methods"></a>Planen von Authentifizierungsmethoden

IKEv2 befindet sich ein VPN-Tunneling-Protokoll, die in beschriebenen [Internet Engineering Task Force Anforderung für Kommentare 7296](https://datatracker.ietf.org/doc/rfc7296/). Der wichtigste Vorteil von IKEv2 ist, dass es sich um Unterbrechungen in die zugrunde liegende Netzwerkverbindung toleriert. Z. B. Wenn einem vorübergehenden Dienstausfall in Verbindung, oder wenn ein Benutzer ein Clientcomputers von verschoben wird ein Netzwerk in ein anderes, wenn die Netzwerkverbindung IKEv2 datenträgeraktualisierung die VPN-Verbindung wird automatisch wiederhergestellt, ohne Eingreifen des Benutzers.

>[!TIP]
>Sie können den Remote Access VPN-Server zur Unterstützung von IKEv2-Verbindungen bei der Deaktivierung auch nicht verwendete Protokolle konfigurieren, der Sicherheitsbedarf des Servers reduziert. 

## <a name="plan-ip-addresses-for-remote-clients"></a>Planen der IP-Adressen für Remoteclients

Sie können die VPN-Server, um die Zuweisung von Adressen zu VPN-Clients über einen Pool statischer Adressen, den Sie konfigurieren oder IP-Adressen von DHCP-Server konfigurieren. 

## <a name="prepare-the-environment"></a>Vorbereiten der Umgebung

- **Stellen Sie sicher, dass Sie über Berechtigungen zum Konfigurieren der externen Firewalls verfügen und Sie eine gültige öffentliche IP-Adresse haben**. Öffnen von Ports in der Firewall zur Unterstützung von IKEv2-VPN-Verbindungen. Sie benötigen auch eine öffentliche IP-Adresse, um Verbindungen von externen Clients zu akzeptieren.

- **Wählen Sie einen Bereich von statischen IP-Adressen für VPN-Clients**. Bestimmen Sie die maximale Anzahl von gleichzeitigen VPN-Clients, die Sie unterstützen möchten. Planen Sie auch, einen Bereich von statischen IP-Adressen im internen Umkreisnetzwerk, die diese Anforderungen erfüllen, nämlich die *statischen Adresspool*. Wenn Sie DHCP verwenden, um die IP-Adressen in der internen DMZ bereitstellen, müssen Sie möglicherweise auch erstellen Sie einen Ausschluss für die statische IP-Adressen im DHCP.

- **Stellen Sie sicher, dass Sie Ihre öffentliche DNS-Zone bearbeiten können**. Der öffentliche DNS-Domäne zur Unterstützung der VPN-Infrastruktur-DNS-Datensätze hinzugefügt. 

- **Stellen Sie sicher, dass alle VPN-Benutzer von Benutzerkonten in Active Directory-Benutzer \(AD DS\)**. Bevor Benutzer über VPN-Verbindungen mit dem Netzwerk verbinden können, müssen sie Benutzerkonten in AD DS zugreifen.

## <a name="prepare-routing-and-firewall"></a>Vorbereiten von Routing und die Firewall 

Installieren des VPN-Servers im Umkreisnetzwerk, die im Umkreisnetzwerk in interne und externe Umkreisnetzwerken partitioniert. Je nach Netzwerkumgebung müssen Sie mehrere routing Änderungen vornehmen.

- **\(Optionale\) Weiterleitung konfigurieren.** Die Edgefirewall öffnen, die Ports und Protokolle zugeordneten ein IKEv2-VPN-IDs und an den VPN-Server weitergeleitet werden. In den meisten Umgebungen erfordert dies also Weiterleitung zu konfigurieren. Umleiten Sie universelle Datagram Protocol (UDP) Ports: 500 und 4500 an den VPN-Server.

- **Konfigurieren des Routings, damit die DNS-Server und VPN-Server im Internet erreichen**. Diese Bereitstellung verwendet wird, IKEv2 "und" Network Address Translation \(NAT\). Stellen Sie sicher, dass der VPN-Server alle erforderlichen interne Netzwerke und Netzwerkressourcen erreichen kann. Die Netzwerk- oder Ressource, die von der VPN-Server nicht erreichbar ist auch über VPN-Verbindungen von Remotestandorten aus nicht erreichbar.

Passen Sie in den meisten Umgebungen um die neuen internen Umkreisnetzwerk zu erreichen, statische Routen, die auf der Edge-Firewall und der VPN-Server ein. In komplexeren Umgebungen allerdings müssen Sie interne Router statische Routen hinzu, oder passen Sie die interne Firewall-Regeln für die VPN-Server und der Block von IP-Adressen mit VPN-Clients.

## <a name="next-step"></a>Nächster Schritt
[Schritt 2. Konfigurieren die Serverinfrastruktur](vpn-deploy-server-infrastructure.md): In diesem Schritt installieren und konfigurieren Sie die serverseitigen Komponenten erforderlich, um das VPN zu unterstützen. Die serverseitigen Komponenten ist die Konfiguration von PKI zum Verteilen der von dem Benutzer, dem VPN-Server und dem NPS-Server verwendeten Zertifikate umfassen. 

---