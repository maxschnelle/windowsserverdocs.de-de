---
ms.assetid: cea6011d-3753-4b95-aaa5-38d4e97d6e42
title: Vorbereiten von Clientcomputern des Kontopartners
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e3a746ec003cf312ffe0b9804f84a55c98aa8089
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190990"
---
# <a name="prepare-client-computers-in-the-account-partner"></a>Vorbereiten von Clientcomputern des Kontopartners

Die einfachste Möglichkeit für eine Administratoren bei kontopartnerunternehmen zur Vorbereitung der Clientcomputer für den Zugriff auf Active Directory Federation Services \(AD FS\) -verbundanwendungen ist die Verwendung von Gruppenrichtlinien. Gruppenrichtlinien bieten eine bequeme Möglichkeit, bestimmte Zertifikate und Einstellungen auf alle für den Verbund erforderlichen Clientcomputer auszubringen, die für den Zugriff auf Verbundanwendungen verwendet werden.  
  
Damit die Clientcomputer nahtlos verbundanwendungen ohne zertifikataufforderungen oder Anweisungen für den vertrauenswürdigen Sites zugreifen können, empfehlen wir, dass Sie zuerst einzelnen Clientcomputer vorzubereiten, bevor Sie AD FS umfassend in Ihrer Organisation bereitstellen. Gruppenrichtlinien können zur Automatisierung folgender Aufgaben verwendet werden:  
  
-   Konfigurieren Sie Internet Explorer auf jedem Clientcomputer, der Kontoverbundserver zu vertrauen.  
  
    Weitere Informationen finden Sie unter [Configure Client Computers to Trust the Account Federation Server](../../ad-fs/deployment/Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md).  
  
-   Installieren Sie die entsprechenden Kontoverbundserver, Ressourcenverbundserver und Webserver Secure Sockets Layer \(SSL\) Zertifikate \(oder die entsprechenden Zertifikate einer vertrauenswürdigen Stammzertifizierungsstelle\) auf jedem Client-Computer.  
  
    Weitere Informationen finden Sie unter [Verteilen von Zertifikaten auf Clientcomputern mithilfe einer Gruppenrichtlinie](../../ad-fs/deployment/Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md).  
  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
