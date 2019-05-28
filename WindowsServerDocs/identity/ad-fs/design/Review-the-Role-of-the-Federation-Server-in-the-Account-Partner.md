---
ms.assetid: d0ba3c0d-869f-4e24-89d7-499da7576f22
title: Überprüfen der Rolle des Verbundservers beim Kontopartner
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5bc304277b872bd9b99b79b84694dd0cb1eb73ba
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190884"
---
# <a name="review-the-role-of-the-federation-server-in-the-account-partner"></a>Überprüfen der Rolle des Verbundservers beim Kontopartner

Einen Verbundserver in Active Directory Federation Services \(AD FS\) fungiert als sicherheitstokenaussteller. Ein Verbundserver generiert basierend auf kontenwerten speichern Werte, die in ein lokales Element befinden, Ansprüche und verpackt sie in Sicherheitstoken, sodass Benutzer nahtlos Web zugreifen können\-Browser\--basierte Anwendungen \(verwenden Einmaliges Anmelden\-auf \(SSO\) \) , die in einer Ressourcenpartnerorganisation gehostet werden.  
  
> [!NOTE]  
> Wenn Ihre Benutzer über einen Webbrowser auf verbundanwendungen zugreifen, ein Verbundserver automatisch Cookies für die Benutzer können den Anmeldestatus für dieses Web verwalten\-Browser\--basierten Anwendung. Diese Cookies enthalten die Ansprüche für den Benutzer. Die Cookies ermöglichen SSO-Funktionen, damit die Benutzer keine Anmeldeinformationen über jedes Mal eingeben, dass sie anderen besuchen\-Browser\--basierte Anwendungen in der Ressourcenpartnerorganisation.  
  
In den Web-SSO-Entwurf müssen Organisationen mit einem Umkreisnetzwerk, die Internet-Benutzer auf Anwendungen zugreifen möchten, einen Verbundserverproxy im Umkreisnetzwerk installieren. Im Federated-Web-SSO-Entwurf muss mindestens ein Verbundserver im Unternehmensnetzwerk der Kontopartnerorganisation installiert und mindestens ein Verbundserver im Unternehmensnetzwerk der Ressourcenpartnerorganisation installiert vorhanden sein.  
  
> [!NOTE]  
> Bevor Sie einen Verbund-Server-Computer in der Kontopartnerorganisation einrichten können, müssen Sie den Computer einer beliebigen Domäne in Active Directory-Gesamtstruktur hinzufügen, in dem die Verbundserver zum Authentifizieren von Benutzern in dieser Gesamtstruktur verwendet wird. Weitere Informationen finden Sie unter [Prüfliste: Das Einrichten eines Verbundservers](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
