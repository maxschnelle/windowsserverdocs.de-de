---
ms.assetid: dc24adb7-385d-4a92-ab81-78ba73df0118
title: Zertifikatanforderungen für Verbundserverproxies
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 51eb0e72f52fafdb2f1b8bbb3f9a2850602c3f75
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954336"
---
# <a name="certificate-requirements-for-federation-server-proxies"></a>Zertifikatanforderungen für Verbundserverproxies

Server, die in Active Directory-Verbunddienste (AD FS) AD FS in der Verbund Server Proxy-Rolle ausgeführt werden \( \) , müssen Secure Sockets Layer \( SSL- \) Server Authentifizierungs Zertifikate verwenden. Verbundserverproxys verwenden SSL-Serverauthentifizierungszertifikate zum Schützen der Datenkommunikation von Webservern mit Webclients.

Verbund Server Proxys werden in der Regel für Computer im Internet verfügbar gemacht, die nicht in der Public Key-Infrastruktur-PKI Ihres Unternehmens enthalten sind \( \) . Verwenden Sie deshalb ein Server Authentifizierungszertifikat, das von einer öffentlichen Zertifizierungsstellen-Zertifizierungsstelle ausgestellt wird \( \- \) \( \) , z. b. VeriSign.

Wenn Sie über eine Verbund Server Proxy-Farm verfügen, müssen alle Verbund Server Proxy-Computer das gleiche Server Authentifizierungszertifikat verwenden. Weitere Informationen finden Sie unter [When to Create a Federation Server Proxy Farm](When-to-Create-a-Federation-Server-Proxy-Farm.md).

Es ist wichtig sicherzustellen, dass der Antragsteller Name im Server Authentifizierungszertifikat mit dem Wert des Verbunddienst namens übereinstimmt, der im Snap-in AD FS Verwaltung angegeben ist \- . Öffnen Sie zum Suchen dieses Werts das Snap- \- in, \- Klicken Sie mit der rechten Maustaste auf **Dienst**, klicken Sie auf **Verbunddienst Eigenschaften bearbeiten**, und suchen Sie dann den Wert im Textfeld **Verbunddienst Name** .

Allgemeine Informationen zur Verwendung von SSL-Zertifikaten finden Sie unter Konfigurieren von Secure Sockets Layer in IIS 7,0 \( [http: \/ \/ go.Microsoft.com \/ fwlink \/ ? LinkId \= 108544](https://go.microsoft.com/fwlink/?LinkID=108544) \) und Konfigurieren von Server Zertifikaten in IIS 7,0 \( [http: \/ \/ go.Microsoft.com \/ fwlink \/ ? LinkId \= 108545](https://go.microsoft.com/fwlink/?LinkID=108545) \) .

> [!NOTE]
> Client Authentifizierungs Zertifikate sind für AD FS Verbund Server Proxys nicht erforderlich.

Wenn ein beliebiges Zertifikat, das Sie verwenden, Zertifikat Sperr Listen enthält \( \) , muss der Server mit dem konfigurierten Zertifikat in der Lage sein, den Server zu kontaktieren, von dem die CRLs verteilt werden. Anhand des CRL-Typs wird vorgegeben, welche Ports verwendet werden.

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
