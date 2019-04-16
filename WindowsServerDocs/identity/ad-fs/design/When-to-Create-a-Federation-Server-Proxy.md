---
ms.assetid: aa20c8b3-7f01-4165-8b73-92642bff9676
title: "Gründe für das Erstellen eines Verbundserverproxys"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1f0253dfb5a690371dae1a2bfcb6b7520077d473
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="when-to-create-a-federation-server-proxy"></a>Gründe für das Erstellen eines Verbundserverproxys

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Erstellen eines Verbundserverproxys in Ihrer Organisation hinzugefügt die Bereitstellung der Active Directory-Verbunddienste \(AD FS\) zusätzliche Sicherheitsstufen. Beachten Sie, einen Verbundserverproxy im Umkreisnetzwerk Ihrer Organisation bereitstellen, wenn Sie möchten:  
  
-   Verhindern Sie, dass externe Clientcomputer direkten Zugriff auf Ihren Verbundserver. Durch Bereitstellen eines Verbundserverproxys in Ihrem Umkreisnetzwerk, isolieren Sie effektiv Ihren Verbundserver, sodass sie nur von Clientcomputern zugegriffen werden kann, die mit dem Unternehmensnetzwerk über Verbundserverproxys, angemeldet sind, die im Auftrag der externen Clientcomputer Verhalten. Verbundserverproxys können nicht auf die privaten Schlüssel zugreifen, die verwendet werden, um Token zu erzeugen. Weitere Informationen finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md).  
  
-   Bieten Sie eine bequeme Möglichkeit, die Standardparameter in Erfahrung für Benutzer zu unterscheiden, die aus dem Internet im Gegensatz zu Benutzern, die von Ihrem Unternehmensnetzwerk vertraut sind, über die integrierte Windows-Authentifizierung kommen. Ein Verbundserverproxys sammelt Anmeldeinformationen oder startbereichdetails von internetclientcomputern mit der Anmeldung, Abmeldung und Identity Provider Ermittlung \(homerealmdiscovery.aspx\) Seiten, die für den Verbundserverproxy gespeichert sind.  
  
    Im Gegensatz dazu Clientcomputer, die aus dem Unternehmensnetzwerk Berührungspunkt eine andere Erfahrung, stammen basierend auf der Konfiguration des Verbundservers. Der Verbundserver Unternehmensnetzwerk ist häufig für die integrierte Windows-Authentifizierung, ein Standardparameter-in für Benutzer im Unternehmensnetzwerk nahtloses konfiguriert.  
  
Die Rolle, die ein Verbundserverproxy in Ihrer Organisation spielt, hängt davon ab, ob den Verbundserverproxy in der Kontopartnerorganisation oder in der Ressourcenpartnerorganisation platzieren. Wenn ein Verbundserverproxys im Umkreisnetzwerk des Kontopartners platziert wird, wird seine Rolle z.B. die Benutzeranmeldeinformationen von Browserclients zu erfassen. Wenn ein Verbundserverproxys im Umkreisnetzwerk des Ressourcenpartners platziert wird, sicherheitstokenanforderungen an einen Ressourcenverbundserver und erzeugt organisatorische Sicherheitstoken in Reaktion auf die Sicherheitstoken, die von den Kontopartnern bereitgestellt werden.  
  
Weitere Informationen finden Sie unter [Überprüfen der Rolle des Verbundserverproxys beim Kontopartner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md) und [Überprüfen der Rolle des Verbundserverproxys beim Ressourcenpartner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md)  
  
## <a name="how-to-create-a-federation-server-proxy"></a>Vorgehensweise beim Erstellen eines Verbundserverproxys  
Sie können einen Verbundserverproxy mit AD FS Federation Server Proxy-Konfigurations-Assistenten oder das Befehlszeilentool Fsconfig.exe erstellen. Weitere Informationen hierzu finden Sie unter [Konfigurieren eines Computers für die Verbundserverproxy-Rolle](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md).  
  
Allgemeine Informationen zum Einrichten der Voraussetzungen zum Bereitstellen eines Verbundserverproxys finden Sie unter [Checkliste: Einrichten eines Verbundserverproxys](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
