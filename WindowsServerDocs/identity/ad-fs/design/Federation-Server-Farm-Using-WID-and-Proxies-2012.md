---
ms.assetid: 8890ccc9-068d-4da2-bd51-8a2964173ff1
title: Verbundserverfarm mit WID und Proxys
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 60072037aea4ecd81376e1334f3a89b7bb2ff851
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408081"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>Verbundserverfarm mit WID und Proxys

Diese Bereitstellungs Topologie für Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 ist mit der Verbund Serverfarm mit der internen Windows-Datenbank \(WiD @ no__t-3-Topologie identisch, fügt jedoch Verbund Server Proxys zum Umkreis Netzwerk hinzu. externe Benutzer werden unterstützt. Die Verbund Server Proxys leiten Client Authentifizierungsanforderungen, die von außerhalb Ihres Unternehmensnetzwerks stammen, an die Verbund Serverfarm weiter.  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
In diesem Abschnitt werden verschiedene Überlegungen zu den beabsichtigten Zielgruppen, Vorteilen und Einschränkungen beschrieben, die mit dieser Bereitstellungs Topologie verknüpft sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Organisationen mit 100 oder weniger konfigurierten Vertrauens Stellungen, die sowohl interne als auch externe Benutzer \(bereit stellen müssen, die auf Computern angemeldet sind, die sich physisch außerhalb des Unternehmensnetzwerks befinden @ no__t-1 mit einmaligem Vorzeichen @ no__t-2ON \(sso @ no__t-4-Zugriff auf Verbund Anwendungen oder-Dienste  
  
-   Organisationen, die sowohl internen als auch externen Benutzern SSO-Zugriff auf Microsoft Office 365 bereitstellen müssen  
  
-   Kleinere Unternehmen, die externe Benutzer haben und redundante, skalierbare Dienste benötigen  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Welche Vorteile bietet die Verwendung dieser Topologie?  
  
-   Die gleichen Vorteile wie für die Verbund [Server Farm mit der wid](Federation-Server-Farm-Using-WID-2012.md) -Topologie sowie die Vorteile der Bereitstellung von zusätzlichem Zugriff für externe Benutzer.  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Welche Einschränkungen gelten für die Verwendung dieser Topologie?  
  
-   Die gleichen Einschränkungen wie für die Verbund [Server Farm werden mithilfe der wid](Federation-Server-Farm-Using-WID-2012.md) -Topologie aufgelistet.  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Empfehlungen zur Server Platzierung und zum Netzwerk Layout  
Um diese Topologie zusätzlich zum Hinzufügen von zwei Verbund Server Proxys bereitzustellen, müssen Sie sicherstellen, dass Ihr Umkreis Netzwerk auch Zugriff auf einen Domain Name System \(dns @ no__t-1-Server und auf einen zweiten Netzwerk Lastenausgleich \(nlb @ no__t-3-Host bereitstellen kann. Der zweite NLB-Host muss mit einem NLB-Cluster konfiguriert werden, der eine IP-Adresse für den Internet basierten @ no__t-IP-Cluster verwendet, und er muss die gleiche DNS-Namen Einstellung für den Cluster wie der vorherige NLB-Cluster verwenden, den Sie im Unternehmensnetzwerk @no__t -1FS. fabrikam. com @ no__t-2 konfiguriert haben. Die Verbund Server Proxys sollten auch mit Internet @ no__t-0accessible IP-Adressen konfiguriert werden.  
  
Die folgende Abbildung zeigt die vorhandene Verbund Serverfarm mit der zuvor beschriebenen wid-Topologie und die Funktionsweise der fiktiven fabrikam. Inc., Unternehmen ermöglicht den Zugriff auf einen Umkreis-DNS-Server, fügt einen zweiten NLB-Host mit dem gleichen DNS-Cluster Namen @no__t -0FS. fabrikam. com @ no__t-1 hinzu und fügt dem Umkreis Netzwerk zwei Verbund Server Proxys \(fsp1 und fsp2 @ no__t-3 hinzu.  
  
![Serverfarm mit wid](media/FarmWIDProxies.gif)  
  
Weitere Informationen zum Konfigurieren der Netzwerkumgebung für die Verwendung mit Verbund Servern oder Verbund Server Proxys finden Sie unter Anforderungen für die [Namensauflösung für Verbund Server](Name-Resolution-Requirements-for-Federation-Servers.md) oder [Anforderungen für die Namensauflösung für den Verbund. Server](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)Proxys.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
