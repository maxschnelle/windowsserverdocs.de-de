---
ms.assetid: cea6011d-3753-4b95-aaa5-38d4e97d6e42
title: Vorbereiten von Clientcomputern des Kontopartners
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 014524c78312c6fcd478b40ec47e212a194b0531
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858593"
---
# <a name="prepare-client-computers-in-the-account-partner"></a>Vorbereiten von Clientcomputern des Kontopartners

Die einfachste Möglichkeit für einen Administrator in einer Konto Partnerorganisation, Client Computer für den Zugriff auf die Active Directory-Verbunddienste (AD FS) \(AD FS\) Verbund Anwendungen vorzubereiten, ist die Verwendung von Gruppenrichtlinie. Gruppenrichtlinien bieten eine bequeme Möglichkeit, bestimmte Zertifikate und Einstellungen auf alle für den Verbund erforderlichen Clientcomputer auszubringen, die für den Zugriff auf Verbundanwendungen verwendet werden.  
  
Damit Ihre Client Computer nahtlos auf Verbund Anwendungen zugreifen können, ohne dass Zertifikat Aufforderungen oder vertrauenswürdige Website – entsprechende Eingabe Aufforderungen angezeigt werden, empfiehlt es sich, zuerst jeden Client Computer vorzubereiten, bevor Sie AD FS in Ihrer Organisation umfassend bereitstellen. Gruppenrichtlinien können zur Automatisierung folgender Aufgaben verwendet werden:  
  
-   Konfigurieren Sie Internet Explorer auf jedem Client Computer, um dem Konto Verbund Server zu vertrauen.  
  
    Weitere Informationen finden Sie unter [Configure Client Computers to Trust the Account Federation Server](../../ad-fs/deployment/Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md).  
  
-   Installieren Sie den entsprechenden Konto Verbund Server, den Ressourcen Verbund Server und den Webserver Secure Sockets Layer \(SSL-\) Zertifikate \(oder gleichwertige Zertifikate, die mit einer vertrauenswürdigen Stamm\) auf jedem Client Computer verkettet sind.  
  
    Weitere Informationen finden Sie unter [Verteilen von Zertifikaten an Client Computer mithilfe Gruppenrichtlinie](../../ad-fs/deployment/Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md).  
  

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
