---
title: Virtuelle private Netzwerke (Virtual Private Networks, VPNs)
description: In diesem Thema erfahren Sie mehr über Windows Server 2016-und Windows 10-VPN-Features und-Funktionen.
ms.topic: article
ms.assetid: cd4908f0-0d6f-4c02-8f98-4dc88c3dcb65
ms.date: 11/05/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.openlocfilehash: 30f08f02bf7a06619b9a32206863a9ddefc0fc2d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87968917"
---
# <a name="virtual-private-networking-vpn"></a>Virtuelle private Netzwerke (Virtual Private Networks, VPNs)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10

## <a name="ras-gateway-as-a-single-tenant-vpn-server"></a>RAS-Gateway als einzelner Mandanten-VPN-Server

In Windows Server 2016 ist die Remote Zugriffs-Server Rolle eine logische Gruppierung der folgenden verwandten Netzwerk Zugriffs Technologien.

- RAS-Dienst (RAS)
- Routing
- Webanwendungsproxy

Diese Technologien sind die Rollendienste der Serverrolle "Remotezugriff".

Wenn Sie die Remote Zugriffs-Server Rolle mit dem Assistenten zum Hinzufügen von Rollen und Features oder mit Windows PowerShell installieren, können Sie einen oder mehrere dieser drei Rollen Dienste installieren.

Wenn Sie den **DirectAccess-und VPN-Rollen Dienst (RAS)** installieren, stellen Sie das**RAS-Gateway**bereit. Sie können das RAS-Gateway als ein virtuelles privates Netzwerk (VPN) mit einem Mandanten RAS-Gateway bereitstellen, das viele erweiterte Features und erweiterte Funktionen bereitstellt.

>[!NOTE]
>Sie können das RAS-Gateway auch als mehr Instanzen fähigen VPN-Server für die Verwendung mit Software-Defined Networking (SDN) oder als DirectAccess-Server bereitstellen. Weitere Informationen finden Sie unter [RAS-Gateway](../ras-gateway/ras-gateway.md), [Software-Defined Networking (SDN)](../../../networking/sdn/software-defined-networking.md)und [DirectAccess](../directaccess/directaccess.md).

## <a name="related-topics"></a>Verwandte Themen
- [Always on von VPN-Features und-Funktionen](vpn-map-da.md): in diesem Thema erfahren Sie mehr über die Features und Funktionen von Always on VPN.

- [Konfigurieren von VPN-Geräte Tunneln in Windows 10](vpn-device-tunnel-config.md): Always on-VPN bietet Ihnen die Möglichkeit, ein dediziertes VPN-Profil für das Gerät oder den Computer zu erstellen. Always on-VPN-Verbindungen umfassen zwei Arten von Tunneln: _Geräte Tunnel_ und _Benutzer Tunnel_. Der Geräte Tunnel wird für Konnektivitätsszenarien vor der Anmeldung und für Geräteverwaltung verwendet. Mit dem Benutzertunnel können Benutzer über VPN-Server auf Organisationsressourcen zugreifen.

- [Always on-VPN-Bereitstellung für Windows Server 2016 und Windows 10](always-on-vpn/deploy/always-on-vpn-deploy.md): enthält Anweisungen zum Bereitstellen des Remote Zugriffs als ein einzelnes Mandanten-VPN-RAS-Gateway für Punkt-zu-Standort-VPN-Verbindungen, mit denen Ihre Remote Mitarbeiter mit Always on VPN-Verbindungen eine Verbindung mit Ihrem Unternehmensnetzwerk herstellen können. Es wird empfohlen, dass Sie die Entwurfs-und Bereitstellungs Handbücher für jede der in dieser Bereitstellung verwendeten Technologien überprüfen.

- [Technische Anleitung zu Windows 10-VPN](/windows/access-protection/vpn/vpn-guide): erläutert die Entscheidungen, die Sie für Windows 10-Clients in Ihrer Enterprise-VPN-Lösung treffen werden, und wie Sie die Bereitstellung konfigurieren. Verweise auf den VPNv2-Konfigurations Dienstanbieter (CSP) finden Sie unter Konfigurations Anweisungen für die Verwaltung mobiler Geräte (Mobile Device Management, MDM) mithilfe von Microsoft InTune und der VPN-Profil Vorlage für Windows 10.

- [Erstellen von VPN-Profilen in Configuration Manager](/configmgr/protect/deploy-use/create-vpn-profiles): in diesem Thema erfahren Sie, wie Sie in Configuration Manager VPN-Profile erstellen.

- [Konfigurieren von Windows 10-Client Always on-VPN-Verbindungen](./always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md): in diesem Thema werden die profileXML-Optionen und das-Schema beschrieben und das profileXML-VPN erstellt. Nachdem Sie die Serverinfrastruktur eingerichtet haben, müssen Sie die Windows 10-Client Computer für die Kommunikation mit dieser Infrastruktur über eine VPN-Verbindung konfigurieren.

- [VPN-Profil Optionen](/windows/access-protection/vpn/vpn-profile-options): in diesem Thema werden die VPN-Profileinstellungen in Windows 10 beschrieben und erfahren, wie Sie VPN-Profile mithilfe von InTune oder Configuration Manager konfigurieren. Sie können alle VPN-Einstellungen in Windows 10 konfigurieren, indem Sie den profileXML-Knoten im VPNv2-CSP verwenden.
