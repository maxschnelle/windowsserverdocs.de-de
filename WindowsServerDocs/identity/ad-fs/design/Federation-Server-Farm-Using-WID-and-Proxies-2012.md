---
ms.assetid: 8890ccc9-068d-4da2-bd51-8a2964173ff1
title: AD FS Verbund Server Farm mit wid und Proxys
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e70359b5a05fed8e7cfb467d3410e12939a1de1b
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864051"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>Verbundserverfarm mit WID und Proxies

Diese Bereitstellungs Topologie für Active Directory-Verbunddienste (AD FS) \( AD FS \) ist mit der Verbund Serverfarm mit der internen Windows-Datenbank- \( wid- \) Topologie identisch, fügt jedoch Verbund Server Proxys zum Umkreis Netzwerk hinzu, um externe Benutzer zu unterstützen. Die Verbund Server Proxys leiten Client Authentifizierungsanforderungen, die von außerhalb Ihres Unternehmensnetzwerks stammen, an die Verbund Serverfarm weiter.  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
In diesem Abschnitt werden verschiedene Überlegungen zu den beabsichtigten Zielgruppen, Vorteilen und Einschränkungen beschrieben, die mit dieser Bereitstellungs Topologie verknüpft sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Organisationen mit 100 oder weniger konfigurierten Vertrauens Stellungen, die sowohl interne als auch externe Benutzer, \( die auf Computern angemeldet sind, die sich physisch außerhalb des Unternehmensnetzwerks befinden, \) mit einmaligem \- Anmelden \( SSO- \) Zugriff auf Verbund Anwendungen oder-Dienste bereitstellen müssen  
  
-   Organisationen, die sowohl internen als auch externen Benutzern SSO-Zugriff auf Microsoft Office 365 bereitstellen müssen  
  
-   Kleinere Unternehmen, die externe Benutzer haben und redundante, skalierbare Dienste benötigen  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Welche Vorteile bietet die Verwendung dieser Topologie?  
  
-   Die gleichen Vorteile wie für die Verbund [Server Farm mit der wid](Federation-Server-Farm-Using-WID-2012.md) -Topologie sowie die Vorteile der Bereitstellung von zusätzlichem Zugriff für externe Benutzer.  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Welche Einschränkungen gelten für die Verwendung dieser Topologie?  
  
-   Die gleichen Einschränkungen wie für die Verbund [Server Farm werden mithilfe der wid](Federation-Server-Farm-Using-WID-2012.md) -Topologie aufgelistet.  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Empfehlungen zur Server Platzierung und zum Netzwerk Layout  
Um diese Topologie zusätzlich zum Hinzufügen von zwei Verbund Server Proxys bereitzustellen, müssen Sie sicherstellen, dass Ihr Umkreis Netzwerk auch Zugriff auf einen Domain Name System \( DNS \) -Server und auf einen zweiten \( NLB-Host für den Netzwerk Lastenausgleich bereitstellen kann \) . Der zweite NLB-Host muss mit einem NLB-Cluster konfiguriert werden, der eine \- IP-Adresse für den Internet zugänglichen Cluster verwendet, und er muss die gleiche DNS-Namen Einstellung des Clusters wie der vorherige NLB-Cluster verwenden, den Sie im Unternehmensnetzwerk FS.fabrikam.com konfiguriert haben \( \) . Die Verbund Server Proxys sollten auch mit Internet \- zugänglichen IP-Adressen konfiguriert werden.  
  
In der folgenden Abbildung ist die vorhandene Verbund Serverfarm mit der bereits beschriebenen wid-Topologie dargestellt, und es wird erläutert, wie das fiktive Fabrikam, Inc., Unternehmen Zugriff auf einen Umkreis-DNS-Server bietet, einen zweiten NLB-Host mit dem gleichen DNS-Cluster Namen \( FS.fabrikam.com hinzufügt \) und dem Umkreis Netzwerk zwei Verbund Server Proxys \( fsp1 und fsp2 hinzufügt \) .  
  
![Serverfarm mit wid](media/FarmWIDProxies.gif)  
  
Weitere Informationen zum Konfigurieren der Netzwerkumgebung für die Verwendung mit Verbund Servern oder Verbund Server Proxys finden Sie unter Anforderungen für die [Namensauflösung für Verbund Server](Name-Resolution-Requirements-for-Federation-Servers.md) oder [Anforderungen für die Namensauflösung für Verbund Server](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)Proxys.  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
