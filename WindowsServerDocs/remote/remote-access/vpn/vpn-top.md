---
title: Virtual Private Networking (VPN)
description: Sie können in diesem Thema erfahren Sie mehr über Windows Server 2016 und Windows 10-VPN-Features und Funktionen verwenden.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: cd4908f0-0d6f-4c02-8f98-4dc88c3dcb65
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: bf38995f0a2b396044d1f45b45eff8c3c2de329d
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067303"
---
# Virtual Private Networking \(VPN\)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows 10

## RAS-Gateway als einzelne Mandanten-VPN-Server

In Windows Server 2016 ist die RAS-Server-Rolle eine logische Gruppierung von den folgenden verwandten Netzwerk Access-Technologien.

- RAS-Dienst (RAS)
- Routing
- Webanwendungsproxy

Diese Technologien sind die Rollendienste der Remote Access-Serverrolle.

Wenn Sie die RAS-Server-Rolle mit dem Hinzufügen von Rollen und Features Assistenten oder Windows PowerShell installieren, können Sie eine oder mehrere der folgenden drei Rollendienste installieren.

Bei der Installation des Rollendiensts **DirectAccess und VPN (RAS)** Sie Remote Access-Service-Gateway bereitstellen \ (**RAS-Gateway**\). Sie können RAS-Gateway als einzelne Mandanten RAS-Gateway virtuelles privates Netzwerk \(VPN\) Server bereitstellen, die viele erweiterte Funktionen und erweiterte Funktionen bereitstellt.

>[!NOTE]
>Sie können auch als mehrinstanzenfähigen VPN-Server für die Verwendung mit Software Defined Networking \(SDN\) oder als Server DirectAccess RAS-Gateway bereitstellen. Weitere Informationen finden Sie unter [RAS-Gateway](https://docs.microsoft.com/windows-server/remote/remote-access/ras-gateway/ras-gateway), [Software Defined Networking (SDN)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)und [DirectAccess](https://docs.microsoft.com/windows-server/remote/remote-access/directaccess/directaccess).

## Verwandte Themen
- [Always On VPN-Features und Funktionen](vpn-map-da.md): In diesem Thema erfahren Sie, über die Features und Funktionen von Always On VPN. 

- [Konfigurieren von VPN-Gerät Tunnel in Windows 10](vpn-device-tunnel-config.md): Always On VPN bietet Ihnen die Möglichkeit, eine dedizierte VPN-Profil für Computer oder Gerät zu erstellen. Always On VPN-Verbindungen verfügen über zwei Arten von Tunneln: _gerätetunnelfunktion_ und _Benutzer Tunnel_. Gerätetunnelfunktion wird für Pre-Logon konnektivitätsszenarien und Device Management Zwecke verwendet. Benutzer Tunnel ermöglicht Benutzern den Zugriff auf Unternehmensressourcen über VPN-Servern.

- [Always On VPN Bereitstellung für Windows Server 2016 und Windows 10](always-on-vpn/deploy/always-on-vpn-deploy.md): enthält Informationen zum Bereitstellen von Remotezugriff als einzelne Mandanten-VPN-RAS-Gateway für fließkomma\-mit\-Standort-VPN-Verbindungen, mit denen Ihre remote Mitarbeiter Ihrer Organisation herstellen Netzwerk mit Always On VPN-Verbindungen. Es wird empfohlen, dass Sie die Entwurf und zur Bereitstellung Handbüchern für die einzelnen Technologien überprüfen, die in dieser Bereitstellung verwendet werden.

- [Windows 10 technische VPN-Anleitung](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide): führt Sie durch die Entscheidungen, die Sie in der Enterprise-VPN-Lösung sowie zum Konfigurieren der Bereitstellung für Windows 10-Clients stellen. Sie können Verweise auf VPNv2 Configuration Service Provider (CSP) suchen und Verwaltung mobiler Geräte (MDM) Konfiguration unter Verwendung von Microsoft Intune und der VPN-Profilvorlage für Windows 10 bietet.

- [So erstellen Sie VPN-Profile in System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/create-vpn-profiles): In diesem Thema erfahren Sie, wie Sie VPN-Profile in System Center Configuration Manager (SCCM) erstellen.

- [Konfigurieren von Windows 10 Client immer auf VPN-Verbindungen](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections): in diesem Thema werden die ProfileXML Optionen und Schema und wie Sie das VPN-ProfileXML erstellen. Nach dem Einrichten der Server-Infrastruktur, müssen Sie die Windows 10-Clientcomputern für die Kommunikation mit dieser Infrastruktur mit einer VPN-Verbindung konfigurieren. 

- [VPN-Profiloptionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options): in diesem Thema wird beschrieben, die VPN-profileinstellungen in Windows 10 und erfahren, wie Sie mithilfe von Intune oder SCCM VPN-Profile zu konfigurieren. Sie können alle VPN-Einstellungen in Windows 10 mit dem Knoten "ProfileXML" in dem VPNv2-CSP konfigurieren.

---