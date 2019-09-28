---
ms.assetid: d0ba3c0d-869f-4e24-89d7-499da7576f22
title: Überprüfen der Rolle des Verbundservers beim Kontopartner
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ead8868f38faa570a0e524630e23d99e276a7c79
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407921"
---
# <a name="review-the-role-of-the-federation-server-in-the-account-partner"></a>Überprüfen der Rolle des Verbundservers beim Kontopartner

Ein Verbund Server in Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 fungiert als sicherheitstokenaussteller. Ein Verbund Server generiert Ansprüche basierend auf Konto Werten, die sich in einem lokalen Attribut Speicher befinden, und verpackt Sie in Sicherheits Token, sodass Benutzer nahtlos auf Web @ no__t-0browser @ no__t-1based Applications zugreifen können \(using Single Sign @ no__t-3on. \(sso @ no__t-5 @ no__t-6, die in einer Ressourcen Partnerorganisation gehostet werden.  
  
> [!NOTE]  
> Wenn Ihre Benutzer mithilfe eines Webbrowsers auf Verbund Anwendungen zugreifen, gibt ein Verbund Server automatisch Cookies für die Benutzer aus, um Ihren Anmeldestatus für diese Web @ no__t-0browser @ no__t-1based-Anwendung zu erhalten. Diese Cookies enthalten die Ansprüche für den Benutzer. Die Cookies ermöglichen SSO-Funktionen, damit die Benutzer die Anmelde Informationen nicht jedes Mal eingeben müssen, wenn Sie unterschiedliche Web @ no__t-0browser @ no__t-1based-Anwendungen im Ressourcen Partner besuchen.  
  
Im Web-SSO-Entwurf müssen Organisationen mit einem Umkreis Netzwerk, die Internet Benutzern den Zugriff auf Anwendungen erlauben möchten, einen Verbund Server Proxy im Umkreis Netzwerk installieren. Im Federated-Web-SSO-Entwurf muss mindestens ein Verbund Server im Unternehmensnetzwerk der Konto Partnerorganisation und mindestens ein Verbund Server im Unternehmensnetzwerk der Ressourcen Partnerorganisation installiert sein.  
  
> [!NOTE]  
> Bevor Sie in der Konto Partnerorganisation einen Verbund Server Computer einrichten können, müssen Sie den Computer zunächst einer beliebigen Domäne in der Active Directory-Gesamtstruktur hinzufügen, in der der Verbund Server verwendet wird, um Benutzer aus dieser Gesamtstruktur zu authentifizieren. Weitere Informationen finden Sie unter [checkliste: Einrichten eines Verbund Servers @ no__t-0.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
