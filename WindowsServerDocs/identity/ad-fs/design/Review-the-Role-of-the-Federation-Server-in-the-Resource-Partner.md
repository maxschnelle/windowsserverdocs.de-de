---
ms.assetid: f88238ea-d851-4129-8b4e-a3a62b813614
title: Überprüfen der Rolle des Verbundservers beim Ressourcenpartner
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: fd9f20eb7559f5862ee50bdd8364fa1604d3c1b6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358966"
---
# <a name="review-the-role-of-the-federation-server-in-the-resource-partner"></a>Überprüfen der Rolle des Verbundservers beim Ressourcenpartner

Der Verbund Server in der Ressourcen Partnerorganisation fängt eingehende Sicherheits Token ab, die von einem Konto Verbund Server gesendet werden, überprüft und signiert Sie und gibt dann eigene Sicherheits Token aus, die für die Web @ no__t-0based-Anwendung bestimmt sind. .  
  
> [!NOTE]  
> Wenn Verbund Benutzer mit ihren Webbrowsern auf Web @ no__t-0basierte Anwendungen zugreifen, erstellt der Verbund Server in der Ressourcen Partnerorganisation ein neues Authentifizierungs Cookie und schreibt es in den Browser. Dieses Cookie aktiviert das einmalige @ no__t-0sign @ no__t-1On \(sso @ no__t-3-Funktionen, damit Benutzer sich nicht erneut beim Verbund Server beim Konto Partner anmelden müssen, wenn die Benutzer versuchen, auf verschiedene Web @ no__t-4based-Anwendungen in der Ressource zuzugreifen. Partners.  
  
Im Web-SSO-Entwurf muss mindestens ein Verbund Server im Umkreis Netzwerk installiert sein. Im Federated-Web-SSO-Entwurf muss mindestens ein Verbund Server im Unternehmensnetzwerk der Konto Partnerorganisation und mindestens ein Verbund Server im Unternehmensnetzwerk der Ressourcen Partnerorganisation installiert sein.  
  
> [!NOTE]  
> Vor dem Einrichten eines Verbund Server Computers in der Ressourcen Partnerorganisation müssen Sie den Computer zunächst einer beliebigen Active Directory Domäne in der Ressourcen Partnerorganisation hinzufügen. Weitere Informationen finden Sie unter [checkliste: Einrichten eines Verbund Servers @ no__t-0.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

