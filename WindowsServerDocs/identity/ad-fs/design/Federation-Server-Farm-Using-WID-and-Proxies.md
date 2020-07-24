---
ms.assetid: f0464182-56a2-4bfa-a8c8-7e39c1bd62d3
title: Verbundserverfarm mit WID und Proxies
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9d2fb6485a742afd177428f3f6bdc8ea0c89d66d
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86963532"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>Verbundserverfarm mit WID und Proxies

Diese Bereitstellungs Topologie für Active Directory-Verbunddienste (AD FS) \( AD FS \) ist mit der Verbund Serverfarm mit der internen Windows-Datenbank- \( wid- \) Topologie identisch, fügt jedoch dem Umkreis Netzwerk Proxy Computer zur Unterstützung externer Benutzer hinzu. Diese Proxys leiten Client Authentifizierungsanforderungen, die von außerhalb Ihres Unternehmensnetzwerks stammen, an die Verbund Serverfarm um. In früheren Versionen von AD FS wurden diese Proxys als Verbund Server Proxys bezeichnet.  
  
> [!IMPORTANT]  
> In Active Directory-Verbunddienste (AD FS) \( AD FS \) in Windows Server 2012 R2 wird die Rolle eines Verbund Server Proxys von einem neuen Remote Zugriffs Rollen Dienst namens webanwendungsproxy behandelt. Um Ihre AD FS für den Zugriff von außerhalb des Unternehmensnetzwerks zu aktivieren. Dies war der Zweck der Bereitstellung eines Verbund Server Proxys in Legacy Versionen von AD FS, wie z. b. AD FS 2,0 und AD FS in Windows Server 2012, Sie können einen oder mehrere webanwendungsproxys für AD FS in Windows Server 2012 R2 bereitstellen.  
>   
> Im Kontext von AD FS fungiert der webanwendungsproxy als AD FS Verbund Server Proxy. Darüber hinaus bietet der Webanwendungsproxy Reverseproxyfunktionen für Webanwendungen in Ihrem Unternehmensnetzwerk, damit Benutzer außerhalb des Unternehmensnetzwerks von allen Geräten auf die Anwendungen zugreifen können. Weitere Informationen zum Webanwendungsproxy-Rollendienst finden Sie unter „Übersicht über den Webanwendungsproxy“.  
>   
> Bei der Planung die Bereitstellung von Web Application Proxy können Sie die Informationen in den folgenden Themen lesen:  
>   
> -   [Planen der Infrastruktur für den webanwendungsproxy (WAP)](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))  
> -   [Planen des Webanwendungsproxy-Servers](/previous-versions/orphan-topics/ws.11/dn383647(v=ws.11))  
  
## <a name="deployment-considerations"></a>Überlegungen zu Bereitstellungen  
In diesem Abschnitt werden verschiedene Überlegungen zu den beabsichtigten Zielgruppen, Vorteilen und Einschränkungen beschrieben, die mit dieser Bereitstellungs Topologie verknüpft sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Organisationen mit 100 oder weniger konfigurierten Vertrauens Stellungen, die sowohl interne als auch externe Benutzer, \( die auf Computern angemeldet sind, die sich physisch außerhalb des Unternehmensnetzwerks befinden, \) mit einmaligem \- Anmelden \( SSO- \) Zugriff auf Verbund Anwendungen oder-Dienste bereitstellen müssen  
  
-   Organisationen, die sowohl internen als auch externen Benutzern SSO-Zugriff auf Microsoft Office 365 bereitstellen müssen  
  
-   Kleinere Unternehmen, die externe Benutzer haben und redundante, skalierbare Dienste benötigen  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Welche Vorteile bietet die Verwendung dieser Topologie?  
  
-   Die gleichen Vorteile wie für die Verbund [Server Farm mit der wid](Federation-Server-Farm-Using-WID.md) -Topologie sowie die Vorteile der Bereitstellung von zusätzlichem Zugriff für externe Benutzer.  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Welche Einschränkungen gelten für die Verwendung dieser Topologie?  
  
-   Die gleichen Einschränkungen wie für die Verbund [Server Farm werden mithilfe der wid](Federation-Server-Farm-Using-WID.md) -Topologie aufgelistet.  

||1 \- 100 RP-Vertrauens Stellungen|Mehr als 100 RP-Vertrauens Stellungen 
| ----- |-----| ------ |
|1 \- 30 AD FS Knoten|Von WID unterstützt|Nicht unterstützt, wenn wid \- SQL erforderlich ist 
|Mehr als 30 AD FS Knoten|Nicht unterstützt, wenn wid \- SQL erforderlich ist|Nicht unterstützt, wenn wid \- SQL erforderlich ist  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Empfehlungen zur Server Platzierung und zum Netzwerk Layout  
Um diese Topologie zusätzlich zum Hinzufügen von zwei webanwendungsproxys bereitzustellen, müssen Sie sicherstellen, dass Ihr Umkreis Netzwerk auch Zugriff auf einen Domain Name System \( DNS \) -Server und einen zweiten NLB-Host für den Netzwerk Lastenausgleich bereitstellen kann \( \) . Der zweite NLB-Host muss mit einem NLB-Cluster konfiguriert werden, der eine \- IP-Adresse für den Internet zugänglichen Cluster verwendet, und er muss die gleiche DNS-Namen Einstellung des Clusters wie der vorherige NLB-Cluster verwenden, den Sie im Unternehmensnetzwerk FS.fabrikam.com konfiguriert haben \( \) . Die webanwendungsproxys sollten auch mit Internet \- zugänglichen IP-Adressen konfiguriert werden.  
  
In der folgenden Abbildung ist die vorhandene Verbund Serverfarm mit der bereits beschriebenen wid-Topologie dargestellt, und es wird erläutert, wie das fiktive Fabrikam, Inc., Unternehmen Zugriff auf einen Umkreis-DNS-Server bietet, einen zweiten NLB-Host mit dem gleichen DNS-Cluster Namen \( FS.fabrikam.com hinzufügt \) und dem Umkreis Netzwerk zwei webanwendungsproxys \( wap1 und WAP2 hinzufügt \) .  
  
![WID-Farm und Proxys](media/WIDFarmADFSBlue.gif)  
  
Weitere Informationen zum Konfigurieren der Netzwerkumgebung für die Verwendung mit Verbund Servern oder webanwendungsproxys finden Sie im Abschnitt "Anforderungen für die Namensauflösung" unter [AD FS Anforderungen](AD-FS-Requirements.md) und [Planen der webanwendungsproxy-Infrastruktur (WAP)](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11)).  
  
## <a name="see-also"></a>Weitere Informationen  
[Planen der AD FS-Bereitstellungstopologie](Plan-Your-AD-FS-Deployment-Topology.md)  
[AD FS-Entwurfshandbuch in Windows Server 2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  
