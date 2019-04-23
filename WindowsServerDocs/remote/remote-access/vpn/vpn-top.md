---
title: Virtual Private Networking (VPN)
description: Sie können in diesem Thema verwenden, um mehr über Windows Server 2016 und Windows 10-VPN-Features und Funktionen erfahren.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: cd4908f0-0d6f-4c02-8f98-4dc88c3dcb65
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: bf38995f0a2b396044d1f45b45eff8c3c2de329d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891071"
---
# <a name="virtual-private-networking-vpn"></a>Virtuelle Private Netzwerke \(VPN\)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10

## <a name="ras-gateway-as-a-single-tenant-vpn-server"></a>RAS-Gateway einen einzelnen Mandanten VPN-Server

In Windows Server 2016 ist die RAS-Serverrolle für eine logische Gruppierung von den folgenden verwandten netzwerkzugriffstechnologien.

- Remote Access Service (RAS)
- Routing
- Webanwendungsproxy

Diese Technologien sind die Rollendienste der Serverrolle "Remotezugriff".

Wenn Sie die Remotezugriffs-Serverrolle mit dem Hinzufügen von Rollen und Features-Assistenten oder Windows PowerShell installieren, können Sie eine oder mehrere dieser drei Rollendienste installieren.

Bei der Installation der **DirectAccess und VPN (RAS)** Rollendienst Sie das Remote Access Service-Gateway bereitstellen \( **RAS-Gateway**\). Sie können die RAS-Gateway als ein einzelner Mandant RAS-Gateway virtuelles privates Netzwerk bereitstellen \(VPN\) Server, die viele bietet erweiterte Funktionen und verbesserte.

>[!NOTE]
>Sie können auch die RAS-Gateway bereitstellen, als mehrinstanzenfähige VPN-Server für die Verwendung mit der Software Defined Networking \(SDN\), oder als DirectAccess-Server. Weitere Informationen finden Sie unter [RAS-Gateway](https://docs.microsoft.com/windows-server/remote/remote-access/ras-gateway/ras-gateway), [Software Defined Networking (SDN)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking), und [DirectAccess](https://docs.microsoft.com/windows-server/remote/remote-access/directaccess/directaccess).

## <a name="related-topics"></a>Verwandte Themen
- [Always On-VPN-Features und Funktionen](vpn-map-da.md): In diesem Thema erfahren Sie die Features und Funktionen von Always On-VPN. 

- [Konfigurieren von VPN-Gerät Tunnel unter Windows 10](vpn-device-tunnel-config.md): Always On-VPN-bietet Ihnen die Möglichkeit, ein dediziertes VPN-Profil für das Gerät oder Computer zu erstellen. Always On-VPN-Verbindungen enthalten zwei Typen von Tunneln: _Gerät Tunnel_ und _Benutzer Tunnel_. Gerät Tunnel wird vor der Anmeldung konnektivitätsszenarien und geräteverwaltung verwendet. Benutzer-Tunnel ermöglicht Zugriff auf Organisationsressourcen über VPN-Server.

- [Always On-VPN-Bereitstellung für WindowsServer 2016 und Windows 10](always-on-vpn/deploy/always-on-vpn-deploy.md): Enthält Anweisungen zum Bereitstellen des Remotezugriffs als eine einzelne Mandanten für Punkt-VPN-RAS-Gateway\-zu\-site-VPN-Verbindungen, die Ihre Mitarbeiter an entfernten Standorten für die Verbindung mit Ihrem Organisationsnetzwerk mit Always On-VPN-Verbindungen zu ermöglichen. Es wird empfohlen, dass Sie überprüfen, dass die Entwurfs- und Bereitstellungshandbücher für jede der Technologien, die in dieser Bereitstellung verwendet werden.

- [Technische Anleitung für Windows 10-VPN-](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide): Führt Sie durch die Entscheidungen, dass Sie für Windows 10-Clients in Ihrem Unternehmen VPN-Lösung und zur Konfiguration der Bereitstellung machen werden. Sie bietet mobile geräteverwaltung (MDM) mit Microsoft Intune und der VPN-Profil-Vorlage für Windows 10 Anweisungen und Verweise auf die VPNv2 Configuration Service Provider (CSP) finden.

- [Erstellen von VPN-Profilen in System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/create-vpn-profiles): In diesem Thema erfahren Sie, wie zum Erstellen von VPN-Profile in System Center Configuration Manager (SCCM).

- [Konfigurieren Sie Windows 10-Clientsysteme Always On-VPN-Verbindungen](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections): In diesem Thema wird beschrieben, die "profileXML" Optionen und-Schemas und wie Sie das ProfileXML VPN erstellen. Nachdem der Server-Infrastruktur eingerichtet haben, müssen Sie die Windows 10-Clientcomputern für die Kommunikation mit dieser Infrastruktur mit einer VPN-Verbindung konfigurieren. 

- [VPN-Profiloptionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options): In diesem Thema wird beschrieben, die für die VPN-Profil in Windows 10 und Informationen zum Konfigurieren von VPN-Profilen mit Intune oder SCCM. Sie können alle VPN-Einstellungen in Windows 10 unter Verwendung des Knotens "profileXML" im VPNv2 CSP konfigurieren.

---