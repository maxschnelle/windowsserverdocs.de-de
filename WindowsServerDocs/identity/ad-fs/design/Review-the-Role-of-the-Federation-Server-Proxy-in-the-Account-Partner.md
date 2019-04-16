---
ms.assetid: 1b3a03c0-5558-4177-9b2f-e9d6ce3271cd
title: Review the Role of the Federation Serverproxy in the Account Partner
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d2b60ce593c2ca7eb902595ee6a42850cb7605d9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-account-partner"></a>Review the Role of the Federation Serverproxy in the Account Partner

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Die primäre Rolle des Verbundserverproxys im Umkreisnetzwerk der Kontopartnerorganisation in Active Directory Federation Services \(AD FS\) ist die Anmeldeinformationen für die Authentifizierung von einem Clientcomputer zu sammeln, die über das Internet anmelden und diese Anmeldeinformationen an den Verbundserver im Unternehmensnetzwerk der Kontopartnerorganisation befindet sich zu übergeben. Das Konto für den Clientcomputer wird in der Kontopartner-Attribut gespeichert.  
  
Ein Verbundserverproxy kann auch verwendet, in einem oder mehreren der folgenden Rollen, je nachdem, wie Sie darauf, um die Anforderungen der Kontopartnerorganisation konfigurieren:  
  
-   Relaysicherheitstoken – der Verbundserver stellt ein Sicherheitstoken an den Verbundserverproxy, die das Token an den Clientcomputer dann leitet. Das Token wird verwendet, den Zugriff für den Clientcomputer auf eine bestimmte vertrauende Seite.  
  
-   Sammeln von Anmeldeinformationen – der Verbundserverproxy verwendet eine standardmäßige Client Anmeldung Web Form \(clientlogon.aspx\) Password\ basierende Anmeldeinformationen über Forms\-basierte Authentifizierung zu sammeln. Allerdings können Sie dieses Formular, um andere unterstützten Arten von Authentifizierung, z.B. Secure Sockets Layer \(SSL\) Clientauthentifizierung akzeptieren anpassen. Weitere Informationen zum Anpassen dieser Seite finden Sie unter Anpassung der Clientanmeldung und Home Realm Discovery Seiten \ ([http:///\/go.microsoft.com\/fwlink\/? LinkId\ = 104275](https://go.microsoft.com/fwlink/?LinkId=104275)\). Ein Verbundserverproxy akzeptiert keine Anmeldeinformationen über die integrierte Windows-Authentifizierung.  
  
Zusammenfassend lässt sich sagen, verhält sich ein Verbundserverproxys beim Kontopartner als Proxy für Clientanmeldungen bei einem Verbundserver, der im Unternehmensnetzwerk befindet. Der Verbundserverproxy ermöglicht auch die Verteilung von Sicherheitstokens für Internetclients, die für bestimmte Parteien bestimmt sind.  
  
> [!CAUTION]  
> Verfügbarmachen eines Verbundserverproxys in der Kontopartner Extranet wird die Clientanmeldung zugegriffen werden von jedem Benutzer mit dem Internet zugreifen. Dadurch kann potenziell anfällig Ihrer Organisation für einige Password\ basierende Angriffe sein, z.B. Wörterbuchangriffe oder brute-Force-Angriffe, die Kontensperrungen für Benutzerkonten auslösen können, die in der Corporate \(AD DS\) Active Directory-Domänendiensten gespeichert sind.  
  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
