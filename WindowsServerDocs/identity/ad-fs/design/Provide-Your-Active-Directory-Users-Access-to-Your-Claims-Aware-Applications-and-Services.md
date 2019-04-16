---
ms.assetid: d254fca3-85a1-424d-ac22-d6687ec3798e
title: "Bereitstellen der Active Directory-Benutzern den Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f6fb37c16c20915c0051e3a24cdb0c147ae92d9c
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="provide-your-active-directory-users-access-to-your-claims-aware-applications-and-services"></a>Bereitstellen der Active Directory-Benutzern den Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Wenn Sie ein Administrator in der Kontopartnerorganisation in einer Active Directory-Verbunddienste \(AD FS\) Bereitstellung sind und Sie Bereitstellungsziel Singlethread-Standardparameter auf \(SSO\) für Mitarbeiter im Unternehmensnetzwerk auf Ihre gehosteten Ressourcen zugreifen:  
  
-   SSO können Mitarbeiter, die Active Directory-Gesamtstruktur im Unternehmensnetzwerk angemeldet sind, auf mehrere Programme oder Dienste im Umkreisnetzwerk in Ihrer Organisation zugreifen. Diese Programme und Dienste werden von AD FS geschützt.  
  
    Fabrikam möchte z.B. Mitarbeiter Unternehmensnetzwerk Zugriff auf webbasierte Anwendungen verbunden haben, die im Umkreisnetzwerk für Fabrikam gehostet werden.  
  
-   Remotemitarbeiter, die Active Directory-Domäne angemeldet sind, können AD FS-Token abrufen, von dem Verbundserver in Ihrer Organisation verschaffen verbundzugriff auf AD FS\ gesicherte webbasierte Anwendungen oder Dienste, die auch in Ihrer Organisation befinden.  
  
-   In AD FS-Tokens der Mitarbeiter können mit Informationen in den Active Directory-Attributspeicher aufgefüllt werden.  
  
Die folgenden Komponenten sind für dieses Bereitstellungsziel erforderlich:  
  
-   **Active Directory-Domänendienste \(AD DS\):** AD DS enthält die mitarbeiterbenutzerkonten, die zum Generieren von AD FS-Token verwendet werden. Informationen, z.B. Gruppenmitgliedschaften und Attribute, wird AD FS-Tokens als Gruppenansprüche und benutzerdefinierte Ansprüche aufgefüllt.  
  
    > [!NOTE]  
    > Sie können auch Lightweight Directory Access Protocol \(LDAP\) oder Structured Query Language \(SQL\) zur Aufnahme die Identitäten zur Generierung von AD FS-Tokens verwenden.  
  
-   **Unternehmens-DNS:** diese Implementierung des Domain Name System \(DNS\) enthält einen einfachen Hostressourceneintrag für \(A\), sodass Intranetclients den Kontoverbundserver finden können. Diese DNS-Implementierung kann auch andere DNS-Einträge hosten, die im Unternehmensnetzwerk erforderlich sind. Weitere Informationen finden Sie unter [Name Resolution Requirements for Federation Servers](Name-Resolution-Requirements-for-Federation-Servers.md).  
  
-   **Kontoverbundserver für Partner:** dieser Verbundserver zu einer Domäne in der Kontopartner-Gesamtstruktur hinzugefügt wird. Er authentifiziert mitarbeiterbenutzerkonten und generiert AD FS-Tokens. Der Clientcomputer für den Mitarbeiter führt die integrierte Windows-Authentifizierung für diese Verbundserver ein AD FS-Token zu generieren. Weitere Informationen finden Sie unter [Überprüfen der Rolle des Verbundservers beim Kontopartner](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md).  
  
    Der Kontoverbundserver Partner kann die folgenden Benutzer authentifizieren:  
  
    -   Mitarbeiter mit Benutzerkonten in dieser Domäne  
  
    -   Mitarbeiter mit Benutzerkonten an beliebiger Stelle in dieser Gesamtstruktur  
  
    -   Mitarbeiter mit Benutzerkonten, die überall in Gesamtstrukturen, die von dieser Gesamtstruktur vertraut sind \ (über eine Two\-Wege-Windows-Trust\)  
  
-   **Mitarbeiter:** ein Mitarbeiter greift auf einen webbasierten Dienst \(through an application\) oder einer webbasierten Anwendung \ (über einen unterstützten Web-Browser\), während er sich mit dem Unternehmensnetzwerk angemeldet ist. Clientcomputer des Mitarbeiters im Unternehmensnetzwerk kommuniziert direkt mit dem Verbundserver für die Authentifizierung.  
  
Nach dem Überprüfen der Informationen in den verknüpften Themen können Sie beginnen, Umsetzung dieses Bereitstellungsziels anhand der Schrittein [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md).  
  
Die folgende Abbildungzeigt die einzelnen der erforderlichen Komponenten für dieses Bereitstellungsziel für AD FS.  
  
![Der Zugriff auf Ihre Ansprüche](media/31394ea8-fecb-4372-ac3f-cc3cf566ffc9.gif)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
