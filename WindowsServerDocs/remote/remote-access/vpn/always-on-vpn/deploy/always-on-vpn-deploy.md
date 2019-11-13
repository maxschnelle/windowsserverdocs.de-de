---
title: Always On VPN-Bereitstellung für Windows Server und Windows 10
description: Mithilfe dieser Bereitstellung können Sie Always on VPN-Verbindungen (virtuelles privates Netzwerk) für Remote Mitarbeiter mithilfe des Remote Zugriffs in Windows Server 2016 oder höher und Always on VPN-Profilen für Windows 10-Client Computer bereitstellen.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 5ae1a40b-4f10-4ace-8aaf-13f7ab581f4f
ms.localizationpriority: medium
ms.date: 12/20/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5eba89cf61354627b63bcdf2420c25e7a44e3d9a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388144"
---
# <a name="always-on-vpn-deployment-for-windows-server-and-windows-10"></a>Always on der VPN-Bereitstellung für Windows Server und Windows 10

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorheriges:** Remote Zugriff](../../../Remote-Access.md)<br>
- [**Weiter:** Erfahren Sie mehr über die Always on VPN-Features und-Funktionen](../../vpn-map-da.md)

Always on-VPN bietet eine einheitliche Lösung für den Remote Zugriff und unterstützt in die Domäne eingebundenen, nicht in die Domäne eingebundenen (Arbeitsgruppen) oder Azure AD –-Geräte, auch private Geräte. Mit Always On-VPN muss der Verbindungstyp nicht ausschließlich Benutzer oder Gerät, sondern kann eine Kombination aus beidem sein. Sie könnten z.B. die Geräteauthentifizierung für die Remotegeräteverwaltung aktivieren und dann die Benutzerauthentifizierung für Konnektivität mit internen Unternehmenssites und -diensten.

## <a name="prerequisites"></a>Voraussetzungen

Wahrscheinlich verfügen Sie über die bereitgestellten Technologien, die Sie zum Bereitstellen Always on VPN verwenden können. Abgesehen von Ihren DC/DNS-Servern erfordert die Always on-VPN-Bereitstellung einen NPS-Server (RADIUS), einen Zertifizierungsstellen Server (ca) und einen RAS-Server (Routing/VPN). Nachdem Sie die Infrastruktur eingerichtet haben, müssen Sie Clients registrieren und die Clients dann mithilfe mehrerer Netzwerk Änderungen sicher mit Ihrem lokalen Standort verbinden.

- Active Directory Domänen Infrastruktur, einschließlich eines oder mehrerer Domain Name System (DNS)-Server. Sowohl interne als auch externe Domain Name System (DNS-Zonen) sind erforderlich. dabei wird davon ausgegangen, dass die interne Zone eine delegierte Unterdomäne der externen Zone ist (z. b. Corp.contoso.com und contoso.com).
- Active Directory basierte Public Key-Infrastruktur (PKI) und Active Directory Zertifikat Dienste (AD CS).
- Server (virtuell oder physisch, vorhandener oder neuer) zum Installieren von Netzwerk Richtlinien Server (NPS). Wenn Sie bereits über NPS-Server in Ihrem Netzwerk verfügen, können Sie eine vorhandene NPS-Serverkonfiguration ändern, anstatt einen neuen Server hinzuzufügen.
- Remote Zugriff als RAS-Gateway-VPN-Server mit einer kleinen Teilmenge von Features, die IKEv2-VPN-Verbindungen und LAN-Routing unterstützen.
- Umkreis Netzwerk, das zwei Firewalls umfasst.  Stellen Sie sicher, dass ihre Firewalls den Datenverkehr, der für die VPN-und RADIUS-Kommunikation erforderlich ist, ordnungsgemäß funktionieren. Weitere Informationen finden Sie unter [Übersicht über Always on VPN-Technologie](../always-on-vpn-technology-overview.md).
- Physischer Server oder virtueller Computer (VM) in Ihrem Umkreis Netzwerk mit zwei physischen Ethernet-Netzwerkadaptern, um den Remote Zugriff als RAS-Gateway-VPN-Server zu installieren. Virtuelle Computer erfordern ein virtuelles LAN (VLAN) für den Host. 
- Sie müssen mindestens Mitglied der Gruppe Administratoren oder einer entsprechenden Gruppe sein.
- Lesen Sie den Abschnitt Planning dieses Handbuchs, um sicherzustellen, dass Sie für diese Bereitstellung vorbereitet sind, bevor Sie die Bereitstellung ausführen.
- Überprüfen Sie die Entwurfs-und Bereitstellungs Handbücher für die einzelnen verwendeten Technologien. Mithilfe dieser Leitfäden können Sie feststellen, ob die Bereitstellungs Szenarien die Dienste und die Konfiguration bereitstellen, die Sie für das Netzwerk Ihrer Organisation benötigen. Weitere Informationen finden Sie unter [Übersicht über Always on VPN-Technologie](../always-on-vpn-technology-overview.md).
- Die Verwaltungsplattform Ihrer Wahl für die Bereitstellung der Always on-VPN-Konfiguration, da der CSP nicht Hersteller spezifisch ist.

>[!IMPORTANT]
>Für diese Bereitstellung ist es nicht erforderlich, dass auf Ihren Infrastruktur Servern, z. b. Computern, auf denen Active Directory Domain Services, Active Directory Zertifikat Dienste und Netzwerk Richtlinien Server ausgeführt wird, Windows Server 2016 ausgeführt wird. Sie können frühere Versionen von Windows Server, wie z. b. Windows Server 2012 R2, für die Infrastruktur Server und für den Server verwenden, auf dem Remote Zugriff ausgeführt wird.
>
>Versuchen Sie nicht, den Remote Zugriff auf einem virtuellen Computer (VM) in Microsoft Azure bereitzustellen. Die Verwendung des Remote Zugriffs in Microsoft Azure wird nicht unterstützt, einschließlich RAS-VPN und DirectAccess. Weitere Informationen finden Sie [unter Microsoft Server Software Support for Microsoft Azure Virtual Machines](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).

## <a name="about-this-deployment"></a>Informationen zu dieser Bereitstellung

Die bereitgestellten Anweisungen führen Sie durch die Bereitstellung des Remote Zugriffs als ein einzelnes Mandanten-VPN-RAS-Gateway für Punkt-zu-Standort-VPN-Verbindungen mithilfe eines der unten erwähnten Szenarien für Remote Client Computer, auf denen Windows 10 ausgeführt wird. Außerdem finden Sie Anweisungen zum Ändern einiger Ihrer vorhandenen Infrastruktur für die Bereitstellung. Außerdem finden Sie in dieser Bereitstellung Links, die Ihnen helfen, mehr über den VPN-Verbindungsprozess, die zu konfigurier fähigen Server, den profileXML VPNv2 CSP-Knoten und andere Technologien zum Bereitstellen Always on VPN zu erfahren.

**Always on von VPN-Bereitstellungs Szenarien:**

1. Stellen Sie nur Always on-VPN bereit.
2. Stellen Sie Always on-VPN mit bedingtem Zugriff für VPN-Konnektivität mithilfe Azure AD bereit.

Weitere Informationen und einen Workflow der dargestellten Szenarien finden Sie unter Bereitstellen [Always on VPN](always-on-vpn-deploy-deployment.md).

## <a name="what-isnt-provided-in-this-deployment"></a>Bereitstellung in dieser Bereitstellung nicht

Diese Bereitstellung stellt keine Anweisungen für Folgendes bereit:

- Active Directory Domain Services (AD DS).
- Active Directory Zertifikat Dienste (AD CS) und eine Public Key-Infrastruktur (PKI).
- Dynamic Host Configuration-Protokoll (DHCP).
- Netzwerkhardware, z. b. Ethernet-Verkabelung, Firewalls, Switches und Hubs.
- Zusätzliche Netzwerkressourcen, z. b. Anwendungs-und Dateiserver, auf die Remote Benutzer über eine Always on VPN-Verbindung zugreifen können.
- Internet Konnektivität oder bedingter Zugriff für die Internet Konnektivität mit Azure AD. Weitere Informationen finden Sie unter [bedingter Zugriff in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal).

## <a name="next-steps"></a>Nächste Schritte

- [Weitere Informationen zu den Always on VPN-Features und-Funktionen](../../vpn-map-da.md)

- [Weitere Informationen zu den Always on-VPN-Erweiterungen](../always-on-vpn-enhancements.md)

- [Erfahren Sie mehr über die erweiterten Always on-VPN-Features](always-on-vpn-adv-options.md)

- [Weitere Informationen zum Always on VPN-Technologie](../always-on-vpn-technology-overview.md)

- [Beginnen der Planung Ihrer Always on-VPN-Bereitstellung](always-on-vpn-deploy-deployment.md)