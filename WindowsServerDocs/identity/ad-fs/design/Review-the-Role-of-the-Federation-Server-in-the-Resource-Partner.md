---
ms.assetid: f88238ea-d851-4129-8b4e-a3a62b813614
title: Überprüfen der Rolle des Verbundservers beim Ressourcenpartner
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b2ed7a09bbc50c83d3bf6f8f2688152ed5202abc
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190818"
---
# <a name="review-the-role-of-the-federation-server-in-the-resource-partner"></a>Überprüfen der Rolle des Verbundservers beim Ressourcenpartner

Der Verbundserver in der Ressourcenpartnerorganisation fängt eingehende Sicherheitstoken, die von einem Kontoverbundserver gesendet werden, überprüft und signiert sie und gibt dann eigene Sicherheitstoken, die für das Web bestimmt sind\-basierend die Anwendung.  
  
> [!NOTE]  
> Wenn Verbundbenutzer ihren Webbrowser verwenden, um den Zugriff auf Web\-basierenden Anwendungen, die Verbundserver in der Ressourcenpartnerorganisation erstellt ein neues Authentifizierungscookie und schreibt sie in den Browser. Dieses Cookie ermöglicht einzelnen\-anmelden\-auf \(SSO\) Funktionen, damit Benutzer nicht erneut anmelden auf dem Verbundserver in der Kontopartner, wenn die Benutzer versuchen, den Zugriff auf verschiedene Web verfügen\- -basierte Anwendungen in der Ressourcenpartnerorganisation.  
  
In den Web-SSO-Entwurf muss mindestens eine Verbundservers im Umkreisnetzwerk installiert sein. Im Federated-Web-SSO-Entwurf muss mindestens ein Verbundserver im Unternehmensnetzwerk der Kontopartnerorganisation installiert und mindestens ein Verbundserver im Unternehmensnetzwerk der Ressourcenpartnerorganisation installiert vorhanden sein.  
  
> [!NOTE]  
> Bevor Sie einen Verbund-Server-Computer in der Ressourcenpartnerorganisation einrichten können, müssen Sie den Computer einer Active Directory-Domäne in der Ressourcenpartnerorganisation hinzufügen. Weitere Informationen finden Sie unter [Prüfliste: Das Einrichten eines Verbundservers](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

