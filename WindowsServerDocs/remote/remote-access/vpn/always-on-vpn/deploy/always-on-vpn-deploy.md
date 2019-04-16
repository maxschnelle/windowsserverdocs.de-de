---
title: Always On VPN-Bereitstellung für Windows Server und Windows 10
description: Diese Bereitstellung können Sie immer auf Virtual Private Network (VPN)-Verbindungen für Mitarbeiter mithilfe von Remotezugriff in Windows Server 2016 oder höher und Always On VPN-Profile für Windows 10-Clientcomputer bereitstellen.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 5ae1a40b-4f10-4ace-8aaf-13f7ab581f4f
ms.localizationpriority: medium
ms.date: 12/20/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7cb60bdc6d6f3ff074f04827aa95c9e8e8abf35b
ms.sourcegitcommit: c435f91ef6f3ff5ffd2661291264b939d5ce4e2a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2018
ms.locfileid: "8981130"
---
# Always On VPN-Bereitstellung für Windows Server und Windows 10

>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **Vorherigen:** Remotezugriff](../../../Remote-Access.md)<br>
& #187; [ **Weiter:** erfahren Sie mehr über die Always On VPN-Features und Funktionen](../../vpn-map-da.md)


Always On VPN bietet eine zusammenhängende Lösung für Remotezugriff und Domäne unterstützt, die keiner Domäne beigetreten sind (Arbeitsgruppe) oder Azure AD eingebundene Geräte auch privat genutzte Geräte.  Mit Always On VPN kann den Typ der Verbindung keinen Benutzer oder das Gerät ausschließlich sein jedoch eine Kombination aus beidem. Sie können z. B. Aktivieren der Geräteauthentifizierung für remote Device Management und aktivieren Sie Benutzerauthentifizierung für eine Verbindung zu interne Unternehmens-Websites und Diensten.



## Voraussetzungen

Wahrscheinlich haben Technologien bereitgestellt, dass Sie verwenden können, um die Always On VPN bereitstellen. Als Ihre Domänencontroller/DNS-Server erfordert die Always On VPN-Bereitstellung ein NPS RADIUS-Server, eine Zertifizierungsstelle (CA)-Server und RAS (Routing/VPN)-Server. Nachdem Sie die Infrastruktur eingerichtet haben, müssen Sie Clients zu registrieren und zu Ihrer lokalen sicher über mehrere netzwerkänderungen herstellen.

- Active Directory-Domäne-Infrastruktur, z. B. einen oder mehrere Domain Name System (DNS)-Server. Interne und externe Domain Name System (DNS)-Zonen erforderlich ist, sind die wird davon ausgegangen, dass die interne Zone eine delegierte Unterdomäne der externe Zone (z. B. corp.contoso.com und contoso.com) ist.
- Active Directory-basierte public Key-Infrastruktur (PKI) und Active Directory-Zertifikatdienste (AD CS).
- Server, entweder in virtuellen oder physischen, vorhandene oder neue, Netzwerkrichtlinienserver (Network Policy Server, NPS) zu installieren. Wenn Sie bereits NPS-Servern in Ihrem Netzwerk verfügen, können Sie eine vorhandene NPS-Serverkonfiguration ändern, anstatt einen neuen Server hinzufügen.
- Remotezugriff als RAS-Gateway VPN-Server mit einer kleinen Teilmenge von Funktionen zur Unterstützung von IKEv2-VPN-Verbindungen und LAN-routing.
- Umkreisnetzwerk, die zwei Firewalls enthält.  Stellen Sie sicher, dass Ihre Firewalls der Datenverkehr zulässt, der für die VPN- und RADIUS-Kommunikation ordnungsgemäß funktionieren erforderlich ist. Weitere Informationen finden Sie [Immer auf VPN-Übersicht über die Technologie](../always-on-vpn-technology-overview.md).
- Physischen Servers oder virtuellen Computer (VM) auf das Umkreisnetzwerk mit zwei physische Ethernet-Netzwerkadapter Remote Access als RAS-Gateway VPN-Server zu installieren. VMs erfordern virtuellen LAN (VLAN) für den Host. 
- Mitgliedschaft Administratoren oder einer entsprechenden, ist das erforderliche Minimum.
- Lesen des planungsabschnitts dieses Handbuchs, um sicherzustellen, dass Sie für die Bereitstellung vorbereitet sind, bevor Sie die Bereitstellung ausführen.
- Überprüfen Sie die Entwurf und zur Bereitstellung Anleitungen für die einzelnen Technologien verwendet. Diesen Handbüchern aus, können Sie ermitteln, ob die Szenarien für die Bereitstellung liefern, die Dienste und die Konfiguration, die Sie für das Netzwerk der Organisation benötigen. Weitere Informationen finden Sie [Immer auf VPN-Übersicht über die Technologie](../always-on-vpn-technology-overview.md).
- Management-Plattform Ihrer Wahl für die Bereitstellung von Always On VPN-Konfiguration, da der CSP nicht anbieterspezifische ist.


>[!IMPORTANT]
>Für diese Bereitstellung ist es nicht erforderlich, dass Ihre Infrastrukturserver, z. B. Computer mit Active Directory Domain Services, Active Directory Certificate Services und Network Policy Server, Windows Server 2016 ausgeführt werden. Sie können frühere Versionen von Windows Server, z. B. Windows Server 2012 R2 verwenden, für die Infrastrukturserver und der Server, der Remote Access ausgeführt wird.
>
>Versuchen Sie nicht zum Bereitstellen von Remotezugriff auf einem virtuellen Computer \(VM\) in Microsoft Azure. Verwenden des Remotezugriffs in Microsoft Azure wird nicht unterstützt einschließlich Remote Access VPN und DirectAccess. Weitere Informationen finden Sie unter [Microsoft-Server-Software für Microsoft Azure-VMs zu unterstützen](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).


## <a name="bkmk_about"></a>Über diese Bereitstellung

Anleitung im erläutern das Bereitstellen von Remotezugriff als eines einzelnen Mandanten RAS-Gateway VPN-fließkomma\-mit\-Standort-VPN-Verbindungen mit einem beliebigen beschriebenen Fälle weiter unten für remote Clientcomputer, auf denen Windows 10 ausgeführt wird. Außerdem finden Sie Anweisungen für das ändern einige Ihrer vorhandenen Infrastruktur für die Bereitstellung. Außerdem finden in der gesamten diese Bereitstellung Links, um mehr über den Prozess der VPN-Verbindung, Server so konfigurieren, ProfileXML VPNv2-CSP-Knoten und anderen Technologien zum Bereitstellen von Always On VPN vertraut zu machen.

**Always On VPN-Bereitstellungsszenarien:**

1. Stellen Sie immer auf VPN nur.
2. Bereitstellen Sie Always On VPN mit bedingtem Zugriff für VPN-Konnektivität mit Azure AD.


Weitere Informationen und Workflow der Szenarios finden Sie unter [Bereitstellen von Always On VPN](always-on-vpn-deploy-deployment.md).


## <a name="bkmk_not"></a>Was ist nicht in dieser Bereitstellung bereitgestellt.

Diese Bereitstellung bietet keine Anweisungen für die:

- Active Directory-Domänendienste \(AD DS\).
- Active Directory-Zertifikatdienste \(AD CS\) und eine Public Key-Infrastruktur \(PKI\).
- Dynamic Host Configuration-Protokoll \(DHCP\). 
- Netzwerk-Hardware, z. B. Ethernet-Kabel, Firewalls, Switches und Hubs.
- Zusätzliche Netzwerkressourcen, z. B. Anwendung und Datei-Server, die remote-Benutzer über eine Always On VPN-Verbindung zugreifen können.
- Internetkonnektivität oder bedingten Zugriff für die Internetkonnektivität mithilfe von Azure AD. Weitere Informationen finden Sie unter [bedingten Zugriff in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal).




## Nächste Schritte

- [Erfahren Sie mehr über die Always On VPN-Features und Funktionen](../../vpn-map-da.md)

- [Erfahren Sie mehr über die Always On VPN-Erweiterungen](../always-on-vpn-enhancements.md)

- [Erfahren Sie mehr über die erweiterten Funktionen von Always On VPN](always-on-vpn-adv-options.md)

- [Erfahren Sie mehr über die Technologie von Always On VPN](../always-on-vpn-technology-overview.md)

- [Planen der Always On VPN-Bereitstellung](always-on-vpn-deploy-deployment.md)


---
