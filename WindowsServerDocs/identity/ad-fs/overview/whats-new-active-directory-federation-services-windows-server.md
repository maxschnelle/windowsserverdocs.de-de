---
ms.assetid: aa892a85-f95a-4bf1-acbb-e3c36ef02b0d
title: Neuerungen in Active Directory-Verbunddienste für Windows Server 2016
author: billmath
ms.author: billmath
manager: daveba
ms.date: 01/22/2020
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 424c0ad75e33adbbb243f07da4f1d0f3deec16dc
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961312"
---
# <a name="whats-new-in-active-directory-federation-services"></a>Neuerungen in Active Directory-Verbunddienste


## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2019"></a>Neuerungen in Active Directory-Verbunddienste für Windows Server 2019

### <a name="protected-logins"></a>Geschützte Anmeldungen

Es folgt eine kurze Zusammenfassung der Aktualisierungen geschützter Anmeldungen, die in AD FS 2019 verfügbar sind:
- **Externe Authentifizierungsanbieter als primäre Authentifizierung**: Kunden können jetzt Authentifizierungsprodukte von Drittanbietern als ersten Faktor verwenden und müssen Kennwörter nicht als ersten Faktor verfügbar machen. In Fällen, in denen ein externer Authentifizierungsanbieter zwei Faktoren nachweisen kann, besteht MFA-Anspruch.
- **Kennwortauthentifizierung als zusätzliche Authentifizierung**: Kunden verfügen über eine vollständig unterstützte Eingangsoption, um das Kennwort nur für den zusätzlichen Faktor zu verwenden, nachdem eine Option ohne Kennwort als erster Faktor verwendet wurde. Dies verbessert die Benutzerfreundlichkeit von AD FS 2016. Bei dieser Komponente mussten Kunden einen GitHub-Adapter herunterladen, der unverändert unterstützt wird.
- **Austauschbares Risikobewertungsmodul**: Kunden können jetzt eigene Plug-In-Module erstellen, um bestimmte Anforderungstypen während der Vorauthentifizierung zu blockieren. Dadurch können Kunden Cloud Intelligence-Lösungen wie Identity Protection (Identitätsschutz) einfacher verwenden, um Anmeldungen für riskante Benutzer oder riskante Transaktionen zu blockieren.  Weitere Informationen findest du unter [Erstellen von Plug-Ins mit dem Risikobewertungsmodell von AD FS 2019](../../ad-fs/development/ad-fs-risk-assessment-model.md).
- **ESL-Verbesserungen**: Durch Hinzufügen der folgenden Funktionen wird das ESL-QFE in 2016 verbessert.
    - Ermöglicht es Kunden, sich im Überwachungsmodus zu befinden und gleichzeitig durch die „klassische“ Extranetsperrfunktion geschützt zu sein, die ab AD FS 2012R2 verfügbar ist. Derzeit sind 2016-Kunden im Überwachungsmodus nicht geschützt.
    - Aktiviert einen unabhängigen Sperrschwellenwert für bekannte Orte. Dadurch können mehrere Instanzen von Apps, die mit einem gemeinsamen Dienstkonto ausgeführt werden, einen Rollover für Kennwörter mit minimalen Auswirkungen durchführen.


### <a name="additional-security-improvements"></a>Zusätzliche Sicherheitsverbesserungen

In AD FS 2019 sind die folgenden zusätzlichen Sicherheitsverbesserungen verfügbar:
- **Remote PowerShell (PSH) mithilfe von SmartCard-Anmeldung**: Kunden können jetzt mithilfe von Smartcards über PSH eine Remoteverbindung mit ADFS herstellen und diese zum Verwalten aller PSH-Funktionen verwenden, einschließlich PSH-Cmdlets mit mehreren Knoten.
- **Anpassung von HTTP-Headern**: Kunden können jetzt HTTP-Header anpassen, die bei AD FS-Antworten ausgegeben werden. Dies schließt die folgenden Header ein:
     - HSTS: Dadurch wird vermittelt, dass AD FS-Endpunkte nur für HTTPS-Endpunkte verwendet werden können, damit ein kompatibler Browser erzwungen wird.
     - x-frame-options: Ermöglicht es AD FS-Administratoren, bestimmten vertrauenden Seiten das Einbetten von iFrames für interaktive AD FS-Anmeldeseiten zu gestatten. Dies sollte mit Bedacht und nur auf HTTPS-Hosts erfolgen.
     - Zukünftige Header: Es können auch weitere zukünftige Header konfiguriert werden.

Weitere Informationen findest du unter [Anpassen der HTTP-Sicherheitsantwortheader mit AD FS 2019](../../ad-fs/operations/customize-http-security-headers-ad-fs.md).


### <a name="authenticationpolicy-capabilities"></a>Authentifizierungs-/Richtlinienfunktionen

In AD FS 2019 sind die folgenden Authentifizierungs-/Richtlinienfunktionen verfügbar:
- **Authentifizierungsmethode für zusätzliche Authentifizierung pro RP angeben**: Kunden können jetzt Anspruchsregeln verwenden, um zu entscheiden, welcher weitere Authentifizierungsanbieter als zusätzlicher Authentifizierungsanbieter aufgerufen werden soll. Dies ist in zwei Anwendungsfällen nützlich.
    - Kunden wechseln von einem zusätzlichen Authentifizierungsanbieter zu einem anderen. Wenn diese Kunden Benutzer in einen neueren Authentifizierungsanbieter integrieren, können sie Gruppen verwenden, um zu steuern, welcher zusätzliche Authentifizierungsanbieter aufgerufen wird.
    - Kunden müssen für bestimmte Anwendungen einen bestimmten zusätzlichen Authentifizierungsanbieter (z. B. ein Zertifikat) verwenden.
- **TLS-basierte Geräteauthentifizierung nur auf Anwendungen beschränken, die sie erfordern**: Kunden können jetzt clientseitige TLS-basierte Geräteauthentifizierungen auf Anwendungen beschränken, die gerätebasierten bedingten Zugriff ausführen. Dadurch werden unerwünschte Eingabeaufforderungen zur Geräteauthentifizierung (oder Fehler, wenn die Clientanwendung diese nicht verarbeiten kann) für Anwendungen verhindert, die keine TLS-basierte Geräteauthentifizierung erfordern.
- **Unterstützung von MFA-Aktualität**: AD FS unterstützt jetzt die Möglichkeit, die Anmeldeinformationen des zweiten Faktors auf der Grundlage der Aktualität dieser Anmeldeinformationen wieder zu verwenden. Dadurch können Kunden eine erste Transaktion mit zwei Faktoren ausführen und nur in regelmäßigen Abständen den zweiten Faktor anfordern. Dies ist nur für Anwendungen verfügbar, die einen zusätzlichen Parameter in der Anforderung bereitstellen können. Dies ist keine konfigurierbare Einstellung in AD FS. Dieser Parameter wird von Azure AD unterstützt, wenn „Meine MFA für X Tage speichern“ konfiguriert ist und in Azure AD das Flag „supportsMFA“ in den Vertrauenseinstellungen der Verbunddomäne auf „true“ festgelegt ist.


### <a name="sign-in-sso-improvements"></a>Verbesserungen beim einmaligen Anmelden

In AD FS 2019 wurden die folgenden Verbesserungen beim einmaligen Anmelden vorgenommen:

- [Paginierte Benutzeroberfläche mit zentriertem Design](../operations/AD-FS-paginated-sign-in.md): In AD FS wurde die Benutzeroberfläche zu einem paginierten UX-Flow umgestaltet, sodass AD FS eine optimierte Anmeldeoberfläche validieren und bereitstellen kann. In AD FS wird jetzt eine zentrierte Benutzeroberfläche (anstelle der rechten Seite des Bildschirms) verwendet. Möglicherweise benötigst du ein neueres Logo und neuere Hintergrundbilder, die an diese Oberfläche angepasst sind. Dadurch wird auch die in Azure AD angebotene Funktionalität widergespiegelt.
- **Programmfehlerbehebung: Persistenter SSO-Status für Windows 10-Geräte bei der PRT-Authentifizierung**: Damit wird ein Problem behoben, bei dem der MFA-Status bei Verwendung der PRT-Authentifizierung für Windows 10-Geräte nicht persistent war. Dieses Problem führte dazu, dass Endbenutzer häufig zur Eingabe von Anmeldeinformationen des zweiten Faktors (MFA) aufgefordert wurden. Durch die Fehlerbehebung wird auch die Benutzererfahrung konsistent, wenn die Geräteauthentifizierung erfolgreich über Client-TLS und über den PRT-Mechanismus durchgeführt wird.


### <a name="suppport-for-building-modern-line-of-business-apps"></a>Unterstützung für das Erstellen von modernen branchenspezifischen Apps

In AD FS 2019 wurde die folgende Unterstützung für das Erstellen von modernen branchenspezifischen Apps hinzugefügt:

- **OAuth-Geräteflow/-Profil**: AD FS unterstützt jetzt das OAuth-Geräteflowprofil zum Ausführen von Anmeldungen auf Geräten, die nicht über einen Benutzeroberflächenbereich verfügen, der umfangreiche Anmeldefunktionen unterstützt. Dadurch können Benutzer die Anmeldung auf einem anderen Gerät durchführen. Diese Funktion ist für Azure CLI in Azure Stack erforderlich und kann auch in anderen Fällen verwendet werden.
- **Entfernung des Ressourcenparameters**: In AD FS muss jetzt kein Ressourcenparameter mehr angegeben werden, der mit den aktuellen OAuth-Spezifikationen übereinstimmt. Clients können jetzt zusätzlich zu den angeforderten Berechtigungen den Bezeichner der Vertrauensstellung der vertrauenden Seite als Bereichsparameter angeben.
- **CORS-Header in AD FS-Antworten**: Kunden können jetzt Single-Page-Anwendungen erstellen, mit denen clientseitige JS-Bibliotheken die Signatur des ID-Tokens (id_token) überprüfen können, indem sie die Signaturschlüssel aus dem OIDC-Discovery-Dokument in AD FS abfragen.
- **PKCE-Unterstützung**: AD FS umfasst jetzt PKCE-Unterstützung, um einen sicheren Authentifizierungscodeflow in OAuth zu ermöglichen. Dadurch wird diesem Flow eine zusätzliche Sicherheitsebene hinzugefügt, um den Code vor Hijacking zu schützen und zu verhindern, dass er von einem anderen Client wiedergegeben werden kann.
- **Programmfehlerbehebung: „x5t“- und „kid“-Anspruch senden**: Hierbei handelt es sich um eine kleinere Programmfehlerbehebung. AD FS sendet jetzt zusätzlich den „kid“-Anspruch, um den Schlüssel-ID-Hinweis zum Überprüfen der Signatur anzugeben. Zuvor hat AD FS dies nur als „x5t“-Anspruch gesendet.


### <a name="supportability-improvements"></a>Verbesserungen der Unterstützbarkeit

Die folgenden Verbesserungen der Unterstützbarkeit sind nicht Teil von AD FS 2019:
- **Fehlerdetails an AD FS-Administratoren senden**: Dadurch können Administratoren Endbenutzer so konfigurieren, dass Debugprotokolle zu einem Fehler bei der Endbenutzerauthentifizierung gesendet werden, die zur einfachen Nutzung als ZIP-Datei gespeichert werden. Administratoren können auch eine SMTP-Verbindung konfigurieren, um die ZIP-Datei automatisch an ein Triage-E-Mail-Konto zu senden oder ein Ticket auf der Grundlage der E-Mail automatisch zu erstellen.


### <a name="deployment-updates"></a>Bereitstellungsaktualisierungen

Die folgenden Bereitstellungsaktualisierungen sind jetzt in AD FS 2019 enthalten:
- **Farmverhaltensebene 2019**: Wie in AD FS 2016 gibt es eine neue Version der Farmverhaltensebene, die zum Aktivieren von neuen Funktionen erforderlich ist, die oben erläutert werden. Dies ermöglicht einen Wechsel von:
    - 2012 R2 -> 2019
    - 2016 -> 2019


### <a name="saml-updates"></a>SAML-Updates

In AD FS 2019 ist das folgende SAML-Update enthalten:
- **Programmfehlerbehebung: Beheben von Fehlern im aggregierten Verbund**: Es gibt zahlreiche Fehlerbehebungen für die Unterstützung des aggregierten Verbunds (z. B. „InCommon“). Die Fehlerbehebungen beziehen sich auf die folgenden Punkte:
  - Verbesserte Skalierung für eine große Anzahl von Entitäten im Dokument für aggregierte Verbundmetadaten. Zuvor ist dabei der Fehler „ADMIN0017“ aufgetreten.
  - Abfragen mit dem Parameter „ScopeGroupID“ über das PSH-Cmdlet „Get-AdfsRelyingPartyTrustsGroup PSH“ (PowerShell).
  - Behandeln von Fehlerbedingungen im Zusammenhang mit einer doppelten Entitäts-ID (entityID)


### <a name="azure-ad-style-resource-specification-in-scope-parameter"></a>Azure AD-Stilressourcenspezifikation im Bereichsparameter

Zuvor war es in AD FS erforderlich, dass die gewünschte Ressource und der gewünschte Bereich in einem separaten Parameter in jeder Authentifizierungsanforderung enthalten waren. Eine typische OAuth-Anforderung sieht beispielsweise wie folgt aus: 7 **https:&#47;&#47;fs.contoso.com/adfs/oauth2/authorize?</br>response_type=code&client_id=claimsxrayclient&resource=urn:microsoft:</br>adfs:claimsxray&scope=oauth&redirect_uri=https:&#47;&#47;adfshelp.microsoft.com/</br> ClaimsXray/TokenResponse&prompt=login**

Bei AD FS unter Windows Server 2019 kann jetzt der im Bereichsparameter eingebettete Ressourcenwert übergeben werden. Dies entspricht auch der Art und Weise, wie eine Authentifizierung bei Azure AD durchgeführt werden kann.

Der Bereichsparameter kann jetzt als eine durch Leerzeichen getrennte Liste organisiert werden, wobei jeder Eintrag als Ressource/Bereich strukturiert ist.

> [!NOTE]
> In der Authentifizierungsanforderung kann nur eine Ressource angegeben werden. Wenn in der Anforderung mehrere Ressourcen enthalten sind, gibt AD FS einen Fehler zurück, und die Authentifizierung kann nicht erfolgreich ausgeführt werden.


### <a name="proof-key-for-code-exchange-pkce-support-for-oauth"></a>Proof Key for Code Exchange-Unterstützung (PKCE-Unterstützung) für OAuth

Öffentliche OAuth-Clients die den Authorization Code Grant-Typ verwenden, sind anfällig für den Angriff zum Abfangen des Autorisierungscodes.  Der Angriff ist in RFC 7636 gut beschrieben. Um diesen Angriff zu entschärfen, unterstützt AD FS unter Windows Server 2019 die Erweiterung „Proof Key for Code Exchange“ (PKCE) für den OAuth Authorization Code Grant-Datenfluss.

Um die PKCE-Unterstützung zu nutzen, fügt diese Spezifikation den OAuth 2.0-Autorisierungs- und Zugriffstokenanforderungen zusätzliche Parameter hinzu.

![Prüfschlüssel](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/adfs2019.png)

A. Der Client erstellt einen geheimen Schlüssel mit dem Namen „code_verifier“, zeichnet diesen auf und leitet eine transformierte Version „t(code_verifier)“ (als „code_challenge“ bezeichnet) ab, die zusammen mit der Transformationsmethode „t_m“ in der OAuth 2.0-Autorisierungsanforderung gesendet wird.

B. Der Autorisierungsendpunkt antwortet wie gewohnt, zeichnet jedoch „t(code_verifier)“ und die Transformationsmethode auf.

C. Der Client sendet dann den Autorisierungscode in der Zugriffstokenanforderung wie gewohnt, schließt jedoch den unter (A) generierten geheimen Schlüssel „code_verifier“ ein.

D. AD FS transformiert den geheimen Schlüssel „code_verifier“ und vergleicht ihn mit „t(code_verifier)“ aus (B).  Wenn sie nicht gleich sind, wird der Zugriff verweigert.


#### <a name="faq"></a>Häufig gestellte Fragen

> [!NOTE]
> Dieser Fehler kann in den Ereignisprotokollen von ADFS Admin auftreten: Es wurde eine ungültige OAuth-Anforderung empfangen. Dem Client „NAME“ ist der Zugriff auf die Ressource mit dem Bereich „ugs“ untersagt.
> So behebst du diesen Fehler
> 1. Starte die AD FS-Verwaltungskonsole. Navigieren Sie zu „Dienste > Bereichsbeschreibungen“.
> 2. Klicke mit der rechten Maustaste auf „Bereichsbeschreibungen“ und wähle „Bereichsbeschreibung hinzufügen“ aus.
> 3. Gebe unter Name den Namen „ugs“ ein und klicke dann auf „Übernehmen“ > „OK“.
> 4. Führen Sie PowerShell als Administrator aus.
> 5. Führe den Befehl „Get-AdfsApplicationPermission“ aus. Suche nach „ScopeNames :{openid, aza}“, die „ClientRoleIdentifier“ aufweisen. Notiere den „ObjectIdentifier“.
> 6. Führe den Befehl „Set-AdfsApplicationPermission -TargetIdentifier <ObjectIdentifier aus Schritt 5> -AddScope 'ugs'“ aus.
> 7. Starte den ADFS-Dienst neu.
> 8. Auf dem Client: Starte den Client neu. Der Benutzer sollte zur Bereitstellung von WHFB aufgefordert werden.
> 9. Wenn das Bereitstellungsfenster nicht angezeigt wird, musst du Protokolle zur NGC-Nachverfolgung sammeln und eine weitere Problembehandlung durchführen.

**F.** Kann ich den Ressourcenwert als Teil des Bereichswerts übergeben, so wie Anforderungen für Azure AD durchgeführt werden?</br>
**A.** Bei AD FS unter Windows Server 2019 kann jetzt der im Bereichsparameter eingebettete Ressourcenwert übergeben werden. Der Bereichsparameter kann jetzt als eine durch Leerzeichen getrennte Liste organisiert werden, wobei jeder Eintrag als Ressource/Bereich strukturiert ist. Zum Beispiel **<eine gültige Beispielanforderung erstellen>**

**F.** Unterstützt AD FS die PKCE-Erweiterung?</br>
**A.** AD FS unter Windows Server 2019 unterstützt die Erweiterung „Proof Key for Code Exchange“ (PKCE) für den OAuth Authorization Code Grant-Datenfluss.


## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Neuerungen in Active Directory-Verbunddienste für Windows Server 2016

Informationen zu früheren Versionen von AD FS findest du in den folgenden Artikeln: [Active Directory-Verbunddienste (AD FS) für Windows Server 2012 oder 2012 R2](../../active-directory-federation-services.md) und [Active Directory-Verbunddienste (AD FS) 2.0](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd727958(v=ws.10))

 Active Directory-Verbunddienste (AD FS) ermöglicht die Zugriffssteuerung und einmaliges Anmelden für eine Vielzahl von Anwendungen einschließlich Office 365, cloudbasierter SaaS-Anwendungen und Anwendungen im Unternehmensnetzwerk.
* Der IT-Organisation ermöglicht AD FS das Bereitstellen der Anmeldung und Zugriffssteuerung sowohl für moderne als auch für ältere Anwendungen, lokal und in der Cloud, basierend auf demselben Satz von Anmeldeinformationen und Richtlinien.
* Dem Benutzer ermöglicht AD FS eine nahtlose Anmeldung mit denselben, vertrauten Kontoanmeldeinformationen.
* Dem Entwickler bietet AD FS eine einfache Möglichkeit zum Authentifizieren von Benutzern, deren Identitäten im Organisationsverzeichnis gespeichert sind, sodass du dich auf die Anwendung konzentrieren kannst und dich nicht mit der Authentifizierung oder Identität befassen musst.

In diesem Artikel werden die Neuerungen in AD FS für Windows Server 2016 (AD FS 2016) beschrieben.


## <a name="eliminate-passwords-from-the-extranet"></a>Vermeiden von Kennwörtern im Extranet

AD FS 2016 bietet drei neue Optionen für die Anmeldung ohne Kennwörter, sodass Organisationen das Risiko einer Netzwerkgefährdung durch über Phishing erlangte, kompromittierte oder gestohlene Kennwörter vermeiden können.


### <a name="sign-in-with-azure-multi-factor-authentication"></a>Anmelden mit Azure Multi-Factor Authentication

AD FS 2016 basiert auf den Funktionen für die mehrstufige Authentifizierung (Multi-Factor Authentication, MFA) von AD FS unter Windows Server 2012 R2, wobei die Anmeldung nur mit einem Azure MFA-Code zugelassen wird, ohne zuvor einen Benutzernamen und ein Kennwort einzugeben.

* Wenn Azure MFA die primäre Authentifizierungsmethode ist, wird der Benutzer zur Eingabe seines Benutzernamens und des OTP-Codes aus der Microsoft Authenticator-App aufgefordert.
* Wenn Azure MFA als sekundäre oder zusätzliche Authentifizierungsmethode verwendet wird, stellt der Benutzer Anmeldeinformationen für die primäre Authentifizierung bereit (mittels integrierter Windows-Authentifizierung, Benutzername und Kennwort, Smartcard oder Benutzer- oder Gerätezertifikat). Und dann wird dem Benutzer eine Eingabeaufforderung für die text-, sprach- oder OTP-basierte Azure MFA-Anmeldung angezeigt.
* Dank des neuen integrierten Azure MFA-Adapters ist die Einrichtung und Konfiguration von Azure MFA mit AD FS einfacher als jemals zuvor.
* Organisationen können Azure MFA nutzen, ohne einen lokalen Azure MFA-Server verwenden zu müssen.
* Azure MFA kann für das Intranet oder Extranet oder als Teil einer Zugriffssteuerungsrichtlinie konfiguriert werden.

Weitere Informationen zu Azure MFA mit AD FS:
*  [Konfigurieren von AD FS 2016 und Azure MFA](../operations/configure-ad-fs-and-azure-mfa.md)


### <a name="password-less-access-from-compliant-devices"></a>Kennwortloser Zugriff über kompatible Geräte

AD FS 2016 baut auf früheren Geräteregistrierungsfunktionen auf, um die Anmeldung und Zugriffssteuerung basierend auf dem Konformitätsstatus der Geräte zu ermöglichen. Benutzer können sich mit den Geräteanmeldeinformationen anmelden, und die Konformität wird bei Änderungen der Geräteattribute erneut ausgewertet, sodass immer sichergestellt wird, dass Richtlinien erzwungen werden.  Dadurch können beispielsweise die folgenden Richtlinien angewendet werden:

* Zugriff nur von verwalteten und/oder kompatiblen Geräten zulassen
* Extranetzugriff nur von verwalteten und/oder kompatiblen Geräten zulassen
* Mehrstufige Authentifizierung für nicht verwaltete oder nicht kompatible Computer erforderlich

AD FS bietet die lokale Komponente der Richtlinien für bedingten Zugriff in einem Hybridszenario. Wenn du Geräte bei Azure AD für den bedingten Zugriff auf Cloudressourcen registrierst, kann die Geräteidentität auch für AD FS-Richtlinien verwendet werden.

![Neuerungen](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/ADFS_ITPRO4.png)

 Weitere Informationen zum Verwenden des gerätebasierten bedingten Zugriffs in der Cloud:
 * [Bedingter Zugriff in Azure Active Directory](/azure/active-directory/conditional-access/overview)

Weitere Informationen zum Verwenden des gerätebasierten bedingten Zugriffs mit AD FS:
* [Planen des gerätebasierten bedingten Zugriffs mit AD FS](../../ad-fs/deployment/Plan-Device-based-Conditional-Access-on-Premises.md)
* [Zugriffssteuerungsrichtlinien in AD FS](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)


### <a name="sign-in-with-windows-hello-for-business"></a>Anmelden mit Windows Hello for Business

> [!NOTE]
> Derzeit werden Google Chrome und die [neuen Chromium-basierten Microsoft Edge](https://www.microsoft.com/edge?form=MB110A&OCID=MB110A)-Open-Source-Projektbrowser nicht für browserbasiertes einmaliges Anmelden (Single-Sign On, SSO) mit Microsoft Windows Hello for Business unterstützt. Verwende Internet Explorer oder eine ältere Version von Microsoft Edge.

Auf Windows 10-Geräten werden Windows Hello und Windows Hello for Business eingeführt, wobei Benutzerkennwörter durch sichere gerätegebundene Benutzeranmeldeinformationen ersetzt werden, die durch eine Benutzergeste (eine PIN, eine biometrische Geste wie ein Fingerabdruck oder Gesichtserkennung) geschützt sind. AD FS 2016 unterstützt diese neuen Windows 10-Funktionen, sodass sich Benutzer sich über das Intranet oder Extranet bei AD FS-Anwendungen anmelden können, ohne ein Kennwort angeben zu müssen.

Weitere Informationen zum Verwenden von Microsoft Windows Hello for Business in der Organisation:
* [Aktivieren von Windows Hello for Business in der Organisation](/windows/security/identity-protection/hello-for-business/hello-identity-verification)


## <a name="secure-access-to-applications"></a>Sicherer Zugriff auf Anwendungen

### <a name="modern-authentication"></a>Moderne Authentifizierung

AD FS 2016 unterstützt die neuesten modernen Protokolle, die mehr Benutzerfreundlichkeit für Windows 10- sowie für die neuesten iOS- und Android-Geräte und -Apps bieten.

Weitere Informationen findest du unter [AD FS-Szenarien für Entwickler](../../ad-fs/overview/ad-fs-openid-connect-oauth-flows-scenarios.md).


### <a name="configure-access-control-policies-without-having-to-know-claim-rules-language"></a>Konfigurieren von Zugriffssteuerungsrichtlinien ohne Kenntnis der Anspruchsregelsprache

Bisher mussten AD FS-Administratoren Richtlinien mithilfe der AD FS-Anspruchsregelsprache konfigurieren, wodurch das Konfigurieren und Verwalten von Richtlinien erschwert wurde. Bei Zugriffssteuerungsrichtlinien können Administratoren integrierte Vorlagen verwenden, um allgemeine Richtlinien anzuwenden, wie beispielsweise:
* Nur Intranetzugriff zulassen
* Jedem Einzelnen Zugriff gewähren und MFA für Extranetzugriffe verlangen
* Jedem Einzelnen Zugriff gewähren und MFA für bestimmte Gruppe verlangen

Die Vorlagen können mithilfe eines assistentengesteuerten Prozesses problemlos angepasst werden, um Ausnahmen oder zusätzliche Richtlinienregeln hinzuzufügen, und auf eine oder mehrere Anwendungen angewendet werden, um eine konsistente Richtlinienerzwingung zu erreichen.

Weitere Informationen findest du unter [Zugriffssteuerungsrichtlinien in AD FS](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md).


### <a name="enable-sign-on-with-non-ad-ldap-directories"></a>Aktivieren der Anmeldung mit Nicht-AD-LDAP-Verzeichnissen

Viele Organisationen verwenden eine Kombination aus Active Directory-Verzeichnissen und Verzeichnissen von Drittanbietern. Durch die hinzugefügte AD FS-Unterstützung für das Authentifizieren von Benutzern, die in LDAP v3-kompatiblen Verzeichnissen gespeichert sind, kann AD FS jetzt für Folgendes verwendet werden:
* Benutzer in LDAP v3-kompatiblen Verzeichnissen von Drittanbietern
* Benutzer in Active Directory-Gesamtstrukturen, für die keine bidirektionale Active Directory-Vertrauensstellung konfiguriert ist
* Benutzer in Active Directory Lightweight Directory Services (AD LDS)

Weitere Informationen findest du unter [Konfigurieren von AD FS zum Authentifizieren von Benutzern, die in LDAP-Verzeichnissen gespeichert sind](../../ad-fs/operations/Configure-AD-FS-to-authenticate-users-stored-in-LDAP-directories.md).


## <a name="better-sign-in-experience"></a>Bessere Anmeldeoberfläche

### <a name="customize-sign-in-experience-for-ad-fs-applications"></a>Anpassen der Anmeldeoberfläche für AD FS-Anwendungen

Wir haben gehört, dass die Möglichkeit, die Anmeldeoberfläche für jede Anwendung anzupassen, eine erhebliche Verbesserung der Benutzerfreundlichkeit darstellen würde, insbesondere für Organisationen, die Anmeldungen für Anwendungen bereitstellen, die mehrere verschiedene Unternehmen oder Marken umfassen.

In AD FS für Windows Server 2012 R2 wurde zuvor eine gemeinsame Anmeldeoberfläche für alle Anwendungen der vertrauenden Seite bereitgestellt, mit der Möglichkeit, eine Teilmenge von textbasierten Inhalten pro Anwendung anzupassen. Unter Windows Server 2016 kannst du nicht nur die Meldungen, sondern auch die Bilder, das Logo und das Webdesign pro Anwendung anpassen. Darüber hinaus kannst du neue, benutzerdefinierte Webdesigns erstellen und diese pro vertrauende Seite anwenden.

Weitere Informationen findest du unter [AD FS: Anpassung der Benutzeranmeldung](../../ad-fs/operations/AD-FS-user-sign-in-customization.md).


## <a name="manageability-and-operational-enhancements"></a>Verwaltbarkeit und operative Erweiterungen

Im folgenden Abschnitt werden die verbesserten operativen Szenarien beschrieben, die in Active Directory-Verbunddienste (AD FS) für Windows Server 2016 eingeführt werden.


### <a name="streamlined-auditing-for-easier-administrative-management"></a>Optimierte Überwachung für eine einfachere administrative Verwaltung

In AD FS für Windows Server 2012 R2 wurden zahlreiche Überwachungsereignisse für eine einzige Anforderung generiert, und die relevanten Informationen zu einer Anmelde- oder Tokenausstellungsaktivität sind entweder nicht vorhanden (in einigen Versionen von AD FS) oder auf mehrere Überwachungsereignisse verteilt. Die AD FS-Überwachungsereignisse sind aufgrund ihrer Ausführlichkeit standardmäßig deaktiviert.
Mit der Veröffentlichung von AD FS 2016 ist die Überwachung optimiert und weniger ausführlich.

Weitere Informationen findest du unter [Überwachen von Erweiterungen für AD FS unter Windows Server 2016](../../ad-fs/technical-reference/auditing-enhancements-to-ad-fs-in-windows-server.md).


### <a name="improved-interoperability-with-saml-20-for-participation-in-confederations"></a>Verbesserte Interoperabilität mit SAML 2.0 für die Teilnahme an Verbünden

AD FS 2016 umfasst zusätzliche Unterstützung für das SAML-Protokoll, einschließlich der Unterstützung für das Importieren von Vertrauensstellungen basierend auf Metadaten, die mehrere Entitäten enthalten. Dadurch kann AD FS für die Teilnahme an Verbünden wie der InCommon Federation und anderen Implementierungen konfiguriert werden, die dem eGov 2.0-Standard entsprechen.

Weitere Informationen findest du unter [Verbesserte Interoperabilität mit SAML 2.0](../../ad-fs/operations/Improved-interoperability-with-SAML-2.0.md).


### <a name="simplified-password-management-for-federated-o365-users"></a>Vereinfachte Kennwortverwaltung für Office 365-Verbundbenutzer

Du kannst Active Directory Federation Services (AD FS) so konfigurieren, dass Ansprüche beim Kennwortablauf an die Vertrauensstellungen der vertrauenden Seite (Anwendungen) gesendet werden, die durch AD FS geschützt sind. Wie diese Ansprüche verwendet werden, hängt von der jeweiligen Anwendung ab. Beispiel: Bei Office 365 als vertrauende Seite werden Updates in Exchange und Outlook implementiert, damit Verbundbenutzer über ihre bald ablaufenden Kennwörter benachrichtigt werden.

Weitere Informationen findest du unter [Konfigurieren von AD FS zum Senden von Ansprüchen beim Kennwortablauf](../../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md).


### <a name="moving-from-ad-fs-in-windows-server-2012-r2-to-ad-fs-in-windows-server-2016-is-easier"></a>Einfachere Umstellung von AD FS für Windows Server 2012 R2 auf AD FS für Windows Server 2016

Bisher erforderte die Migration zu einer neuen Version von AD FS das Exportieren der Konfiguration aus der alten Farm und das Importieren in eine ganz neue parallele Farm.

Die Umstellung von AD FS für Windows Server 2012 R2 auf AD FS für Windows Server 2016 gestaltet sich jetzt viel einfacher. Füge einfach einer Windows Server 2012 R2-Farm einen neuen Windows Server 2016-Server hinzu. Die Farm verhält sich dann auf der Verhaltensebene der Windows Server 2012 R2-Farm, sodass sie das Aussehen und Verhalten einer Windows Server 2012 R2-Farm aufweist.

Füge der Farm dann neue Windows Server 2016-Server hinzu, überprüfe die Funktionalität, und entferne die älteren Server aus dem Lastenausgleich. Sobald alle Farmknoten unter Windows Server 2016 ausgeführt werden, kannst du die Farmverhaltensebene auf 2016 aktualisieren und die neuen Features verwenden.

Weitere Informationen findest du unter [Aktualisieren auf AD FS unter Windows Server 2016](../deployment/upgrading-to-ad-fs-in-windows-server.md).
