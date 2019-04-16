---
ms.assetid: de7e1e4a-f96d-4b59-ac9b-f65f5d37a96f
title: "Bieten Sie Benutzern in einer anderen Organisationszugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b4ec08182e2523b0fcb16088ec9c1d094a5923fe
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="provide-users-in-another-organization-access-to-your-claims-aware-applications-and-services"></a>Bieten Sie Benutzern in einer anderen Organisationszugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Wenn Sie ein Administrator in der Ressourcenpartnerorganisation in Active Directory Federation Services \(AD FS\) sind und Sie haben ein Bereitstellungsziel darin besteht, verbundzugriff für Benutzer in einer anderen Organisation bereitstellen \ (das Konto Partner Organization\) in eine Claims\-fähigen Anwendung oder einen webbasierten Dienst, der in Ihrer Organisation befindet \ (die Ressource Partner Organization\):  
  
-   Verbundbenutzer in Ihrer Organisation und in Organisationen, die ein Verbund konfiguriert haben für Ihre Organisation vertrauen \ (Konto Partner Organizations\) erreichen des AD FS gesicherten Anwendungen oder Dienste, die von Ihrer Organisation gehostet werden. Weitere Informationen finden Sie unter [Federated Web SSO Design](Federated-Web-SSO-Design.md).  
  
    Fabrikam möchte z.B. seine Mitarbeiter Unternehmensnetzwerk Zugriff auf Webdienste verbunden haben, die von Contoso gehostet werden.  
  
-   Verbundbenutzer, die keine direkte Zuordnung zu einer vertrauenswürdigen Organisation \ (z.B. einzelne Customers\), angemeldet sind einem Attributspeicher, die in Ihrem Umkreisnetzwerk gehostet wird, können mehrere AD FS\ gesicherte auf Anwendungen zugreifen, die auch im Umkreisnetzwerk, gehostet werden indem die Anmeldung einmalig von Clientcomputern, die sich im Internet befinden. Anders ausgedrückt, wenn Sie Kundenkonten zum Aktivieren des Zugriffs auf Anwendungen oder Dienste in Ihrem Umkreisnetzwerk hosten, können Kunden, die Sie in einem Attributspeicher hosten eine oder mehrere Programme oder Dienste im Umkreisnetzwerk zugreifen einfach durch die Protokollierung auf einmal. Weitere Informationen finden Sie unter [Web-SSO-Entwurf](Web-SSO-Design.md).  
  
    Fabrikam möchte beispielsweise seinen Kunden haben Singlethread-Standardparameter-\(SSO\) Zugriff auf mehrere Programme oder Dienste, die im Umkreisnetzwerk gehostet werden.  
  
Die folgenden Komponenten sind für dieses Bereitstellungsziel erforderlich:  
  
-   **Active Directory-Domänendienste \(AD DS\):** Ressourcenverbundserver Partner muss zu einer Active Directory-Domäne gehören.  
  
-   **Umkreis-DNS:** Domain Name System \(DNS\) sollte einen einfachen Hostressourceneintrag für \(A\) enthalten, sodass Clientcomputer den ressourcenpartnerverbundserver und den Webserver finden können. Der DNS-Server kann andere DNS-Einträge hosten, die auch im Umkreisnetzwerk erforderlich sind. Weitere Informationen finden Sie unter [Name Resolution Requirements for Federation Servers](Name-Resolution-Requirements-for-Federation-Servers.md).  
  
-   **Ressourcenpartnerverbundserver:** der Ressourcenverbundserver der Partner überprüft, ob AD FS-Token, die der Kontopartner sendet. Ermittlung von Kontopartnern erfolgt über diese Verbundserver. Weitere Informationen finden Sie unter [Überprüfen der Rolle des Verbundservers beim Ressourcenpartner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md).  
  
-   **Webserver:** der Webserver kann eine Webanwendung oder einen Webdienst hosten. Der Webserver bestätigt, dass er gültige AD FS-Token von Verbundbenutzer erhält, bevor er Zugriff auf die geschützte Webanwendung oder den Webdienst gestattet.  
  
    Mithilfe von Windows Identity Foundation \(WIF\) können Sie Ihre Web-Anwendung oder Dienste entwickeln, so, dass sie Anmeldeanfragen Verbundbenutzer akzeptiert, die mit jeder standardanmeldemethode, z.B. Benutzername und Kennwort vorgenommen werden.  
  
Nach dem Überprüfen der Informationen in den verknüpften Themen können Sie beginnen, Umsetzung dieses Bereitstellungsziels anhand der Schrittein [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md) und [Prüfliste: Implementieren eines Web-SSO-Entwurfs](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md).  
  
Die folgende Abbildungzeigt die einzelnen der erforderlichen Komponenten für dieses Bereitstellungsziel für AD FS.  
  
![Der Zugriff auf Ihre Ansprüche](media/75358b16-2a6f-4e16-9cc4-b0e614480305.gif)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
