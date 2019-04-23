---
title: Always On VPN bereitstellen
description: Dieses Thema enthält detaillierte Anweisungen zum Bereitstellen von Always On-VPN-unter Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ad748de2-d175-47bf-b05f-707dc48692cf
ms.localizationpriority: medium
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 15c60f2986d3837c5c6e03f9e0a25c7e0a4e0cc0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867141"
---
# <a name="deploy-always-on-vpn"></a>Always On VPN bereitstellen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

&#0171;[ **Vorherigen:** Erfahren Sie mehr über die Always On-VPN-erweiterte features](always-on-vpn-adv-options.md)<br>
&#0187;[ **Weiter:** Schritt 1 Planen der Always On-VPN-Bereitstellung](always-on-vpn-deploy-planning.md)

In diesem Abschnitt erfahren Sie, über den Workflow für die Bereitstellung von Always On-VPN-Verbindungen für die remote-Domäne eingebundenen Windows 10-Clientcomputern. Wenn Sie möchten **Konfigurieren des bedingten Zugriffs** Replikationslink wie VPN-Benutzer Ihre Ressourcen zugreifen, finden Sie unter [für bedingten Zugriff für VPN-Verbindungen mithilfe von Azure AD](../../ad-ca-vpn-connectivity-windows10.md). Weitere Informationen zum bedingten Zugriff für VPN-Verbindungen mithilfe von Azure AD finden Sie unter [Bedingter Zugriff in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). 


Das folgende Diagramm veranschaulicht den Workflow-Prozess für die verschiedenen Szenarien, bei der Always On-VPN-Bereitstellung: 

_Klicken Sie zum Vergrößern auf_.

<a href="../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow.png" alt="Full-sized view of the Always On VPN deployment workflow" target="_blank">![Miniaturansicht](../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow-sm.png)
</a> 

>[!IMPORTANT]
>Für diese Bereitstellung ist es nicht erforderlich, dass Ihre Infrastrukturserver, z. B. Computer mit Active Directory Domain Services, Active Directory Certificate Services und Network Policy Server, Windows Server 2016 ausgeführt werden. Sie können die frühere Versionen von Windows-Server, z. B. Windows Server 2012 R2 verwenden, für die Infrastrukturserver und für den Server, der den Remotezugriff ausgeführt wird.

## <a name="step-1-plan-the-always-on-vpn-deploymentalways-on-vpn-deploy-planningmd"></a>[Schritt 1. Planen der Always On-VPN-Bereitstellung](always-on-vpn-deploy-planning.md)

In diesem Schritt starten Sie zum Planen und Vorbereiten der Always On-VPN-Bereitstellung. Bevor Sie die Remotezugriffs-Serverrolle auf dem Computer, die Sie zur Verwendung als VPN-Server planen installieren. Nach dem ordnungsgemäßen Planen können Sie Always On VPN bereitstellen und optional den bedingten Zugriff für VPN-Konnektivität mit Azure AD konfigurieren.

## <a name="step-2-configure-the-always-on-vpn-server-infrastructurevpn-deploy-server-infrastructuremd"></a>[Schritt 2. Konfigurieren der Always On-VPN-Server-Infrastruktur](vpn-deploy-server-infrastructure.md)

In diesem Schritt installieren und konfigurieren Sie die serverseitigen Komponenten erforderlich, um das VPN zu unterstützen. Die serverseitigen Komponenten ist die Konfiguration von PKI zum Verteilen der von dem Benutzer, dem VPN-Server und dem NPS-Server verwendeten Zertifikate umfassen.  Außerdem konfigurieren Sie RRAS, um IKEv2-Verbindungen und der NPS-Server für die Autorisierung für die VPN-Verbindungen zu unterstützen.

Um die Serverinfrastruktur zu konfigurieren, müssen Sie die folgenden Aufgaben ausführen:
- **Auf einem Server mit Active Directory Domain Services konfiguriert:** Aktivieren Sie der automatischen Registrierung von Zertifikaten in der Gruppenrichtlinie für Computer und Benutzer, erstellen Sie die Gruppe der VPN-Benutzer, der VPN-Servers-Gruppe und der NPS-Servers-Gruppe und jede Gruppe fügen Sie Mitglieder hinzu.
- **Auf einem Active Directory Certificate Server Zertifizierungsstelle:** Erstellen Sie die Zertifikatvorlagen Benutzerauthentifizierung, VPN-Server-Authentifizierung und NPS-Server-Authentifizierung.
- **Auf die Domäne eingebundenen Windows 10-Clients:** Registrieren, und Überprüfen von Benutzerzertifikaten.

## <a name="step-3-configure-the-remote-access-server-for-always-on-vpnvpn-deploy-rasmd"></a>[Schritt 3. Konfigurieren der RAS-Server für Always On-VPN](vpn-deploy-ras.md)

In diesem Schritt konfigurieren Sie RAS-VPN IKEv2-VPN-Verbindungen zulassen, verweigern Verbindungen von anderen VPN-Protokolle und zuweisen einen statischen IP-Adresspool für die Ausstellung von IP-Adressen zum Herstellen einer Verbindung autorisierte VPN-Clients.

Um RAS konfigurieren zu können, müssen Sie die folgenden Aufgaben ausführen:
- Registrieren Sie und überprüfen Sie des VPN-Server-Zertifikats
- Installieren und Konfigurieren von Remote Access VPN

## <a name="step-4-install-and-configure-the-nps-servervpn-deploy-npsmd"></a>[Schritt 4. Installieren und Konfigurieren des NPS-Servers](vpn-deploy-nps.md)

In diesem Schritt installieren Sie Windows-Verwaltungsinstrumentation (Network Policy Server, NPS) mit Windows PowerShell oder die Rollen von Server-Manager hinzufügen und Features-Assistenten. Außerdem konfigurieren Sie NPS zum Behandeln aller Authentifizierung, Autorisierung und Kontoführung von Aufgaben für die Anforderung für die Verbindung, die von der VPN-Server empfangen.

Um NPS zu konfigurieren, müssen Sie die folgenden Aufgaben ausführen:
- Registrieren Sie den NPS-Server in Active Directory.
- Konfigurieren Sie RADIUS-Kontoführung für den NPS-Server
- Fügen Sie den VPNServer als RADIUS-Client auf dem Netzwerkrichtlinienserver
- Konfigurieren der Netzwerkrichtlinie auf dem Netzwerkrichtlinienserver
- Automatisch registrieren des NPS-Serverzertifikats

## <a name="step-5-configure-dns-and-firewall-settings-for-always-on-vpnvpn-deploy-dns-firewallmd"></a>[Schritt 5. Konfigurieren von DNS und Firewall-Einstellungen für Always On-VPN](vpn-deploy-dns-firewall.md)

In diesem Schritt konfigurieren Sie DNS und die Firewall Einstellungen. Wenn remote-VPN-Clients verbunden sind, verwenden sie die gleichen DNS-Servern, die internen Clients verwenden, wodurch sie zum Auflösen von Namen auf die gleiche Weise wie der Rest von Ihren internen Arbeitsstationen. 

## <a name="step-6-configure-windows-10-client-always-on-vpn-connectionsvpn-deploy-client-vpn-connectionsmd"></a>[Schritt 6. Konfigurieren Sie Windows 10-Clientsysteme Always On-VPN-Verbindungen](vpn-deploy-client-vpn-connections.md)

In diesem Schritt konfigurieren Sie die Windows 10-Clientcomputern für die Kommunikation mit dieser Infrastruktur mit einer VPN-Verbindung. Sie können mehrere Technologien verwenden, so konfigurieren Sie Windows 10-VPN-Clients, einschließlich Windows PowerShell, System Center Configuration Manager und Intune. Alle drei erfordern ein XML VPN-Profil so konfigurieren Sie die entsprechenden VPN-Einstellungen. 

## <a name="step-7-optional-configure-conditional-access-for-vpn-connectivityad-ca-vpn-connectivity-windows10md"></a>[Schritt 7 fort. (Optional) Konfigurieren des bedingten Zugriffs für VPN-Verbindungen](../../ad-ca-vpn-connectivity-windows10.md) 
In diesem optionalen Schritt können Sie optimieren, wie autorisierte-VPN-Benutzer Zugriff auf Ihre Ressourcen. Mit bedingten Zugriff von Azure AD für VPN-Verbindungen können Sie besser, die VPN-Verbindungen zu schützen. Für den Bedingter Zugriff ist, dass eine Auswertung Richtlinie der richtlinienbasierten-Engine, die Ihnen ermöglicht, erstellen Regeln für den Zugriff für alle Azure AD-Anwendung verbunden. Weitere Informationen finden Sie unter [Azure Active Directory (Azure AD) bedingten Zugriff](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal).


## <a name="next-step"></a>Nächster Schritt
[Schritt 1. Planen der Bereitstellung des Always On-VPN-](always-on-vpn-deploy-planning.md): Bevor Sie die Remotezugriffs-Serverrolle auf dem Computer, die Sie zur Verwendung als VPN-Server planen installieren. Nach dem ordnungsgemäßen Planen können Sie Always On VPN bereitstellen und optional den bedingten Zugriff für VPN-Konnektivität mit Azure AD konfigurieren.  



---