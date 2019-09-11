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
ms.openlocfilehash: eb0547ac1d84fffed31360f0ee510504510c24ce
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867667"
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-account-partner"></a>Überprüfen der Rolle des Verbundserverproxys beim Kontopartner

Die primäre Rolle des Verbund Server Proxys im Umkreis Netzwerk der Konto Partnerorganisation in Active Directory-Verbunddienste (AD FS) \(AD FS\) besteht darin, Anmelde Informationen für die Authentifizierung von einem Client Computer zu sammeln, der sich anmeldet. über das Internet und, um diese Anmelde Informationen an den Verbund Server zu übergeben, der sich im Unternehmensnetzwerk der Konto Partnerorganisation befindet. Das Konto für den Client Computer wird im Attribut Speicher des Konto Partners gespeichert.  
  
Ein Verbund Server Proxy kann in Abhängigkeit davon, wie Sie ihn so konfigurieren, dass er den Anforderungen der Konto Partnerorganisation entspricht, auch in einer oder mehreren der folgenden Rollen funktionieren:  
  
-   Relaysicherheitstoken – der Verbund Server gibt ein Sicherheits Token für den Verbund Server Proxy aus, der das Token dann an den Client Computer überträgt. Mit dem Sicherheitstoken wird einer bestimmten Partei der Zugriff auf diesen Clientcomputer ermöglicht.  
  
-   Sammeln von Anmelde Informationen – der Verbund Server Proxy verwendet ein Standardmäßiges \(Clientlogon-Webformular Clientlogon. aspx\) , um per\-Formular basierter Authentifizierung Kenn Wort\-basierte Anmelde Informationen zu sammeln. Sie können dieses Formular jedoch anpassen, um andere unterstützte Arten von Authentifizierung zu akzeptieren, z \(.\) b. Secure Sockets Layer SSL-Client Authentifizierung. Weitere Informationen zum Anpassen dieser Seite finden Sie unter Anpassen von Client Anmelde-und Start \(Bereichs Ermittlungs Seiten [http:\/\/go.Microsoft.com\/fwlink\/? LinkId\=104275.](https://go.microsoft.com/fwlink/?LinkId=104275)\) Ein Verbund Server Proxy akzeptiert keine Anmelde Informationen über die integrierte Windows-Authentifizierung.  
  
Zusammenfassend gilt: ein Verbund Server Proxy im Konto Partner fungiert als Proxy für Client Anmeldungen bei einem Verbund Server, der sich im Unternehmensnetzwerk befindet. Der Verbund Server Proxy ermöglicht auch die Verteilung von Sicherheits Token an Internet Clients, die für vertrauende Seiten bestimmt sind.  
  
> [!CAUTION]  
> Beim verfügbar machen eines Verbund Server Proxys im Konto Partner-Extranet ist das Webformular für die Client Anmeldung für alle Benutzer mit Internet Zugriff zugänglich. Dadurch kann Ihre Organisation potenziell anfällig für einige Kenn Wort\-basierte Angriffe sein, z. b. Wörterbuchangriffe oder Brute-Force-Angriffe, die Konto Sperrungen für Benutzerkonten, die im Unternehmens Active Directory-Domäne gespeichert sind, auslöst. Dienste \(AD DS\).  
  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
