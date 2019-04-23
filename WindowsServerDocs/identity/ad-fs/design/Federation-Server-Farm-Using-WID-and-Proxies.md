---
ms.assetid: f0464182-56a2-4bfa-a8c8-7e39c1bd62d3
title: Verbundserverfarm mit WID und Proxys
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e372f066fc82b9857d438234b491732a177e24fa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860391"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>Verbundserverfarm mit WID und Proxys

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Dieser Bereitstellungstopologie für Active Directory Federation Services \(AD FS\) ist mit der Verbundserverfarm mit internen Windows-Datenbank \(WID\) Topologie, sondern fügt Proxycomputer, auf die Umkreisnetzwerk zur Unterstützung von externer Benutzern. Diese Proxys umleiten clientauthentifizierungsanforderungen, die von außerhalb des Unternehmensnetzwerks an die Verbundserverfarm stammen. In früheren Versionen von AD FS wurden diese Proxys Verbundserverproxys aufgerufen.  
  
> [!IMPORTANT]  
> In Active Directory-Verbunddienste \(AD FS\) in Windows Server 2012 R2, ist die Rolle eines Verbundserverproxys durch einen neuen Remotezugriff-Rollendienst namens Webanwendungsproxy übernommen. Zum Aktivieren von AD FS für Zugriff von außerhalb des Unternehmensnetzwerks, das war der Zweck der Bereitstellung eines Verbundserverproxys in Legacyversionen von AD FS, z. B. AD FS 2.0 und AD FS unter Windows Server 2012 können Sie eine oder mehrere webanwendungsproxys für ein bereitstellen. D-FS unter Windows Server 2012 R2.  
>   
> Im Kontext von AD FS-Webanwendungsproxy als einen AD FS-Verbundserverproxy Funktionen. Darüber hinaus bietet der Webanwendungsproxy Reverseproxyfunktionen für Webanwendungen in Ihrem Unternehmensnetzwerk, damit Benutzer außerhalb des Unternehmensnetzwerks von allen Geräten auf die Anwendungen zugreifen können. Weitere Informationen zum Webanwendungsproxy-Rollendienst finden Sie unter „Übersicht über den Webanwendungsproxy“.  
>   
> Bei der Planung die Bereitstellung von Web Application Proxy können Sie die Informationen in den folgenden Themen lesen:  
>   
> -   [Planen der Infrastruktur für Webanwendungsproxy (WAP)](https://technet.microsoft.com/library/dn383648.aspx)  
> -   [Planen Sie die Webanwendungsproxy-Servers](https://technet.microsoft.com/library/dn383647.aspx)  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
Dieser Abschnitt beschreibt verschiedene Überlegungen zu den Zielgruppe, Vorteile und Einschränkungen, die mit dieser Bereitstellungstopologie verknüpft sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Organisationen mit bis zu 100 konfigurierten Vertrauensstellungen, die sowohl für ihre interne Benutzer und externe Benutzer bieten \(angemeldet sind auf Computern, die physisch außerhalb des Unternehmensnetzwerks befinden\) mit einzelnen Anmeldung\-auf \(SSO\) Zugriff auf verbundanwendungen oder-Dienste  
  
-   Organisationen, die sowohl ihre internen Benutzer als auch die externe Benutzer SSO-Zugriff für Microsoft Office 365 bereitstellen müssen  
  
-   Kleinere Organisationen, die externe Benutzer und redundant, skalierbare Dienste erfordern  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Was sind die Vorteile der Verwendung dieser Topologie?  
  
-   Die gleichen Vorteile wie für die [Federation Server Farm mit WID](Federation-Server-Farm-Using-WID.md) Topologie sowie den Vorteil, dass bietet zusätzlichen Zugriff für externe Benutzer  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Was sind die Einschränkungen bei der Verwendung dieser Topologie?  
  
-   Dieselben Einschränkungen wie für die aufgelisteten der [Federation Server Farm mit WID](Federation-Server-Farm-Using-WID.md) Topologie  

||1 \- 100 RP-Vertrauensstellungen|Mehr als 100 RP-Vertrauensstellungen 
| ----- |-----| ------ |
|1 \- 30 AD FS-Knoten|WID unterstützt|Nicht unterstützt, mit WID \- SQL erforderlich 
|Mehr als 30 AD FS-Knoten|Nicht unterstützt, mit WID \- SQL erforderlich|Nicht unterstützt, mit WID \- SQL erforderlich  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Server Platzierung und Netzwerk-Layout-Empfehlungen  
Zum Bereitstellen dieser Topologie wird zusätzlich zum Hinzufügen von zwei webanwendungsproxys, achten Sie darauf, dass es sich bei Ihrem Umkreisnetzwerk, auch über Zugriff auf einen Domain Name System ermöglicht \(DNS\) Server und eine zweite Netzwerklastenausgleich \( NLB\) Host. Der zweite NLB-Host muss konfiguriert werden, mit einem NLB-Cluster, die einen mit dem Internet verwendet\-zugegriffen werden Cluster-IP-Adresse, und es müssen die gleiche Cluster-DNS-namenseinstellung verwenden, wie der vorherige NLB-Cluster, die Sie über das Unternehmensnetzwerk konfiguriert \( "FS.Fabrikam.com"\). Die webanwendungsproxys auch mit dem Internet konfiguriert werden\-zugegriffen werden IP-Adressen.  
  
Die folgende Abbildung zeigt die vorhandenen Verbundserverfarm mit WID-Topologie, die zuvor beschrieben wurde, und wie das fiktive Unternehmen Fabrikam, Inc., einem Umkreis-DNS-Server, ermöglicht hinzugefügt ein zweiter NLB-Host mit dem gleichen DNS-Clusternamen \("FS.Fabrikam.com"\), und fügt zwei webanwendungsproxys \(wap1 und wap2\) mit dem Umkreisnetzwerk.  
  
![Farm mit WID und Proxys](media/WIDFarmADFSBlue.gif)  
  
Weitere Informationen dazu, wie Sie Ihre Netzwerkumgebung für die Verwendung mit Verbundserver oder webanwendungsproxys konfigurieren zu können, finden Sie unter "Anforderungen für die namensauflösung" im Abschnitt [AD FS-Anforderungen](AD-FS-Requirements.md) und [planen Sie das Web Infrastruktur für Webanwendungsproxy (WAP)](https://technet.microsoft.com/library/dn383648.aspx).  
  
## <a name="see-also"></a>Siehe auch  
[Planen der AD FS-Bereitstellungstopologie](Plan-Your-AD-FS-Deployment-Topology.md)  
[AD FS-Entwurfshandbuch in Windows Server 2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

