---
ms.assetid: ec26705c-4446-4226-b9b4-b775b642f0f4
title: Where to Place a Federation Serverproxy
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4bde30f694c6490962edaa0c3fe1543e74ba7fd7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="where-to-place-a-federation-server-proxy"></a>Where to Place a Federation Serverproxy

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sie können Active Directory Federation Services \(AD FS\) Verbundserverproxys platzieren, in einem Umkreisnetzwerk, um eine Schutzebene vor böswilligen Benutzern bereitzustellen, die über das Internet zugreifen könnten. Verbundserverproxys sind ideal für die umkreisnetzwerkumgebung, da sie nicht über Zugriff auf die privaten Schlüssel verfügen, die zum Erstellen von Token verwendet werden. Allerdings können Verbundserverproxys effizient eingehende Anforderungen an Verbundserver weiterleiten, die berechtigt sind, diese Token zu erzeugen.  
  
Es ist nicht erforderlich, einen Verbundserverproxy innerhalb des Unternehmensnetzwerks für den Kontopartner oder der Ressourcenpartnerorganisation platzieren, da Clientcomputer, die mit dem Unternehmensnetzwerk verbunden sind direkt mit dem Verbundserver kommunizieren können. In diesem Szenario bietet der Verbundserver auch Federation Server Proxy-Funktionalität für Clientcomputer, die aus dem Unternehmensnetzwerk kommen.  
  
Wie bei Umkreisnetzwerken ist, wird eine Intranet\ gerichtete Firewall zwischen dem Umkreisnetzwerk und dem Unternehmensnetzwerk eingerichtet, und eine Firewall möglicherweise gerichtete wird häufig zwischen dem Umkreisnetzwerk und dem Internet eingerichtet. Befindet sich in diesem Szenario wird der Verbundserverproxy zwischen diesen Firewalls im Umkreisnetzwerk.  
  
## <a name="configuring-your-firewall-servers-for-a-federation-server-proxy"></a>Konfigurieren der Firewallserver für einen Verbundserverproxy  
Für die Federation Server Proxy-Weiterleitung erfolgreich ausgeführt werden kann müssen alle Firewallserver für die Secure Hypertext Transfer Protocol-\(HTTPS\) Datenverkehr zugelassen konfiguriert werden. Die Verwendung von HTTPS ist erforderlich, weil die Firewallserver veröffentlichen müssen Verbundserverproxys, über den Port 443, sodass der Verbundserverproxy im Umkreisnetzwerk den Verbundserver im Unternehmensnetzwerk zugreifen kann.  
  
> [!NOTE]  
> Gesamte Kommunikation zu und von Clientcomputern auch über HTTPS abgewickelt.  
  
Darüber hinaus möglicherweise gerichtete Firewall-Server, z.B. einem Computer mit Microsoft Internet Security and Acceleration \(ISA\)-Server verwendet einen als serververöffentlichung bezeichneten Prozess, um Internet-Clientanforderungen an die entsprechenden Umkreisnetzwerk- und Unternehmensnetzwerk-Server, z.B. Verbundserverproxys oder Verbundserver zu verteilen.  
  
Regeln zur Server-Veröffentlichung bestimmen, wie Server-Veröffentlichung funktioniert – im Wesentlichen Filtern aller eingehende und ausgehende Anforderungen über den ISA Server-Computer. Regeln zur Server-Veröffentlichung ordnen eingehende Clientanforderungen den entsprechenden Servern hinter dem ISA Server-Computer. Informationen zur Vorgehensweise beim Konfigurieren von ISA Server zum Veröffentlichen eines Servers finden Sie unter [Erstellen einer sicheren Webveröffentlichungsregel](https://go.microsoft.com/fwlink/?LinkId=75182).  
  
In der verbundumgebung von AD FS werden diese Clientanforderungen normalerweise an eine bestimmte URL, z.B. eine Federation Server Bezeichner-URL wie http://fs.fabrikam.com vorgenommen. Da diese Clientanforderungen kommt in aus dem Internet, die möglicherweise Firewallserver muss konfiguriert werden um die Verbundserverproxy-Bezeichner-URL für jeden Verbundserverproxy zu veröffentlichen, die im Umkreisnetzwerk bereitgestellt wird.  
  
### <a name="configuring-isa-server-to-allow-ssl"></a>Konfigurieren von ISA Server zum Zulassen von SSL  
Um sichere AD FS-Kommunikation zu ermöglichen, müssen Sie ISA Server zum Zulassen von Secure Sockets Layer \(SSL\) Kommunikation zwischen den folgenden konfigurieren:  
  
-   **Verbundserver und Verbundserverproxys.** Ein SSL-Kanal ist für die gesamte Kommunikation zwischen Verbundservern und Verbundserverproxys erforderlich. Aus diesem Grund müssen Sie ISA Server zum Zulassen einer SSL-Verbindungs zwischen dem Unternehmensnetzwerk und dem Umkreisnetzwerk konfigurieren.  
  
-   **Clientcomputer, Verbundserver und Verbundserverproxys.** So, dass die Kommunikation zwischen Clientcomputern und Verbundserver oder zwischen Clientcomputern und Verbundserverproxys ausgeführt werden können, können Sie einen Computer mit ISA Server vor der Verbundserver oder Verbundserverproxy platzieren.  
  
    Wenn Ihre Organisation SSL-Clientauthentifizierung auf dem Verbundserver oder Verbundserverproxy, führt Wenn Sie einen Computer mit ISA Server vor der Verbundserver oder Verbundserverproxy platzieren, muss der Server konfiguriert werden, für Pass\-durch die SSL-Verbindung, da die SSL-Verbindung auf den Verbundserver oder Verbundserverproxy beendet werden muss.  
  
    Wenn Ihre Organisation nicht über SSL-Clientauthentifizierung auf dem Verbundserver oder Verbundserverproxy durchführt, wird eine zusätzliche Option zum Beenden des SSL-Verbindungs auf dem Computer mit ISA Server, und klicken Sie dann erneut-SSL-Verbindung an den Verbundserver oder Verbundserverproxy herstellen.  
  
> [!NOTE]  
> Der Verbundserver oder Verbundserverproxy erfordert, dass die Verbindung durch SSL auf den Inhalt des Sicherheitstokens zu schützen gesichert werden.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
