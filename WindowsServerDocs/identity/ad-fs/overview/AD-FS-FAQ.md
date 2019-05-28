---
ms.assetid: acc9101b-841c-4540-8b3c-62a53869ef7a
title: FAQ zu AD FS 2016
description: Häufig gestellte Fragen für AD FS 2016
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 04/17/2019
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fdd31a8b7c2c6ef87d1d22d901b5c6ca69b5c70d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188719"
---
# <a name="ad-fs-frequently-asked-questions-faq"></a>AD FS-häufig gestellte Fragen (FAQ)


Die folgende Dokumentation ist ein Zuhause auf häufig gestellte Fragen in Bezug auf Active Directory Federation Services.  Das Dokument wurde basierend auf der Art der Frage in Gruppen aufgeteilt.

## <a name="deployment"></a>Bereitstellung

### <a name="how-can-i-upgrademigrate-from-previous-versions-of-ad-fs"></a>Wie kann ich Upgrade/aus früheren Versionen von AD FS migrieren
Sie können AD FS mithilfe einer der folgenden aktualisieren:


- Windows Server 2012 R2 AD FS Windows Server 2016 AD FS
    - [Aktualisieren auf AD FS unter Windows Server 2016 unter Verwendung einer WID-Datenbank](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)
    - [Aktualisieren auf AD FS unter Windows Server 2016 unter Verwendung einer SQL-Datenbank](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL.md)
- Windows Server 2012 AD FS für Windows Server 2012 R2 AD FS
    - [Migrieren von AD FS unter Windows Server 2012 R2](https://technet.microsoft.com/library/dn486815.aspx)
- AD FS 2.0 für Windows Server 2012 AD FS
    - [Migrieren von AD FS unter WindowsServer 2012](https://technet.microsoft.com/library/jj647765.aspx)
- AD FS 1.x auf AD FS 2.0
    - [Upgrade von AD FS 1.x auf AD FS 2.0](https://technet.microsoft.com/library/ff678035.aspx)

Wenn Sie ein Upgrade von AD FS 2.0 oder 2.1 (Windows Server 2008 R2 oder Windows Server 2012) durchführen möchten, müssen Sie den integrierten Skripts (C:\Windows\ADFS) verwenden.

### <a name="why-does-ad-fs-installation-require-a-reboot-of-the-server"></a>Warum erfordert AD FS-Installation einen Neustart des Servers?

HTTP/2-Unterstützung wurde in Windows Server 2016 hinzugefügt, aber die HTTP/2 kann nicht für die Authentifizierung per Clientzertifikat verwendet werden.  Da viele AD FS-Szenarien Verwendung der Authentifizierung per Clientzertifikat und eine große Anzahl von Clients führen keine Unterstützung für Wiederholung vornehmen fordert die Verwendung von HTTP/1.1, AD FS-Farm Konfiguration neu konfiguriert HTTP-Einstellungen des lokalen Servers auf HTTP/1.1.  Dies erfordert einen Neustart des Servers.  

### <a name="is-using-windows-2016-wap-servers-to-publish-the-ad-fs-farm-to-the-internet-without-upgrading-the-back-end-ad-fs-farm-supported"></a>Verwendet Windows 2016-WAP-Server, um AD FS-Farm mit dem Internet zu veröffentlichen, ohne dass ein Upgrade der Back-End-AD FS-Farm unterstützt?
Ja, wird diese Konfiguration unterstützt, jedoch keine neuen AD FS 2016-Funktionen in dieser Konfiguration unterstützt werden.  Diese Konfiguration wird während der Migration von AD FS 2012 R2 AD FS 2016 temporär sein und für längere Zeit nicht bereitgestellt werden.

### <a name="is-it-possible-to-deploy-ad-fs-for-office-365-without-publishing-a-proxy-to-office-365"></a>Ist es möglich, AD FS für Office 365 bereitstellen, ohne einen Proxy in Office 365 veröffentlichen?
Ja, dies wird unterstützt. Allerdings als Nebeneffekt

1. Sie müssen für das manuelle Verwalten der Tokensignaturzertifikate aktualisieren, da es sich bei Azure AD nicht auf die Metadaten des Verbunds zugreifen kann. Lesen Sie weitere Informationen zum manuellen Aktualisieren Tokensignaturzertifikat [Erneuern von verbundzertifikaten für Office 365 und Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs)
2. Sie werden nicht die legacyauthentifizierung Flows (z. B. ExO-Proxy Authentication Flow) nutzen können

### <a name="what-are-load-balancing-requirements-for-ad-fs-and-wap-servers"></a>Was sind Lastenausgleich lastanforderungen für AD FS und WAP-Server?

AD FS ist einem zustandslosen System. Daher ist des Lastenausgleichs für Anmeldungen recht einfach. Im folgenden werden die wichtigsten Empfehlungen für den Lastenausgleich von Systemen.


- Load Balancer sollte nicht mit der IP-Affinität konfiguriert werden. Dies kann unrechtmäßigen auf eine Teilmenge Ihrer Server in bestimmten Szenarien mit Exchange Online belasten.
- Load Balancer müssen nicht die HTTPS-Verbindungen zu beenden und initiieren Sie eine neue Verbindung mit dem ADFS-Server erneut.
- Lastenausgleichsmodule sorgen dafür, dass sich die IP-Adresse als die Quell-IP in der HTTP-Paket übersetzt werden soll, wenn AD FS gesendet werden. Wenn ein Lastenausgleich die Quell-IP in der HTTP-Paket senden kann, muss der Load Balancer hinzufügen (oder bei einem vorhandenen anfügen) die IP-Adresse für den X-forwarded-for-Header. Dies ist erforderlich, für die richtige Verarbeitung von bestimmten IP-bezogene Features (gesperrter IP-Adressen, Extranet Smart Lockout,...) und kann zur reduzierten Sicherheit nicht ordnungsgemäß konfiguriert.
- Load Balancer sollte SNI unterstützen. In der ereignismeldung nicht der Fall, stellen Sie sicher, dass AD FS für die HTTPS-Bindungen, um keine SNI-fähige Clients verarbeiten Erstellung konfiguriert ist.
- Load Balancer sollten erkennen, wenn die AD FS oder WAP-Server ausgeführt werden, und sie ausschließen, wenn eine 200 OK wird nicht zurückgegeben, die AD FS-HTTP-Endpunkt für Integritätstests verwenden.

### <a name="what-multi-forest-configurations-are-supported-by-ad-fs"></a>Welche Konfigurationen mit mehreren Gesamtstrukturen werden von AD FS unterstützt?

AD FS unterstützt die Konfiguration mit mehreren mit mehreren Gesamtstrukturen und basiert auf dem zugrunde liegenden AD DS-Trust-Netzwerk zum Authentifizieren von Benutzern in mehreren vertrauenswürdigen Bereichen. Wir empfehlen dringend die 2-Wege, Gesamtstrukturvertrauensstellungen, da es sich handelt es sich um ein einfacheres Setup aus, um sicherzustellen, dass die vertrauenswürdigen Subsystem ohne Probleme funktioniert. Darüber hinaus

- Im Falle eine unidirektionale Gesamtstruktur-Vertrauensstellung wie z. B. eine DMZ-Gesamtstruktur, die mit der partneridentitäten empfehlen wir, Bereitstellen von AD FS in der corp-Gesamtstruktur, und zum Behandeln der DMZ-Gesamtstruktur als einen anderen lokalen Anspruchsanbieter-Vertrauensstellung über LDAP verbunden. In diesem Fall Windows integrierte Authentifizierung funktioniert nicht für die Benutzer der DMZ-Gesamtstruktur, und sie werden aufgefordert, das Kennwort-Authentifizierung ausgeführt werden, da dies der einzige unterstützte Mechanismus für LDAP ist. Den Fall, dass Sie diese Option können nicht zu verfolgen, müssten Sie zu einer anderen AD FS einrichten, in der DMZ-Gesamtstruktur hinzuzufügen, die als Anspruchsanbieter-Vertrauensstellung in der AD FS in der corp-Gesamtstruktur. Benutzer müssen auf der Registerkarte Home Realm Discovery, HDR, aber sowohl die integrierte Windows-Authentifizierung als auch die Kennwort-Authentifizierung funktionieren. Stellen Sie entsprechende Änderungen in den Regeln für die anspruchsausstellung in AD FS in DMZ Gesamtstruktur fest, wie AD FS in der corp-Gesamtstruktur nicht zusätzliche Benutzerinformationen über den Benutzer aus der DMZ-Gesamtstruktur abrufen kann.
- Während Vertrauensstellungen auf domäneneben werden unterstützt, und arbeiten können, empfehlen wir ausdrücklich eine Gesamtstruktur-Vertrauensstellung auf Gesamtstrukturebene-Modell zu verschieben. Darüber hinaus müssen Sie sicherstellen, dass der UPN routing und NetBIOS-namensauflösung mit den Namen der müssen korrekt arbeiten.



## <a name="design"></a>Entwurf

### <a name="what-third-party-multi-factor-authentication-providers-are-available-for-ad-fs"></a>Welche Multi-Factor Authentication-Anbieter von Drittanbietern sind für AD FS verfügbar?
Es folgt eine Liste von Drittanbietern, die, denen wir bekannt sind.  Möglicherweise gibt es immer Anbieter verfügbar, die wir nicht zu kennen, und wir lernen Sie die Liste aktualisieren.

- [Gemalto Identitäts- & Sicherheitsdienste](http://www.gemalto.com/identity)
- [InWebo Enterprise Authentication-Dienst](http://www.inwebo.com/)
- [Login People MFA-API-connector](https://www.loginpeople.com)
- [RSA SecurID-Authentifizierung-Agent für Microsoft Active Directory-Verbunddienste](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)
- [SafeNet-Authentifizierung (SAS)-Dienst-Agent für AD FS](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)
- [Swisscom Mobile-ID-Authentifizierungsdienst](http://swisscom.ch/mid)
- [Symantec-Überprüfung und ID-Schutzdienst (VIP)](http://www.symantec.com/vip-authentication-service)

### <a name="are-third-party-proxies-supported-with-ad-fs"></a>Sind Drittanbieter-Proxys mit AD FS unterstützt?
Ja, Drittanbieter-Proxys platziert werden können, vor der Web Application Proxy, sondern muss jeden beliebigen Proxy von Drittanbietern unterstützen die [MS-ADFSPIP Protokoll](https://msdn.microsoft.com/library/dn392811.aspx) anstelle der Web Application Proxy verwendet wird.

### <a name="what-third-party-proxies-are-available-for-ad-fs-that-support-ms-adfspip"></a>Welche Drittanbieter-Proxys für AD FS verfügbar sind, die MS-ADFSPIP unterstützen?

Es folgt eine Liste von Drittanbietern, die, denen wir bekannt sind.  Möglicherweise gibt es immer Anbieter verfügbar, die wir nicht zu kennen, und wir lernen Sie die Liste aktualisieren.

- [F5 Access Policy Manager](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-third-party-integration-13-1-0/12.html#guid-1ee8fbb3-1b33-4982-8bb3-05ae6868d9ee)

### <a name="where-is-the-capacity-planning-sizing-spreadsheet-for-ad-fs-2016"></a>Wo ist die Kapazität Arbeitsblatt zur Dimensionierung für AD FS 2016 planen?
Die AD FS 2016-Version des Arbeitsblatts kann heruntergeladen werden [hier](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx).
Dies kann auch für AD FS in Windows Server 2012 R2 verwendet werden.

### <a name="how-can-i-ensure-my-ad-fs-and-wap-servers-support-apples-atp-requirements"></a>Wie kann ich meine AD FS und WAP-Server-Unterstützung von Apple ATP Anforderungen sicherstellen?

Apple hat einen Satz von Anforderungen, die Namen der App Transport Security (ATS), die Aufrufe von iOS-apps beeinträchtigen können, die mit AD FS authentifizieren.  Sie können sicherstellen, dass Ihre AD FS und WAP-Servern entsprechen, indem Sie sicherstellen, dass sie unterstützen die [Anforderungen für die Verbindung mithilfe von ATS](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57).  
Insbesondere sollten Sie sicherstellen, dass Ihre AD FS und WAP-Server TLS 1.2-Unterstützung und ausgehandelten Verschlüsselungssammlung der TLS-Verbindung mit perfect forward Secrecy unterstützt wird.

Sie aktivieren und Deaktivieren von SSL 2.0 und 3.0 und TLS-Versionen 1.0, 1.1 und 1.2 mit [Verwalten von SSL-Protokolle in AD FS](../operations/Manage-SSL-Protocols-in-AD-FS.md).

Um sicherzustellen, dass Ihre AD FS und WAP Server aushandeln nur TLS-Verschlüsselungssammlungen, die ATP unterstützen möchten, können Sie alle Verschlüsselungssammlungen, die nicht in Deaktivieren der [Liste von ATP-kompatible Verschlüsselungssammlungen](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57).  Verwenden Sie hierzu die [Windows TLS-PowerShell-Cmdlets](https://technet.microsoft.com/itpro/powershell/windows/tls/index).

## <a name="developer"></a>Entwickler

### <a name="when-generating-an-idtoken-with-adfs-for-a-user-authenticated-against-ad-how-is-the-sub-claim-generated-in-the-idtoken"></a>Zur Erstellung eines Benutzers authentifiziert AD ein ID-Token mit AD FS ist der Anspruch "sub" wie im ID-Token werden generiert?
Der Wert des Anspruchs mit "Sub" ist der Hash des Client-ID + Anker Anspruchswert.

### <a name="what-is-the-lifetime-of-the-refresh-tokenaccess-token-when-the-user-logs-in-via-a-remote-claims-provider-trust-over-ws-fedsaml-p"></a>Was ist die Lebensdauer des aktualisierungstokens Token/Zugriff, bei der Anmeldung des Benutzers über eine remote-Anspruchsanbieter-Vertrauensstellung über WS-Fed/SAML-P?
Die Lebensdauer der Aktualisierungstoken werden die Lebensdauer des Tokens, die AD FS vom remote-Anspruchsanbieter-Vertrauensstellung erhalten haben. Die Lebensdauer des Zugriffstokens werden die Lebensdauer des Tokens der vertrauenden Seite für die Zugriffstoken ausgestellt wird.

### <a name="i-need-to-return-profile-and-email-scopes-as-well-in-addition-to-the-openid-scope-can-i-obtain-additional-information-using-scopes-how-to-do-it-in-ad-fs"></a>Ich möchte Profil und e-Mail-Bereiche sowie zusätzlich zu den OpenId-Bereich zurück. Erhalte ich weitere Informationen, die Verwendung von Bereichen? Wie in der AD FS?
Sie können benutzerdefinierte ID-Token verwenden, relevante Informationen in das ID-Token hinzufügen. Weitere Informationen finden Sie im Artikel [Anpassen von Ansprüchen in ID-Token an](../development/Custom-Id-Tokens-in-AD-FS.md).

### <a name="how-to-issue-json-blobs-inside-jwt-tokens"></a>Wie Sie Json-Blobs im JWT-Token zu stellen?
Eine spezielle ValueType ("http://www.w3.org/2001/XMLSchema#json") und character(\x22) Escapezeichen zu versehen, dies in AD FS 2016 hinzugefügt wurde. Führen Sie im folgenden Beispiel für die Regel für die Ausstellung und auch die endgültige Ausgabe aus dem Zugriffstoken aus.

Beispielregel für Ausstellung:

    => issue(Type = "array_in_json", ValueType = "http://www.w3.org/2001/XMLSchema#json", Value = "{\x22Items\x22:[{\x22Name\x22:\x22Apple\x22,\x22Price\x22:12.3},{\x22Name\x22:\x22Grape\x22,\x22Price\x22:3.21}],\x22Date\x22:\x2221/11/2010\x22}");

-Anspruch in Zugriffstoken ausgestellt:

    "array_in_json":{"Items":[{"Name":"Apple","Price":12.3},{"Name":"Grape","Price":3.21}],"Date":"21/11/2010"}

### <a name="can-i-pass-resource-value-as-part-of-the-scope-value-like-how-requests-are-done-against-azure-ad"></a>Kann ich übergeben Ressourcenwert als Teil des Bereichswerts wie wie Anforderungen für Azure AD erfolgen?
Mit AD FS-Server 2019 können Sie jetzt in der Parameter "Scope" eingebetteten Ressourcenwert übergeben. Der Parameter "Scope" kann jetzt als eine durch Leerzeichen getrennte Liste organisiert werden, in dem jeder Eintrag Struktur als Ressourcenbereich/ist. Zum Beispiel  
**< erstellen Sie eine gültige beispielanforderung >**

### <a name="does-ad-fs-support-pkce-extension"></a>Unterstützt AD FS PKCE-Erweiterung?
AD FS-Server 2019 unterstützt Proof Key für Code Exchange (PKCE) für OAuth Authorization Code Grant-flow

### <a name="what-permitted-scopes-are-supported-by-ad-fs"></a>Welche zulässigen Bereiche werden von AD FS unterstützt?
- Aza – Wenn [OAuth 2.0-Protokoll-Erweiterungen für Broker-Clients](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-oapxbc/2f7d8875-0383-4058-956d-2fb216b44706) und wenn der Parameter "Scope" Bereich "Aza" enthält, wird der Server gibt ein neues primäre Aktualisierungstoken und wird im Feld Aktualisierungstoken aus, der die Antwort sowie die Einstellung das Feld Refresh_token_expires_in die Lebensdauer des neuen primären aktualisierungstokens, das eine wird erzwungen.
- OpenID - Anwendung für die Verwendung des OpenID Connect Authorization-Protokolls anfordern können.
- Logon_cert --Bereich Logon_cert kann eine Anwendung anfordern Anmeldung von Zertifikaten, die authentifizierte Benutzer interaktiv anmelden verwendet werden kann. AD FS-Server, den Access_token-Parameter aus der Antwort ausgelassen und stattdessen bieten Sie eine base64-codierte CMS-Zertifikatkette oder einer vollständigen CMC-PKI-Antwort. Weitere Informationen zur Verfügung [hier](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-oapx/32ce8878-7d33-4c02-818b-6c9164cc731e). 
- "user_impersonation" - ist der Bereich "user_impersonation" erforderlich, um ein im-Auftrag-von-Zugriffstoken erfolgreich von AD FS anzufordern. Informationen zur Verwendung von diesem Bereich finden Sie unter [Erstellen einer Multi-Tier-Anwendung, die im-Auftrag (OBO) mithilfe von OAuth in AD FS 2016 mit](../../ad-fs/development/ad-fs-on-behalf-of-authentication-in-windows-server.md).
- Vpn_cert - ermöglicht der Vpn_cert Bereich einer Anwendung, Anforderung-VPN-Clientzertifikate, die verwendet werden kann, um VPN-Verbindungen mithilfe von EAP-TLS-Authentifizierung herzustellen. Dies wird nicht mehr unterstützt.
- e-Mail - Anwendung für die e-Mail-Anspruch für den angemeldeten Benutzer anfordern können. Dies wird nicht mehr unterstützt. 
- Profil - ermöglicht die Anwendung für die Anforderung im Zusammenhang Ansprüche für den Benutzer anmelden. Dies wird nicht mehr unterstützt. 


## <a name="operations"></a>Vorgänge

### <a name="how-do-i-replace-the-ssl-certificate-for-ad-fs"></a>Wie ersetzen ich das SSL-Zertifikat für AD FS?
Das AD FS-SSL-Zertifikat ist nicht identisch mit AD FS dienstkommunikationszertifikat finden Sie in das AD FS-Verwaltungs-Snap-in.  Um das AD FS-SSL-Zertifikat zu ändern, müssen Sie PowerShell verwenden. Führen Sie die Anweisungen in der folgenden Artikel:

[Verwalten von SSL-Zertifikaten in AD FS und WAP 2016](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)

### <a name="how-can-i-enable-or-disable-tlsssl-settings-for-ad-fs"></a>Wie kann ich zu aktivieren oder Deaktivieren von TLS/SSL-Einstellungen für AD FS
Verwenden Sie zum Deaktivieren oder aktivieren Sie die SSL-Protokolle und Verschlüsselungssammlungen, folgende Schritte aus:

[Verwalten von SSL-Protokolle in AD FS](../operations/Manage-SSL-Protocols-in-AD-FS.md)

### <a name="does-the-proxy-ssl-certificate-have-to-be-the-same-as-the-ad-fs-ssl-certificate"></a>Muss das SSL-Zertifikat des AD FS-SSL-Zertifikats übereinstimmen?  
Verwenden Sie die folgende Anleitungen in Bezug auf die SSL-Zertifikat und das AD FS-SSL-Zertifikat:


- Wenn der Proxy, um verwendet wird müssen AD FS-Proxy für Anforderungen, die integrierte Windows-Authentifizierung, die SSL-Zertifikat verwenden identisch sein (verwenden Sie den gleichen Schlüssel) als Verbund-Server SSL-Zertifikat
- Wenn die AD FS-Eigenschaft, die "ExtendedProtectionTokenCheck" ist (die Standardeinstellung bei AD FS) aktiviert, muss die SSL-Zertifikat identisch sein (verwenden Sie den gleichen Schlüssel) als Verbund-Server SSL-Zertifikat
- Andernfalls die SSL-Zertifikat kann über einen anderen Schlüssel aus dem AD FS-SSL-Zertifikat verfügen, aber erfüllt die gleiche [Anforderungen](../overview/AD-FS-2016-Requirements.md)

### <a name="how-can-i-configure-promptlogin-behavior-for-ad-fs"></a>Wie kann ich konfigurieren Prompt = Login-Verhalten für AD FS?
Informationen zum Konfigurieren der Eingabeaufforderung = Anmeldung finden Sie unter [Active Directory Federation Services auffordern = der Anmeldename die parameterunterstützung](../operations/AD-FS-Prompt-Login.md).

### <a name="how-can-i-change-the-ad-fs-service-account"></a>Wie kann ich das AD FS-Dienstkonto ändern?
Führen Sie die Anweisungen, die mit der AD FS-Toolbox, um die AD FS-Dienstkonto zu ändern, [Powershell-Modul für Service-Konto](https://github.com/Microsoft/adfsToolbox/tree/master/serviceAccountModule). 

### <a name="how-can-i-configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>Wie kann ich Windows integrierte Authentifizierung (WIA) mit AD FS Verwendung durch Browser konfigurieren?

Informationen zum Konfigurieren von Browsern finden Sie unter [Browser, um die Verwendung von Windows integrierte Authentifizierung (WIA) mit AD FS konfigurieren](../operations/Configure-AD-FS-Browser-WIA.md).

### <a name="can-i-trun-off-browserssoenabled"></a>Kann ich schalten Sie BrowserSsoEnabled?
Wenn Sie nicht über Richtlinien für die Zugriffssteuerung basierend auf dem Gerät auf die AD FS oder Windows Hello für Business-zertifikatregistrierung mithilfe von ADFS verfügen; Sie können die BrowserSsoEnabled deaktivieren. BrowserSsoEnabled kann AD FS eine PRT (Primary Refresh Token) vom Client zu sammeln der Geräteinformationen enthält. Ohne das Gerät funktioniert nicht auf Windows 10-Geräten Authentifizierung von AD FS.

### <a name="how-long-are-ad-fs-tokens-valid"></a>Wie lange werden die AD FS-Token ist gültig?

Häufig bedeutet, dass diese Frage "wie lange Benutzer erhalte einmalige Anmelden (SSO) ohne neue Anmeldeinformationen eingeben zu müssen und wie kann ich als Administrator steuern,?"  Dieses Verhalten und die Konfigurationseinstellungen, die steuern, werden in diesem Artikel beschrieben [AD FS Sign-Einstellungen für einmaliges](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-2016-single-sign-on-settings).

Die Standardgültigkeitsdauer von den verschiedenen Cookies und Token sind nachfolgend aufgeführt, (sowie die Parameter, die steuern, die Lebensdauer):

**Registrierte Geräte**

- PRT und SSO-Cookies: bis 90 Tage, PSSOLifeTimeMins unterliegt. (Bereitgestellte Gerät mindestens alle 14 Tage verwendet die von DeviceUsageWindow gesteuert wird)

- Aktualisierungstoken: berechnet auf Grundlage des obigen in konsistentes Verhalten bereitzustellen.

- access_token: 1 Stunde standardmäßig basierend auf die vertrauende Seite

- ID-Token: identisch mit dem Zugriffstoken

**Nicht registrierte Geräte**

- SSO-Cookies: 8 Stunden in der Standardeinstellung SSOLifetimeMins unterliegen.  Wenn bleiben angemeldet ("angemeldet bleiben") aktiviert ist, Standardwert ist 24 Stunden und kann über KMSILifetimeMins konfiguriert.


- Aktualisierungstoken: standardmäßig acht Stunden. 24 Stunden mit "angemeldet bleiben" aktiviert

- access_token: 1 Stunde standardmäßig basierend auf die vertrauende Seite

- ID-Token: identisch mit dem Zugriffstoken

### <a name="does-ad-fs-support-http-strict-transport-security-hsts"></a>Unterstützt AD FS HTTP Strict Transport Security (HSTS)?  

HTTP Strict Transport Security (HSTS) ist ein Web-Richtlinie Sicherheitsmechanismus wodurch zu verringern, Protokoll Downgrade-Angriffe und Cookie-Hijacking für Dienste, die HTTP- und HTTPS-Endpunkte haben. Sie können Webserver deklarieren, dass der Webbrowser (oder anderen leitete Benutzer-Agents) nur mithilfe von HTTPS und nie über das HTTP-Protokoll interagieren müssen.

Alle AD FS-Endpunkte für die Authentifizierung von Webverkehr werden ausschließlich über HTTPS geöffnet.  AD FS werden daher effektiv die Risiken, die HTTP Strict Transport Security richtlinienmechanismus bereitstellt (ist es kein Downgrade auf HTTP da es sich um keine Listener in HTTP). Darüber hinaus verhindert, dass AD FS die Cookies, die auf einen anderen Server mit HTTP-Protokoll-Endpunkten gesendet werden, indem Sie alle Cookies mit dem sicheren Flag markiert.

Aus diesem Grund ist die Implementierung von HSTS auf AD FS-Server nicht erforderlich, da es nie herabgestuft werden kann.  Zur Einhaltung von Vorschriften erfüllt die AD FS-Server diese Anforderungen können nie HTTP und alle Cookies werden als sicher markiert.

### <a name="x-ms-forwarded-client-ip-does-not-contain-the-ip-of-the-client-but-contains-ip-of-the-firewall-in-front-of-the-proxy-where-can-i-get-the-right-ip-of-the-client"></a>X-ms-forwarded-Client-Ip enthält nicht die IP-Adresse des Clients jedoch IP-Adresse der Firewall vor dem Proxy enthält. Wo erhalte ich die richtige IP-Adresse des Clients?
Es wird nicht empfohlen, vor dem WAP-SSL-Beendigung zu tun. Für den Fall, dass Sie vor der WAP SSL-Beendigung abgeschlossen ist, wird die X-ms-weitergeleitet-Client-IP-Adresse die IP-Adresse des Netzwerkgeräts vor WAP enthalten. Im folgenden finden Sie wahrscheinlich nicht durch eine kurze Beschreibung der verschiedenen IP-Ansprüche, die von AD FS unterstützt werden:
 - X-ms-Client-Ip: Netzwerk-IP-Adresse des Geräts, das Verbindung mit dem STS.  Im Fall von einer extranet-Anforderung enthält immer die IP-Adresse der WAP.
 - X-ms-forwarded-Client-Ip: Mehrwertigen Anspruch enthält alle Werte, die AD FS von Exchange Online sowie die IP-Adresse des Geräts, das Verbindung mit dem drahtlosen Zugriffspunkt weitergeleitet.
 - Userip: Dieser Anspruch wird den Wert der X-ms-forwarded-Client-Ip enthalten, für extranet-Anforderungen.  Für Intranet-Anforderungen wird dieser Anspruch auf den gleichen Wert wie X-ms-Client-Ip enthalten.

### <a name="i-am-trying-to-get-additional-claims-on-the-user-info-endpoint-but-its-only-returning-subject-how-can-i-get-additional-claims"></a>Ich versuche, um zusätzliche Ansprüche auf UserInfo-Endpoint, aber die einzige zurückgeben Betreff zu erhalten. Wie erhalte ich weitere Ansprüche?
Der AD FS-Userinfo-Endpunkt gibt immer den Anspruch "Antragsteller" gemäß den Standards OpenID zurück. AD FS bietet keine zusätzliche Ansprüche, die über den UserInfo-Endpunkt angefordert. Wenn Sie zusätzliche Ansprüche in ID-Token benötigen, finden Sie unter [benutzerdefinierte ID-Token in AD FS](../development/custom-id-tokens-in-ad-fs.md).

### <a name="why-do-i-see-a-lot-of-1021-errors-on-my-ad-fs-servers"></a>Warum sehe ich auf meinen AD FS-Servern viele 1021 Fehler?
Dieses Ereignis wird in der Regel für eine ungültige Ressource den Zugriff auf AD FS für die Ressource 00000003-0000-0000-c000-000000000000 protokolliert. Dieser Fehler wird durch eine fehlerhafte Verhalten des Clients verursacht, in denen versucht wird, ein Zugriffstoken für den Azure AD Graph-Dienst abzurufen. Da die Ressource nicht in AD FS vorhanden ist, führt dies im Ereignis-ID 1021 auf AD FS-Servern. Es ist sicher keine Warnungen oder Fehler für Ressourcen 00000003-0000-0000-c000-000000000000 in AD FS ignoriert werden sollen.

### <a name="why-am-i-seeing-a-warning-for-failure-to-add-the-ad-fs-service-account-to-the-enterprise-key-admins-group"></a>Warum sehe ich eine Warnung für Fehler beim Hinzufügen der AD FS-Dienstkonto der Gruppe der Unternehmensadministratoren-Schlüssel?
Diese Gruppe wird nur erstellt, wenn ein Windows-2016-Domänencontroller mit die FSMO-PDC-Rolle in der Domäne vorhanden ist. Um den Fehler zu beheben, können Sie die Gruppe manuell erstellen und befolgen Sie die unten, um die erforderliche Berechtigung nach dem Hinzufügen des Dienstkontos als Mitglied der Gruppe erhalten.
1.  Öffnen Sie **Active Directory-Benutzer und -Computer**.
2.  **Mit der rechten Maustaste** Ihren Domänennamen im Navigationsbereich und **klicken Sie auf** Eigenschaften.
3.  **Klicken Sie auf** Sicherheit (wenn die Registerkarte "Sicherheit" nicht vorhanden ist, aktivieren Sie erweiterte Funktionen aus dem Menü "Ansicht").
4.  **Klicken Sie auf** erweitert. **Klicken Sie auf** hinzufügen. **Klicken Sie auf** Prinzipal auswählen.
5.  Das Dialogfeld Benutzer, Computer, Dienstkonto oder Gruppe angezeigt wird.  Geben Sie im Feld Geben Sie den Objektnamen ein Textfeld Schlüssel-Administratorgruppe.  Klicken Sie auf „OK“.
6.  Wählen Sie in das Listenfeld, **untergeordnete Benutzerobjekte**.
7.  Verwenden die Bildlaufleiste, scrollen Sie zum unteren Rand der Seite und **klicken Sie auf** Auswahl aufheben.
8.  In der **Eigenschaften** wählen Sie im Abschnitt **MsDS-KeyCredentialLink lesen** und **schreiben MsDS-KeyCredentialLink**.

### <a name="why-does-modern-authentication-from-android-devices-fail-if-the-server-does-not-send-all-the-intermediate-certificates-in-the-chain-with-the-ssl-cert"></a>Warum misslingt die moderner Authentifizierung auf Android-Geräten nicht, wenn der Server nicht alle Zwischenzertifikate in der Kette mit der SSL-Zertifikat sendet?

Verbundbenutzer können Authentifizierung an Azure AD für apps auftreten, die die Android-ADAL-Bibliothek fehlerhaften verwenden. Die app erhält ein **AuthenticationException** wenn er versucht, die Anmeldeseite angezeigt. In Chrome die AD FS kann Anmeldeseite als unsicher hingewiesen.

Android – für alle Versionen und alle Geräte: unterstützt nicht heruntergeladen zusätzliche Zertifikate aus dem **AuthorityInformationAccess** Feld des Zertifikats. Dies gilt auch den Chrome-Browser. Alle-Authentifizierung-Serverauthentifizierungszertifikat, das Fehlen der Zwischenzertifizierungsstellen-Zertifikate führt zu diesem Fehler, wenn die gesamte Zertifikatkette nicht von AD FS übergeben wird.

Eine richtige Lösung für dieses Problem wird so konfigurieren Sie die AD FS und WAP-Server, um die erforderlichen Zwischenzertifikate zusammen mit dem SSL-Zertifikat zu senden.

Achten Sie beim Exportieren des SSL-Zertifikats von einem Computer, auf dem persönlichen Speicher, der die AD FS und WAP-Servern, des Computers importiert werden Sie darauf, exportieren den privaten Schlüssel, und wählen **privater Informationsaustausch – PKCS #12**.

Es ist wichtig, dass das Kontrollkästchen zum **möglichst alle Zertifikate im Zertifizierungspfad einbeziehen** aktiviert ist, als auch **alle erweiterten Eigenschaften exportieren**.  

Führen Sie "certlm.msc" auf den Windows-Servern und importieren Sie die *. PFX in persönlichen Zertifikatspeicher des Computers. Dies bewirkt, dass den Server die gesamte Zertifikatkette an die ADAL-Bibliothek zu übergeben.

>[!NOTE]
> Die Zertifikat-Speicher von Netzwerk-Load Balancer sollte ebenfalls aktualisiert und umfassen die gesamte Zertifikatkette, falls vorhanden

### <a name="does-ad-fs-support-head-requests"></a>Unterstützt HEAD-Anforderungen werden von AD FS?
AD FS unterstützt nicht die HEAD-Anforderungen.  Anwendungen sollten nicht HEAD-Anforderungen für AD FS-Endpunkte verwendet werden.  Dies verursacht möglicherweise HTTP-Fehlerseiten, die unerwartete und/oder verzögert werden.  Darüber hinaus möglicherweise unerwartete Fehlerereignisse in das AD FS-Ereignisprotokoll angezeigt.

### <a name="why-am-i-not-seeing-a-refresh-token-when-i-am-logging-in-with-a-remote-idp"></a>Warum angezeigt ich kein Aktualisierungstoken wird, wenn ich mit einem remote-Identitätsanbieter werde?
Ein Aktualisierungstoken wird nicht ausgegeben, wenn das vom Identitätsanbieter ausgestellte Token einen Validty von weniger als einer Stunde verfügt. Um sicherzustellen, dass ein Aktualisierungstoken ausgegeben wird, erhöhen Sie die Gültigkeit des Tokens, die vom Identitätsanbieter ausgestellt werden, auf mehr als 1 Stunde.

### <a name="do-we-have-any-way-to-change-rp-token-encryption-algorithm"></a>Haben wir eine Möglichkeit, die RP-token-Verschlüsselungsalgorithmus ändern?
Standardmäßig ist die Verschlüsselung von token der vertrauenden Seite, AES256 festgelegt und kann nicht auf einen anderen Wert geändert werden.

### <a name="on-a-mixed-mode-farm-i-get-error-when-trying-to-set-the-new-ssl-certificate-using-set-adfssslcertificate--thumbprint-how-can-i-update-the-ssl-certificate-in-a-mixed-mode-ad-fs-farm"></a>In einer Farm im gemischten Modus Fehlermeldung beim Versuch, legen Sie das neue SSL-Zertifikat mithilfe der Set-AdfsSslCertificate-Thumbprint. Wie kann ich die SSL-Zertifikat in einem AD FS-Farm im gemischten Modus aktualisieren?
Für WAP-Server können Sie die Set-WebApplicationProxySslCertificate weiterhin verwenden. Auf den AD FS-Servern müssen Sie Netsh verwenden. Gehen Sie wie folgt:

1. Wählen Sie die Teilmenge der AD FS 2016-Server für die Wartung (z. B. aus dem Load Balancer entfernen)
2. Importieren Sie auf den Servern in #1 ausgewählt haben das neue Zertifikat über MMC
3. Löschen Sie die vorhandenen Zertifikate

    a. netsh http delete sslcert hostnameport=fs.contoso.com:443 b. netsh http delete sslcert hostnameport=localhost:443 c. Netsh http Delete Sslcert hostnameport=fs.contoso.com:49443

4.  Fügen Sie das neue Zertifikat hinzu.

    a. Netsh http hinzufügen Sslcert hostnameport=fs.contoso.com:443 Certhash = CERTTHUMBPRINT Appid = {5d89a20c-beab-4389-9447-324788eb944a} Certstorename = Meine Sslctlstorename AdfsTrustedDevices =

    b. Netsh http hinzufügen Sslcert Hostnameport = Localhost:443 Certhash CERTTHUMBPRINT Appid = {5d89a20c-beab-4389-9447-324788eb944a} Certstorename = = Meine Sslctlstorename AdfsTrustedDevices =

    c. Netsh http hinzufügen Sslcert hostnameport=fs.contoso.com:49443 Certhash = CERTTHUMBPRINT Appid = {5d89a20c-beab-4389-9447-324788eb944a} Certstorename = Meine Sslctlstorename AdfsTrustedDevices =

5. AD FS-Dienst auf dem ausgewählten Server neu starten
6. Entfernen Sie die Teilmenge der WAP-Server für die Wartung
7. Importieren Sie auf den ausgewählten WAP-Servern das neue Zertifikat über MMC
8. Legen Sie das neue Zertifikat für WAP, die mithilfe von Cmdlets

    a. Set-WebApplicationProxySslCertificate-Fingerabdruck "CERTTHUMBPRINT"

9. Dienst für die ausgewählte WAP-Server neu starten
10. Fügen Sie die ausgewählten WAP und AD FS-Server wieder in die produktionsumgebung.

Führen Sie das Update auf dem Rest der AD FS und WAP-Server, auf ähnliche Weise.

### <a name="is-adfs-supported-when-web-application-proxy-wap-servers-are-behind-azure-web-application-firewallwaf"></a>Werden AD FS wird unterstützt, wenn der Web Application Proxy (WAP)-Server hinter dem Azure-Web-Anwendung Firewall(WAF) sind?
AD FS und Web Application-Server unterstützt Firewall, die keine SSL-Tunnelabschluss für den Endpunkt durchführt. Darüber hinaus AD FS/WAP-Servern über eine integrierte Mechanismen, um zu verhindern, dass allgemeinen Webangriffen wie z. B. Cross-Site scripting, AD FS-Proxy und erfüllen alle Anforderungen von definiert die [MS-ADFSPIP Protokoll](https://msdn.microsoft.com/library/dn392811.aspx).
