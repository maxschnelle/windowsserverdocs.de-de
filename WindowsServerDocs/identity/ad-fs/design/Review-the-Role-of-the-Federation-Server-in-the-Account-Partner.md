---
ms.assetid: d0ba3c0d-869f-4e24-89d7-499da7576f22
title: "Überprüfen der Rolle des Verbundservers beim Kontopartner"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0914d32e8f24d5e7db0a25c733342c1bde3e0329
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="review-the-role-of-the-federation-server-in-the-account-partner"></a>Überprüfen der Rolle des Verbundservers beim Kontopartner

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Ein Verbundserver in Active Directory Federation Services \(AD FS\) fungiert als sicherheitstokenaussteller. Ein Verbundserver generiert Ansprüche basierend auf Speichern von Werten, die sich in einem lokalen Attribut befinden und verpackt sie in Sicherheitstoken, sodass Benutzer nahtlos Browser\-webbasierten Anwendungen zugreifen können \ (mit einzelnen Standardparameter auf \(SSO\)\), die in einer Ressourcenpartnerorganisation gehostet werden.  
  
> [!NOTE]  
> Bei Ihren Benutzern den Zugriff Anwendungen mithilfe eines Webbrowsers Verbund-, Probleme ein Verbundservers automatisch Cookies für die Benutzer den Anmeldestatus für diese Browser\-webbasierten Anwendung zu verwalten. Diese Cookies enthalten die Ansprüche für den Benutzer. Die Cookies ermöglichen SSO-Funktionen, damit die Benutzer nicht unbedingt immer eingeben muss, dass sie verschiedene Browser\-webbasierten Anwendungen im Ressourcenpartner besuchen.  
  
Im Web-SSO-Entwurf müssen Organisationen mit einem Umkreisnetzwerk, die Internetbenutzern den Zugriff auf Anwendungen sollen ein Verbundserverproxys im Umkreisnetzwerk installieren. Im Federated-Web-SSO-Entwurf muss mindestens ein Verbundserver im Unternehmensnetzwerk der Kontopartnerorganisation installiert und mindestens einen Verbundserver im Unternehmensnetzwerk der Ressourcenpartnerorganisation installiert vorhanden sein.  
  
> [!NOTE]  
> Bevor Sie einem Verbund-Server-Computer in der Kontopartnerorganisation einrichten können, müssen Sie den Computer einer Domäne in Active Directory-Gesamtstruktur hinzufügen, in denen der Verbundserver zur Authentifizierung von Benutzern in dieser Gesamtstruktur verwendet wird. Weitere Informationen finden Sie unter [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
