---
ms.assetid: f0464182-56a2-4bfa-a8c8-7e39c1bd62d3
title: Verbundserverfarm mit WID und Proxys
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e372f066fc82b9857d438234b491732a177e24fa
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>Verbundserverfarm mit WID und Proxys

>Gilt für: Windows Server 2016, Windows Server2012 R2

Dieser Bereitstellungstopologie für Active Directory Federation Services \(AD FS\) ist identisch mit der Verbundserverfarm mit internen Windows-Datenbank \(WID\) Topologie-Computer mit dem Umkreisnetzwerk zur Unterstützung von externer Benutzern hinzugefügt. Diese Proxys umleiten clientauthentifizierungsanfragen, die von außerhalb des Unternehmensnetzwerks an die Verbundserverfarm stammen. In früheren Versionen von AD FS wurden diese Proxys Verbundserverproxys bezeichnet.  
  
> [!IMPORTANT]  
> In Active Directory Federation Services \(AD FS\) in Windows Server2012 R2 wird die Rolle eines Verbundserverproxys durch einen neuen Remotezugriff-Rollendienst namens Webanwendungsproxy behandelt. Zum Aktivieren von AD FS ermöglichen den Zugriff von außerhalb des Unternehmensnetzwerks, war der Zweck der Bereitstellung eines Verbundserverproxys in Legacyversionen von AD FS, z.B. AD FS 2.0 und AD FS unter Windows Server2012 können Sie eine oder mehrere webanwendungsproxys für AD FS unter Windows Server2012 R2 bereitstellen.  
>   
> Im Kontext von AD FS funktioniert Web Application Proxy als ein AD FS-Verbundserverproxy. Darüber hinaus bietet Webanwendungsproxy Reverseproxyfunktionen für Webanwendungen in Ihrem Unternehmensnetzwerk So ermöglichen Sie Benutzern auf einem beliebigen Gerät für den Zugriff darauf von außerhalb des Unternehmensnetzwerks. Weitere Informationen über den Webanwendungsproxy-Rollendienst finden Sie im Web Application Proxy (Übersicht).  
>   
> Bei der Planung die Bereitstellung von Web Application Proxy können Sie überprüfen, die Informationen in den folgenden Themen:  
>   
> -   [Planen der Infrastruktur für Webanwendungsproxy (WAP)](https://technet.microsoft.com/library/dn383648.aspx)  
> -   [Planen der Webanwendungsproxy-Servers](https://technet.microsoft.com/library/dn383647.aspx)  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
Dieser Abschnittbeschreibt die verschiedenen Aspekte über die Zielgruppe, Vorteile und Einschränkungen, die dieser Bereitstellungstopologie zugeordnet sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Organisationen mit bis zu 100 konfigurierten Vertrauensstellungen, die ihre interne Benutzer und die externe Benutzer angeben müssen \ (angemeldet sind für Computer, die physisch außerhalb der Unternehmen vom Netzwerk befinden) mit einzelnen Standardparameter-\(SSO\) Zugriff auf verbundanwendungen oder -Dienste  
  
-   Organisationen, die ihre interne Benutzer und den externen Benutzern SSO-Zugriff auf Microsoft Office365 zu ermöglichen  
  
-   Kleinere Organisationen, die externe Benutzer zugreifen und erfordern redundante, skalierbare Dienste  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Was sind die Vorteile der Verwendung dieser Topologie?  
  
-   Die gleichen Vorteile für die aufgeführten der [Verbundserver mit WID](Federation-Server-Farm-Using-WID.md) Topologie sowie die dafür gesorgt, zusätzliche Zugriffsrechte für externe Benutzer  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Was sind die Grenzen der Verwendung dieser Topologie?  
  
-   Die gleichen Einschränkungen aufgeführt sind, für die [Verbundserver mit WID](Federation-Server-Farm-Using-WID.md) Topologie  

||1 \-100 RP-Vertrauensstellungen|Mehr als 100 RP-Vertrauensstellungen 
| ----- |-----| ------ |
|1 \-30-AD FS-Knoten|Interne Windows-Datenbank unterstützt|Nicht unterstützt, mit WID \-SQL erforderlich 
|Mehr als 30 AD FS-Knoten|Nicht unterstützt, mit WID \-SQL erforderlich|Nicht unterstützt, mit WID \-SQL erforderlich  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Der Empfehlungen für die Platzierung und Netzwerk Layout Server  
Zum Bereitstellen dieser Topologie wird zusätzlich zum Hinzufügen von zwei webanwendungsproxys, müssen Sie sicherstellen, dass das Umkreisnetzwerk ebenfalls Zugriff auf einen Server Domain Name System \(DNS\) und einen zweiten Netzwerklastenausgleich \(NLB\)-Host bereitgestellt werden kann. Der zweite NLB-Host muss konfiguriert werden, mit einem NLB-Cluster, die eine möglicherweise zugängliche Cluster-IP-Adresse verwendet, und es muss dieselbe Einstellung der Cluster-DNS-Namen verwenden, als die vorherigen NLB-Cluster, den Sie auf das Unternehmensnetzwerk \(fs.fabrikam.com\) konfiguriert. Die webanwendungsproxys sollten auch mit möglicherweise erreichbaren IP-Adressen konfiguriert werden.  
  
Die folgende Abbildungzeigt die vorhandenen Verbundserverfarm mit WID-Topologie, die zuvor beschriebenen und wie die fiktive Unternehmen Fabrikam, Inc., Zugriff auf ein Umkreisnetzwerk-DNS-Server bietet ein zweiter NLB-Host mit dem gleichen Cluster-DNS-Namen \(fs.fabrikam.com\) hinzugefügt, und fügt zwei webanwendungsproxys \(wap1 and wap2\) mit dem Umkreisnetzwerk.  
  
![Farm mit WID und Proxys](media/WIDFarmADFSBlue.gif)  
  
Weitere Informationen zum Konfigurieren der Netzwerkumgebung für die Verwendung mit Verbundserver oder webanwendungsproxys finden Sie unter "Namensauflösungsanforderungen" im Abschnitt [AD FS-Anforderungen](AD-FS-Requirements.md) und [Planen der Web Application Proxy-Infrastruktur (WAP)](https://technet.microsoft.com/library/dn383648.aspx).  
  
## <a name="see-also"></a>Siehe auch  
[Planen der AD FS-Bereitstellungstopologie](Plan-Your-AD-FS-Deployment-Topology.md)  
[AD FS-Entwurfshandbuch in Windows Server2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

