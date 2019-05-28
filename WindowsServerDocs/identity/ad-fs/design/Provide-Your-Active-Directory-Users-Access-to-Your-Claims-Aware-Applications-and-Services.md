---
ms.assetid: d254fca3-85a1-424d-ac22-d6687ec3798e
title: Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für Active Directory-Benutzer
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8c3db2873e1c7a0fa217ba37b9439cc38dfafc36
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191001"
---
# <a name="provide-your-active-directory-users-access-to-your-claims-aware-applications-and-services"></a>Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für Active Directory-Benutzer

Wenn Sie ein Administrator in der Kontopartnerorganisation in einer Active Directory Federation Services sind \(AD FS\) Bereitstellung, und Sie haben ein Bereitstellungsziel darin besteht, zu einzelnen\-anmelden\-auf \( SSO\) Zugriff für Mitarbeiter im Unternehmensnetzwerk auf Ihre gehosteten Ressourcen:  
  
-   Mitarbeiter, die im Unternehmensnetzwerk bei der Active Directory-Gesamtstruktur angemeldet sind, können mit SSO im Umkreisnetzwerk in Ihrer Organisation auf mehrere Programme oder Dienste zugreifen. Diese Anwendungen und Dienste werden von AD FS geschützt werden.  
  
    Fabrikam kann z. B. Mitarbeiter im Unternehmensnetzwerk verbundzugriff auf Web verbundzugriff\--basierte Anwendungen, die im Umkreisnetzwerk für Fabrikam gehostet werden.  
  
-   Remotemitarbeiter, die Active Directory-Domäne angemeldet sind, können AD FS-Token erhalten, von dem Verbundserver in Ihrer Organisation, um verbundzugriff auf AD FS zu erhalten\-gesicherte Web\-basierte Anwendungen oder Dienste, die auch im befinden. Ihre Organisation.  
  
-   Die AD FS-Tokens der Mitarbeiter können mit Informationen aus dem Active Directory-Attributspeicher aufgefüllt werden.  
  
Die folgenden Komponenten sind für dieses Bereitstellungsziel erforderlich:  
  
-   **Active Directory-Domänendienste \(AD DS\):** AD DS enthält die Mitarbeiterbenutzerkonten, die zum Generieren von AD FS-Token verwendet werden. Informationen, wie z. B. Gruppenmitgliedschaften und Attribute, werden als Gruppenansprüche und benutzerdefinierte Ansprüche in AD FS-Tokens kopiert.  
  
    > [!NOTE]  
    > Sie können auch Lightweight Directory Access Protocol \(LDAP\) oder Structured Query Language \(SQL\) enthalten die Identitäten für AD FS-token generieren.  
  
-   **Unternehmens-DNS:** Diese Implementierung des Domain Name System \(DNS\) enthält einen einfachen Host \(ein\) Ressource aufzeichnen, sodass Intranetclients den Konto-Verbund-Server lokalisieren können. Diese DNS-Implementierung kann auch andere DNS-Einträge hosten, die im Unternehmensnetzwerk erforderlich sind. Weitere Informationen finden Sie unter [Name Resolution Requirements for Federation Servers](Name-Resolution-Requirements-for-Federation-Servers.md).  
  
-   **Kontoverbundserver Partner:** Dieser Verbundserver gehört zu einer Domäne in der Kontopartner-Gesamtstruktur. Er authentifiziert Mitarbeiterbenutzerkonten und generiert AD FS-Tokens. Der Clientcomputer für den Mitarbeiter führt die integrierte Windows-Authentifizierung für den Verbundserver ein AD FS-Token zu generieren. Weitere Informationen finden Sie unter [Review the Role of the Federation Server in the Account Partner](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md).  
  
    Die Konto-Partnerverbundserver kann die folgenden Benutzer authentifizieren:  
  
    -   Mitarbeiter mit Benutzerkonten in dieser Domäne  
  
    -   Mitarbeiter mit Benutzerkonten an beliebiger Stelle in der Gesamtstruktur  
  
    -   Mitarbeiter mit Benutzerkonten, die überall in Gesamtstrukturen, die von dieser Gesamtstruktur als vertrauenswürdig eingestuft werden \(über ein\-wie Windows-Vertrauensstellung\)  
  
-   **Mitarbeiter:** Ein Mitarbeiter greift auf eine Web\--basierten Diensts \(durch eine Anwendung\) oder eines Webdiensts\--basierten Anwendung \(über einen unterstützten Webbrowser\) während er angemeldet ist die Unternehmensnetzwerk. Client-Computer des Mitarbeiters im Unternehmensnetzwerk kommuniziert direkt mit der Verbundserver für die Authentifizierung.  
  
Nach dem Durchlesen der Informationen in den verknüpften Themen können Sie beginnen können, Umsetzung dieses Bereitstellungsziels anhand der Schritte in [Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md).  
  
Die folgende Abbildung zeigt jede der erforderlichen Komponenten für dieses Bereitstellungsziel für AD FS.  
  
![der Zugriff auf Ihre Ansprüche](media/31394ea8-fecb-4372-ac3f-cc3cf566ffc9.gif)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
