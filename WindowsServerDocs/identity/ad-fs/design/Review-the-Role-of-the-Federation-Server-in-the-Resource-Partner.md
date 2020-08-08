---
ms.assetid: f88238ea-d851-4129-8b4e-a3a62b813614
title: Überprüfen der Rolle des Verbundservers beim Ressourcenpartner
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: b090384cebd5213ec10799f4b2c0d594de3a3fd6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972067"
---
# <a name="review-the-role-of-the-federation-server-in-the-resource-partner"></a>Überprüfen der Rolle des Verbundservers beim Ressourcenpartner

Der Verbund Server in der Ressourcen Partnerorganisation fängt eingehende Sicherheits Token ab, die von einem Konto Verbund Server gesendet werden, überprüft und signiert Sie und gibt dann eigene Sicherheits Token aus, die für die webbasierte Anwendung bestimmt sind \- .

> [!NOTE]
> Wenn Verbund Benutzer mit ihren Webbrowsern auf webbasierte Anwendungen zugreifen \- , erstellt der Verbund Server in der Ressourcen Partnerorganisation ein neues Authentifizierungs Cookie und schreibt es in den Browser. Dieses Cookie aktiviert \- SSO- \- Funktionen für einmaliges Anmelden \( \) , sodass Benutzer sich nicht erneut beim Verbund Server beim Konto Partner anmelden müssen, wenn die Benutzer versuchen, auf verschiedene webbasierte \- Anwendungen im Ressourcen Partner zuzugreifen.

Im Web-SSO-Entwurf muss mindestens ein Verbund Server im Umkreis Netzwerk installiert sein. Im Federated-Web-SSO-Entwurf muss mindestens ein Verbund Server im Unternehmensnetzwerk der Konto Partnerorganisation und mindestens ein Verbund Server im Unternehmensnetzwerk der Ressourcen Partnerorganisation installiert sein.

> [!NOTE]
> Vor dem Einrichten eines Verbund Server Computers in der Ressourcen Partnerorganisation müssen Sie den Computer zunächst einer beliebigen Active Directory Domäne in der Ressourcen Partnerorganisation hinzufügen. Weitere Informationen finden Sie unter [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

