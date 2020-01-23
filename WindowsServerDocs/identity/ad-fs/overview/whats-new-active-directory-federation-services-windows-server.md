---
ms.assetid: aa892a85-f95a-4bf1-acbb-e3c36ef02b0d
title: Neuerungen in Active Directory-Verbunddienste (AD FS) für Windows Server 2016
description: ''
author: billmath
ms.author: billmath
manager: daveba
ms.date: 01/22/2020
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: adce37d8d06399d3a00221a12f3449244720ade7
ms.sourcegitcommit: 840d1d8851f68936db3934c80796fb8722d3c64a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519482"
---
# <a name="whats-new-in-active-directory-federation-services"></a>Neues in Active Directory-Verbunddienste (AD FS)


## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2019"></a>What's new in Active Directory Federation Services for Windows Server 2019

### <a name="protected-logins"></a>Protected Logins
The following is a brief summary of updates to protected logins available in AD FS 2019:
- **External Auth Providers as Primary** - Customers can now use 3rd party authentication products as the first factor and not expose passwords as the first factor. In the cases where an external auth provider can prove 2 factors it can claim MFA. 
- **Password Authentication as additional Authentication** - Customers have a fully supported inbox option to use password only for the additional factor after a password less option is used as the first factor. This improves the customer experience from ADFS 2016 where customers had to download a github adapter which is supported as is. 
- **Pluggable Risk Assessment Module** - Customers can now build their own plug in modules to block certain types of requests during pre-authentication stage. This makes it easier for customers to use cloud intelligence such as Identity protection to block logins for risky users or risky transactions.  For more information see [ Build Plug-ins with AD FS 2019 Risk Assessment Model](../../ad-fs/development/ad-fs-risk-assessment-model.md) 
- **ESL improvements** - Improves on the ESL QFE in 2016 by adding the following capabilities
    - Enables customers to be in audit mode while being protected by 'classic' extranet lockout functionality available since ADFS 2012R2. Currently 2016 customers would have no protection while in audit mode. 
    - Enables independent lockout threshold for familiar locations. This makes it possible for multiple instances of apps running with a common service account to roll over passwords with the least amount of impact. 

### <a name="additional-security-improvements"></a>Additional security improvements
The following additional security improvements are available in AD FS 2019:
- **Remote PSH using SmartCard Login** - Customers can now use smartcards to remote connect to ADFS via PSH and use that to manage all PSH functions include multi-node PSH cmdlets.
- **HTTP Header customization** - Customers can now customize HTTP headers emitted during ADFS responses. This includes the following headers
     - HSTS: This conveys that ADFS endpoints can only be used on HTTPS endpoints for a compliant browser to enforce
     - x-Frame-Options: ermöglicht ADFS-Administratoren das Einbetten von iframes für interaktive ADFS-Anmelde Seiten. Dies sollte nur mit Sorgfalt und nur auf HTTPS-Hosts verwendet werden. 
     - Zukünftiger Header: weitere zukünftige Header können ebenfalls konfiguriert werden. 

Weitere Informationen finden Sie [unter Anpassen von http-Sicherheits Antwort Headern mit AD FS 2019](../../ad-fs/operations/customize-http-security-headers-ad-fs.md) 

### <a name="authenticationpolicy-capabilities"></a>Authentifizierungs-/Richtlinienfunktionen
Die folgenden Authentifizierungs-/Richtlinienfunktionen sind in AD FS 2019:
- Authentifizierungs **Methode für zusätzliche Authentifizierung pro RP angeben** : Kunden können jetzt Anspruchs Regeln verwenden, um zu entscheiden, welcher zusätzliche Authentifizierungs Anbieter für zusätzlichen Authentifizierungs Anbieter aufgerufen werden soll. Dies ist für zwei Anwendungsfälle nützlich.
    - Kunden wechseln von einem zusätzlichen Authentifizierungs Anbieter zu einem anderen. Auf diese Weise können Benutzer, die Benutzer in einen neueren Authentifizierungs Anbieter integrieren, Gruppen verwenden, um zu steuern, welcher zusätzliche Authentifizierungs Anbieter aufgerufen wird.
    - Kunden müssen für bestimmte Anwendungen einen bestimmten zusätzlichen Authentifizierungs Anbieter (z. b. ein Zertifikat) benötigen. 
- **Beschränken Sie die TLS-basierte Geräte Authentifizierung nur auf Anwendungen, für die Sie erforderlich** ist: Kunden können jetzt Client-TLS-basierte Geräte Authentifizierungen auf Anwendungen beschränken, die gerätebasierten bedingten Zugriff ausführen. Dadurch werden unerwünschte Eingabe Aufforderungen an Geräte Authentifizierung (oder Fehler, wenn die Client Anwendung nicht verarbeiten kann) für Anwendungen verhindert, die keine TLS-basierte Geräte Authentifizierung erfordern.
- **Unterstützung für die MFA** -Aktualität: AD FS unterstützt jetzt die Möglichkeit, zweistufige Anmelde Informationen auf der Grundlage der Aktualität der 2. Factor Anmelde Informationen wieder zu verwenden. Dadurch können Kunden eine anfängliche Transaktion mit zwei Faktoren ausführen und nur in regelmäßigen Abständen den zweiten Faktor anfordern. Dies ist nur für Anwendungen verfügbar, die einen zusätzlichen Parameter in der Anforderung bereitstellen können und in AD FS keine konfigurierbare Einstellung ist. Dieser Parameter wird von Azure Ad unterstützt, wenn "MFA für X Tage speichern" konfiguriert ist und das Flag "supportsmfa" in den Vertrauens Einstellungen der Verbund Domäne in Azure AD auf "true" festgelegt ist. 

### <a name="sign-in-sso-improvements"></a>Verbesserungen bei der SSO-Anmeldung
Die folgenden Verbesserungen bei der SSO-Anmeldung wurden in AD FS 2019 vorgenommen:

- [Paginierte UX mit zentriertem](../operations/AD-FS-paginated-sign-in.md) Design: ADFS wurde nun in einen paginierten UX-Flow verlagert, der es AD FS ermöglicht, eine optimierte Anmelde Erfahrung zu gewährleisten. ADFS verwendet jetzt eine zentrierte Benutzeroberfläche (anstelle der rechten Seite des Bildschirms). Möglicherweise benötigen Sie neuere Logo-und Hintergrundbilder, um sich an dieser Erfahrung anzupassen. Dadurch wird auch die in Azure AD angebotene Funktionalität widerspiegeln.
- Programm **Fehlerbehebung: persistentes SSO-Status für Win10-Geräte bei der PRT** -Authentifizierung.   Dadurch wird ein Problem behoben, bei dem der MFA-Status bei Verwendung der PRT-Authentifizierung für Windows 10-Geräte nicht beibehalten wurde. Das Ergebnis dieses Problems war, dass Endbenutzer häufig zur Eingabe von 2. Factor Anmelde Informationen (MFA) aufgefordert werden. Durch die Behebung ist die Leistung auch dann konsistent, wenn die Geräte Authentifizierung über Client TLS und über den PRT-Mechanismus erfolgreich durchgeführt wurde. 


### <a name="suppport-for-building-modern-line-of-business-apps"></a>Suppport zum Entwickeln moderner Branchen-apps
Die folgende Unterstützung für das Entwickeln von modernen Lob-Apps wurde AD FS 2019 hinzugefügt:

 - **OAuth-Geräte Fluss/-Profil** -AD FS unterstützt jetzt das OAuth-Geräte Fluss Profil zum Ausführen von Anmeldungen auf Geräten, die nicht über eine Oberfläche für die Benutzeroberfläche verfügen. Dadurch kann der Benutzer die Anmeldung auf einem anderen Gerät durchführen. Diese Funktion ist für die Azure CLI-Funktionalität in Azure Stack erforderlich und kann in anderen Fällen verwendet werden. 
 - Beim **Entfernen des "Resource"-Parameters** -AD FS wurde nun die Anforderung zum Angeben eines Ressourcen Parameters, der mit den aktuellen OAuth-Spezifikationen übereinstimmt, entfernt. Clients können nun den Bezeichner für die Vertrauensstellung der vertrauenden Seite zusätzlich zu den angeforderten Berechtigungen als Bereichs Parameter bereitstellen. 
 - **Cors-Header in AD FS Antworten** : Kunden können jetzt einseitige Anwendungen erstellen, mit denen Client seitige js-Bibliotheken die Signatur der id_token validieren können, indem Sie die Signatur Schlüssel aus dem oidc Discovery-Dokument auf AD FS Abfragen. 
 - **Pkce-Unterstützung** : AD FS fügt pkce-Unterstützung hinzu, um einen sicheren Authentifizierungscode Fluss innerhalb von OAuth bereitzustellen. Dadurch wird diesem Flow eine zusätzliche Sicherheitsebene hinzugefügt, um zu verhindern, dass der Code von einem anderen Client wiedergegeben wird. 
 - Programm **Fehlerbehebung: Send x5t und Kid Claim:** Dies ist eine geringfügige Fehlerbehebung. AD FS jetzt zusätzlich den "Kid"-Anspruch an, um den Schlüssel-ID-Hinweis zum Überprüfen der Signatur anzugeben. Zuvor AD FS als Anspruch "x5t" gesendet.

### <a name="supportability-improvements"></a>Unterstützungs Verbesserungen
Die folgenden Verbesserungen der unter Stütz barkeit sind nicht Teil AD FS 2019:
- **Fehlerdetails an AD FS Administratoren senden** : erlaubt Administratoren, Endbenutzer so zu konfigurieren, dass Debugprotokolle im Zusammenhang mit einem Fehler in der Endbenutzer Authentifizierung gesendet werden, damit Sie als ZIP-Datei für eine einfache Nutzung gespeichert werden. Administratoren können auch eine SMTP-Verbindung konfigurieren, um die ZIP-Datei in einem e-Mail-selektiert-Konto zu automatisieren oder basierend auf der e-Mail-Adresse automatisch ein Ticket zu erstellen. 

### <a name="deployment-updates"></a>Bereitstellungs Updates
Die folgenden Bereitstellungs Updates sind jetzt in AD FS 2019 enthalten:
- **Farm verhaltensstufe 2019** : wie bei AD FS 2016 gibt es eine neue Version der Farm Verhaltensebene, die erforderlich ist, um neue Funktionen zu aktivieren, die oben erläutert werden. Dies ermöglicht Folgendes:
    - 2012 R2-> 2019
    - 2016-> 2019   

### <a name="saml-updates"></a>SAML-Updates
Das folgende SAML-Update befindet sich in AD FS 2019:
- Programm **Fehlerbehebung: Beheben von Fehlern im aggregierten Verbund:** es gibt zahlreiche Fehlerbehebungen für die aggregierte Verbund Unterstützung (z. b. "InCommon"). Die Fehlerbehebungen liegen in etwa wie folgt: 
  - Verbesserte Skalierung für große Anzahl von Entitäten im aggregierten Verbund Metadaten-Dokument. zuvor konnte der Fehler "ADMIN0017" auftreten. 
  - Abfragen mithilfe des Parameters "scopegroupid" über das Get-adfsrelyingpartytrustsgroup PSH-Cmdlet. 
  - Behandeln von Fehlerbedingungen im Zusammenhang mit doppelter EntityID


### <a name="azure-ad-style-resource-specification-in-scope-parameter"></a>Azure AD-Stil Ressourcen Spezifikation im scope-Parameter 
Zuvor mussten AD FS, dass die gewünschte Ressource und der gewünschte Bereich in einer beliebigen Authentifizierungsanforderung in einem separaten Parameter vorhanden waren. Beispielsweise sieht eine typische OAuth-Anforderung wie folgt aus: 7 **https:&#47;&#47;FS.contoso.com/ADFS/oauth2/Authorize?</br>response_type = Code & client_id = claimsxrayclient & Resource = urn: Microsoft:</br>ADFS: claimsxray & Scope = OAuth & redirect_uri = https:&#47;&#47;adfshelp.Microsoft.com/</br> claimsxray/tokenresponse & prompt = Login**
 
Mit AD FS auf Server 2019 können Sie nun den Ressourcen Wert übergeben, der in den Scope-Parameter eingebettet ist. Dies entspricht der Art und Weise, wie eine Authentifizierung gegen Azure AD durchführen kann. 

Der Bereichs Parameter kann nun als durch Leerzeichen getrennte Liste organisiert werden, wobei jeder Eintrag als Ressource/Bereich strukturiert ist. 

> [!NOTE]
> In der Authentifizierungsanforderung kann nur eine Ressource angegeben werden. Wenn in der Anforderung mehr als eine Ressource enthalten ist, gibt AD FS einen Fehler zurück, und die Authentifizierung kann nicht erfolgreich ausgeführt werden. 

### <a name="proof-key-for-code-exchange-pkce-support-for-oauth"></a>Prüfpunkt für die Unterstützung von Code Austausch vorschlüsseln (pkce) für OAuth 
Öffentliche OAuth-Clients, die die Autorisierungs Code Gewährung verwenden, sind anfällig für den Abfang der Autorisierungs Code.  Der Angriff ist in RFC 7636 gut beschrieben. Um diesen Angriff zu entschärfen, unterstützt AD FS in Server 2019 den Prüfschlüssel für Code Austausch (pkce) für den OAuth-Autorisierungs Code Grant-Flow. 
 
Um die pkce-Unterstützung zu nutzen, fügt diese Spezifikation den OAuth 2,0-Autorisierungs-und Zugriffs Token-Anforderungen zusätzliche Parameter hinzu.

![Proof Key](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/adfs2019.png)

A. Der Client erstellt und zeichnet einen geheimen Schlüssel mit dem Namen "code_verifier" auf und leitet eine transformierte Version "t (code_verifier)" (als "code_challenge" bezeichnet) ab, die zusammen mit der Transformations Methode "T_M" in der Autorisierungs Anforderung von OAuth 2,0 gesendet wird. 

B. Der Autorisierungs Endpunkt antwortet wie üblich, zeichnet jedoch "t (code_verifier)" und die Transformations Methode auf. 

C. Der Client sendet dann den Autorisierungs Code in der zugriffstokenanforderung wie gewohnt, aber schließt den "code_verifier"-Schlüssel ein, der unter (A) generiert wird. 

D. Der AD FS transformiert "code_verifier" und vergleicht ihn mit "t (code_verifier)" von (B).  Der Zugriff wird verweigert, wenn Sie nicht gleich sind. 

#### <a name="faq"></a>Häufig gestellte Fragen 
**F.** Kann ich den Ressourcen Wert als Teil des Bereichs Werts übergeben, wie z. b. wie Anforderungen gegen Azure AD durchgeführt werden? 
</br>**A.** Mit AD FS auf Server 2019 können Sie nun den Ressourcen Wert übergeben, der in den Scope-Parameter eingebettet ist. Der Bereichs Parameter kann nun als durch Leerzeichen getrennte Liste organisiert werden, wobei jeder Eintrag als Ressource/Bereich strukturiert ist. Beispiel:  
**< eine gültige Beispiel Anforderung erstellen >**

**F.** Unterstützt AD FS die pkce-Erweiterung?
</br>**A.** AD FS in Server 2019 unterstützt den Prüfschlüssel für Code Austausch (pkce) für den OAuth-Autorisierungs Code Grant-Flow. 

## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Neuerungen in Active Directory-Verbunddienste (AD FS) für Windows Server 2016   
Informationen zu früheren Versionen von AD FS finden Sie in den folgenden Artikeln:  
 [AD FS in Windows Server 2012 oder 2012 R2](https://technet.microsoft.com/library/hh831502.aspx) und [AD FS 2,0](https://technet.microsoft.com/library/adfs2.aspx)  

 Active Directory-Verbunddienste (AD FS) bietet Zugriffs Steuerung und einmaliges Anmelden für eine Vielzahl von Anwendungen, darunter Office 365, cloudbasierte SaaS-Anwendungen und Anwendungen im Unternehmensnetzwerk.  
* Für die IT-Organisation können Sie die Anmeldung und die Zugriffs Steuerung sowohl für moderne als auch für ältere Anwendungen, lokal und in der Cloud, basierend auf demselben Satz von Anmelde Informationen und Richtlinien bereitstellen.    
* Für den Benutzer bietet er eine nahtlose Anmeldung mit denselben, vertrauten Anmelde Informationen für das Konto.  
* Für den Entwickler bietet es eine einfache Möglichkeit zum Authentifizieren von Benutzern, deren Identitäten im Organisations Verzeichnis Leben, sodass Sie sich auf Ihre Anwendung konzentrieren können, nicht auf die Authentifizierung oder Identität.  

In diesem Artikel wird beschrieben, was in AD FS in Windows Server 2016 (AD FS 2016) neu ist.  

## <a name="eliminate-passwords-from-the-extranet"></a>Entfernen von Kenn Wörtern aus dem Extranet  
In AD FS 2016 werden drei neue Optionen für die Anmeldung ohne Kenn Wörter aktiviert, sodass Organisationen das Risiko einer Netzwerk Gefährdung durch phierte, kompromittierte oder gestohlene Kenn Wörter vermeiden können. 

### <a name="sign-in-with-azure-multi-factor-authentication"></a>Anmelden mit Azure Multi-Factor Authentication
AD FS 2016 basiert auf den MFA-Funktionen (Multi-Factor Authentication) der AD FS in Windows Server 2012 R2, indem die Anmeldung nur mit einem Azure MFA-Code zugelassen wird, ohne zuvor einen Benutzernamen und ein Kennwort einzugeben.

* Mit Azure MFA als primäre Authentifizierungsmethode wird der Benutzer zur Eingabe des Benutzernamens und des OTP-Codes in der Azure Authenticator-App aufgefordert.  
* Mit Azure MFA als sekundäre oder zusätzliche Authentifizierungsmethode stellt der Benutzer primäre Anmelde Informationen für die Authentifizierung bereit (unter Verwendung der integrierten Windows-Authentifizierung, Benutzername und Kennwort, Smartcard oder Benutzer-oder Gerätezertifikat) und dann eine Eingabeaufforderung für Text. Stimme oder OTP-basierter Azure MFA-Anmelde Name.  
* Mit dem neuen integrierten Azure MFA-Adapter war das Einrichten und Konfigurieren von Azure MFA mit AD FS nie einfacher.
* Organisationen können Azure MFA nutzen, ohne dass ein lokaler Azure MFA-Server erforderlich ist.
* Azure MFA kann für Intranet oder Extranet oder als Teil einer Zugriffs Steuerungs Richtlinie konfiguriert werden.

Weitere Informationen zu Azure MFA mit AD FS
*  [Konfigurieren von AD FS 2016 und Azure MFA](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-and-azure-mfa)  

### <a name="password-less-access-from-compliant-devices"></a>Zugriff ohne Kennwort von kompatiblen Geräten
AD FS 2016 baut auf früheren Geräte Registrierungsfunktionen auf, um die Anmeldung und Zugriffs Steuerung basierend auf dem Geräte Konformitäts Status zu aktivieren. Benutzer können sich mit den Geräte Anmelde Informationen anmelden, und die Konformität wird erneut ausgewertet, wenn sich die Geräte Attribute ändern, sodass Sie jederzeit sicherstellen können, dass Richtlinien erzwungen werden.  Dies ermöglicht Richtlinien wie

* Zugriff nur auf verwalteten und/oder kompatiblen Geräten aktivieren  
* Aktivieren Sie den Extranetzugriff nur von verwalteten und/oder kompatiblen Geräten.  
* Multi-Factor Authentication für nicht verwaltete oder nicht kompatible Computer erforderlich  

AD FS bietet die lokale Komponente der Richtlinien für den bedingten Zugriff in einem Hybrid Szenario. Wenn Sie Geräte mit Azure AD für den bedingten Zugriff auf cloudressourcen registrieren, kann die Geräte Identität auch für AD FS Richtlinien verwendet werden.

![Neuerungen](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/ADFS_ITPRO4.png)  

 Weitere Informationen zur Verwendung des gerätebasierten bedingten Zugriffs in der Cloud   
 *  [Bedingter Zugriff mit Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access/)

Weitere Informationen zur Verwendung des gerätebasierten bedingten Zugriffs mit AD FS
*  [Planen des gerätebasierten bedingten Zugriffs mit AD FS](../../ad-fs/deployment/Plan-Device-based-Conditional-Access-on-Premises.md)  
* [Access Control Richtlinien in AD FS](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="sign-in-with-windows-hello-for-business"></a>Mit Windows Hello for Business anmelden  

> [!NOTE]
> Zurzeit werden Google Chrome und das [neue Microsoft Edge](https://www.microsoft.com/edge?form=MB110A&OCID=MB110A) -Paket, das auf den Chroms Open Source-Projekt Browsern basiert, nicht für browserbasiertes einmaliges Anmelden (Single Sign on, SSO) mit Microsoft Windows Hello for Business unterstützt. Verwenden Sie Internet Explorer oder eine ältere Version von Microsoft Edge.  

Windows 10-Geräte stellen Windows Hello und Windows Hello for Business vor und ersetzen Benutzer Kennwörter durch starke Geräte gebundene Benutzer Anmelde Informationen, die durch die Geste eines Benutzers geschützt sind (eine PIN, eine biometrische Geste wie Fingerabdruck oder Gesichtserkennung). AD FS 2016 unterstützt diese neuen Windows 10-Funktionen, damit Benutzer sich über das Intranet oder das Extranet bei AD FS Anwendungen anmelden können, ohne dass ein Kennwort bereitgestellt werden muss.

Weitere Informationen zur Verwendung von Microsoft Windows Hello for Business in Ihrer Organisation
*  [Aktivieren von Windows Hello for Business in Ihrer Organisation](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)

## <a name="secure-access-to-applications"></a>Sicherer Zugriff auf Anwendungen

### <a name="modern-authentication"></a>Moderne Authentifizierung
AD FS 2016 unterstützt die neuesten modernen Protokolle, die eine bessere Benutzer Leistung für Windows 10 sowie die neuesten IOS-und Android-Geräte und-Apps bieten.  

Weitere Informationen finden Sie unter [AD FS Szenarien für Entwickler](../../ad-fs/overview/ad-fs-openid-connect-oauth-flows-scenarios.md) .  


### <a name="configure-access-control-policies-without-having-to-know-claim-rules-language"></a>Konfigurieren von Richtlinien für die Zugriffs Steuerung ohne Kenntnis der Anspruchs Regel Sprache  
Zuvor mussten AD FS Administratoren Richtlinien mithilfe der AD FS Anspruchs Regel Sprache konfigurieren, sodass das Konfigurieren und Verwalten von Richtlinien erschwert wird. Mit Zugriffs Steuerungs Richtlinien können Administratoren integrierte Vorlagen verwenden, um allgemeine Richtlinien anzuwenden, z. b.
* Nur Intranetzugriff zulassen
* Alle zulassen und MFA vom Extranet verlangen
* Alle zulassen und MFA von einer bestimmten Gruppe verlangen

Die Vorlagen können mithilfe eines Assistenten gestützten Prozesses leicht angepasst werden, um Ausnahmen oder zusätzliche Richtlinien Regeln hinzuzufügen, und können auf eine oder mehrere Anwendungen angewendet werden, um eine konsistente Richtlinien Erzwingung zu erreichen.

Weitere Informationen finden Sie [unter Richtlinien für die Zugriffs Steuerung in AD FS.](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="enable-sign-on-with-non-ad-ldap-directories"></a>Aktivieren der Anmeldung mit nicht-AD-LDAP-Verzeichnissen  
Viele Organisationen verfügen über eine Kombination aus Active Directory und Verzeichnissen von Drittanbietern. Durch das Hinzufügen AD FS Unterstützung für die Authentifizierung von Benutzern, die in LDAP-kompatiblen Verzeichnissen gespeichert sind, kann AD FS jetzt für Folgendes verwendet werden:
* Benutzer in Drittanbietern, LDAP V3-kompatible Verzeichnisse
* Benutzer in Active Directory Gesamtstrukturen, für die eine Active Directory bidirektionale Vertrauensstellung nicht konfiguriert ist
* Benutzer in Active Directory Lightweight Directory Services (AD LDS)

Weitere Informationen finden [Sie unter Konfigurieren von AD FS zum Authentifizieren von Benutzern, die in LDAP-Verzeichnissen gespeichert sind.](../../ad-fs/operations/Configure-AD-FS-to-authenticate-users-stored-in-LDAP-directories.md)  

## <a name="better-sign-in-experience"></a>Bessere Anmelde Leistung
### <a name="customize-sign-in-experience-for-ad-fs-applications"></a>Anpassen der Anmelde Funktion für AD FS-Anwendungen  
Wir haben von Ihnen gehört, dass die Möglichkeit zum Anpassen der Anmelde Freundlichkeit für jede Anwendung eine gute Verbesserung der Benutzerfreundlichkeit ist, insbesondere für Organisationen, die sich für Anwendungen anmelden, die mehrere Unternehmen oder Marken darstellen.  

Previously, AD FS in Windows Server 2012 R2 provided a common sign on experience for all relying party applications, with the ability to customize a subset of text based content per application. With Windows Server 2016, you can customize not only the messages, but images, logo and web theme per application. Additionally, you can create new, custom web themes and apply these per relying party.  

For more information see [AD FS user sign-in customization.](../../ad-fs/operations/AD-FS-user-sign-in-customization.md)  



## <a name="manageability-and-operational-enhancements"></a>Manageability and Operational Enhancements  
The following section describes the improved operational scenarios that are introduced with Active Directory Federation Services in Windows Server 2016.  

### <a name="streamlined-auditing-for-easier-administrative-management"></a>Streamlined auditing for easier administrative management  
In AD FS for Windows Server 2012 R2 there were numerous audit events generated for a single request and the relevant information about a log-in or token issuance activity is either absent (in some versions of AD FS) or spread across multiple audit events. By default the AD FS audit events are turned off due to their verbose nature.  
With the release of AD FS 2016, auditing has become more streamlined and less verbose.  

For more information see [Auditing enhancements to AD FS in Windows Server 2016.](../../ad-fs/technical-reference/auditing-enhancements-to-ad-fs-in-windows-server.md)  

### <a name="improved-interoperability-with-saml-20-for-participation-in-confederations"></a>Improved interoperability with SAML 2.0 for participation in confederations  
AD FS 2016 contains additional SAML protocol support, including support for importing trusts based on metadata that contains multiple entities. This enables you to configure AD FS to participate in confederations such as InCommon Federation and other implementations conforming to the eGov 2.0 standard.  

For more information see [Improved interoperability with SAML 2.0.](../../ad-fs/operations/Improved-interoperability-with-SAML-2.0.md)  

### <a name="simplified-password-management-for-federated-o365-users"></a>Simplified password management for federated O365 users  
You can configure Active Directory Federation Services (AD FS) to send password expiry claims to the relying party trusts (applications) that are protected by AD FS. How these claims are used depends on the application. For example, with Office 365 as your relying party, updates have been implemented to Exchange and Outlook to notify federated users of their soon-to-be-expired passwords.  

For more information see [Configure AD FS to send password expiry claims.](../../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md)  

### <a name="moving-from-ad-fs-in-windows-server-2012-r2-to-ad-fs-in-windows-server-2016-is-easier"></a>Moving from AD FS in Windows Server 2012 R2 to AD FS in Windows Server 2016 is easier  
Previously, migrating to a new version of AD FS required exporting configuration from the old farm and importing to a brand new, parallel farm.  

Now, moving from AD FS on Windows Server 2012 R2 to AD FS on Windows Server 2016 has become much easier. Simply add a new Windows Server 2016 server to a Windows Server 2012 R2 farm, and the farm will act at the Windows Server 2012 R2 farm behavior level, so it looks and behaves just like a Windows Server 2012 R2 farm.  

Then, add new Windows Server 2016 servers to the farm, verify the functionality and remove the older servers from the load balancer. Once all farm nodes are running Windows Server 2016, you are ready to upgrade the farm behavior level to 2016 and begin using the new features.  

For more information see [Upgrading to AD FS in Windows Server 2016.](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)  
