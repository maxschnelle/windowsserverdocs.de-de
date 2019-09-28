---
ms.assetid: ec26705c-4446-4226-b9b4-b775b642f0f4
title: Platzieren eines Verbundserverproxys
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 73e68d03e4f2f76dbaf4a497da551640476d0438
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407827"
---
# <a name="where-to-place-a-federation-server-proxy"></a>Platzieren eines Verbundserverproxys

Sie können Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1federation-Server Proxys in einem Umkreis Netzwerk platzieren, um eine Schutz Ebene vor böswilligen Benutzern bereitzustellen, die aus dem Internet stammen können. Verbundserverproxys sind ideal für die Umkreisnetzwerkumgebung, da sie nicht über Zugriff auf die privaten Schlüssel verfügen, die zum Erstellen von Token verwendet werden. Allerdings können Verbund Server Proxys eingehende Anforderungen effizient an Verbund Server weiterleiten, die autorisiert sind, diese Token zu liefern.  
  
Es ist nicht erforderlich, einen Verbund Server Proxy sowohl für den Konto Partner als auch für den Ressourcen Partner im Unternehmensnetzwerk zu platzieren, da Client Computer, die mit dem Unternehmensnetzwerk verbunden sind, direkt mit dem Verbund Server kommunizieren können. In diesem Szenario stellt der Verbund Server auch Verbund Server Proxy-Funktionen für Client Computer bereit, die aus dem Unternehmensnetzwerk stammen.  
  
Wie bei Umkreis Netzwerken üblich, wird zwischen dem Umkreis Netzwerk und dem Unternehmensnetzwerk eine Intranetbereitstellung mit dem Wert no__t und eine Internetverbindung mit der no__t-IP-Adresse, die häufig zwischen dem Umkreis Netzwerk und dem Internet hergestellt wird. In diesem Szenario befindet sich der Verbund Server Proxy zwischen beiden Firewalls im Umkreis Netzwerk.  
  
## <a name="configuring-your-firewall-servers-for-a-federation-server-proxy"></a>Konfigurieren Ihrer Firewallserver für einen Verbundserverproxy  
Damit der Prozess des Verbund Server Proxys erfolgreich ausgeführt werden kann, müssen alle Firewallserver so konfiguriert sein, dass Secure Hypertext Transfer Protocol \(https @ no__t-1-Datenverkehr zugelassen wird. Die Verwendung von HTTPS ist erforderlich, da die Firewallserver den Verbund Server Proxy mithilfe von Port 443 veröffentlichen müssen, damit der Verbund Server Proxy im Umkreis Netzwerk auf den Verbund Server im Unternehmensnetzwerk zugreifen kann.  
  
> [!NOTE]  
> Die gesamte Kommunikation zu und von Clientcomputern wird ebenfalls über HTTPS abgewickelt.  
  
Außerdem verwendet der Firewallserver mit Internet @ no__t-0 (z. b. ein Computer, auf dem Microsoft Internet Security und Acceleration \(ISA @ no__t-2 Server ausgeführt wird) einen als Server Veröffentlichung bezeichneten Prozess, um Internet Client Anforderungen an die entsprechende Umkreis Netzwerk-und Unternehmensnetzwerk Server, z. b. Verbund Server Proxys oder Verbund Server.  
  
Regeln zur Server-Veröffentlichung bestimmen, wie die Server-Veröffentlichung funktioniert – im Wesentlichen Filtern aller über den ISA Server-Computer eingehenden und ausgehenden Anforderungen. Die Regeln zur Server-Veröffentlichung ordnen eingehende Clientanforderungen den entsprechenden Servern hinter dem ISA Server-Computer zu. Informationen zum Konfigurieren von ISA Server zum Veröffentlichen eines Servers finden Sie unter [Erstellen einer sicheren Webpublishing Regel](https://go.microsoft.com/fwlink/?LinkId=75182).  
  
In der Verbund Umgebung von AD FS werden diese Client Anforderungen normalerweise an eine bestimmte URL gerichtet, z. b. an eine Verbund Server-Bezeichner-URL wie z. b. http: \//FS. fabrikam. com. Da diese Client Anforderungen aus dem Internet stammen, muss der Firewallserver mit Internet @ no__t-0 für die Veröffentlichung der Verbund Server-ID-URL für jeden im Umkreis Netzwerk bereitgestellten Verbund Server Proxy konfiguriert werden.  
  
### <a name="configuring-isa-server-to-allow-ssl"></a>Konfigurieren von ISA Server zum Zulassen von SSL  
Um die sichere AD FS Kommunikation zu vereinfachen, müssen Sie ISA Server so konfigurieren, dass die Kommunikation zwischen den folgenden Secure Sockets Layer \(ssl @ no__t-1 ermöglicht wird:  
  
-   **Verbund Server und Verbund Server Proxys.** Ein SSL-Kanal ist für die gesamte Kommunikation zwischen Verbund Servern und Verbund Server Proxys erforderlich. Daher müssen Sie ISA Server zum Zulassen einer SSL-Verbindung zwischen dem Firmennetzwerk und dem Umkreisnetzwerk konfigurieren.  
  
-   **Client Computer, Verbund Server und Verbund Server Proxys.** Damit die Kommunikation zwischen Client Computern und Verbund Servern oder zwischen Client Computern und Verbund Server Proxys erfolgen kann, können Sie einen Computer, auf dem ISA Server ausgeführt wird, vor dem Verbund Server oder dem Verbund Server Proxy platzieren.  
  
    Wenn Ihre Organisation SSL-Client Authentifizierung auf dem Verbund Server oder Verbund Server Proxy ausführt, muss der Server für Pass @ no__ konfiguriert werden, wenn Sie einen Computer, auf dem ISA Server ausgeführt wird, vor dem Verbund Server oder Verbund Server Proxy platzieren. t-0through der SSL-Verbindung, da die SSL-Verbindung auf dem Verbund Server oder dem Verbund Server Proxy beendet werden muss.  
  
    Wenn Ihre Organisation keine SSL-Client Authentifizierung auf dem Verbund Server oder Verbund Server Proxy ausführt, besteht eine zusätzliche Möglichkeit darin, die SSL-Verbindung auf dem Computer zu beenden, der ISA Server ausführt, und dann erneut @ no__t-0herstellen einer SSL-Verbindung mit dem Verbund Server oder Verbund Server Proxy.  
  
> [!NOTE]  
> Der Verbund Server oder Verbund Server Proxy erfordert, dass die Verbindung durch SSL gesichert wird, um den Inhalt des Sicherheits Tokens zu schützen.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
