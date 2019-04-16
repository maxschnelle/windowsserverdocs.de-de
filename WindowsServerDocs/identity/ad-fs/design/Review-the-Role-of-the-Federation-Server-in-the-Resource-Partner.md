---
ms.assetid: f88238ea-d851-4129-8b4e-a3a62b813614
title: "Überprüfen der Rolle des Verbundservers beim Ressourcenpartner"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6d4c7763d7204dd2340d10a234e48f47c96788dc
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="review-the-role-of-the-federation-server-in-the-resource-partner"></a>Überprüfen der Rolle des Verbundservers beim Ressourcenpartner

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Der Verbundserver in der Ressource Partner Organisation fängt eingehende Sicherheitstoken, die von einem Kontoverbundserver gesendet werden überprüft und signiert sie, und stellt dann eigene Sicherheitstoken, die für die webbasierte Anwendung bestimmt sind.  
  
> [!NOTE]  
> Wenn Verbundbenutzer ein Webbrowser den Zugriff auf webbasierte Anwendungen verwenden, wird der Verbundserver in der Ressourcenpartnerorganisation erstellt ein neues Authentifizierungscookie und schreibt sie in den Browser. Dieses Cookie aktiviert Singlethread-Standardparameter-\(SSO\) Funktionen, sodass die Benutzer nicht erneut anmelden, auf dem Verbundserver in der Kontopartner Wenn die Benutzer versuchen, verschiedene webbasierte Anwendungen im Ressourcenpartner zugreifen.  
  
Im Web-SSO-Entwurf muss mindestens ein Verbundserver im Umkreisnetzwerk installiert werden. Im Federated-Web-SSO-Entwurf muss mindestens ein Verbundserver im Unternehmensnetzwerk der Kontopartnerorganisation installiert und mindestens einen Verbundserver im Unternehmensnetzwerk der Ressourcenpartnerorganisation installiert vorhanden sein.  
  
> [!NOTE]  
> Bevor Sie einem Verbund-Server-Computer in der Ressourcenpartnerorganisation einrichten können, müssen Sie den Computer einer Active Directory-Domäne in der Ressourcenpartnerorganisation hinzufügen. Weitere Informationen finden Sie unter [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

