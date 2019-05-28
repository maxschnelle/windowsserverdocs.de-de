---
ms.assetid: 1b3a03c0-5558-4177-9b2f-e9d6ce3271cd
title: Überprüfen der Rolle des Verbundserverproxys beim Kontopartner
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: dbceb19d31738bdc5b628a9a2b069e5d3022d145
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190955"
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-account-partner"></a>Überprüfen der Rolle des Verbundserverproxys beim Kontopartner

Die primäre Rolle des des Verbundserverproxys im Umkreisnetzwerk der Kontopartnerorganisation in Active Directory-Verbunddienste \(AD FS\) besteht darin, Anmeldeinformationen für die Authentifizierung von einem Clientcomputer zu sammeln, die sich anmeldet über das Internet und die Anmeldeinformationen an den Verbundserver übergeben wird die im Unternehmensnetzwerk der Kontopartnerorganisation befindet. Das Konto für den Clientcomputer wird im Kontopartner-Attribut gespeichert.  
  
Auch kann ein Verbundserverproxy fungieren, in einer oder mehreren der folgenden Rollen, je nachdem, wie Sie darauf, um die Anforderungen der Kontopartnerorganisation konfigurieren:  
  
-   Relaysicherheitstoken – der Verbundserver stellt ein Sicherheitstoken, des Verbundserverproxys, dem leitet dann das Token für den Clientcomputer verfügt. Mit dem Sicherheitstoken wird einer bestimmten Partei der Zugriff auf diesen Clientcomputer ermöglicht.  
  
-   Sammeln von Anmeldeinformationen – der Verbundserverproxy verwendet ein standardwebformular für Clientanmeldung Webformular \(clientlogon.aspx\) zum Sammeln von Kennwort\-basierende Anmeldeinformationen über Formulare\--basierte Authentifizierung. Sie können jedoch dieses Formular, um andere unterstützte Arten von Authentifizierung, z. B. Secure Sockets Layer akzeptieren anpassen \(SSL\) Clientauthentifizierung. Weitere Informationen zum Anpassen dieser Seite finden Sie unter Anpassung der Clientanmeldung und Home Realm Discovery-Seiten \( [http:\/\/"go.Microsoft.com"\/Fwlink\/? LinkId\=104275](https://go.microsoft.com/fwlink/?LinkId=104275)\). Ein Verbundserverproxy akzeptiert keine Anmeldeinformationen über die integrierte Windows-Authentifizierung.  
  
Zusammenfassend lässt sich sagen, fungiert ein Verbundserverproxys beim Kontopartner als Proxy für Clientanmeldungen bei einem Verbundserver, der im Unternehmensnetzwerk befindet. Der Verbundserverproxy ermöglicht auch die Verteilung von Sicherheitstokens für Internetclients, die für vertrauende Seiten bestimmt sind.  
  
> [!CAUTION]  
> Bereitstellen eines Verbundserverproxys in der Kontopartner extranet greift die Clientanmeldung Webformular, die von jedem Benutzer mit dem Internet zugegriffen werden kann. Dies kann potenziell anfällig Ihrer Organisation auf einige Kennwort\-basierte Angriffe, z. B. Wörterbuchangriffe oder brute-Force-Angriffe, die Kontensperrungen für Benutzerkonten auslösen können, die in den Active Directory-Unternehmensdomäne gespeichert sind Dienste \(AD DS\).  
  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
