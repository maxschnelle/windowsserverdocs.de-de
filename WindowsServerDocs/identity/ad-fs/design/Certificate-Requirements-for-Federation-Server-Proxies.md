---
ms.assetid: dc24adb7-385d-4a92-ab81-78ba73df0118
title: Certificate Requirements for Federation Server Proxies
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e7fb8e71afed1c0eb6b55857835d95f2dd0ec9d5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="certificate-requirements-for-federation-server-proxies"></a>Certificate Requirements for Federation Server Proxies

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Server, die in der Verbundserverproxy-Rolle in Active Directory Federation Services \(AD FS\) ausgeführt werden sind zur Verwendung von Secure Sockets Layer \(SSL\) Serverauthentifizierungszertifikate erforderlich. Verbundserverproxys verwenden SSL-Serverauthentifizierungszertifikate zum Schützen der Datenkommunikation von Webservern mit Webclients.  
  
Verbundserverproxys werden in der Regel für Computer im Internet, die nicht in der public Key-Infrastruktur des Unternehmens enthalten sind verfügbar gemacht \(PKI\). Verwenden Sie ein Serverauthentifizierungszertifikat, das von einer öffentlichen \(third\-party\) Zertifizierungsstelle ausgestellt wird daher \(CA\), z. B. VeriSign.  
  
Wenn Sie eine Verbundserverproxy-Farm verfügen, müssen alle Verbundserverproxy-Computer die gleiche Serverauthentifizierungszertifikat verwenden. Weitere Informationen finden Sie unter [When to Create a Federation Server Proxy Farm](When-to-Create-a-Federation-Server-Proxy-Farm.md).  
  
Es ist wichtig, um sicherzustellen, dass der Antragstellername des Serverzertifikats für die Authentifizierung den Verbunddienst-Namenswert entspricht, der in AD FS-Verwaltungs-Snap-in angegeben ist. Öffnen Sie zum Suchen dieses Werts das Snap-in, mit der rechten Maustaste auf **Service**, klicken Sie auf **Verbunddiensteigenschaften bearbeiten**, und suchen Sie den Wert im **verbunddienstname** Textfeld.  
  
Allgemeine Informationen zur Verwendung von SSL-Zertifikaten finden Sie unter Konfigurieren von Secure Sockets Layer in IIS 7.0 \ ([http:///\/go.microsoft.com\/fwlink\/? LinkID\ = 108544](https://go.microsoft.com/fwlink/?LinkID=108544)\) und Konfigurieren von Serverzertifikaten in IIS 7.0 \ ([http:///\/go.microsoft.com\/fwlink\/? LinkID\ = 108545](https://go.microsoft.com/fwlink/?LinkID=108545)\).  
  
> [!NOTE]  
> Clientauthentifizierungszertifikate sind nicht für AD FS-Verbundserverproxys erforderlich.  
  
Verfügt ein Zertifikat, mit denen Sie Zertifikatssperrlisten \(CRLs\), muss der Server mit dem konfigurierten Zertifikat eine Verbindung mit den Server herstellen, mit dem die CRLs verteilt. Der Typ der Zertifikatsperrliste wird bestimmt, welche Ports verwendet werden.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
