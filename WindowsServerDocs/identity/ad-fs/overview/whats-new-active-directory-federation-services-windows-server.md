---
ms.assetid: aa892a85-f95a-4bf1-acbb-e3c36ef02b0d
title: Neuerungen in Active Directory-Verbunddienste für Windows Server 2016
description: ''
author: billmath
ms.author: billmath
manager: daveba
ms.date: 04/23/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6294c7b6ead0a9fa338f8b2cc8134b750f7e3e8f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385549"
---
# <a name="whats-new-in-active-directory-federation-services"></a>Neues in Active Directory-Verbunddienste (AD FS)


## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2019"></a>Neues in Active Directory-Verbunddienste (AD FS) für Windows Server 2019

### <a name="protected-logins"></a>Geschützte Anmeldungen
Im folgenden finden Sie eine kurze Zusammenfassung der Änderungen an geschützten Anmeldungen, die in AD FS 2019 verfügbar sind:
- **Externe Authentifizierungs Anbieter als primäre** Kunden können jetzt Authentifizierungs Produkte von Drittanbietern als ersten Faktor verwenden und Kenn Wörter nicht als ersten Faktor verfügbar machen. In Fällen, in denen ein externer Authentifizierungs Anbieter zwei Faktoren belegen kann, kann er MFA beanspruchen. 
- Kenn **Wort Authentifizierung als zusätzliche Authentifizierung** : Kunden verfügen über eine vollständig unterstützte Eingangsbox Option, um das Kennwort nur für den zusätzlichen Faktor zu verwenden, wenn die Option "Kennwort weniger" als erster Faktor Dies verbessert die Kundenfreundlichkeit von ADFS 2016, bei der Kunden einen GitHub-Adapter herunterladen mussten, der unverändert unterstützt wird. 
- **Austauschbares Risiko Bewertungs Modul** : Kunden können jetzt eigene Plug-in-Module erstellen, um bestimmte Anforderungs Typen während der Vorauthentifizierung zu blockieren. Dies erleichtert es Kunden, Cloud Intelligence wie z. b. Identity Protection zum Blockieren von Anmeldungen für riskante Benutzer oder riskante Transaktionen zu verwenden.  Weitere Informationen finden Sie [unter Erstellen von Plug-ins mit AD FS 2019-Risiko Bewertungsmodell](../../ad-fs/development/ad-fs-risk-assessment-model.md) . 
- **ESL-Verbesserungen** : verbessert die ESL-QFE in 2016 durch Hinzufügen der folgenden Funktionen:
    - Ermöglicht es Kunden, sich im Überwachungsmodus zu befinden, während Sie durch die "klassische" extranetsperrungsfunktionalität geschützt sind, die seit ADFS 2012r2 verfügbar ist Derzeit haben 2016 Kunden keinen Schutz im Überwachungsmodus. 
    - Aktiviert einen unabhängigen Sperr Schwellenwert für vertraute Standorte. Dies ermöglicht es, dass mehrere Instanzen von apps, die mit einem gemeinsamen Dienst Konto ausgeführt werden, ein Rollback für Kenn Wörter mit den geringsten Auswirkungen ausführen können. 

### <a name="additional-security-improvements"></a>Zusätzliche Sicherheitsverbesserungen
Die folgenden zusätzlichen Sicherheitsverbesserungen sind in AD FS 2019 verfügbar:
- **Remote-PSH mithilfe der Smartcard-Anmeldung** : Kunden können nun mithilfe von Smartcards per PSH eine Remote Verbindung mit AD FS herstellen und diese zum Verwalten aller PSH-Funktionen verwenden, die PSH-Cmdlets mit mehreren Knoten enthalten.
- **Http-Header Anpassung** : Kunden können nun HTTP-Header anpassen, die während der ADFS-Antworten ausgegeben werden. Dies schließt die folgenden Header ein.
     - HSTS Dies stellt dar, dass ADFS-Endpunkte nur für HTTPS-Endpunkte verwendet werden können, damit ein kompatibler Browser
     - x-Frame-Optionen: Ermöglicht ADFS-Administratoren das Einbetten von iframes für interaktive ADFS-Anmelde Seiten. Dies sollte nur mit Sorgfalt und nur auf HTTPS-Hosts verwendet werden. 
     - Zukünftiger Header: Weitere zukünftige Header können ebenfalls konfiguriert werden. 

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
- **bug Fix: Persistenter SSO-Status für Win10-Geräte bei der PRT-Authentifizierung @ no__t-0: Dies ist ein Problem, bei dem der MFA-Status bei Verwendung der PRT-Authentifizierung für Windows 10-Geräte nicht beibehalten wurde. Das Ergebnis dieses Problems war, dass Endbenutzer häufig zur Eingabe von 2. Factor Anmelde Informationen (MFA) aufgefordert werden. Durch die Behebung ist die Leistung auch dann konsistent, wenn die Geräte Authentifizierung über Client TLS und über den PRT-Mechanismus erfolgreich durchgeführt wurde. 


### <a name="suppport-for-building-modern-line-of-business-apps"></a>Suppport zum Entwickeln moderner Branchen-apps
Die folgende Unterstützung für das Entwickeln von modernen Lob-Apps wurde AD FS 2019 hinzugefügt:

 - **OAuth-Geräte Fluss/-Profil** -AD FS unterstützt jetzt das OAuth-Geräte Fluss Profil zum Ausführen von Anmeldungen auf Geräten, die nicht über eine Oberfläche für die Benutzeroberfläche verfügen. Dadurch kann der Benutzer die Anmeldung auf einem anderen Gerät durchführen. Diese Funktion ist für die Azure CLI-Funktionalität in Azure Stack erforderlich und kann in anderen Fällen verwendet werden. 
 - Beim **Entfernen des "Resource"-Parameters** -AD FS wurde nun die Anforderung zum Angeben eines Ressourcen Parameters, der mit den aktuellen OAuth-Spezifikationen übereinstimmt, entfernt. Clients können nun den Bezeichner für die Vertrauensstellung der vertrauenden Seite zusätzlich zu den angeforderten Berechtigungen als Bereichs Parameter bereitstellen. 
 - **Cors-Header in AD FS Antworten** : Kunden können nun einseitige Anwendungen erstellen, mit denen Client seitige js-Bibliotheken die Signatur der ID validieren können, indem Sie die Signatur Schlüssel aus dem oidc Discovery-Dokument auf AD FS Abfragen. 
 - **Pkce-Unterstützung** : AD FS fügt pkce-Unterstützung hinzu, um einen sicheren Authentifizierungscode Fluss innerhalb von OAuth bereitzustellen. Dadurch wird diesem Flow eine zusätzliche Sicherheitsebene hinzugefügt, um zu verhindern, dass der Code von einem anderen Client wiedergegeben wird. 
 - **bug Fix: Send x5t und Kid Claim @ no__t-0: Dies ist eine kleine Fehlerbehebung. AD FS jetzt zusätzlich den "Kid"-Anspruch an, um den Schlüssel-ID-Hinweis zum Überprüfen der Signatur anzugeben. Zuvor AD FS als Anspruch "x5t" gesendet.

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
- **bug Fix: Beheben von Fehlern im aggregierten Verbund @ no__t-0: Es gibt zahlreiche Fehlerbehebungen für die aggregierte Verbund Unterstützung (z. b. "InCommon"). Die Fehlerbehebungen liegen in etwa wie folgt: 
  - Verbesserte Skalierung für große Anzahl von Entitäten im aggregierten Verbund Metadaten-Dokument. Zuvor hat dies den Fehler "ADMIN0017" verursacht. 
  - Abfragen mithilfe des Parameters "scopegroupid" über das Get-adfsrelyingpartytrustsgroup PSH-Cmdlet. 
  - Behandeln von Fehlerbedingungen im Zusammenhang mit doppelter EntityID


### <a name="azure-ad-style-resource-specification-in-scope-parameter"></a>Azure AD-Stil Ressourcen Spezifikation im scope-Parameter 
Zuvor mussten AD FS, dass die gewünschte Ressource und der gewünschte Bereich in einer beliebigen Authentifizierungsanforderung in einem separaten Parameter vorhanden waren. Beispielsweise sieht eine typische OAuth-Anforderung wie folgt aus: 7 **https:&#47;&#47;FS.contoso.com/ADFS/oauth2/Authorize? </br>response_type = Code & client_id = claimsxrayclient & Resource = urn: Microsoft: </br>adfs: claimsxray & Scope = OAuth & redirect_uri = https:&#47; &#47; adfshelp.Microsoft.com/</br> claimsxray/tokenresponse & prompt = Login**
 
Mit AD FS auf Server 2019 können Sie nun den Ressourcen Wert übergeben, der in den Scope-Parameter eingebettet ist. Dies entspricht der Art und Weise, wie eine Authentifizierung gegen Azure AD durchführen kann. 

Der Bereichs Parameter kann nun als durch Leerzeichen getrennte Liste organisiert werden, wobei jeder Eintrag als Ressource/Bereich strukturiert ist. Zum Beispiel  

**< eine gültige Beispiel Anforderung erstellen >**
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

#### <a name="faq"></a>FAQ 
**Q1.** Kann ich den Ressourcen Wert als Teil des Bereichs Werts übergeben, wie z. b. wie Anforderungen gegen Azure AD durchgeführt werden? 
</br>**EIN.** Mit AD FS auf Server 2019 können Sie nun den Ressourcen Wert übergeben, der in den Scope-Parameter eingebettet ist. Der Bereichs Parameter kann nun als durch Leerzeichen getrennte Liste organisiert werden, wobei jeder Eintrag als Ressource/Bereich strukturiert ist. Zum Beispiel  
**< eine gültige Beispiel Anforderung erstellen >**

**Q1.** Unterstützt AD FS die pkce-Erweiterung?
</br>**EIN.** AD FS in Server 2019 unterstützt den Prüfschlüssel für Code Austausch (pkce) für den OAuth-Autorisierungs Code Grant-Flow. 

## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Neuerungen in Active Directory-Verbunddienste für Windows Server 2016   
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
 *  [Bedingter Zugriff Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access/)

Weitere Informationen zur Verwendung des gerätebasierten bedingten Zugriffs mit AD FS
*  [Planen des gerätebasierten bedingten Zugriffs mit AD FS](../../ad-fs/deployment/Plan-Device-based-Conditional-Access-on-Premises.md)  
* [Access Control Richtlinien in AD FS](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="sign-in-with-windows-hello-for-business"></a>Mit Windows Hello for Business anmelden   
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

Zuvor haben AD FS in Windows Server 2012 R2 eine gängige Anmelde Funktion für alle Anwendungen der vertrauenden Seite bereitgestellt, mit der Möglichkeit, eine Teilmenge textbasierter Inhalte pro Anwendung anzupassen. Mit Windows Server 2016 können Sie nicht nur die Nachrichten anpassen, sondern auch Bilder, Logos und das Webdesign pro Anwendung. Darüber hinaus können Sie neue, benutzerdefinierte Webdesigns erstellen und diese pro vertrauende Seite anwenden.  

Weitere Informationen finden Sie [unter AD FS Anpassung der Benutzeranmeldung.](../../ad-fs/operations/AD-FS-user-sign-in-customization.md)  



## <a name="manageability-and-operational-enhancements"></a>Verwaltbarkeit und betriebliche Erweiterungen  
Im folgenden Abschnitt werden die verbesserten Betriebs Szenarios beschrieben, die mit Active Directory-Verbunddienste (AD FS) in Windows Server 2016 eingeführt werden.  

### <a name="streamlined-auditing-for-easier-administrative-management"></a>Optimierte Überwachung für eine einfachere verwaltungsverwaltung  
In AD FS für Windows Server 2012 R2 gab es zahlreiche Überwachungs Ereignisse, die für eine einzelne Anforderung generiert wurden, und die relevanten Informationen zu einer Anmelde-oder tokenausstellungsaktivität sind entweder nicht vorhanden (in einigen Versionen von AD FS) oder auf mehrere Überwachungs Ereignisse verteilt. Standardmäßig sind die AD FS Überwachungs Ereignisse aufgrund ihrer ausführlichen Art deaktiviert.  
Mit der Veröffentlichung von AD FS 2016 wird die Überwachung optimiert und ist weniger ausführlich.  

Weitere Informationen finden Sie unter Überwachen von [Verbesserungen bei der AD FS in Windows Server 2016.](../../ad-fs/technical-reference/auditing-enhancements-to-ad-fs-in-windows-server.md)  

### <a name="improved-interoperability-with-saml-20-for-participation-in-confederations"></a>Verbesserte Interoperabilität mit SAML 2,0 für die Teilnahme an Verbund Verbund  
AD FS 2016 enthält zusätzliche SAML-Protokoll Unterstützung, einschließlich der Unterstützung für den Import von Vertrauens Stellungen basierend auf Metadaten, die mehrere Entitäten enthalten. Dies ermöglicht es Ihnen, AD FS für die Teilnahme an Verbund-, wie z. b. einem gemeinsamen Verbund und anderen Implementierungen zu konfigurieren, die mit dem eGov 2,0-Standard  

Weitere Informationen finden Sie [unter verbesserte Interoperabilität mit SAML 2,0.](../../ad-fs/operations/Improved-interoperability-with-SAML-2.0.md)  

### <a name="simplified-password-management-for-federated-o365-users"></a>Vereinfachte Kenn Wort Verwaltung für Verbund O365 Benutzer  
Sie können Active Directory-Verbunddienste (AD FS) (AD FS) konfigurieren, um Kenn Wort Ablauf Ansprüche an die Vertrauens Stellungen der vertrauenden Seite (Anwendungen) zu senden, die durch AD FS geschützt sind. Wie diese Ansprüche verwendet werden, hängt von der Anwendung ab. Beispielsweise wurden mit Office 365 als vertrauende Seite Updates in Exchange und Outlook implementiert, damit Verbund Benutzer über Ihre bald abgelaufenen Kenn Wörter benachrichtigt werden.  

Weitere Informationen finden [Sie unter Konfigurieren von AD FS zum Senden von Kenn Wort Ablauf Ansprüchen.](../../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md)  

### <a name="moving-from-ad-fs-in-windows-server-2012-r2-to-ad-fs-in-windows-server-2016-is-easier"></a>Die Umstellung von AD FS in Windows Server 2012 R2 auf AD FS in Windows Server 2016 ist einfacher.  
Bisher erforderte die Migration zu einer neuen Version von AD FS das Exportieren der Konfiguration aus der alten Farm und das Importieren in eine ganz neue, parallele Farm.  

Die Umstellung von AD FS auf Windows Server 2012 R2 auf AD FS unter Windows Server 2016 ist nun viel einfacher geworden. Fügen Sie einfach einen neuen Windows Server 2016-Server zu einer Windows Server 2012 R2-Farm hinzu, und die Farm verhält sich auf der Windows Server 2012 R2-Farm Verhalten, sodass Sie genau wie eine Windows Server 2012 R2-Farm aussieht und verhält.  

Fügen Sie dann der Farm neue Windows Server 2016-Server hinzu, überprüfen Sie die Funktionalität, und entfernen Sie die älteren Server aus dem Load Balancer. Sobald alle Farm Knoten unter Windows Server 2016 ausgeführt werden, können Sie die Farm verhaltensstufe auf 2016 aktualisieren und die neuen Features verwenden.  

Weitere Informationen finden [Sie unter Aktualisieren auf AD FS in Windows Server 2016.](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)  
