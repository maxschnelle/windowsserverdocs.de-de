---
ms.assetid: de7e1e4a-f96d-4b59-ac9b-f65f5d37a96f
title: Bereitstellen des Zugriffs auf Ihre Ansprüche unterstützende Anwendungen und Dienste für die Benutzer anderer Organisationen
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 03b9e4142d522ce8a455bb9cb18dbae48a89f302
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969737"
---
# <a name="provide-users-in-another-organization-access-to-your-claims-aware-applications-and-services"></a>Bereitstellen des Zugriffs auf Ihre Ansprüche unterstützende Anwendungen und Dienste für die Benutzer anderer Organisationen


Wenn Sie ein Administrator in der Ressourcen Partnerorganisation in Active Directory-Verbunddienste (AD FS) \( AD FS sind \) und ein Bereitstellungs Ziel haben, einem Verbund Zugriff für Benutzer in einer anderen Organisation, \( die der Konto Partnerorganisation \) , für eine Ansprüche unterstützende \- Anwendung oder einen \- webbasierten Dienst, der sich in Ihrer Organisation in \( der Ressourcen Partnerorganisation befindet, \) bereitzustellen:

-   Verbund Benutzer in Ihrer Organisation und in Organisationen, die eine Verbund Vertrauensstellung für Ihre Organisations Konto-Partnerorganisationen konfiguriert haben, \( können auf \) die AD FS gesicherte Anwendung oder den Dienst zugreifen, die von Ihrer Organisation gehostet wird. Weitere Informationen finden Sie unter [Federated Web SSO Design](Federated-Web-SSO-Design.md).

    Beispielsweise könnte Fabrikam anfragen, dass Mitarbeiter im Unternehmensnetzwerk Verbundzugriff auf Webdienste erhalten, die von Contoso gehostet werden.

-   Verbund Benutzer, die keine direkte Zuordnung zu einer vertrauenswürdigen Organisation haben, z. b. \( einzelne Kunden \) , die bei einem Attribut Speicher angemeldet sind, der in Ihrem Umkreis Netzwerk gehostet wird, können auf mehrere AD FS \- gesicherte Anwendungen zugreifen, die auch in Ihrem Umkreis Netzwerk gehostet werden, indem Sie sich einmal von Client Computern im Internet anmelden. Wenn Sie also Kundenkonten zum Aktivieren des Zugriffs auf Anwendungen oder Dienste in Ihrem Umkreisnetzwerk hosten, können Kunden, die Sie in einem Attributspeicher hosten, auf ein oder mehrere Anwendungen oder Dienste im Umkreisnetzwerk zugreifen, indem Sie sich einfach einmalig anmelden. Weitere Informationen finden Sie unter [Web SSO Design](Web-SSO-Design.md).

    Fabrikam könnte z. b. möchten, dass Ihre Kunden einmaliges Anmelden (SSO) auf \- \- \( \) mehrere Anwendungen oder Dienste zugreifen können, die in Ihrem Umkreis Netzwerk gehostet werden.

Die folgenden Komponenten sind für dieses Bereitstellungsziel erforderlich:

-   **Active Directory Domain Services \( AD DS \) :** der Ressourcen Partner Verbund Server muss einer Active Directory Domäne beitreten.

-   **Umkreis-DNS:** Domain Name System \( DNS \) sollte einen einfachen Host \( einen \) Ressourcen Daten Satz enthalten, sodass Client Computer den Ressourcen Partner Verbund Server und den Webserver finden können. Der DNS-Server kann andere DNS-Einträge hosten, die auch im Umkreisnetzwerk erforderlich sind. Weitere Informationen finden Sie unter [Anforderungen an die Namensauflösung für Verbundserver](Name-Resolution-Requirements-for-Federation-Servers.md).

-   **Ressourcen Partner-Verbund Server:** Der Ressourcen Partner Verbund Server überprüft AD FS Token, die von den Konto Partnern gesendet werden. Die Ermittlung von Konto Partnern erfolgt über diesen Verbund Server. Weitere Informationen finden Sie unter [Review the Role of the Federation Server in the Resource Partner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md).

-   **Webserver:** Der Webserver kann eine Webanwendung oder einen Webdienst hosten. Der Webserver bestätigt, dass er gültige AD FS-Token von Verbundbenutzer erhält, bevor er Zugriff auf die geschützte Webanwendung oder den Webdienst gestattet.

    Mithilfe von Windows Identity Foundation \( WIF \) können Sie Ihre Webanwendung oder ihren Dienst so entwickeln, dass Sie Anmelde Anforderungen für Verbund Benutzer akzeptieren, die mit jeder Standard Anmelde Methode (z. b. Benutzername und Kennwort) vorgenommen werden.

Nachdem Sie die Informationen in den verknüpften Themen überprüft haben, können Sie mit der Bereitstellung dieses Ziels beginnen, indem Sie die Schritte in Prüfliste [: Implementieren eines Federated-Web-SSO-Entwurfs](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md) und [einer](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)Prüfliste ausführen.

Die folgende Abbildung zeigt die einzelnen erforderlichen Komponenten für dieses AD FS Bereitstellungs Ziel.

![Zugriff auf Ihre Ansprüche](media/75358b16-2a6f-4e16-9cc4-b0e614480305.gif)

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
