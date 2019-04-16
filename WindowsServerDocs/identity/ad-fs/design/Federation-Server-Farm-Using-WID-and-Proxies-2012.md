---
ms.assetid: 8890ccc9-068d-4da2-bd51-8a2964173ff1
title: Verbundserverfarm mit WID und Proxys
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4bd815daccdd72a8c612b9b728ce12378c1926e7
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>Verbundserverfarm mit WID und Proxys

>Gilt für: Windows Server 2012

Dieser Bereitstellungstopologie für Active Directory Federation Services \(AD FS\) ist identisch mit der Verbundserverfarm mit internen Windows-Datenbank \(WID\) Topologie, jedoch mit dem Umkreisnetzwerk zur Unterstützung von externer Benutzern Verbundserverproxys hinzugefügt. Die Verbundserverproxys umleiten clientauthentifizierungsanfragen, die von außerhalb des Unternehmensnetzwerks an die Verbundserverfarm stammen.  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
Dieser Abschnittbeschreibt die verschiedenen Aspekte über die Zielgruppe, Vorteile und Einschränkungen, die dieser Bereitstellungstopologie zugeordnet sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Organisationen mit bis zu 100 konfigurierten Vertrauensstellungen, die ihre interne Benutzer und die externe Benutzer angeben müssen \ (angemeldet sind für Computer, die physisch außerhalb der Unternehmen vom Netzwerk befinden) mit einzelnen Standardparameter-\(SSO\) Zugriff auf verbundanwendungen oder -Dienste  
  
-   Organisationen, die ihre interne Benutzer und den externen Benutzern SSO-Zugriff auf Microsoft Office365 zu ermöglichen  
  
-   Kleinere Organisationen, die externe Benutzer zugreifen und erfordern redundante, skalierbare Dienste  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Was sind die Vorteile der Verwendung dieser Topologie?  
  
-   Die gleichen Vorteile für die aufgeführten der [Verbundserver mit WID](Federation-Server-Farm-Using-WID-2012.md) Topologie sowie die dafür gesorgt, zusätzliche Zugriffsrechte für externe Benutzer  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Was sind die Grenzen der Verwendung dieser Topologie?  
  
-   Die gleichen Einschränkungen aufgeführt sind, für die [Verbundserver mit WID](Federation-Server-Farm-Using-WID-2012.md) Topologie  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Der Empfehlungen für die Platzierung und Netzwerk Layout Server  
Zum Bereitstellen dieser Topologie wird zusätzlich zum Hinzufügen von zwei Verbundserverproxys, müssen Sie sicherstellen, dass das Umkreisnetzwerk ebenfalls Zugriff auf einen Server Domain Name System \(DNS\) und einen zweiten Netzwerklastenausgleich \(NLB\)-Host bereitgestellt werden kann. Der zweite NLB-Host muss konfiguriert werden, mit einem NLB-Cluster, die eine möglicherweise zugängliche Cluster-IP-Adresse verwendet, und es muss dieselbe Einstellung der Cluster-DNS-Namen verwenden, als die vorherigen NLB-Cluster, den Sie auf das Unternehmensnetzwerk \(fs.fabrikam.com\) konfiguriert. Die Verbundserverproxys sollten auch mit möglicherweise erreichbaren IP-Adressen konfiguriert werden.  
  
Die folgende Abbildungzeigt die vorhandenen Verbundserverfarm mit WID-Topologie, die zuvor beschriebenen und wie die fiktive Unternehmen Fabrikam, Inc., Zugriff auf ein Umkreisnetzwerk-DNS-Server bietet ein zweiter NLB-Host mit dem gleichen Cluster-DNS-Namen \(fs.fabrikam.com\) hinzugefügt, und fügt zwei Verbundserverproxys \(fsp1 and fsp2\) mit dem Umkreisnetzwerk.  
  
![Server-Farm mit WID](media/FarmWIDProxies.gif)  
  
Weitere Informationen zum Konfigurieren der Netzwerkumgebung für die Verwendung Verbundserver und Verbundserverproxys finden Sie unter [Name Resolution Requirements for Federation Servers](Name-Resolution-Requirements-for-Federation-Servers.md) oder [Name Resolution Requirements for Federation Server Proxies](Name-Resolution-Requirements-for-Federation-Server-Proxies.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
