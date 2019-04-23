---
ms.assetid: aa20c8b3-7f01-4165-8b73-92642bff9676
title: Wann sollte ein Verbundserverproxy erstellt werden?
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1f0253dfb5a690371dae1a2bfcb6b7520077d473
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883201"
---
# <a name="when-to-create-a-federation-server-proxy"></a>Wann sollte ein Verbundserverproxy erstellt werden?

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellen einen Verbundserverproxy in Ihrer Organisation Ihre Active Directory Federation Services zusätzliche Sicherheitsstufen hinzugefügt \(AD FS\) Bereitstellung. Erwägen Sie einen Verbundserverproxy im Umkreisnetzwerk Ihrer Organisation bereitzustellen, wenn Sie möchten:  
  
-   Verhindern Sie, dass externe Clientcomputer direkten Zugriff auf Ihre Verbundserver. Durch Bereitstellen eines Verbundserverproxys in Ihrem Umkreisnetzwerk isolieren Sie effektiv Ihre Verbundserver, damit sie nur von den Clientcomputern zugegriffen werden kann, die mit dem Unternehmensnetzwerk über Verbundserverproxys protokolliert werden, denen handeln von der externen Clientcomputer. Verbundserverproxys können nicht auf die privaten Schlüssel zugreifen, die verwendet werden, um Token zu erzeugen. Weitere Informationen finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md).  
  
-   Geben Sie eine einfache Möglichkeit, die die Vorzeichen unterscheiden\-Erfahrung für Benutzer, die aus dem Internet im Gegensatz zu Benutzern, die von Ihrem Unternehmensnetzwerk stammen, über die integrierte Windows-Authentifizierung zu kommen. Ein Verbundserverproxys sammelt Anmeldeinformationen oder startbereichdetails von internetclientcomputern, mithilfe der Anmeldung, Abmeldung und Ermittlung von Anbietern \(homerealmdiscovery.aspx\) Seiten, die auf den Verbund gespeichert sind Server-Proxy.  
  
    Im Gegensatz dazu-Clientcomputern, die aus dem Unternehmensnetzwerk auftreten eine andere benutzererfahrung bereitstellt, auf Basis der Konfiguration des Verbundservers. Der Unternehmensnetzwerk-Verbundserver ist häufig für die integrierte Windows-Authentifizierung, bietet eine nahtlose Anmeldung konfiguriert\-Erfahrung für Benutzer mit dem Unternehmensnetzwerk verbunden.  
  
Die Rolle, die ein Verbundserverproxy in Ihrer Organisation spielt, hängt davon ab, ob Sie Verbundserverproxys in der Kontopartnerorganisation oder in der Ressourcenpartnerorganisation platzieren. Z. B. wenn ein Verbundserverproxy im Umkreisnetzwerk des Kontopartners platziert wird, werden seine Rolle die Benutzeranmeldeinformationen von Browserclients zu erfassen. Wenn ein Verbundserverproxy im Umkreisnetzwerk des Ressourcenpartners platziert wird, überträgt Sie Sicherheitstoken Anforderungen an einen Ressourcenverbundserver und erzeugt organisatorische Sicherheitstoken in Reaktion auf die Sicherheitstoken, die von bereitgestellt werden die Kontopartner.  
  
Weitere Informationen finden Sie unter [Review the Role of the Federation Server Proxy in the Account Partner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md) und [Review the Role of the Federation Server Proxy in the Resource Partner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md).  
  
## <a name="how-to-create-a-federation-server-proxy"></a>Erstellen eines Verbundserverproxys  
Sie können einen Verbundserverproxy mithilfe des AD FS Federation Server Proxy-Assistenten oder den Befehl Fsconfig.exe erstellen\-Tools "Linie". Anleitungen hierzu finden Sie unter [Configure a Computer for the Federation Server Proxy Role](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md).  
  
Allgemeine Informationen zum Einrichten der erforderlichen Komponenten zum Bereitstellen eines Verbundserverproxys erforderlich sind, finden Sie unter [Prüfliste: Das Einrichten eines Verbundserverproxys](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
