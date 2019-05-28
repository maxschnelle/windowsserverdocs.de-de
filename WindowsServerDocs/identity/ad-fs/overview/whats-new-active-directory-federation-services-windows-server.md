---
ms.assetid: aa892a85-f95a-4bf1-acbb-e3c36ef02b0d
title: Neuerungen in Active Directory-Verbunddienste für Windows Server 2016
description: ''
author: billmath
ms.author: billmath
manager: daveba
ms.date: 04/23/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fbb289c16d82da79aded49e3af4134ac7f6df325
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188698"
---
# <a name="whats-new-in-active-directory-federation-services"></a>Neues in Active Directory-Verbunddienste (AD FS)


## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2019"></a>Neuerungen in Active Directory Federation Services für Windows Server 2019

### <a name="protected-logins"></a>Geschützte Anmeldungen
Im folgenden finden eine kurze Zusammenfassung der Updates für geschützte Anmeldungen, die in AD FS-2019 verfügbar:
- **Externe Authentifizierungsanbieter als primäre** -Kunden können jetzt 3. Produkte von Drittanbietern-Authentifizierung verwenden, als der erste Faktor und keine Kennwörter als der erste Faktor verfügbar. Es kann die MFA anfordern, in den Fällen, in denen ein externen Authentifizierungsanbieters 2 Faktoren sein kann. 
- **Kennwort-Authentifizierung als zusätzliche Authentifizierung** -Kunden haben eine vollständig unterstützte Posteingangsoption aus, um das Kennwort zu verwenden, nur für die zusätzliche nach der ein Kennwort weniger Option rechnen Sie als der erste Faktor verwendet wird. Dies verbessert die benutzerfreundlichkeit von AD FS 2016, in denen Kunden hatten, unterstützt wird, wie, einen Adapter Github herunterladen. 
- **Austauschbare Risk Assessment Modul** -Kunden können jetzt ihre eigenen-Plug-in zu blockieren, bestimmte Arten von Anforderungen während der vorauthentifizierungsphase Module erstellen. Dies erleichtert es Kunden Cloudfunktionen wie z.B. Identitätsschutz zu verwenden, um Anmeldungen für riskante Benutzer oder riskante Transaktionen blockieren.  Weitere Informationen finden Sie unter [ -Plug-ins mit AD FS 2019 Risk Assessment Modell erstellen](../../ad-fs/development/ad-fs-risk-assessment-model.md) 
- **Zusammenfassender Meldung Verbesserungen** -verbessert das QFE zusammenfassender Meldung 2016 durch die folgenden Funktionen hinzufügen
    - Ermöglicht Kunden, die im Überwachungsmodus werden, während von "klassische" extranetsperre Funktionsumfang, da AD FS 2012 R2 geschützt wird. 2016-Kunden müssen derzeit kein Schutz im Modus "Audit". 
    - Ermöglicht die unabhängige Sperrschwellenwert für vertrauten Standorte. Dadurch kann für mehrere Instanzen von apps, die mit einem allgemeinen Dienstkonto Kennwörter mit den geringstmöglichen Auswirkungen Rollover ausgeführt. 

### <a name="additional-security-improvements"></a>Weitere sicherheitsverbesserungen
Die folgenden Verbesserungen für die Erhöhung der Sicherheit sind in AD FS-2019 verfügbar:
- **Remote mit SmartCard-Anmeldung PSH** - Kunden können jetzt mit Smartcards mit Verbindung mit AD FS über PSH und verwenden Sie, dass Funktionen, um alle PSH verwalten möchten, verwenden mit mehreren Knoten PSH-Cmdlets.
- **HTTP-Header-Anpassung** -Kunden können jetzt anpassen, HTTP-Header, die während der AD FS-Antworten ausgegeben wurden. Dies umfasst die folgenden Header
     - HSTS: Dadurch vermittelt, dass AD FS-Endpunkte nur für HTTPS-Endpunkte für einen kompatiblen Browser verwendet werden können, zu erzwingen
     - x-frame-options: Ermöglicht AD FS-Administratoren können bestimmte vertrauende Seiten, iFrames für interaktive AD FS-Anmeldeseiten einzubetten. Dies sollte mit Vorsicht und nur auf Hosts für HTTPS verwendet werden. 
     - Zukünftige Header: Zusätzliche zukünftige Header können auch konfiguriert werden. 

Weitere Informationen finden Sie unter [Anpassen von HTTP-Antwort Sicherheitsheader mit AD FS-2019](../../ad-fs/operations/customize-http-security-headers-ad-fs.md) 

### <a name="authenticationpolicy-capabilities"></a>Authentifizierungsrichtlinie/Funktionen
Die folgenden Authentifizierungsrichtlinie/Funktionen sind in AD FS 2019:
- **Geben Sie die Authentifizierungsmethode für die zusätzliche Authentifizierung pro RP** -Kunden können nun die Verwendung von Regeln, um zu entscheiden, welche zusätzlicher Authentifizierungsanbieter für zusätzlicher Authentifizierungsanbieter aufgerufen Ansprüchen. Dies ist nützlich, für die 2-Anwendungsfälle
    - Kunden werden über eine zusätzliche Authentifizierung-Anbieter zum anderen übergeführt wird. Diese Weise als sie integrieren von Benutzern für eine neuere Authentication-Anbieter können Gruppen steuern verwenden die zusätzliche Authentifizierung Anbieter aufgerufen wird.
    - Kunden haben Anforderungen für einen bestimmten zusätzlicher Authentifizierungsanbieter (z. B. "Zertifikat") für bestimmte Anwendungen. 
- **Einschränken von TLS-basierten Gerät Authentifizierung nur für Anwendungen, die dies erfordern** -Kunden können jetzt clientbasierte TLS Gerät Authentifizierungen, um nur Anwendungen, in denen Geräte für den bedingten Zugriff basierend einschränken. Dadurch wird verhindert, dass unerwünschten aufforderungen für Gerät-Authentifizierung (oder Fehler, wenn die Clientanwendung nicht verarbeiten kann) für Anwendungen, die keine TLS-basierten Geräteauthentifizierung erforderlich ist.
- **Unterstützung für MFA Aktualität** -AD FS unterstützt jetzt die Möglichkeit, 2nd Factor-Anmeldeinformationen, die basierend auf die Aktualität der 2nd Factor Anmeldeinformationen erneut durchführen. Dadurch können Kunden eine anfängliche Transaktion mit 2 Faktoren und nur die Eingabeaufforderung für die 2. Stufe in regelmäßigen Abständen tun. Dies ist nur für Anwendungen, die einen zusätzlichen Parameter in der Anforderung bieten und ist nicht in AD FS eine konfigurierbare Einstellung verfügbar. Dieser Parameter wird unterstützt von Azure AD, wenn "Denken Sie daran, meine MFA für X Tage" konfiguriert sind und das "SupportsMFA"-Flag wird festgelegt, auf "true", auf die Einstellungen für die verbunddomäne-Vertrauensstellung in Azure AD. 

### <a name="sign-in-sso-improvements"></a>Verbesserungen der SSO-Anmeldung
Die folgenden Sign-in SSO in AD FS-2019 wurden Verbesserungen vorgenommen:

- [Paginiert UX mit Design zentriert](../operations/AD-FS-paginated-sign-in.md) -AD FS wurde nun zu einem paginierten UX-Flow, der AD FS, um zu überprüfen, und geben Sie eine weitere Anmeldung reibungsloseren ermöglicht. AD FS verwendet jetzt eine zentrierte Benutzeroberfläche (anstelle von der rechten Seite des Bildschirms). Sie können neuere Logo und Hintergrund Bilder an das Dank dieser Benutzeroberfläche benötigen. Dies spiegelt sich auch um Funktionen in Azure AD.
- **Fehlerbehebung: Persistente Status von SSO für Win10-Geräte, die bei der PRT-Auth** dies behebt ein Problem, in dem MFA-Status nicht beibehalten wurde, wenn PRT-Authentifizierung für Windows 10-Geräte verwenden. Das Ergebnis des Problems war, dass Endbenutzer 2nd Factor Anmeldeinformationen (MFA) für häufig aufgefordert wird. Die Lösung können Sie auch die konsistente bei der Authentifizierung des Geräts über TLS-Client und PRT-Mechanismus wurde erfolgreich ausgeführt wird. 


### <a name="suppport-for-building-modern-line-of-business-apps"></a>Unterstützung zum Erstellen moderner Branchen-apps
Die folgende Unterstützung zum Erstellen moderner Branchen-apps wurde mit AD FS-2019 hinzugefügt:

 - **OAuth Flow/Geräteprofil** -AD FS unterstützt jetzt das OAuth-Geräteprofil Flow zum Durchführen von Anmeldungen für Geräte, die nicht über eine UI-Oberfläche zur Unterstützung von umfangreichen anmeldeabläufe verfügen. Dadurch wird den Benutzer die Anmeldung auf einem anderen Gerät ausführen. Diese Funktionalität ist für die Azure-CLI-Umgebung in Azure Stack erforderlich und kann in anderen Fällen verwendet werden. 
 - **Entfernen des "Resource"-Parameters** -AD FS hat die Anforderung, die einen Ressourcenparameter angeben, d. h. unter Berücksichtigung aktuellen Oauth-Spezifikationen entfernt. Clients können nun die Relying Party Trust-ID als Bereichsparameter darüber hinaus auf die angeforderten Berechtigungen angeben. 
 - **CORS-Header in AD FS-Antworten** -Kunden können nun Single Page Applications, mit denen clientseitige JS-Bibliotheken, die Signatur des ID-Tokens überprüft durch Abfragen der Signaturschlüssel aus den OIDC-Discovery-Dokument in AD FS erstellen. 
 - **Unterstützung für PKCE** -AD FS unterstützt PKCE um eine sichere Authentifizierung Codefluss in OAuth zu ermöglichen. Dadurch wird eine zusätzliche Sicherheitsschicht hinzugefügt, um diesen Flow, um zu verhindern, dass hijacking-Code, und es auf einem anderen Client wiedergeben. 
 - **Fehlerbehebung: X5t und "Kid"-Anspruch senden** – Dies ist eine kleine Fehlerbehebung. AD FS sendet jetzt außerdem den Anspruch "Kid", um den Schlüssel-Id-Hinweis zum Überprüfen der Signatur zu kennzeichnen. Zuvor gesendeten AD FS nur dies als "x5t" Anspruch.

### <a name="supportability-improvements"></a>Verbesserungen hinsichtlich der unterstützbarkeit
Die folgenden Verbesserungen hinsichtlich der unterstützbarkeit sind nicht Teil der AD FS-2019:
- **Senden von Fehlerdetails an AD FS-Administratoren** -ermöglicht Administratoren das Konfigurieren Endbenutzer zum Senden von Debug-Protokolle, die im Zusammenhang mit der ein Fehler bei der Authentifizierung der Benutzer gespeichert werden, da zur einfachen Nutzung eines komprimierten abgelegt. Administratoren können auch eine SMTP-Verbindung mit Automail, die die ZIP-Datei in ein "Selektierung"-e-Mail-Konto oder zum automatischen Erstellen Sie ein Ticket, das basierend auf die e-Mail-Adresse konfigurieren. 

### <a name="deployment-updates"></a>Von Bereitstellungsupdates
Die folgenden Bereitstellungsupdates sind jetzt in AD FS-2019 enthalten:
- **Farm Verhalten Ebene 2019** – wie bei AD FS 2016 gibt es eine neue Farmen mit Verhaltensebene-Version, die erforderlich sind, um neue Funktionen, die weiter oben erläuterten zu aktivieren. Dadurch kann der Übergang von:
    - 2012 R2-> 2019
    - 2016 -> 2019   

### <a name="saml-updates"></a>SAML-updates
Das folgende SAML-Update ist in AD FS 2019:
- **Fehlerbehebung: Beheben von Fehlern in aggregierte Verbund** -zahlreiche Programmfehlerbehebungen, um aggregierte verbundunterstützung stattgefunden haben (z. B. InCommon). Die Korrekturen wurden für Folgendes: 
  - Verbesserte Skalierung für große Anzahl von Entitäten in der aggregierten Verbund-Metadaten-Dokument. Zuvor, würde dies mit "ADMIN0017"-Fehler fehl. 
  - Die Abfrage mit 'ScopeGroupID'-Parameter über das Cmdlet "Get-AdfsRelyingPartyTrustsGroup PSH". 
  - Behandeln von fehlerbedingungen auf doppelte entityID


### <a name="azure-ad-style-resource-specification-in-scope-parameter"></a>Azure AD-Ressource Stilspezifikation im Parameter "Scope" 
Zuvor mussten AD FS, die gewünschte Ressource und der Bereich in einen separaten Parameter in allen authentifizierungsanforderungen werden. Beispielsweise würde eine typische Oauth-Anforderung wie folgt aussehen: 7 **Https:&#47;&#47;fs.contoso.com/adfs/oauth2/authorize?</br> Response_type = Code & Client_id = Claimsxrayclient & Resource = Urn: Microsoft:</br>Adfs:claimsxray & Bereich = Oauth und umleitungs-URI = Https:&#47;&#47;adfshelp.microsoft.com/</br> ClaimsXray / TokenResponse & Prompt = Login**
 
Mit AD FS-Server 2019 können Sie jetzt in der Parameter "Scope" eingebetteten Ressourcenwert übergeben. Dies ist konsistent mit, wie eine Authentifizierung gegenüber Azure AD auch erreichen kann. 

Der Parameter "Scope" kann jetzt als eine durch Leerzeichen getrennte Liste organisiert werden, in dem jeder Eintrag Struktur als Ressourcenbereich/ist. Zum Beispiel  

**< erstellen Sie eine gültige beispielanforderung >**
> [!NOTE]
> Nur eine Ressource kann in der Authentifizierungsanforderung angegeben werden. Wenn mehr als eine Ressource in der Anforderung enthalten ist, gibt AD FS, dass ein Fehler und die Authentifizierung nicht erfolgreich ist. 

### <a name="proof-key-for-code-exchange-pkce-support-for-oauth"></a>Proof Key for Code Exchange (PKCE)-Unterstützung für oAuth 
Öffentliche OAuth-Clients verwenden die Autorisierungscodegewährung sind anfällig für den Angriff Code abfangen.  Der Angriff wird auch in RFC 7636 beschrieben. Um diesen Angriff zu entschärfen, unterstützt AD FS in Server-2019 Proof Key für Code Exchange (PKCE) für OAuth Authorization Code Grant-Flow. 
 
Um die Unterstützung für PKCE nutzen zu können, fügt dieser Spezifikation zusätzliche Parameter zum OAuth 2.0-Autorisierung und Anforderungen, die Zugriff an.

![Proofkey](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/adfs2019.png)

A. Der Client erstellt und zeichnet einen geheimen Schlüssel mit dem Namen "code_verifier""" und leitet eine transformierte Version "t(code_verifier)" (die "Code_challenge" genannt), die in der OAuth 2.0 Autorisierung anfordern zusammen mit der Transformationsmethode "T_m" gesendet wird. 

B. Der Autorisierungsendpunkt reagiert wie gewohnt jedoch Datensätze "t(code_verifier)" und der Transformationsmethode. 

C. Der Client sendet den Autorisierungscode in Access Token Request wie gewohnt dann aber enthält den ""code_verifier "" geheime Schlüssel, die auf der (A) generiert. 

D. Die AD FS transformiert ""code_verifier "" und (b) um "t(code_verifier)" verglichen.  Zugriff wird verweigert, wenn sie nicht gleich sind. 

#### <a name="faq"></a>Häufig gestellte Fragen 
**Q.** Kann ich übergeben Ressourcenwert als Teil des Bereichswerts wie wie Anforderungen für Azure AD erfolgen? 
</br>**A.** Mit AD FS-Server 2019 können Sie jetzt in der Parameter "Scope" eingebetteten Ressourcenwert übergeben. Der Parameter "Scope" kann jetzt als eine durch Leerzeichen getrennte Liste organisiert werden, in dem jeder Eintrag Struktur als Ressourcenbereich/ist. Zum Beispiel  
**< erstellen Sie eine gültige beispielanforderung >**

**Q.** Unterstützt AD FS PKCE-Erweiterung?
</br>**A.** AD FS-Server 2019 unterstützt Proof Key für Code Exchange (PKCE) für OAuth Authorization Code Grant-flow 

## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Neuerungen in Active Directory-Verbunddienste für Windows Server 2016   
Wenn Sie Informationen zu früheren Versionen von AD FS suchen, finden Sie unter den folgenden Artikeln:  
 [AD FS unter Windows Server 2012 oder 2012 R2](https://technet.microsoft.com/library/hh831502.aspx) und [AD FS 2.0](https://technet.microsoft.com/library/adfs2.aspx)  

 Active Directory Federation Services bietet, Zugriffssteuerung, und single Sign-on für eine Vielzahl von Anwendungen, einschließlich Office 365 Cloud-basierten SaaS-Anwendungen und Anwendungen mit dem Unternehmensnetzwerk verbunden.  
* Für die IT-Organisation können Sie zum Bereitstellen von SSO auf und Steuerung des Zugriffs auf moderne und legacy-Anwendungen lokal und in der Cloud, basierend auf den gleichen Satz von Anmeldeinformationen und Richtlinien.    
* Für den Benutzer bietet es nahtlose Anmelden mit den gleichen, vertrauten Kontoanmeldeinformationen an.  
* Für Entwickler bietet es sich um eine einfache Möglichkeit zum Authentifizieren von Benutzern, deren Identitäten im Organisation Verzeichnis vorhanden, sodass Sie Ihre bemühungen auf Ihre Anwendung, nicht Authentifizierungs- oder Identitätsfunktionen konzentrieren können.  

Dieser Artikel beschreibt die neuerungen in AD FS unter Windows Server 2016 (AD FS 2016).  

## <a name="eliminate-passwords-from-the-extranet"></a>Vermeiden Sie Kennwörter über das Extranet  
AD FS 2016 können drei neue Optionen für die Anmeldung ohne Kennwort, das Unternehmen die Risiken des Netzwerks zu vermeiden, die von phishingziel, verlorene oder gestohlene Kennwörter beeinträchtigt werden. 

### <a name="sign-in-with-azure-multi-factor-authentication"></a>Melden Sie sich mit Azure Multi-Factor Authentication
AD FS 2016 baut auf Multi-Factor Authentication (MFA)-Funktionen von AD FS unter Windows Server 2012 R2 durch Zulassen der Anmeldung mit nur einem Azure MFA-Code, ohne Eingabe eines Benutzernamens und Kennworts.

* Mit Azure MFA als primäre Authentifizierungsmethode wird der Benutzer für ihren Benutzernamen und das OTP-Code aus der Azure Authenticator-app aufgefordert.  
* Mit Azure MFA als sekundäre oder zusätzliche Authentifizierungsmethode gewährt dem Benutzer die primäre Authentifizierung Anmeldeinformationen (mithilfe der integrierten Windows-Authentifizierung, Benutzername und Kennwort, Smartcard oder Zertifikat für Benutzer oder Gerät), und klicken Sie dann eine Eingabeaufforderung für Text angezeigt, Voice oder OTP je Azure MFA-Anmeldung.  
* Mit den neuen integrierten Azure MFA-Adapter war Setup und Konfiguration für Azure MFA mit AD FS noch nie einfacher.
* Organisationen können von Azure MFA ohne die Notwendigkeit einer lokalen Azure MFA Server nutzen.
* Azure MFA kann für das Intranet oder extranet oder als Teil des Access Control-Richtlinie konfiguriert werden.

Weitere Informationen zu Azure MFA mit AD FS
*  [Konfigurieren von AD FS 2016 und Azure MFA](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-and-azure-mfa)  

### <a name="password-less-access-from-compliant-devices"></a>Kennwortlosen Zugriff über kompatible Geräte
AD FS 2016 baut auf früheren Funktionen für die geräteregistrierung um anmelden zu aktivieren und Zugriffssteuerung basierend Kompatibilitätsstatus des Geräts. Benutzer können sich anmelden, auf die mit den Anmeldeinformationen des Geräts und Compliance wird erneut ausgewertet, wenn Geräteattribute ändern, damit Sie immer sicherstellen können, dass Richtlinien eingehalten werden.  Dies ermöglicht z. B. Richtlinien

* Aktivieren des Zugriffs nur auf Geräten, die verwalteten und/oder kompatibel sind.  
* Aktivieren der Extranet-Zugriff nur von Geräten, die verwalteten und/oder kompatibel sind.  
* Erfordert mehrstufige Authentifizierung für Computer, die nicht verwalteten oder nicht kompatibel sind  

AD FS verfügt, die auf lokale-Komponente der Richtlinien für bedingten Zugriff in einem hybridszenario. Wenn Sie Geräte mit Azure AD für den bedingten Zugriff auf Cloud-Ressourcen registrieren, kann die geräteidentität für AD FS-Richtlinien und verwendet werden.

![Neuigkeiten](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/ADFS_ITPRO4.png)  

 Weitere Informationen zur Verwendung von Gerät-basierter Bedingter Zugriff in der cloud   
 *  [Bedingter Zugriff mit Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access/)

Weitere Informationen zur Verwendung von Gerät-basierter Bedingter Zugriff mit AD FS
*  [Planen der Gerät-basierter Bedingter Zugriff mit AD FS](../../ad-fs/deployment/Plan-Device-based-Conditional-Access-on-Premises.md)  
* [Richtlinien für die Zugriffssteuerung in AD FS](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="sign-in-with-windows-hello-for-business"></a>Melden Sie sich Windows Hello für Unternehmen   
Windows 10-Geräte eine Einführung in Windows Hello und Windows Hello for Business verwenden, ersetzen Kennwörter mit starken gerätegebundene-Benutzeranmeldeinformationen, die durch eine Benutzeraktion (eine PIN, eine biometrische Gesten wie z. B. Fingerabdruck oder gesichtserkennung) geschützt. AD FS 2016 unterstützt diese neuen Funktionen von Windows 10, sodass Benutzer auf AD FS-Anwendungen über das Intranet oder extranet, ohne dass ein Kennwort anmelden können.

Weitere Informationen zur Verwendung von Microsoft Windows Hello für Unternehmen in Ihrer Organisation
*  [Aktivieren von Windows Hello for Business in Ihrer Organisation](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)

## <a name="secure-access-to-applications"></a>Sicherer Zugriff auf Anwendungen

### <a name="modern-authentication"></a>Moderne Authentifizierung
AD FS 2016 unterstützt die neuesten modernen Protokollen, die Verbesserung der benutzerfreundlichkeit für Windows 10 als auch die aktuelle iOS und Android-Geräte und apps bereitstellen.  

Weitere Informationen finden Sie unter [AD FS-Szenarien für Entwickler](../../ad-fs/overview/AD-FS-Scenarios-for-Developers.md)  


### <a name="configure-access-control-policies-without-having-to-know-claim-rules-language"></a>Access Control-Richtlinien konfigurieren, ohne zu wissen Anspruch Regeln Sprache  
Zuvor mussten AD FS-Administratoren zum Konfigurieren von Richtlinien mithilfe der AD FS-anspruchsregelsprache darum nur schwer zu konfigurieren und Verwalten von Richtlinien. Mit Richtlinien für die Zugriffssteuerung Administratoren integrierte Vorlagen können Sie allgemeine Richtlinien wie z. B. anwenden
* Nur Intranetzugriff zulassen
* Alle zulassen und MFA über Extranet anfordern
* Alle zulassen und MFA bei einer bestimmten Gruppe

Die Vorlagen sind leicht anpassen, verwenden eine assistentengesteuerte Prozess zum Hinzufügen von Ausnahmen oder weitere Richtlinienregeln und können auf eine oder mehrere Anwendungen für die richtlinienerzwingung konsistent angewendet werden.

Weitere Informationen finden Sie unter [Zugriffssteuerungsrichtlinien in AD FS.](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="enable-sign-on-with-non-ad-ldap-directories"></a>Aktivieren Sie Anmelden mit nicht - AD-LDAP-Verzeichnissen  
Viele Organisationen verfügen über eine Kombination von Active Directory und Drittanbieter-Verzeichnisse. Durch das Hinzufügen von AD FS-Unterstützung zum Authentifizieren von Benutzern in LDAP v3-kompatiblen Verzeichnissen gespeichert werden soll können AD FS jetzt für verwendet werden:
* Benutzer in von Drittanbietern, LDAP-v3-kompatiblen Verzeichnissen
* Benutzer in Active Directory-Gesamtstrukturen, die eine bidirektionale Vertrauensstellung mit Active Directory nicht konfiguriert ist
* Benutzer in Active Directory Lightweight Directory Services (AD LDS)

Weitere Informationen finden Sie unter [Configure AD FS zum Authentifizieren von Benutzern in LDAP-Verzeichnissen gespeichert.](../../ad-fs/operations/Configure-AD-FS-to-authenticate-users-stored-in-LDAP-directories.md)  

## <a name="better-sign-in-experience"></a>Besser-Anmeldung
### <a name="customize-sign-in-experience-for-ad-fs-applications"></a>Anpassen der Anmeldung für AD FS-Anwendungen  
Wir gehört Sie, dass die Möglichkeit, die anmeldeerfahrung für jede Anwendung anzupassen. eine Verbesserung hervorragende benutzerfreundlichkeit, insbesondere für Organisationen, die wäre auf Anmelden für Anwendungen bereitstellen, die mehrere verschiedene Unternehmen oder Marken darstellen.  

Zuvor mit AD FS unter Windows Server 2012 R2 eine allgemeine Anmeldeinformationen Erfahrung für alle Anwendungen der vertrauenden Seite bereitgestellt, mit der Möglichkeit zum Anpassen der einer Teilmenge des Texts basierend Inhalt pro Anwendung. Mit Windows Server 2016 können Sie anpassen, nicht nur die Nachrichten jedoch Bilder, Logos und Web-Design pro Anwendung. Sie können darüber hinaus erstellen Sie eine neue, benutzerdefinierte Webdesigns und Anwendung pro vertrauender Seite Partei.  

Weitere Informationen finden Sie unter [AD FS-Anmeldung benutzeranpassung.](../../ad-fs/operations/AD-FS-user-sign-in-customization.md)  



## <a name="manageability-and-operational-enhancements"></a>Verwaltbarkeit und operative Verbesserungen  
Der folgende Abschnitt beschreibt die verbesserten Betriebsszenarien, die mit Active Directory-Verbunddiensten in Windows Server 2016 eingeführt wurden.  

### <a name="streamlined-auditing-for-easier-administrative-management"></a>Optimierte Überwachung für einfachere administrative Verwaltung  
In AD FS für Windows Server 2012 R2 gibt es zahlreiche Überwachungsereignisse, die für eine einzelne Anforderung und die relevanten Informationen zu einer Anmeldung generiert wurden, oder tokenausstellungs-Aktivität ist entweder nicht vorhanden (in einigen Versionen von AD FS) oder über mehrere Überwachungsereignisse verbreiten sich. Der AD FS werden Überwachungsereignisse aufgrund der Natur ausführliche standardmäßig deaktiviert.  
Mit der Version von AD FS 2016 Überwachung optimierte und weniger ausführlich geworden.  

Weitere Informationen finden Sie unter [Überwachung von Erweiterungen für AD FS unter Windows Server 2016.](../../ad-fs/technical-reference/auditing-enhancements-to-ad-fs-in-windows-server.md)  

### <a name="improved-interoperability-with-saml-20-for-participation-in-confederations"></a>Verbesserte Interoperabilität mit SAML 2.0 für die Teilnahme Gewerkschaftsbund  
AD FS 2016 enthält zusätzliche SAML-Protokoll-Unterstützung, einschließlich Unterstützung für das Importieren von Vertrauensstellungen, die basierend auf Metadaten, die mehrere Entitäten enthält. Dadurch können Sie zum Konfigurieren von AD FS für die Teilnahme an Gewerkschaftsbund wie z. B. InCommon Verbund und anderen Implementierungen, die eGov 2.0-Standards entsprechen.  

Weitere Informationen finden Sie unter [Verbesserte Interoperabilität mit SAML 2.0.](../../ad-fs/operations/Improved-interoperability-with-SAML-2.0.md)  

### <a name="simplified-password-management-for-federated-o365-users"></a>Vereinfachte Verwaltung für Office 365-Verbundbenutzer  
Sie können Active Directory-Verbunddienste (AD FS) Kennwort Ablauf Ansprüche senden an die Partei Vertrauensstellungen der vertrauenden Seite (Anwendungen) konfigurieren, die von AD FS geschützt sind. Wie diese Ansprüche verwendet werden, hängt von der Anwendung ab. Beispielsweise wurden mit Office 365 als vertrauende Seite Ihrer Updates auf Exchange Online und Outlook verbundene Benutzer über ihre Kennwörter bald-zu--abgelaufen informiert implementiert.  

Weitere Informationen finden Sie unter [Configure AD FS Kennwort Ablauf Ansprüche senden.](../../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md)  

### <a name="moving-from-ad-fs-in-windows-server-2012-r2-to-ad-fs-in-windows-server-2016-is-easier"></a>Verschieben von AD FS in Windows Server 2012 R2 AD FS in Windows Server 2016 ist ein einfacher  
Zuvor mussten Migrieren zu einer neuen Version von AD FS, exportieren die Konfiguration aus der alten Farm und einer völlig neuen, parallele Farm importieren.  

Verschieben von AD FS unter Windows Server 2012 R2 AD FS unter Windows Server 2016 ist jetzt viel einfacher geworden. Fügen Sie einen neuen Windows Server 2016-Server einfach zu einer Windows Server 2012 R2-Farm hinzu, und die Farm auf der Ebene der Windows Server 2012 R2-Farm-Verhalten, angewendet wird, sodass es aussieht und verhält sich wie eine Windows Server 2012 R2-Farm.  

Klicken Sie dann fügen Sie neue Windows Server 2016-Server der Farm hinzu, überprüfen Sie die Funktionalität ein, und entfernen Sie die ältere Server aus dem Load Balancer. Sobald alle farmknoten auf Windows Server 2016 ausgeführt werden, können Sie sich auf die Farmen mit verhaltensebene 2016 aktualisieren, und beginnen mithilfe der neuen Funktionen.  

Weitere Informationen finden Sie unter [zu AD FS unter Windows Server 2016 aktualisieren.](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)  
