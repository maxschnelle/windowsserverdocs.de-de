---
ms.assetid: ec26705c-4446-4226-b9b4-b775b642f0f4
title: Platzieren eines Verbundserverproxys
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4bde30f694c6490962edaa0c3fe1543e74ba7fd7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842981"
---
# <a name="where-to-place-a-federation-server-proxy"></a>Platzieren eines Verbundserverproxys

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können Active Directory Federation Services platzieren \(AD FS\)Verbundserverproxys in einem Umkreisnetzwerk, eine Schutzebene vor böswilligen Benutzern bereitzustellen, die über das Internet zugreifen könnten. Verbundserverproxys sind ideal für die Umkreisnetzwerkumgebung, da sie nicht über Zugriff auf die privaten Schlüssel verfügen, die zum Erstellen von Token verwendet werden. Allerdings können Verbundserverproxys effizient eingehende Anforderungen für Verbundserver weiterleiten, die autorisiert sind, um die Token zu erzeugen.  
  
Es ist nicht notwendig, einen Verbundserverproxy innerhalb des Unternehmensnetzwerks für den Kontopartner oder der Ressourcenpartnerorganisation platziert werden, da Clientcomputer, die mit dem Unternehmensnetzwerk verbunden sind direkt mit dem Verbundserver kommunizieren können. In diesem Szenario hinaus des Verbundservers Federation Server Proxy-Funktionalität für Clientcomputer, die aus dem Unternehmensnetzwerk kommen.  
  
Wie bei Umkreisnetzwerken, ein Intranet üblich ist\-wird mit der Firewall zwischen dem Umkreisnetzwerk und dem Unternehmensnetzwerk verbunden und einen mit dem Internet hergestellt\-mit der Firewall wird häufig zwischen dem Umkreisnetzwerk eingerichtet und die Internet. In diesem Szenario befindet sich der Verbundserverproxy zwischen diesen Firewalls im Umkreisnetzwerk ein.  
  
## <a name="configuring-your-firewall-servers-for-a-federation-server-proxy"></a>Konfigurieren Ihrer Firewallserver für einen Verbundserverproxy  
Für den Federation Server Proxy Umleitung Prozess erfolgreich ist, müssen alle Firewallserver zum Zulassen von Secure Hypertext Transfer Protocol konfiguriert werden \(HTTPS\) Datenverkehr. Die Verwendung von HTTPS ist erforderlich, weil die Firewallserver veröffentlichen müssen Verbundserverproxys, verwenden Port 443, damit der Verbundserverproxy im Umkreisnetzwerk der Verbundserver im Unternehmensnetzwerk zugreifen kann.  
  
> [!NOTE]  
> Die gesamte Kommunikation zu und von Clientcomputern wird ebenfalls über HTTPS abgewickelt.  
  
Darüber hinaus das Internet\-für Firewallserver, z. B. einen Computer mit Microsoft Internet Security und Acceleration \(ISA\) -Server verwendet einen als serververöffentlichung bezeichneten Prozess zum Verteilen der Internetclient Anforderungen an die entsprechenden Umkreisnetzwerk- und Unternehmensnetzwerk-Server, z. B. Verbundserverproxys oder Verbundserver.  
  
Regeln zur Server-Veröffentlichung bestimmen, wie die Server-Veröffentlichung funktioniert – im Wesentlichen Filtern aller über den ISA Server-Computer eingehenden und ausgehenden Anforderungen. Die Regeln zur Server-Veröffentlichung ordnen eingehende Clientanforderungen den entsprechenden Servern hinter dem ISA Server-Computer zu. Informationen zum Konfigurieren von ISA Server zum Veröffentlichen eines Servers finden Sie unter [Erstellen einer sicheren Webveröffentlichungsregel](https://go.microsoft.com/fwlink/?LinkId=75182).  
  
In der verbundumgebung von AD FS, diese Clientanforderungen werden in der Regel versucht, eine bestimmte URL, z. B. eine Verbund-ID-URL wie z. B. http://fs.fabrikam.com. Da diese Clientanforderungen kommt in aus dem Internet, das Internet\-mit Internetzugriff Firewallserver muss konfiguriert werden, um die Verbund-Server-Bezeichner-URL für jeden Verbundserverproxy zu veröffentlichen, die im Umkreisnetzwerk bereitgestellt wird.  
  
### <a name="configuring-isa-server-to-allow-ssl"></a>Konfigurieren von ISA Server zum Zulassen von SSL  
Um sichere AD FS-Kommunikation zu ermöglichen, müssen Sie ISA Server zum Zulassen von Secure Sockets Layer konfigurieren \(SSL\) Kommunikation zwischen den folgenden:  
  
-   **Verbundserver und Verbundserverproxys bestimmen.** Ein SSL-Kanal ist für die gesamte Kommunikation zwischen Verbundservern und verbundserverproxies erforderlich. Daher müssen Sie ISA Server zum Zulassen einer SSL-Verbindung zwischen dem Firmennetzwerk und dem Umkreisnetzwerk konfigurieren.  
  
-   **Clientcomputer, Verbundservern und Verbundserverproxys bestimmen.** So, dass die Kommunikation zwischen Clientcomputern und Verbundserver oder zwischen Clientcomputern und Verbundserverproxys auftreten können, können Sie einen Computer mit ISA Server vor die Verbundserver- oder Verbundserverproxy platzieren.  
  
    Wenn Ihre Organisation SSL-Clientauthentifizierung für die Verbundserver- oder Verbundserverproxy ausführt, wenn Sie einen Computer mit ISA Server vor die Verbundserver- oder Verbundserverproxy platzieren, muss der Server konfiguriert sein, für die Übergabe\-über SSL-Verbindung, da die SSL-Verbindung an den Verbundserver oder Verbundserverproxy beendet werden muss.  
  
    Wenn Ihre Organisation nicht SSL-Clientauthentifizierung für die Verbundserver- oder Verbundserverproxy durchgeführt wird, wird eine weitere Option ist, um die SSL-Verbindung auf dem Computer mit ISA Server, und klicken Sie dann erneut beenden\-, SSL-Verbindung herstellen die Verbundserver- oder Verbundserverproxy.  
  
> [!NOTE]  
> Die Verbundserver- oder Verbundserverproxy erfordert, dass die Verbindung durch SSL, um den Inhalt des Sicherheitstokens zu schützen gesichert wird.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
