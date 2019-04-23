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
ms.openlocfilehash: 6d4c7763d7204dd2340d10a234e48f47c96788dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841841"
---
# <a name="review-the-role-of-the-federation-server-in-the-resource-partner"></a>Überprüfen der Rolle des Verbundservers beim Ressourcenpartner

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der Verbundserver in der Ressourcenpartnerorganisation fängt eingehende Sicherheitstoken, die von einem Kontoverbundserver gesendet werden, überprüft und signiert sie und gibt dann eigene Sicherheitstoken, die für das Web bestimmt sind\-basierend die Anwendung.  
  
> [!NOTE]  
> Wenn Verbundbenutzer ihren Webbrowser verwenden, um den Zugriff auf Web\-basierenden Anwendungen, die Verbundserver in der Ressourcenpartnerorganisation erstellt ein neues Authentifizierungscookie und schreibt sie in den Browser. Dieses Cookie ermöglicht einzelnen\-anmelden\-auf \(SSO\) Funktionen, damit Benutzer nicht erneut anmelden auf dem Verbundserver in der Kontopartner, wenn die Benutzer versuchen, den Zugriff auf verschiedene Web verfügen\- -basierte Anwendungen in der Ressourcenpartnerorganisation.  
  
In den Web-SSO-Entwurf muss mindestens eine Verbundservers im Umkreisnetzwerk installiert sein. Im Federated-Web-SSO-Entwurf muss mindestens ein Verbundserver im Unternehmensnetzwerk der Kontopartnerorganisation installiert und mindestens ein Verbundserver im Unternehmensnetzwerk der Ressourcenpartnerorganisation installiert vorhanden sein.  
  
> [!NOTE]  
> Bevor Sie einen Verbund-Server-Computer in der Ressourcenpartnerorganisation einrichten können, müssen Sie den Computer einer Active Directory-Domäne in der Ressourcenpartnerorganisation hinzufügen. Weitere Informationen finden Sie unter [Prüfliste: Das Einrichten eines Verbundservers](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

