---
ms.assetid: dc24adb7-385d-4a92-ab81-78ba73df0118
title: Zertifikatanforderungen für Verbundserverproxys
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: cc32288d01d7e1386f146716f45f0e49ced3d48e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858123"
---
# <a name="certificate-requirements-for-federation-server-proxies"></a>Zertifikatanforderungen für Verbundserverproxys

Server, die in Active Directory-Verbunddienste (AD FS) \(AD FS\) in der Verbund Server Proxy-Rolle ausgeführt werden, müssen Secure Sockets Layer \(SSL\) Server-Authentifizierungs Zertifikate verwenden. Verbundserverproxys verwenden SSL-Serverauthentifizierungszertifikate zum Schützen der Datenkommunikation von Webservern mit Webclients.  
  
Verbund Server Proxys werden in der Regel für Computer im Internet verfügbar gemacht, die nicht in der Public Key-Infrastruktur Ihres Unternehmens \(PKI\)enthalten sind. Verwenden Sie deshalb ein Server Authentifizierungszertifikat, das von einer öffentlichen \(dritten\-Partei\) Zertifizierungsstelle \(ca-\)ausgestellt wird, z. b. VeriSign.  
  
Wenn Sie über eine Verbund Server Proxy-Farm verfügen, müssen alle Verbund Server Proxy-Computer das gleiche Server Authentifizierungszertifikat verwenden. Weitere Informationen finden Sie unter [When to Create a Federation Server Proxy Farm](When-to-Create-a-Federation-Server-Proxy-Farm.md).  
  
Es ist wichtig sicherzustellen, dass der Antragsteller Name im Server Authentifizierungszertifikat mit dem Wert für Verbunddienst Name übereinstimmt, der im\-Snap-in für die AD FS Verwaltung angegeben ist. Öffnen Sie zum Suchen dieses Werts das Snap-in\-in, klicken Sie mit der rechten\-auf **Dienst**, klicken Sie auf **Verbunddienst Eigenschaften bearbeiten**, und suchen Sie dann den Wert im Textfeld **Verbunddienst Name** .  
  
Allgemeine Informationen zur Verwendung von SSL-Zertifikaten finden Sie unter Konfigurieren von Secure Sockets Layer in IIS 7,0 \([http:\/\/go.Microsoft.com\/fwlink\/? LinkId\=108544](https://go.microsoft.com/fwlink/?LinkID=108544)\) und Konfigurieren von Server Zertifikaten in IIS 7,0 \([http:\/\/go.Microsoft.com\/fwlink\/? LinkId\=108545](https://go.microsoft.com/fwlink/?LinkID=108545)\).  
  
> [!NOTE]  
> Client Authentifizierungs Zertifikate sind für AD FS Verbund Server Proxys nicht erforderlich.  
  
Wenn für ein beliebiges Zertifikat Zertifikat Sperr Listen \(CRLs\)vorhanden sind, muss der Server mit dem konfigurierten Zertifikat in der Lage sein, den Server zu kontaktieren, von dem die CRLs verteilt werden. Anhand des CRL-Typs wird vorgegeben, welche Ports verwendet werden.  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
