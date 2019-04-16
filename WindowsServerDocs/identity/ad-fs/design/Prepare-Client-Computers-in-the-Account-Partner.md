---
ms.assetid: cea6011d-3753-4b95-aaa5-38d4e97d6e42
title: Vorbereiten von Clientcomputern des Kontopartners
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0c5bdcb0a80b15a1905109229ddd20ee642a8dd7
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="prepare-client-computers-in-the-account-partner"></a>Vorbereiten von Clientcomputern des Kontopartners

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Die einfachste Möglichkeit für einen Administrator in einer Kontopartnerorganisation, Vorbereiten von Clientcomputern für den Zugriff auf Active Directory Federation Services \(AD FS\) federated Anwendungen ist die Verwendung von Gruppenrichtlinien. Gruppenrichtlinien bieten eine bequeme Möglichkeit, bestimmte Zertifikate und Einstellungen, die für den Verbund auf allen Clientcomputern erforderlich sind, die Zugriff auf verbundanwendungen verwendet werden.  
  
Damit die Clientcomputer nahtlos ohne Zertifikat aufforderungen oder vertrauenswürdigen Sites Eingabeaufforderungen verbundanwendungen zugreifen können, empfehlen wir, dass Sie zuerst einzelnen Clientcomputer vorzubereiten, bevor Sie AD FS grob in Ihrer Organisation bereitstellen. Beachten Sie, mit der Gruppenrichtlinie automatisch:  
  
-   Konfigurieren Sie Internet Explorer auf jedem Computer, auf dem Kontoverbundserver vertrauen.  
  
    Weitere Informationen finden Sie unter [Configure Client Computers to Trust the Account Federation Server](../../ad-fs/deployment/Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md).  
  
-   Installieren Sie die entsprechenden Kontoverbundserver Ressourcenverbundserver und Secure Sockets Layer-\(SSL\) für Webserverzertifikate \ (oder äquivalent zu einer vertrauenswürdigen Root\ Zertifikate) auf jedem Clientcomputer.  
  
    Weitere Informationen finden Sie unter [Verteilen von Zertifikaten an Clientcomputer mithilfe von Gruppenrichtlinien](../../ad-fs/deployment/Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md).  
  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
