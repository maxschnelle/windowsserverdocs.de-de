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

Der Verbund Server in der Ressourcen Partnerorganisation fängt eingehende Sicherheits Token ab, die von einem Konto Verbund Server gesendet werden, überprüft und signiert Sie und gibt dann eigene Sicherheits Token aus, die für die auf Web\-basierende Anwendung bestimmt sind.  
  
> [!NOTE]  
> Wenn Verbund Benutzer Ihren Webbrowser verwenden, um auf Web\-basierte Anwendungen zuzugreifen, erstellt der Verbund Server in der Ressourcen Partnerorganisation ein neues Authentifizierungs Cookie und schreibt es in den Browser. Dieses Cookie ermöglicht das einmalige\-Signieren\-auf \(SSO-\) Funktionen, sodass Benutzer sich nicht erneut beim Verbund Server des Konto Partners anmelden müssen, wenn die Benutzer versuchen, auf verschiedene auf Web\-basierende Anwendungen im Ressourcen Partner zuzugreifen.  
  
Im Web-SSO-Entwurf muss mindestens ein Verbund Server im Umkreis Netzwerk installiert sein. Im Federated-Web-SSO-Entwurf muss mindestens ein Verbund Server im Unternehmensnetzwerk der Konto Partnerorganisation und mindestens ein Verbund Server im Unternehmensnetzwerk der Ressourcen Partnerorganisation installiert sein.  
  
> [!NOTE]  
> Vor dem Einrichten eines Verbund Server Computers in der Ressourcen Partnerorganisation müssen Sie den Computer zunächst einer beliebigen Active Directory Domäne in der Ressourcen Partnerorganisation hinzufügen. Weitere Informationen finden Sie unter [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

