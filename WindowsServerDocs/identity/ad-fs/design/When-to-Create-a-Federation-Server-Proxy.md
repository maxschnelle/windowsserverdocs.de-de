---
ms.assetid: aa20c8b3-7f01-4165-8b73-92642bff9676
title: Wann sollte ein Verbundserverproxy erstellt werden?
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: f3325efe7acf8b0b0469489e8d9a42614a5af54a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358849"
---
# <a name="when-to-create-a-federation-server-proxy"></a>Wann sollte ein Verbundserverproxy erstellt werden?

Beim Erstellen eines Verbund Server Proxys in Ihrer Organisation werden Ihrer Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1-Bereitstellung zusätzliche Sicherheitsebenen hinzugefügt. Sie sollten einen Verbund Server Proxy im Umkreis Netzwerk Ihrer Organisation bereitstellen, wenn Sie Folgendes tun möchten:  
  
-   Verhindern, dass externe Client Computer direkt auf Ihre Verbund Server zugreifen. Durch die Bereitstellung eines Verbund Server Proxys in Ihrem Umkreis Netzwerk isolieren Sie effektiv Ihre Verbund Server so, dass nur Client Computer, die über Verbund Server Proxys im Unternehmensnetzwerk angemeldet sind, auf Sie zugreifen können. der externen Client Computer. Verbundserverproxys können nicht auf die privaten Schlüssel zugreifen, die verwendet werden, um Token zu erzeugen. Weitere Informationen finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md).  
  
-   Stellen Sie eine bequeme Möglichkeit dar, das Vorzeichen @ no__t-0in der Benutzer Darstellung für Benutzer zu unterscheiden, die aus dem Internet stammen, und nicht für Benutzer, die über die integrierte Windows-Authentifizierung aus Ihrem Unternehmensnetzwerk kommen. Ein Verbund Server Proxy sammelt Anmelde Informationen oder Startbereichs Details von Internet Client Computern mithilfe der auf dem Verbund Server Proxy gespeicherten Seiten für Anmeldung, Abmeldung und Identitäts Anbieter Ermittlung @no__t -0homerealmdiscovery. aspx @ no__t-1.  
  
    Im Gegensatz dazu stoßen Client Computer, die aus dem Unternehmensnetzwerk stammen, basierend auf der Konfiguration des Verbund Servers auf eine andere Art. Der Verbund Server des Unternehmensnetzwerks ist häufig für die integrierte Windows-Authentifizierung konfiguriert, die für Benutzer im Unternehmensnetzwerk ein nahtloses Signieren von @ no__t-0 bietet.  
  
Die Rolle, die ein Verbund Server Proxy in Ihrer Organisation spielt, hängt davon ab, ob Sie den Verbund Server Proxy in der Konto Partnerorganisation oder in der Ressourcen Partnerorganisation platzieren. Wenn ein Verbund Server Proxy z. b. im Umkreis Netzwerk des Konto Partners platziert wird, besteht seine Rolle darin, die Benutzer Anmelde Informationen von Browser Clients zu erfassen. Wenn ein Verbund Server Proxy im Umkreis Netzwerk des Ressourcen Partners platziert wird, leitet er Sicherheitstokenanforderungen an einen Ressourcen Verbund Server weiter und erstellt Sicherheits Token als Reaktion auf die Sicherheits Token, die von seinem Konto Partner.  
  
Weitere Informationen finden Sie unter [Überprüfen der Rolle des Verbundserverproxys beim Kontopartner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md) und [Überprüfen der Rolle des Verbundserverproxys beim Ressourcenpartner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md).  
  
## <a name="how-to-create-a-federation-server-proxy"></a>Erstellen eines Verbundserverproxys  
Sie können einen Verbund Server Proxy erstellen, indem Sie entweder den Assistenten AD FS zum Konfigurieren von Verbund Server Proxys oder den Befehl "fsconfig. exe" @ no__t-0line verwenden. Anleitungen hierzu finden Sie unter [Konfigurieren eines Computers für die Verbundserverproxy-Rolle](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md).  
  
Allgemeine Informationen zum Einrichten der erforderlichen Voraussetzungen für die Bereitstellung eines Verbund Server Proxys finden Sie unter [checkliste: Einrichten eines Verbund Server Proxys @ no__t-0.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
