---
ms.assetid: 8890ccc9-068d-4da2-bd51-8a2964173ff1
title: Verbundserverfarm mit WID und Proxys
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4bd815daccdd72a8c612b9b728ce12378c1926e7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817621"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>Verbundserverfarm mit WID und Proxys

>Gilt für: Windows Server 2012

Dieser Bereitstellungstopologie für Active Directory Federation Services \(AD FS\) ist mit der Verbundserverfarm mit internen Windows-Datenbank \(WID\) Topologie, sondern fügt Verbundserverproxys mit dem Umkreisnetzwerk zur Unterstützung von externer Benutzern. Die Verbundserverproxys umleiten clientauthentifizierungsanforderungen, die von außerhalb des Unternehmensnetzwerks an die Verbundserverfarm stammen.  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
Dieser Abschnitt beschreibt verschiedene Überlegungen zu den Zielgruppe, Vorteile und Einschränkungen, die mit dieser Bereitstellungstopologie verknüpft sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Organisationen mit bis zu 100 konfigurierten Vertrauensstellungen, die sowohl für ihre interne Benutzer und externe Benutzer bieten \(angemeldet sind auf Computern, die physisch außerhalb des Unternehmensnetzwerks befinden\) mit einzelnen Anmeldung\-auf \(SSO\) Zugriff auf verbundanwendungen oder-Dienste  
  
-   Organisationen, die sowohl ihre internen Benutzer als auch die externe Benutzer SSO-Zugriff für Microsoft Office 365 bereitstellen müssen  
  
-   Kleinere Organisationen, die externe Benutzer und redundant, skalierbare Dienste erfordern  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Was sind die Vorteile der Verwendung dieser Topologie?  
  
-   Die gleichen Vorteile wie für die [Federation Server Farm mit WID](Federation-Server-Farm-Using-WID-2012.md) Topologie sowie den Vorteil, dass bietet zusätzlichen Zugriff für externe Benutzer  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Was sind die Einschränkungen bei der Verwendung dieser Topologie?  
  
-   Dieselben Einschränkungen wie für die aufgelisteten der [Federation Server Farm mit WID](Federation-Server-Farm-Using-WID-2012.md) Topologie  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Server Platzierung und Netzwerk-Layout-Empfehlungen  
Zum Bereitstellen dieser Topologie wird zusätzlich zum Hinzufügen von zwei Verbundserverproxys, achten Sie darauf, dass es sich bei Ihrem Umkreisnetzwerk, auch über Zugriff auf einen Domain Name System ermöglicht \(DNS\) Server und eine zweite Netzwerklastenausgleich \(NLB\) Host. Der zweite NLB-Host muss konfiguriert werden, mit einem NLB-Cluster, die einen mit dem Internet verwendet\-zugegriffen werden Cluster-IP-Adresse, und es müssen die gleiche Cluster-DNS-namenseinstellung verwenden, wie der vorherige NLB-Cluster, die Sie über das Unternehmensnetzwerk konfiguriert \( "FS.Fabrikam.com"\). Die Verbundserverproxys auch mit dem Internet konfiguriert werden\-zugegriffen werden IP-Adressen.  
  
Die folgende Abbildung zeigt die vorhandenen Verbundserverfarm mit WID-Topologie, die zuvor beschrieben wurde, und wie das fiktive Unternehmen Fabrikam, Inc., einem Umkreis-DNS-Server, ermöglicht hinzugefügt ein zweiter NLB-Host mit dem gleichen DNS-Clusternamen \("FS.Fabrikam.com"\), und fügt zwei Verbundserverproxys \(fsp1 und fsp2\) mit dem Umkreisnetzwerk.  
  
![Serverfarm mit WID](media/FarmWIDProxies.gif)  
  
Weitere Informationen dazu, wie Sie Ihre Netzwerkumgebung für die Verwendung mit Verbundserver oder Verbundserverproxys konfigurieren zu können, finden Sie unter [Namensauflösungsanforderungen für Verbundserver](Name-Resolution-Requirements-for-Federation-Servers.md) oder [Name Anforderungen für die namensauflösung für Verbundserverproxies](Name-Resolution-Requirements-for-Federation-Server-Proxies.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
