---
title: Planen der Always On VPN-Bereitstellung
description: Dieses Thema enthält Planungs Anweisungen für die Bereitstellung von Always on-VPN in Windows Server 2016.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 3c9de3ec-4bbd-4db0-b47a-03507a315383
ms.localizationpriority: medium
ms.author: v-tea
author: Teresa-MOTIV
ms.date: 11/05/2018
ms.openlocfilehash: c1e85f2ee44d241bdc04e63d20de36e5cdeafb1a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814493"
---
# <a name="step-1-plan-the-always-on-vpn-deployment"></a>Schritt 1 Planen der Always On VPN-Bereitstellung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorheriges:** Erfahren Sie mehr über den Workflow für die Bereitstellung Always on VPN](always-on-vpn-deploy-deployment.md)
- [**Weiter:** Schritt 2: Konfigurieren der Server Infrastruktur](vpn-deploy-server-infrastructure.md)

In diesem Schritt beginnen Sie mit der Planung und Vorbereitung ihrer Always on-VPN-Bereitstellung. Bevor Sie die Remote Zugriffs-Server Rolle auf dem Computer installieren, den Sie als VPN-Server verwenden möchten, führen Sie die folgenden Aufgaben aus. Nach dem ordnungsgemäßen Planen können Sie Always On VPN bereitstellen und optional den bedingten Zugriff für VPN-Konnektivität mit Azure AD konfigurieren.

[!INCLUDE [always-on-vpn-standard-config-considerations-include](../../../includes/always-on-vpn-standard-config-considerations-include.md)]

## <a name="prepare-the-remote-access-server"></a>Vorbereiten des Remote Zugriffs Servers

Sie müssen auf dem Computer, der als VPN-Server verwendet wird, folgende Schritte ausführen:

- **Stellen Sie sicher, dass die VPN-Server Software und die Hardwarekonfiguration korrekt sind**. Installieren Sie Windows Server 2016 auf dem Computer, den Sie als RAS-VPN-Server verwenden möchten. Auf diesem Server müssen zwei physische Netzwerkadapter installiert sein, eine zum Herstellen einer Verbindung mit dem externen Umkreis Netzwerk und eine, um eine Verbindung mit dem internen Umkreis Netzwerk herzustellen.

- **Identifizieren Sie, welcher Netzwerkadapter eine Verbindung mit dem Internet herstellt und welcher Netzwerkadapter eine Verbindung mit Ihrem privaten Netzwerk**herstellt. Konfigurieren Sie den Netzwerkadapter für das Internet mit einer öffentlichen IP-Adresse, während der Adapter für das Intranet eine IP-Adresse aus dem lokalen Netzwerk verwenden kann.

    >[!TIP]
    >Wenn Sie nicht möchten, dass Sie eine öffentliche IP-Adresse in Ihrem Umkreis Netzwerk verwenden, können Sie die Edge-Firewall mit einer öffentlichen IP-Adresse konfigurieren und dann die Firewall so konfigurieren, dass VPN-Verbindungsanforderungen an den VPN-Server weiterleiten.

- **Verbinden Sie den VPN-Server mit dem Netzwerk**. Installieren Sie den VPN-Server in einem Umkreis Netzwerk zwischen der Edge-Firewall und der Umkreis Firewall.

## <a name="plan-authentication-methods"></a>Planen von Authentifizierungsmethoden

IKEv2 ist ein VPN-Tunnelingprotokoll, das in [Internet Engineering Task Force Request for Comments 7296](https://datatracker.ietf.org/doc/rfc7296/)beschrieben wird. Der Hauptvorteil von IKEv2 besteht darin, dass Unterbrechungen in der zugrunde liegenden Netzwerkverbindung toleriert werden. Wenn z. b. ein vorübergehender Verbindungsverlust oder ein Benutzer einen Client Computer von einem Netzwerk auf einen anderen verschiebt, stellt beim erneuten Herstellen der Netzwerkverbindung die VPN-Verbindung automatisch – ohne Benutzereingriff wieder her.

>[!TIP]
>Sie können den RAS-VPN-Server so konfigurieren, dass IKEv2-Verbindungen unterstützt werden, während nicht verwendete Protokolle deaktiviert werden, wodurch die Sicherheitsanforderungen des Servers reduziert werden. 

## <a name="plan-ip-addresses-for-remote-clients"></a>Planen von IP-Adressen für Remote Clients

Sie können den VPN-Server so konfigurieren, dass er VPN-Clients Adressen von einem statischen Adresspool, den Sie konfigurieren, oder von IP-Adressen eines DHCP-Servers zuweist. 

## <a name="prepare-the-environment"></a>Vorbereiten der Umgebung

- **Stellen Sie sicher, dass Sie über die Berechtigungen zum Konfigurieren der externen Firewall verfügen und dass Sie über eine gültige öffentliche IP-Adresse verfügen**. Öffnen von Ports in der Firewall zur Unterstützung von IKEv2-VPN-Verbindungen. Außerdem benötigen Sie eine öffentliche IP-Adresse, um Verbindungen von externen Clients zu akzeptieren.

- **Wählen Sie einen Bereich statischer IP-Adressen für VPN-Clients aus**. Bestimmen Sie die maximale Anzahl von gleichzeitigen VPN-Clients, die Sie unterstützen möchten. Planen Sie außerdem einen Bereich statischer IP-Adressen im internen Umkreis Netzwerk, um diese Anforderung zu erfüllen, nämlich den *statischen Adresspool*. Wenn Sie DHCP zum Angeben von IP-Adressen für die interne DMZ verwenden, müssen Sie möglicherweise auch einen Ausschluss für diese statischen IP-Adressen in DHCP erstellen.

- **Stellen Sie sicher, dass Sie die öffentliche DNS-Zone bearbeiten können**. Fügen Sie Ihrer öffentlichen DNS-Domäne DNS-Einträge zur Unterstützung der VPN-Infrastruktur hinzu. 

- **Stellen Sie sicher, dass alle VPN-Benutzer über Benutzerkonten in Active Directory Benutzer (AD DS) verfügen**. Bevor Benutzer über VPN-Verbindungen eine Verbindung mit dem Netzwerk herstellen können, müssen Sie über Benutzerkonten in AD DS verfügen.

## <a name="prepare-routing-and-firewall"></a>Vorbereiten von Routing und Firewall 

Installieren Sie den VPN-Server innerhalb des Umkreis Netzwerks, von dem das Umkreis Netzwerk in interne und externe Umkreis Netzwerke partitioniert wird. Abhängig von Ihrer Netzwerkumgebung müssen Sie möglicherweise mehrere Routing Änderungen vornehmen.

- **Optionale Konfigurieren Sie die Port Weiterleitung.** Die Edge-Firewall muss die einem IKEv2-VPN zugeordneten Ports und Protokoll-IDs öffnen und Sie an den VPN-Server weiterleiten. In den meisten Umgebungen erfordert dies, dass Sie die Port Weiterleitung konfigurieren. Leiten Sie die UDP-Ports 500 und 4500 an den VPN-Server um.

- **Konfigurieren Sie das Routing so, dass die DNS-Server und VPN-Server das Internet erreichen können**. Diese Bereitstellung verwendet IKEv2 und Network Address Translation (NAT). Stellen Sie sicher, dass der VPN-Server alle erforderlichen internen Netzwerke und Netzwerkressourcen erreichen kann. Netzwerk oder Ressourcen, die vom VPN-Server nicht erreichbar sind, sind auch über VPN-Verbindungen von Remote Standorten aus nicht erreichbar.

In den meisten Umgebungen können Sie zum Erreichen des neuen internen Umkreis Netzwerks statische Routen auf der Edge-Firewall und dem VPN-Server anpassen. In komplexeren Umgebungen müssen Sie jedoch möglicherweise statische Routen zu internen Routern hinzufügen oder interne Firewallregeln für den VPN-Server und den Block von IP-Adressen, die VPN-Clients zugeordnet sind, anpassen.

## <a name="next-steps"></a>Nächste Schritte

[Schritt 2: Konfigurieren der Serverinfrastruktur](vpn-deploy-server-infrastructure.md): in diesem Schritt installieren und konfigurieren Sie die serverseitigen Komponenten, die zur Unterstützung des VPN erforderlich sind. Zu den serverseitigen Komponenten gehört das Konfigurieren der PKI für die Verteilung der Zertifikate, die von Benutzern, dem VPN-Server und dem NPS-Server verwendet werden.