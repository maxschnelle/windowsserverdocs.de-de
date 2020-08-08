---
ms.assetid: ec26705c-4446-4226-b9b4-b775b642f0f4
title: Platzieren eines Verbundserverproxys
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: e2494da552877e4ee69120f4eaee52a96c65a472
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962674"
---
# <a name="where-to-place-a-federation-server-proxy"></a>Platzieren eines Verbundserverproxys

Sie können Active Directory-Verbunddienste (AD FS) \( AD FS \) Verbund Server Proxys in einem Umkreis Netzwerk platzieren, um eine Schutz Ebene vor böswilligen Benutzern bereitzustellen, die aus dem Internet stammen können. Verbundserverproxys sind ideal für die Umkreisnetzwerkumgebung, da sie nicht über Zugriff auf die privaten Schlüssel verfügen, die zum Erstellen von Token verwendet werden. Allerdings können Verbund Server Proxys eingehende Anforderungen effizient an Verbund Server weiterleiten, die autorisiert sind, diese Token zu liefern.

Es ist nicht erforderlich, einen Verbund Server Proxy sowohl für den Konto Partner als auch für den Ressourcen Partner im Unternehmensnetzwerk zu platzieren, da Client Computer, die mit dem Unternehmensnetzwerk verbunden sind, direkt mit dem Verbund Server kommunizieren können. In diesem Szenario stellt der Verbund Server auch Verbund Server Proxy-Funktionen für Client Computer bereit, die aus dem Unternehmensnetzwerk stammen.

Wie bei Umkreis Netzwerken üblich, wird eine Firewall mit Intranetzugriff \- zwischen dem Umkreis Netzwerk und dem Unternehmensnetzwerk eingerichtet, und eine Firewall mit Internet Zugriff \- wird häufig zwischen dem Umkreis Netzwerk und dem Internet eingerichtet. In diesem Szenario befindet sich der Verbund Server Proxy zwischen beiden Firewalls im Umkreis Netzwerk.

## <a name="configuring-your-firewall-servers-for-a-federation-server-proxy"></a>Konfigurieren Ihrer Firewallserver für einen Verbundserverproxy
Damit der Verbund Server Proxy-Umleitungs Prozess erfolgreich ist, müssen alle Firewallserver so konfiguriert werden, dass \( HTTPS-Datenverkehr mit Secure Hypertext Transfer Protocol zugelassen wird \) . Die Verwendung von HTTPS ist erforderlich, da die Firewallserver den Verbund Server Proxy mithilfe von Port 443 veröffentlichen müssen, damit der Verbund Server Proxy im Umkreis Netzwerk auf den Verbund Server im Unternehmensnetzwerk zugreifen kann.

> [!NOTE]
> Die gesamte Kommunikation zu und von Clientcomputern wird ebenfalls über HTTPS abgewickelt.

Außerdem verwendet der Firewallserver mit Internet Zugriff, z. b. \- ein Computer, auf dem Microsoft Internet Security und Acceleration \( ISA Server ausgeführt \) wird, einen als Server Veröffentlichung bezeichneten Prozess, um Internet Client Anforderungen an die entsprechenden Umkreis-und Unternehmensnetzwerk Server zu verteilen, wie z. b. Verbund Server Proxys oder Verbund Server.

Regeln zur Server-Veröffentlichung bestimmen, wie die Server-Veröffentlichung funktioniert – im Wesentlichen Filtern aller über den ISA Server-Computer eingehenden und ausgehenden Anforderungen. Die Regeln zur Server-Veröffentlichung ordnen eingehende Clientanforderungen den entsprechenden Servern hinter dem ISA Server-Computer zu. Informationen zum Konfigurieren von ISA Server zum Veröffentlichen eines Servers finden Sie unter [Erstellen einer sicheren Webpublishing Regel](https://go.microsoft.com/fwlink/?LinkId=75182).

In der Verbund Umgebung von AD FS werden diese Client Anforderungen normalerweise an eine bestimmte URL gerichtet, z. b. an eine Verbund Server-Bezeichner-URL wie z. b. http: \/ /FS.fabrikam.com. Da diese Client Anforderungen aus dem Internet stammen, \- muss der Firewallserver mit Internet Zugriff so konfiguriert werden, dass die Verbund Server-ID-URL für jeden im Umkreis Netzwerk bereitgestellten Verbund Server Proxy veröffentlicht wird.

### <a name="configuring-isa-server-to-allow-ssl"></a>Konfigurieren von ISA Server zum Zulassen von SSL
Um die sichere AD FS Kommunikation zu vereinfachen, müssen Sie ISA Server so konfigurieren, dass Secure Sockets Layer \( SSL- \) Kommunikation zwischen den folgenden ermöglicht wird:

-   **Verbund Server und Verbund Server Proxys.** Ein SSL-Kanal ist für die gesamte Kommunikation zwischen Verbund Servern und Verbund Server Proxys erforderlich. Daher müssen Sie ISA Server zum Zulassen einer SSL-Verbindung zwischen dem Firmennetzwerk und dem Umkreisnetzwerk konfigurieren.

-   **Client Computer, Verbund Server und Verbund Server Proxys.** Damit die Kommunikation zwischen Client Computern und Verbund Servern oder zwischen Client Computern und Verbund Server Proxys erfolgen kann, können Sie einen Computer, auf dem ISA Server ausgeführt wird, vor dem Verbund Server oder dem Verbund Server Proxy platzieren.

    Wenn Ihre Organisation die SSL-Client Authentifizierung auf dem Verbund Server oder dem Verbund Server Proxy ausführt, muss der Server für die Weiterleitung der SSL-Verbindung konfiguriert werden, wenn Sie einen Computer, auf dem ISA Server ausgeführt wird, vor dem Verbund Server oder dem Verbund Server Proxy platzieren \- .

    Wenn Ihre Organisation keine SSL-Client Authentifizierung auf dem Verbund Server oder Verbund Server Proxy ausführt, besteht eine zusätzliche Möglichkeit darin, die SSL-Verbindung auf dem Computer zu beenden, der ISA Server ausführt, und dann \- eine SSL-Verbindung mit dem Verbund Server oder dem Verbund Server Proxy herzustellen.

> [!NOTE]
> Der Verbund Server oder Verbund Server Proxy erfordert, dass die Verbindung durch SSL gesichert wird, um den Inhalt des Sicherheits Tokens zu schützen.

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
