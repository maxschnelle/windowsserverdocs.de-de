---
title: Always On VPN bereitstellen
description: Dieses Thema enthält ausführliche Anweisungen für die Bereitstellung von Always On VPN in Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ad748de2-d175-47bf-b05f-707dc48692cf
ms.localizationpriority: medium
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 15c60f2986d3837c5c6e03f9e0a25c7e0a4e0cc0
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067327"
---
# Always On VPN bereitstellen

>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #0171; [ **Vorherige:** erfahren Sie mehr über die Always On VPN erweiterte Funktionen](always-on-vpn-adv-options.md)<br>
& #0187; [ **Weiter:** Schritt 1. Planen der Always On VPN-Bereitstellung](always-on-vpn-deploy-planning.md)

In diesem Abschnitt erhalten Sie Informationen über den Workflow für die Bereitstellung von Always On VPN-Verbindungen für remote-Domäne eingebunden Windows 10-Clientcomputern. Wenn Sie zum **Konfigurieren des bedingten Zugriffs** zu optimieren, wie der VPN-Benutzer Ihre Ressourcen zugreifen möchten, finden Sie unter [den bedingten Zugriff für VPN-Konnektivität mit Azure AD](../../ad-ca-vpn-connectivity-windows10.md). Weitere Informationen zu den bedingten Zugriff für VPN-Konnektivität mit Azure AD finden Sie unter [Bedingter Zugriff in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). 


Das folgende Diagramm zeigt den Workflow-Prozess für die verschiedenen Szenarien, bei der Bereitstellung von Always On VPN: 

_Klicken Sie auf Bild zu vergrößern_.

<a href="../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow.png" alt="Full-sized view of the Always On VPN deployment workflow" target="_blank">![Miniaturansicht](../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow-sm.png)
</a> 

>[!IMPORTANT]
>Für diese Bereitstellung ist es nicht erforderlich, dass Ihre Infrastrukturserver, z. B. Computern mit Active Directory Domain Services, Active Directory Certificate Services und Network Policy Server, Windows Server 2016 ausgeführt werden. Sie können frühere Versionen von Windows Server, z. B. Windows Server 2012 R2 verwenden, für die Infrastrukturserver und der Server, der Remote Access ausgeführt wird.

## [Schritt 1. Planen der Always On VPN-Bereitstellung](always-on-vpn-deploy-planning.md)

In diesem Schritt starten Sie zum Planen und Vorbereiten der Always On VPN-Bereitstellung. Bevor Sie die RAS-Server-Rolle auf dem Computer, die Sie beabsichtigen, zur Verwendung als VPN-Server installieren. Nach dem ordnungsgemäßen Planen können Sie Always On VPN bereitstellen und optional den bedingten Zugriff für VPN-Konnektivität mit Azure AD konfigurieren.

## [Schritt 2. Konfigurieren der Always On VPN-Server-Infrastruktur](vpn-deploy-server-infrastructure.md)

In diesem Schritt installieren und Konfigurieren der serverseitigen Komponenten erforderlich, um die VPN-Unterstützung. Die serverseitige Komponenten umfassen konfigurieren PKI, um die vom Benutzer, der VPN-Server und dem Netzwerkrichtlinienserver verwendeten Zertifikate zu verteilen.  Außerdem konfigurieren Sie RRAS zur Unterstützung von IKEv2 Verbindungen und dem Netzwerkrichtlinienserver für die Autorisierung für die VPN-Verbindungen.

Um die Server-Infrastruktur zu konfigurieren, müssen Sie die folgenden Aufgaben ausführen:
- **Auf einen Server mit Active Directory Domain Services:** Aktivieren Sie automatische Registrierung von Zertifikaten in "Gruppenrichtlinie" für Computer und Benutzer zu, erstellen Sie der VPN-Benutzergruppe, die Gruppe der VPN-Server und die Gruppe der NPS-Servers und jede Gruppe hinzufügen.
- **Auf ein Active Directory-Zertifikatserver Zertifizierungsstelle:** Erstellen Sie die Benutzerauthentifizierung, VPN-Serverauthentifizierung und NPS-Serverauthentifizierung Zertifikatvorlagen.
- **Auf Windows 10-Clients Domäne:** Registrieren und Benutzerzertifikate überprüft werden.

## [Schritt 3. Konfigurieren des RAS-Servers für Always On VPN](vpn-deploy-ras.md)

In diesem Schritt konfigurieren Sie Remote Access VPN für IKEv2-VPN-Verbindung zulassen, verweigern, die Verbindungen von anderen VPN-Protokolle und weisen Sie einen statischen IP-Adresspool für die Ausstellung von IP-Adressen zu verbinden von autorisierten VPN-Clients.

Um RAS zu konfigurieren, müssen Sie die folgenden Aufgaben ausführen:
- Registrieren Sie und überprüfen Sie das VPN-Server-Zertifikat
- Installieren und Konfigurieren von Remote Access VPN

## [Schritt 4. Installieren und Konfigurieren von NPS-Servers](vpn-deploy-nps.md)

In diesem Schritt installieren Sie mithilfe von Windows PowerShell oder die Server-Manager Hinzufügen von Rollen und Features-Assistenten (Network Policy Server, NPS). Außerdem konfigurieren Sie NPS zum behandeln alle Authentifizierung, Autorisierung und Kontoführung Aufgaben für die Anforderung der Verbindung, die sie aus der VPN-Server empfängt.

Um NPS zu konfigurieren, müssen Sie die folgenden Aufgaben ausführen:
- Registrieren des Netzwerkrichtlinienservers in Active Directory
- Konfigurieren von RADIUS-Kontoführung für Ihre NPS-Servers
- Der VPN-Server als RADIUS-Client in NPS hinzu
- Konfigurieren von Netzwerkrichtlinien in NPS
- Registrieren des NPS-Serverzertifikats

## [Schritt 5. Konfigurieren von DNS- und Firewalleinstellungen für immer in VPN](vpn-deploy-dns-firewall.md)

In diesem Schritt konfigurieren Sie DNS und Firewall Einstellungen. Wenn remote-VPN-Clients zu verbinden, verwenden sie die gleichen DNS-Server, die Ihre interne Clients verwenden, können sie zur Auflösung von Namen auf die gleiche Weise wie der Rest der Ihre internen Arbeitsstationen. 

## [Schritt 6. Konfigurieren von Windows 10-Client immer auf VPN-Verbindungen](vpn-deploy-client-vpn-connections.md)

In diesem Schritt konfigurieren Sie die Windows 10-Clientcomputern für die Kommunikation mit dieser Infrastruktur mit einer VPN-Verbindung. Sie können verschiedene Technologien zum Konfigurieren von Windows 10-VPN-Clients, einschließlich Windows PowerShell, System Center Configuration Manager und Intune verwenden. Alle drei erfordern eine XML-VPN-Profil so konfigurieren Sie die entsprechenden VPN-Einstellungen. 

## [Schritt 7. (Optional) Konfigurieren des bedingten Zugriffs für VPN-Konnektivität](../../ad-ca-vpn-connectivity-windows10.md) 
Sie können in diesem optionalen Schritt wie autorisierten VPN optimieren Benutzer Zugriff auf Ihre Ressourcen. Mit Azure AD bedingten Zugriff für VPN-Konnektivität helfen Ihnen die VPN-Verbindungen zu schützen. Bedingter Zugriff ist, dass ein richtlinienbasiertes Auswertungsmodul, mit Sie Zugriffsregeln für alle Azure AD erstellen können Anwendung. Weitere Informationen finden Sie unter [Bedingter Zugriff Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal).


## Nächster Schritt
[Schritt 1. Planen der Always On VPN-Bereitstellung](always-on-vpn-deploy-planning.md): Bevor Sie die RAS-Server-Rolle auf dem Computer installieren Sie zur Verwendung als VPN-Server planen. Nach dem ordnungsgemäßen Planen können Sie Always On VPN bereitstellen und optional den bedingten Zugriff für VPN-Konnektivität mit Azure AD konfigurieren.  



---