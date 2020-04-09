---
ms.assetid: d0ba3c0d-869f-4e24-89d7-499da7576f22
title: Überprüfen der Rolle des Verbundservers beim Kontopartner
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2d51f0091746d2d5e816108e3b92d0cb1a8267cd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858533"
---
# <a name="review-the-role-of-the-federation-server-in-the-account-partner"></a>Überprüfen der Rolle des Verbundservers beim Kontopartner

Ein Verbund Server in Active Directory-Verbunddienste (AD FS) \(AD FS\) Funktionen als Aussteller für Sicherheits Token. Ein Verbund Server generiert Ansprüche basierend auf Konto Werten, die sich in einem lokalen Attribut Speicher befinden, und verpackt Sie in Sicherheits Token, sodass Benutzer nahtlos auf Web\-Browser\-basierten Anwendungen zugreifen können, \(mithilfe von einmaligem Anmelden\-auf \(SSO-\)\), die in einer Ressourcen Partnerorganisation gehostet werden.  
  
> [!NOTE]  
> Wenn Ihre Benutzer mithilfe eines Webbrowsers auf Verbund Anwendungen zugreifen, gibt ein Verbund Server automatisch Cookies für die Benutzer aus, um Ihren Anmeldestatus für diese Web\-Browser\-basierte Anwendung zu erhalten. Diese Cookies enthalten die Ansprüche für den Benutzer. Die Cookies ermöglichen SSO-Funktionen, damit die Benutzer die Anmelde Informationen nicht jedes Mal eingeben müssen, wenn Sie unterschiedliche Web\-Browser\-basierten Anwendungen im Ressourcen Partner besuchen.  
  
Im Web-SSO-Entwurf müssen Organisationen mit einem Umkreis Netzwerk, die Internet Benutzern den Zugriff auf Anwendungen erlauben möchten, einen Verbund Server Proxy im Umkreis Netzwerk installieren. Im Federated-Web-SSO-Entwurf muss mindestens ein Verbund Server im Unternehmensnetzwerk der Konto Partnerorganisation und mindestens ein Verbund Server im Unternehmensnetzwerk der Ressourcen Partnerorganisation installiert sein.  
  
> [!NOTE]  
> Bevor Sie in der Konto Partnerorganisation einen Verbund Server Computer einrichten können, müssen Sie den Computer zunächst einer beliebigen Domäne in der Active Directory-Gesamtstruktur hinzufügen, in der der Verbund Server verwendet wird, um Benutzer aus dieser Gesamtstruktur zu authentifizieren. Weitere Informationen finden Sie unter [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
