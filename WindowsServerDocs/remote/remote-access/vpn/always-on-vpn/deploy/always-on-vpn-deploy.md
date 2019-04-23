---
title: Always On VPN-Bereitstellung für Windows Server und Windows 10
description: Sie können diese Bereitstellung verwenden, immer auf Virtuelles privates Netzwerk (VPN) Verbindungen für Remotemitarbeiter mit Remote Access in Windows Server 2016 oder höher und Always On-VPN-Profile für Windows 10-Clientcomputern bereitstellen.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 5ae1a40b-4f10-4ace-8aaf-13f7ab581f4f
ms.localizationpriority: medium
ms.date: 12/20/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7cb60bdc6d6f3ff074f04827aa95c9e8e8abf35b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859621"
---
# <a name="always-on-vpn-deployment-for-windows-server-and-windows-10"></a>Always On-VPN-Bereitstellung für Windows Server und Windows 10

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

&#171;  [**Vorherige:** Remotezugriff](../../../Remote-Access.md)<br>
&#187; [**Next:** Erfahren Sie mehr über die Always On-VPN-Features und Funktionen](../../vpn-map-da.md)


Always On-VPN-Lösung einen einzigen einheitlichen Lösung für RAS- und unterstützt, die Domäne eingebundenen, (nicht-Domänenkonto eingebunden, Arbeitsgruppe) oder Azure AD – eingebundene Geräte, auch Geräte in Privatbesitz.  Mit Always On-VPN-der Verbindungstyp muss nicht ausschließlich auf Benutzer oder Gerät sein, jedoch kann eine Kombination aus beidem sein. Sie können z. B. Aktivieren der Geräteauthentifizierung für die remote-geräteverwaltung und dann ermöglicht die Benutzerauthentifizierung für Verbindungen mit internen Unternehmens-Standorte und-Dienste.



## <a name="prerequisites"></a>Vorraussetzungen

Wahrscheinlich stehen Ihnen die Technologien bereitgestellt, dass Sie zur Always On-VPN-Bereitstellung verwenden können. Als Ihre Domänencontroller/DNS-Server erfordert die Always On-VPN-Bereitstellung einer NPS (RADIUS)-Server, einen Server der Zertifizierungsstelle (Certification Authority, CA) und eines Remotezugriffsservers (Routing/VPN). Nachdem Sie die Infrastruktur eingerichtet haben, müssen Sie Clients registrieren und klicken Sie dann die Clients mit Ihrer lokalen sicher über mehrere Änderungen am Netzwerk verbinden.

- Active Directory-Domäneninfrastruktur, einschließlich der Server für eine oder mehrere Domain Name System (DNS). Interne und externe Domain Name System (DNS)-Zonen sind erforderlich, die davon aus, dass die interne Zone eine delegierte untergeordnete Domäne von der externen Zone (z. B. "corp.contoso.com" und "contoso.com").
- Active Directory-basierten public Key-Infrastruktur (PKI) und Active Directory-Zertifikatdienste (AD CS).
- Server, entweder in virtuellen oder physischen, vorhandene oder neue, (Network Policy Server, NPS) installieren. Wenn Sie NPS-Server in Ihrem Netzwerk vorhanden sind, können Sie die Konfiguration eines vorhandenes NPS-Servers ändern, anstatt einen neuen Server hinzufügen.
- Remotezugriff als RAS-VPN-Gateway-Server mit der eine kleine Teilmenge der Funktionen zur Unterstützung von IKEv2-VPN-Verbindungen und LAN-routing.
- Ein Umkreisnetzwerk, die zwei Firewalls enthält.  Stellen Sie sicher, dass Ihre Firewalls den Datenverkehr zu, der für sowohl VPN- und RADIUS-Kommunikation ermöglichen einwandfrei erforderlich ist. Weitere Informationen finden Sie unter [immer auf VPN-Technologieübersicht](../always-on-vpn-technology-overview.md).
- Physischer Server oder virtuellen Computer (VM) in Ihrem Umkreisnetzwerk mit zwei physische Ethernet-Netzwerkadapter, um den Remotezugriff als RAS-VPN-Gateway-Server zu installieren. Virtuelle Computer, virtuelles LAN (VLAN) für den Host erfordern. 
- Mitgliedschaft in der Administratoren oder einer entsprechenden Gruppe ist die mindestvoraussetzung.
- Lesen Sie im Planungsabschnitt dieses Handbuchs, um sicherzustellen, dass Sie für diese Bereitstellung vorbereitet sind, bevor Sie die Bereitstellung ausführen.
- Überprüfen Sie die Entwurfs- und Bereitstellungshandbücher für jede der Technologien, die verwendet werden soll. Diese Handbücher hilft Ihnen festzustellen, ob die Bereitstellungsszenarien bereitstellen, die Dienste und Konfigurationen, die Sie für das Netzwerk der Organisation benötigen. Weitere Informationen finden Sie unter [immer auf VPN-Technologieübersicht](../always-on-vpn-technology-overview.md).
- Management-Plattform Ihrer Wahl für die Bereitstellung der Always On-VPN-Konfigurations, da der CSP nicht herstellerspezifisches ist.


>[!IMPORTANT]
>Für diese Bereitstellung ist es nicht erforderlich, dass Ihre Infrastrukturserver, z. B. Computer mit Active Directory Domain Services, Active Directory Certificate Services und Network Policy Server, Windows Server 2016 ausgeführt werden. Sie können die frühere Versionen von Windows-Server, z. B. Windows Server 2012 R2 verwenden, für die Infrastrukturserver und für den Server, der den Remotezugriff ausgeführt wird.
>
>Versuchen Sie nicht zum Bereitstellen von Remotezugriff auf einem virtuellen Computer \(VM\) in Microsoft Azure. Verwenden Remote Access in Microsoft Azure wird nicht unterstützt einschließlich Remote Access VPN und DirectAccess. Weitere Informationen finden Sie unter [Unterstützung der Microsoft-Serversoftware für Microsoft Azure-Computern](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).


## <a name="bkmk_about"></a>Zu dieser Bereitstellung

Die bereitgestellten Anweisungen, führen Sie durch die Bereitstellung von Remotezugriff als ein einziger Mandant VPN-RAS-Gateway für Punkt\-zu\-site-VPN-Verbindungen mit einer der erwähnten unten für remote-Client-Computer, auf denen Windows ausgeführt werden Szenarios 10. Außerdem finden Sie Anweisungen zum Ändern einiger Ihrer vorhandenen Infrastruktur für die Bereitstellung. In dieser Bereitstellung finden Sie auch Links können Sie weitere Informationen zu den Prozess der VPN-Verbindung, zu konfigurierende Server, "profileXML" VPNv2 CSP-Knoten und anderen Technologien zum Bereitstellen von Always On-VPN.

**Always On-VPN-Bereitstellungsszenarien:**

1. Immer über das VPN nur bereitstellen.
2. Stellen Sie Always On-VPN-bereit, mit dem bedingten Zugriff für VPN-Verbindungen mithilfe von Azure AD.


Weitere Informationen und Workflows der beschriebenen Szenarios, finden Sie unter [Bereitstellen von Always On-VPN-](always-on-vpn-deploy-deployment.md).


## <a name="bkmk_not"></a>Was wird nicht in dieser Bereitstellung bereitgestellt.

Diese Bereitstellung stellt keine Anweisungen für bereit:

- Active Directory-Domänendienste \(AD DS\).
- Active Directory-Zertifikatdienste \(AD CS\) und einer Public Key-Infrastruktur \(PKI\).
- Dynamic Host Configuration-Protokoll \(DHCP\). 
- Netzwerk-Hardware, wie z. B. Ethernet-Kabel, Firewalls, Switches und Hubs.
- Zusätzliche Netzwerkressourcen wie z. B. Anwendungs- und Dateiservern, die remote-Benutzer über eine Always On-VPN-Verbindung zugreifen können.
- Internetkonnektivität oder bedingten Zugriffs für Internet-Verbindungen mithilfe von Azure AD. Weitere Informationen finden Sie unter [Bedingter Zugriff in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal).




## <a name="next-steps"></a>Nächste Schritte

- [Erfahren Sie mehr über die Always On-VPN-Features und Funktionen](../../vpn-map-da.md)

- [Erfahren Sie mehr über die Always On-VPN-Verbesserungen](../always-on-vpn-enhancements.md)

- [Erfahren Sie mehr über die erweiterte Always On-VPN-Funktionen](always-on-vpn-adv-options.md)

- [Erfahren Sie mehr über die Always On-VPN-Technologie](../always-on-vpn-technology-overview.md)

- [Planen der Always On-VPN-Bereitstellung](always-on-vpn-deploy-deployment.md)


---
