---
title: Virtual Private Networking (VPN)
description: In diesem Thema erfahren Sie mehr über Windows Server 2016-und Windows 10-VPN-Features und-Funktionen.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: cd4908f0-0d6f-4c02-8f98-4dc88c3dcb65
ms.date: 11/05/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.openlocfilehash: 2f8362b5581dbd6c08f3f708f435e8625784e8fe
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818723"
---
# <a name="virtual-private-networking-vpn"></a>Virtual Private Networking (VPN)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows 10

## <a name="ras-gateway-as-a-single-tenant-vpn-server"></a>RAS-Gateway als einzelner Mandanten-VPN-Server

In Windows Server 2016 ist die Remote Zugriffs-Server Rolle eine logische Gruppierung der folgenden verwandten Netzwerk Zugriffs Technologien.

- RAS-Dienst (RAS)
- Routing
- Webanwendungsproxy

Diese Technologien sind die Rollen Dienste der Remote Zugriffs-Server Rolle.

Wenn Sie die Remote Zugriffs-Server Rolle mit dem Assistenten zum Hinzufügen von Rollen und Features oder mit Windows PowerShell installieren, können Sie einen oder mehrere dieser drei Rollen Dienste installieren.

Wenn Sie den **DirectAccess-und VPN-Rollen Dienst (RAS)** installieren, stellen Sie das**RAS-Gateway**bereit. Sie können das RAS-Gateway als ein virtuelles privates Netzwerk (VPN) mit einem Mandanten RAS-Gateway bereitstellen, das viele erweiterte Features und erweiterte Funktionen bereitstellt.

>[!NOTE]
>Sie können das RAS-Gateway auch als mehr Instanzen fähigen VPN-Server für die Verwendung mit Software-Defined Networking (SDN) oder als DirectAccess-Server bereitstellen. Weitere Informationen finden Sie unter [RAS-Gateway](https://docs.microsoft.com/windows-server/remote/remote-access/ras-gateway/ras-gateway), [Software-Defined Networking (SDN)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)und [DirectAccess](https://docs.microsoft.com/windows-server/remote/remote-access/directaccess/directaccess).

## <a name="related-topics"></a>Verwandte Themen
- [Always on von VPN-Features und-Funktionen](vpn-map-da.md): in diesem Thema erfahren Sie mehr über die Features und Funktionen von Always on VPN. 

- [Konfigurieren von VPN-Geräte Tunneln in Windows 10](vpn-device-tunnel-config.md): Always on-VPN bietet Ihnen die Möglichkeit, ein dediziertes VPN-Profil für das Gerät oder den Computer zu erstellen. Always on-VPN-Verbindungen umfassen zwei Arten von Tunneln: _Geräte Tunnel_ und _Benutzer Tunnel_. Der Geräte Tunnel wird für Konnektivitätsszenarien vor der Anmeldung und für Geräteverwaltung verwendet. Der Benutzer Tunnel ermöglicht Benutzern den Zugriff auf Organisations Ressourcen über VPN-Server.

- [Always on-VPN-Bereitstellung für Windows Server 2016 und Windows 10](always-on-vpn/deploy/always-on-vpn-deploy.md): enthält Anweisungen zum Bereitstellen des Remote Zugriffs als ein einzelnes Mandanten-VPN-RAS-Gateway für Punkt-zu-Standort-VPN-Verbindungen, mit denen Ihre Remote Mitarbeiter mit Always on VPN-Verbindungen eine Verbindung mit Ihrem Unternehmensnetzwerk herstellen können. Es wird empfohlen, dass Sie die Entwurfs-und Bereitstellungs Handbücher für jede der in dieser Bereitstellung verwendeten Technologien überprüfen.

- [Technische Anleitung zu Windows 10-VPN](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide): erläutert die Entscheidungen, die Sie für Windows 10-Clients in Ihrer Enterprise-VPN-Lösung treffen werden, und wie Sie die Bereitstellung konfigurieren. Verweise auf den VPNv2-Konfigurations Dienstanbieter (CSP) finden Sie unter Konfigurations Anweisungen für die Verwaltung mobiler Geräte (Mobile Device Management, MDM) mithilfe von Microsoft InTune und der VPN-Profil Vorlage für Windows 10.

- [Erstellen von VPN-Profilen in Configuration Manager](https://docs.microsoft.com/configmgr/protect/deploy-use/create-vpn-profiles): in diesem Thema erfahren Sie, wie Sie in Configuration Manager VPN-Profile erstellen.

- [Konfigurieren von Windows 10-Client Always on-VPN-Verbindungen](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections): in diesem Thema werden die profileXML-Optionen und das-Schema beschrieben und das profileXML-VPN erstellt. Nachdem Sie die Serverinfrastruktur eingerichtet haben, müssen Sie die Windows 10-Client Computer für die Kommunikation mit dieser Infrastruktur über eine VPN-Verbindung konfigurieren.

- [VPN-Profil Optionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options): in diesem Thema werden die VPN-Profileinstellungen in Windows 10 beschrieben und erfahren, wie Sie VPN-Profile mithilfe von InTune oder Configuration Manager konfigurieren. Sie können alle VPN-Einstellungen in Windows 10 konfigurieren, indem Sie den profileXML-Knoten im VPNv2-CSP verwenden.
