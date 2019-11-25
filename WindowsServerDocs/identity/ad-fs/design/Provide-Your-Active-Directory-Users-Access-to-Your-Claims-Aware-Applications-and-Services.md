---
ms.assetid: d254fca3-85a1-424d-ac22-d6687ec3798e
title: Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für Active Directory-Benutzer
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 48436f8e98af965f2bc2b38d296c4a15924e4db1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407950"
---
# <a name="provide-your-active-directory-users-access-to-your-claims-aware-applications-and-services"></a>Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für Active Directory-Benutzer

Wenn Sie ein Administrator in der Konto Partnerorganisation in einer Active Directory-Verbunddienste (AD FS) \(AD FS\) Bereitstellung sind und ein Bereitstellungs Ziel zum Bereitstellen von einzelnen\-Anmelde\-auf \(SSO-\) Zugriff für Mitarbeiter im Unternehmensnetzwerk auf Ihre gehosteten Ressourcen haben:  
  
-   Mitarbeiter, die im Unternehmensnetzwerk bei der Active Directory-Gesamtstruktur angemeldet sind, können mit SSO im Umkreisnetzwerk in Ihrer Organisation auf mehrere Programme oder Dienste zugreifen. Diese Anwendungen und Dienste werden durch AD FS gesichert.  
  
    Fabrikam könnte z. b. wünschen, dass Mitarbeiter im Unternehmensnetzwerk Verbund Zugriff auf Web\-basierte Anwendungen haben, die im Umkreis Netzwerk für Fabrikam gehostet werden.  
  
-   Remote Mitarbeiter, die bei einer Active Directory Domäne angemeldet sind, können AD FS Token vom Verbund Server in Ihrer Organisation erhalten, um Verbund Zugriff auf AD FS\-gesicherten, auf Web\-basierenden Anwendungen oder Dienste zu erhalten, die sich ebenfalls in Ihrer Organisation befinden.  
  
-   Die AD FS-Tokens der Mitarbeiter können mit Informationen aus dem Active Directory-Attributspeicher aufgefüllt werden.  
  
Die folgenden Komponenten sind für dieses Bereitstellungsziel erforderlich:  
  
-   **Active Directory Domain Services \(AD DS\):** AD DS enthält die Benutzerkonten der Mitarbeiter, die zum Generieren von AD FS Token verwendet werden. Informationen, wie z. B. Gruppenmitgliedschaften und Attribute, werden als Gruppenansprüche und benutzerdefinierte Ansprüche in AD FS-Tokens kopiert.  
  
    > [!NOTE]  
    > Sie können auch Lightweight Directory Access Protocol \(LDAP\) oder strukturierte Abfragesprache \(SQL\) verwenden, um die Identitäten für die AD FS tokengenerierung zu enthalten.  
  
-   Unter **nehmens-DNS:** Diese Implementierung von Domain Name System \(DNS-\) enthält einen einfachen Host \(einen\) Ressourcen Daten Satz, sodass Intranetclients den Konto Verbund Server finden können. Diese DNS-Implementierung kann auch andere DNS-Einträge hosten, die im Unternehmensnetzwerk erforderlich sind. Weitere Informationen finden Sie unter [Name Resolution Requirements for Federation Servers](Name-Resolution-Requirements-for-Federation-Servers.md).  
  
-   **Konto Partner Verbund Server:** Dieser Verbund Server ist einer Domäne in der Konto Partner-Gesamtstruktur hinzugefügt. Er authentifiziert Mitarbeiterbenutzerkonten und generiert AD FS-Tokens. Der Client Computer für den Mitarbeiter führt die integrierte Windows-Authentifizierung für diesen Verbund Server aus, um ein AD FS Token zu generieren. Weitere Informationen finden Sie unter [Überprüfen der Rolle des Verbundservers beim Kontopartner](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md).  
  
    Der Verbund Server des Konto Partners kann die folgenden Benutzer authentifizieren:  
  
    -   Mitarbeiter mit Benutzerkonten in dieser Domäne  
  
    -   Mitarbeiter mit Benutzerkonten an beliebiger Stelle in der Gesamtstruktur  
  
    -   Mitarbeiter mit Benutzerkonten an beliebiger Stelle in Gesamtstrukturen, die von dieser Gesamtstruktur als vertrauenswürdig eingestuft werden, \(zwei\-\)  
  
-   **Mitarbeiter:** Ein Mitarbeiter greift auf einen Web\-basierten Dienst zu, der \(über eine Anwendung\) oder eine auf Web\-basierende Anwendung \(über einen unterstützten Webbrowser\), während er am Unternehmensnetzwerk angemeldet ist. Der Client Computer des Mitarbeiters im Unternehmensnetzwerk kommuniziert zur Authentifizierung direkt mit dem Verbund Server.  
  
Nach Einsicht der Informationen in den verknüpften Themen können Sie anhand der Schritte in [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)beginnen, dieses Ziel bereitstellen.  
  
Die folgende Abbildung zeigt die einzelnen erforderlichen Komponenten für dieses AD FS Bereitstellungs Ziel.  
  
![Zugriff auf Ihre Ansprüche](media/31394ea8-fecb-4372-ac3f-cc3cf566ffc9.gif)  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
