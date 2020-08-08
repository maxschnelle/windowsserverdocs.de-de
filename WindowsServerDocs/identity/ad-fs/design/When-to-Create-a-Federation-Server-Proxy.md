---
ms.assetid: aa20c8b3-7f01-4165-8b73-92642bff9676
title: Wann sollte ein Verbundserverproxy erstellt werden?
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 963070a15b075275cd5680fa3a39044abbb6b3ad
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972037"
---
# <a name="when-to-create-a-federation-server-proxy"></a>Wann sollte ein Verbundserverproxy erstellt werden?

Durch das Erstellen eines Verbund Server Proxys in Ihrer Organisation werden Ihrer Active Directory-Verbunddienste (AD FS) \( AD FS-Bereitstellung zusätzliche Sicherheitsebenen hinzugefügt \) . Sie sollten einen Verbund Server Proxy im Umkreis Netzwerk Ihrer Organisation bereitstellen, wenn Sie Folgendes tun möchten:

-   Verhindern, dass externe Client Computer direkt auf Ihre Verbund Server zugreifen. Durch die Bereitstellung eines Verbund Server Proxys in Ihrem Umkreis Netzwerk isolieren Sie effektiv Ihre Verbund Server, sodass nur Client Computer auf Sie zugreifen können, die über Verbund Server Proxys im Unternehmensnetzwerk angemeldet sind, die im Auftrag der externen Client Computer agieren. Verbundserverproxys können nicht auf die privaten Schlüssel zugreifen, die verwendet werden, um Token zu erzeugen. Weitere Informationen hierzu finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md) (Platzieren eines Verbundserverproxys).

-   Stellen Sie eine bequeme Möglichkeit dar, die Anmelde Funktion für Benutzer zu unterscheiden, die aus dem Internet stammen, und nicht für \- Benutzer, die mit der integrierten Windows-Authentifizierung aus Ihrem Unternehmensnetzwerk kommen. Ein Verbund Server Proxy sammelt Anmelde Informationen oder Startbereichs Details von Internet Client Computern mithilfe der auf dem Verbund Server Proxy gespeicherten Seiten für Anmeldung, Abmeldung und Identitäts Anbieter Ermittlung ( \( homerealmdiscovery. aspx) \) .

    Im Gegensatz dazu stoßen Client Computer, die aus dem Unternehmensnetzwerk stammen, basierend auf der Konfiguration des Verbund Servers auf eine andere Art. Der Verbund Server des Unternehmensnetzwerks ist häufig für die integrierte Windows-Authentifizierung konfiguriert, die eine nahtlose Anmelde Funktion \- für Benutzer im Unternehmensnetzwerk bereitstellt.

Die Rolle, die ein Verbund Server Proxy in Ihrer Organisation spielt, hängt davon ab, ob Sie den Verbund Server Proxy in der Konto Partnerorganisation oder in der Ressourcen Partnerorganisation platzieren. Wenn ein Verbund Server Proxy z. b. im Umkreis Netzwerk des Konto Partners platziert wird, besteht seine Rolle darin, die Benutzer Anmelde Informationen von Browser Clients zu erfassen. Wenn ein Verbund Server Proxy im Umkreis Netzwerk des Ressourcen Partners platziert wird, leitet er Sicherheitstokenanforderungen an einen Ressourcen Verbund Server weiter und erstellt in Reaktion auf die Sicherheits Token, die von seinen Konto Partnern bereitgestellt werden, Organisations Sicherheits Token.

Weitere Informationen finden Sie unter [Review the Role of the Federation Server Proxy in the Account Partner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md) und [Review the Role of the Federation Server Proxy in the Resource Partner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md).

## <a name="how-to-create-a-federation-server-proxy"></a>Erstellen eines Verbundserverproxys
Sie können einen Verbund Server Proxy erstellen, indem Sie entweder den Assistenten AD FS zum Konfigurieren von Verbund Server Proxys oder das Fsconfig.exe-Befehls \- Zeilen Tool verwenden. Anleitungen hierzu finden Sie unter [Configure a Computer for the Federation Server Proxy Role](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md).

Allgemeine Informationen zum Einrichten der Voraussetzungen zum Bereitstellen eines Verbundserverproxys finden Sie unter [Checklist: Setting Up a Federation Server Proxy](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md).

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
