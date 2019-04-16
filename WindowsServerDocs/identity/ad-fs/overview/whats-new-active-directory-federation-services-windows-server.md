---
ms.assetid: aa892a85-f95a-4bf1-acbb-e3c36ef02b0d
title: Was ist neu in Active Directory Federation Services für Windows Server2016
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/08/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b8dd9174a869110d98ba1e65cbf2c2b6ec000b71
ms.sourcegitcommit: f26d2668f57624a3865ca4ffd36a698eea7b503e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/12/2018
---
# <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Was ist neu in Active Directory Federation Services für Windows Server2016

>Gilt für: Windows Server 2016

## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Was ist neu in Active Directory Federation Services für Windows Server2016   
Wenn Sie Informationen zu früheren Versionen von AD FS suchen, finden Sie in den folgenden Artikeln:  
 [AD FS unter Windows Server2012 oder 2012 R2](https://technet.microsoft.com/library/hh831502.aspx) und [AD FS 2.0](https://technet.microsoft.com/library/adfs2.aspx)  

 Active Directory Federation Services bietet die Steuerung des Zugriffs und einmaliges Anmelden auf auf einer Vielzahl von Anwendungen, einschließlich Office365, cloudbasierten SaaS-Anwendungen und Anwendungen im Unternehmensnetzwerk.  
* Der IT-Organisation die Möglichkeit bieten anmelden und Steuerung des Zugriffs auf modernen und Legacy-Anwendungen, lokal und in der Cloud, basierend auf den gleichen Satz von Anmeldeinformationen und Richtlinien.    
* Für den Benutzer enthält es eine nahtlose Anmeldung mit den Anmeldeinformationen der gleiche, vertraut.  
* Für Entwickler bietet es eine einfache Möglichkeit zum Authentifizieren von Benutzern, deren Identitäten in das Verzeichnis der Organisation live, damit Sie sich auf Ihre Anwendung, keine Authentifizierung oder Identität konzentrieren können.  

Dieser Artikel beschreibt die Neuigkeiten in AD FS unter Windows Server2016 (AD FS 2016).  

## <a name="eliminate-passwords-from-the-extranet"></a>Vermeiden Sie Kennwörter über das Extranet  
AD FS 2016 ermöglicht drei neue Optionen für die Anmeldung ohne Kennwörter, da Unternehmen Netzwerk vermeiden von Phished verlorene oder gestohlene Kennwörter beeinträchtigt werden. 

### <a name="sign-in-with-azure-multi-factor-authentication"></a>Melden Sie sich mit Azure Multi-Factor Authentication
AD FS 2016 baut auf dem Multi-Factor Authentication (MFA) Funktionen von AD FS unter Windows Server2012 R2 in eigener Regie anmelden mithilfe von nur Azure MFA-Code, ohne Eingabe eines Benutzernamens und Kennworts.

* Mit der Azure MFA als primäre Authentifizierungsmethode wird der Benutzer für seinen Benutzernamen und der OTP-Code aus der Azure Authenticator-App aufgefordert.  
* Mit der Azure MFA als sekundäre oder zusätzliche Authentifizierungsmethode bietet dem Benutzer primäre Authentifizierung Anmeldeinformationen (mithilfe der integrierten Windows-Authentifizierung, Benutzernamen und Kennwörter, Smartcards oder Benutzer bzw. das Gerät ein Zertifikat) und dann wird eine Aufforderung für Text, Stimme oder OTP-basierte Azure MFA-Anmeldung.  
* Mit dem neuen integrierten Azure MFA-Adapter war Installation und Konfiguration für Azure MFA mit AD FS nie einfacher.
* Organisationen können von Azure MFA ohne die Notwendigkeit einer auf lokalen Azure MFA-Server nutzen.
* Azure MFA kann für das Intranet oder Extranet, oder als Teil des Steuerelements Zugriffsrichtlinien konfiguriert werden.

Weitere Informationen zu Azure MFA mit AD FS
*  [Konfigurieren von AD FS 2016 und Azure MFA](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-and-azure-mfa)  

### <a name="password-less-access-from-compliant-devices"></a>Ohne Kennwort Zugriff über kompatible Geräte
AD FS 2016 baut auf vorherige Registrierung Gerätefunktionen zum Anmelden zu aktivieren und die Steuerung des Zugriffs basiert des Kompatibilitätsstatus des Geräts. Benutzer können sich mit den Anmeldeinformationen Gerät anmelden, und die Kompatibilität wird erneut ausgewertet, wenn Geräteattribute ändern, damit Sie immer sicherstellen können, dass die Richtlinien erzwungen werden.  Diese aktiviert Richtlinien wie z.B.

* Aktivieren Sie den Zugriff nur über Geräte, die verwaltete und/oder kompatibel sind  
* Aktivieren Sie Extranet-Zugriff nur auf Geräten, die verwaltete und/oder kompatibel sind  
* Mehrstufige Authentifizierung für Computer, die nicht verwaltete oder nicht kompatibel sind erforderlich.  

AD FS bietet, die auf lokalen-Komponente von Richtlinien für bedingten Zugriff in einem hybridszenario. Wenn Sie Geräte mit Azure AD für bedingten Zugriff auf Cloudressourcen registrieren, kann die Identität des Geräts auch für AD FS-Richtlinien verwendet werden.

![Was ist neu](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/ADFS_ITPRO4.png)  

 Weitere Informationen zur Verwendung von Gerät basierten bedingten Zugriff in der Cloud   
 *  [Azure Active Directory bedingten Zugriff](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access/)

Weitere Informationen zur Verwendung von Gerät basierten bedingten Zugriff mit AD FS
*  [Planen der Geräte basierend bedingten Zugriff mit AD FS](../../ad-fs/deployment/Plan-Device-based-Conditional-Access-on-Premises.md)  
* [Zugriffssteuerungsrichtlinien in AD FS](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="sign-in-with-windows-hello-for-business"></a>Melden Sie sich mit Windows Hello for Business   
Windows10-Geräten eine Einführung in Windows Hello und Windows Hello for Business, ersetzt Kennwörter mit starkem Gerät gebunden-Anmeldeinformationen, die durch eine Benutzergeste (eine PIN, einer biometrischen Geste wie Fingerabdruck oder Gesichtserkennung) geschützt sind. AD FS 2016 unterstützt diese neue diese neuen Funktionen von Windows10, damit Benutzer im Intranet oder das Extranet, ohne dass ein Kennwort angeben müssen für AD FS-Anwendungen anmelden können.

Weitere Informationen zur Verwendung von Microsoft Windows Hello for Business in Ihrer Organisation
*  [Windows Hello for Business in Ihrer Organisation aktivieren](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-passport-deployment/)

## <a name="secure-access-to-applications"></a>Sicherer Zugriff auf Anwendungen

### <a name="modern-authentication"></a>Moderne Authentifizierung
AD FS 2016 unterstützt die neuesten moderne Protokolle, die eine bessere Benutzererfahrung für Windows10 als auch die neuesten iOS und Android-Geräte und Apps bereitstellen.  

Weitere Informationen finden Sie unter [AD FS-Szenarien für Entwickler](../../ad-fs/overview/AD-FS-Scenarios-for-Developers.md)  


### <a name="configure-access-control-policies-without-having-to-know-claim-rules-language"></a>Zugriffsrichtlinien konfigurieren, ohne zu wissen Anspruch Regeln Sprache  
Bisher mussten AD FS-Administratoren zum Konfigurieren von Richtlinien mithilfe der anspruchsregelsprache von AD FS, wodurch es schwierig zu konfigurieren und Verwalten von Richtlinien. Mit Zugriffsrichtlinien können Administratoren in Vorlagen verwenden, z.B. allgemeine Richtlinien gelten
* Erlauben Sie nur auf das Intranet
* Lassen Sie alle Benutzer zu und erfordern Sie MFA von Extranet
* Lassen Sie alle Benutzer zu und erfordern Sie MFA aus einer bestimmten Gruppe

Die Vorlagen sind leicht anpassen mithilfe einer assistentengesteuerte Prozess Ausnahmen oder zusätzliche Regeln hinzu und können auf einen oder mehrere Anwendungen für die Erzwingung der konsistent angewendet werden.

Weitere Informationen finden Sie unter [Zugriffssteuerungsrichtlinien in AD FS.](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="enable-sign-on-with-non-ad-ldap-directories"></a>Aktivieren Sie Anmelden mit nicht - AD-LDAP-Verzeichnissen auf  
Viele Organisationen verfügen über eine Kombination aus Active Directory und Drittanbieter-Verzeichnisse. Durch das Hinzufügen der AD FS-Unterstützung für die Authentifizierung von Benutzern in LDAP-v3-kompatiblen Verzeichnissen gespeichert kann AD FS jetzt für verwendet werden:
* Benutzer von Drittanbietern, LDAP-v3-kompatiblen Verzeichnissen
* Benutzer in Active Directory-Gesamtstrukturen für die eine bidirektionale Vertrauensstellung von Active Directory nicht konfiguriert ist
* Benutzer in Active Directory Lightweight Directory Services (AD LDS)

Weitere Informationen finden Sie unter [Configure AD FS zum Authentifizieren von Benutzern in LDAP-Verzeichnissen gespeichert.](../../ad-fs/operations/Configure-AD-FS-to-authenticate-users-stored-in-LDAP-directories.md)  

## <a name="better-sign-in-experience"></a>Besser Anmeldung
### <a name="customize-sign-in-experience-for-ad-fs-applications"></a>Anpassen von Protokoll-Erlebnis für AD FS-Anwendungen  
Wir haben die Möglichkeit zum Anpassen der Anmeldevorgang für jede Anwendung eine hervorragende Benutzerfreundlichkeit Verbesserung, insbesondere für Organisationen wäre, die Anmeldung auf für Anwendungen bereitstellen, die mehrere verschiedene Unternehmen oder Marken darstellen.  

Zuvor AD FS unter Windows Server2012 R2 eine allgemeinen anmelden Erfahrung für alle relying Party Anwendungen bereitgestellt, mit der Möglichkeit, eine Teilmenge der Text anpassen basierten Inhalt pro Anwendung. Mit Windows Server2016 können Sie nicht nur die Nachrichten jedoch Bilder, Logo und Web Design pro Anwendung anpassen. Darüber hinaus können Sie neue, benutzerdefinierte Webdesigns erstellen und gelten diese pro vertrauende Seite Partei.  

Weitere Informationen finden Sie unter [AD FS-Anmeldung Anpassung durch den Benutzer.](../../ad-fs/operations/AD-FS-user-sign-in-customization.md)  



## <a name="manageability-and-operational-enhancements"></a>Verwaltung und Betrieb Erweiterungen  
Im folgenden Abschnittwerden die verbesserten Betriebsszenarien, die mit Active Directory Federation Services in Windows Server2016 eingeführt wurden.  

### <a name="streamlined-auditing-for-easier-administrative-management"></a>Optimierte Überwachung für einfachere Verwaltung  
In AD FS für die es für Windows Server2012 R2 wurden zahlreiche Überwachungsereignisse für eine einzelne Anforderung generiert und die relevante Informationen über eine Anmeldung oder Token Ausstellung Aktivität ist entweder nicht vorhanden (in einigen Versionen von AD FS) oder über mehrere Überwachungsereignisse. Der AD FS werden Überwachungsereignisse aufgrund ihrer ausführliche Art standardmäßig deaktiviert.  
Mit der Version von AD FS 2016 Überwachung optimierte und weniger ausführlich geworden.  

Weitere Informationen finden Sie unter [Überwachungserweiterungen zu AD FS unter Windows Server2016.](../../ad-fs/technical-reference/auditing-enhancements-to-ad-fs-in-windows-server.md)  

### <a name="improved-interoperability-with-saml-20-for-participation-in-confederations"></a>Verbesserte Interoperabilität mit SAML 2.0 für die Teilnahme am Gewerkschaftsbund  
AD FS 2016 enthält zusätzliche SAML-Protokoll unterstützt, u. a. die Unterstützung für den Import von Vertrauensstellungen, die basierend auf Metadaten, die mehrere Elemente enthält. Dadurch können Sie die Konfiguration von AD FS zur Teilnahme an Gewerkschaftsbund wie InCommon Verbundserver und anderen Implementierungen, die die eGov 2.0-Standard entsprechen.  

Weitere Informationen finden Sie unter [Verbesserte Interoperabilität mit SAML 2.0.](../../ad-fs/operations/Improved-interoperability-with-SAML-2.0.md)  

### <a name="simplified-password-management-for-federated-o365-users"></a>Vereinfachte Verwaltung für Verbundbenutzer Office365  
Sie können Active Directory-Verbunddienste (AD FS) Kennwort Ablauf Ansprüche senden, die Vertrauensstellungen vertrauenden Seite (Anwendungen) konfigurieren, die von AD FS geschützt sind. Wie diese Ansprüche verwendet werden, hängt von der Anwendung. Mit Office365 als der vertrauenden haben z.B. Updates in Exchange und Outlook verbundene Benutzer ihre Kennwörter bald-zu--abgelaufen sein benachrichtigen implementiert wurde.  

Weitere Informationen finden Sie unter [Configure AD FS Kennwort Ablauf Ansprüche senden.](../../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md)  

### <a name="moving-from-ad-fs-in-windows-server-2012-r2-to-ad-fs-in-windows-server-2016-is-easier"></a>Verschieben von AD FS unter Windows Server2012 R2 zu AD FS unter Windows Server2016 ist einfacher  
Bisher auf eine neue Version von AD FS migrieren Konfiguration aus der alten Farm exportieren und Importieren von einer völlig neuen, parallelen Farm.  

Verschieben von AD FS unter Windows Server2012 R2 zu AD FS unter Windows Server2016 ist jetzt viel einfacher geworden. Fügen Sie einfach einen neuen Windows Server2016-Server zu einer Farm mit Windows Server2012 R2, und die Farm wird auf Farmebene Verhalten Windows Server2012 R2 fungieren, damit es aussieht und verhält sich wie eine Windows Server2012 R2-Farm.  

Klicken Sie dann neue Windows Server2016-Server der Farm, überprüfen Sie die Funktionalität Server fügen Sie hinzu und entfernen Sie der älteren aus dem Lastenausgleich. Wenn alle Farmknoten auf Windows Server2016 ausgeführt werden, können Sie sich Verhalten Farmebene auf 2016 aktualisieren, und beginnen mit den neuen Features.  

Weitere Informationen finden Sie unter [zu AD FS unter Windows Server2016 aktualisieren.](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)  
