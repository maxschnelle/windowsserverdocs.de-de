---
ms.assetid: acc9101b-841c-4540-8b3c-62a53869ef7a
title: FAQ ZU AD FS
description: Häufig gestellte Fragen zu AD FS
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 04/17/2019
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 46e8548e24f0d0991f69427741b0e04da6398334
ms.sourcegitcommit: 4fa147d552481d8279a5390f458a9f7788061977
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/23/2019
ms.locfileid: "70009094"
---
# <a name="ad-fs-frequently-asked-questions-faq"></a>AD FS häufig gestellte Fragen (FAQ)


In der folgenden Dokumentation finden Sie Informationen zu häufig gestellten Fragen im Zusammenhang mit Active Directory-Verbunddienste (AD FS).  Das Dokument wurde basierend auf der Art der Frage in Gruppen aufgeteilt.

## <a name="deployment"></a>Bereitstellung

### <a name="how-can-i-upgrademigrate-from-previous-versions-of-ad-fs"></a>Wie kann ich ein Upgrade/eine Migration von früheren Versionen von AD FS
Sie können AD FS mithilfe einer der folgenden Aktionen Aktualisieren:


- Windows Server 2012 R2 AD FS zu Windows Server 2016 AD FS oder höher. Beachten Sie, dass die Methodik identisch ist, wenn Sie von Windows Server 2016 AD FS auf Windows Server 2019 AD FS aktualisieren. 
    - [Aktualisieren auf AD FS unter Windows Server 2016 unter Verwendung einer WID-Datenbank](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)
    - [Aktualisieren auf AD FS unter Windows Server 2016 unter Verwendung einer SQL-Datenbank](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL.md)
- Windows Server 2012 AD FS zu Windows Server 2012 R2 AD FS
    - [Migrieren zu AD FS unter Windows Server 2012 R2](https://technet.microsoft.com/library/dn486815.aspx)
- AD FS 2,0 zu Windows Server 2012 AD FS
    - [Migrieren zu AD FS unter Windows Server 2012](https://technet.microsoft.com/library/jj647765.aspx)
- AD FS 1. x auf AD FS 2,0
    - [Upgrade von AD FS 1. x auf AD FS 2,0](https://technet.microsoft.com/library/ff678035.aspx)

Wenn Sie ein Upgrade von AD FS 2,0 oder 2,1 (Windows Server 2008 R2 oder Windows Server 2012) ausführen müssen, müssen Sie die in-Box-Skripts (in c:\windows\adfs) verwenden.

### <a name="why-does-ad-fs-installation-require-a-reboot-of-the-server"></a>Warum ist für AD FS Installation ein Neustart des Servers erforderlich?

Die http/2-Unterstützung wurde in Windows Server 2016 hinzugefügt, aber http/2 kann nicht für die Client Zertifikat Authentifizierung verwendet werden.  Da viele AD FS Szenarios die Client Zertifikat Authentifizierung nutzen und eine große Anzahl von Clients das Wiederholen von Anforderungen mit HTTP/1.1 nicht unterstützt, werden bei AD FS Farm Konfiguration die http-Einstellungen des lokalen Servers auf HTTP/1.1 neu konfiguriert.  Dies erfordert einen Neustart des Servers.  

### <a name="is-using-windows-2016-wap-servers-to-publish-the-ad-fs-farm-to-the-internet-without-upgrading-the-back-end-ad-fs-farm-supported"></a>Werden Windows 2016-WAP-Server verwendet, um die AD FS-Farm im Internet zu veröffentlichen, ohne die Back-End-AD FS Farm zu aktualisieren?
Ja, diese Konfiguration wird unterstützt, es werden jedoch keine neuen AD FS 2016-Features in dieser Konfiguration unterstützt.  Diese Konfiguration soll während der Migrationsphase von AD FS 2012 R2 zu AD FS 2016 temporär sein und sollte nicht über einen längeren Zeitraum bereitgestellt werden.

### <a name="is-it-possible-to-deploy-ad-fs-for-office-365-without-publishing-a-proxy-to-office-365"></a>Ist es möglich, AD FS für Office 365 bereitzustellen, ohne einen Proxy für Office 365 zu veröffentlichen?
Ja, dies wird unterstützt. Als Nebeneffekt

1. Sie müssen die Aktualisierung von Tokensignaturzertifikaten manuell verwalten, da Azure AD nicht auf die Verbund Metadaten zugreifen kann. Weitere Informationen zum manuellen Aktualisieren des Tokensignaturzertifikats finden Sie unter [Erneuern von Verbund Zertifikaten für Office 365 und Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs)
2. Sie sind nicht in der Lage, ältere Authentifizierungs Abläufe (z. b. den Verlauf der ExO-Proxy Authentifizierung) zu nutzen.

### <a name="what-are-load-balancing-requirements-for-ad-fs-and-wap-servers"></a>Was sind Anforderungen an den Lastenausgleich für AD FS-und WAP-Server?

AD FS ist ein Zustands Loses System. Daher ist der Lastenausgleich für Anmeldungen recht einfach. Im folgenden finden Sie die wichtigsten Empfehlungen für Lasten Ausgleichssysteme.


- Lasten Ausgleichs Module sollten nicht mit IP-Affinität konfiguriert werden. Dadurch kann eine Teilmenge ihrer Server in bestimmten Exchange Online-Szenarios übermäßig geladen werden.
- Load Balancer dürfen die HTTPS-Verbindungen nicht beenden und eine neue Verbindung mit dem AD FS-Server erneut initiieren.
- Lasten Ausgleichs Module sollten sicherstellen, dass die IP-Adressen, die eine Verbindung herstellen, beim Senden an ADFS als Quell-IP im HTTP-Paket übersetzt werden. Wenn ein Lasten Ausgleichs Modul die Quell-IP-Adresse nicht im HTTP-Paket senden kann, muss der Load Balancer die IP-Adresse dem x-weitergeleiteten for-Header hinzufügen (oder bei vorhandener Anfügen). Dies ist für die korrekte Handhabung bestimmter IP-bezogener Features erforderlich (Verbotene IP-Adresse, extranetsmart Lockout-,...) und kann zu eingeschränkter Sicherheit führen, wenn diese nicht ordnungsgemäß konfiguriert ist.
- Lasten Ausgleichs Module sollten SNI unterstützen. Wenn dies nicht der Fall ist, stellen Sie sicher, dass AD FS so konfiguriert ist, dass HTTPS-Bindungen zur Behandlung von nicht SNI-fähigen Clients erstellt werden.
- Lasten Ausgleichs Module sollten den AD FS http-Integritätstest-Endpunkt verwenden, um zu ermitteln, ob die AD FS-oder WAP-Server ausgeführt werden und Sie ausschließen, wenn 200 OK nicht zurückgegeben wird.

### <a name="what-multi-forest-configurations-are-supported-by-ad-fs"></a>Welche Konfigurationen mit mehreren Gesamtstrukturen werden von AD FS unterstützt?

AD FS unterstützt eine Konfiguration mit mehreren Gesamtstrukturen und basiert auf dem zugrunde liegenden AD DS Vertrauensstellungs Netzwerk, um Benutzer über mehrere vertrauenswürdige Bereiche hinweg zu authentifizieren. Es wird dringend empfohlen, 2-Wege-Gesamtstrukturen Vertrauens Stellungen zu gewährleisten, da dies ein einfacheres Setup ist Verfügt

- Bei einer unidirektionalen Gesamtstruktur-Vertrauensstellung, z. b. einer DMZ-Gesamtstruktur, die Partner Identitäten enthält, empfiehlt es sich, ADFS in der Corp-Gesamtstruktur bereitzustellen und die DMZ-Gesamtstruktur als eine andere lokale Anspruchs Anbieter-Vertrauens In diesem Fall funktioniert die integrierte Windows-Authentifizierung für die Benutzer der DMZ-Gesamtstruktur nicht, und Sie müssen die Kenn Wort Authentifizierung durchführen, da dies der einzige unterstützte Mechanismus für LDAP ist. Wenn Sie diese Option nicht durchführen können, müssen Sie ein weiteres ADFS in der DMZ-Gesamtstruktur einrichten und dieses als Anspruchs Anbieter-Vertrauensstellung in den AD FS in der Corp-Gesamtstruktur hinzufügen. Benutzer müssen die Startbereichs Ermittlung durchführen, aber sowohl die integrierte Windows-Authentifizierung als auch die Kenn Wort Authentifizierung funktionieren. Nehmen Sie die entsprechenden Änderungen in den Ausstellungsregeln in ADFS in der DMZ-Gesamtstruktur vor, da ADFS in der Corp-Gesamtstruktur keine zusätzlichen Benutzerinformationen über den Benutzer aus der DMZ-Gesamtstruktur erhalten kann.
- Obwohl Vertrauens Stellungen auf Domänen Ebene unterstützt werden und funktionieren können, wird dringend empfohlen, zu einem Vertrauens Modell auf Gesamtstruktur Ebene zu wechseln. Außerdem müssen Sie sicherstellen, dass das UPN-Routing und die NetBIOS-Namensauflösung von Namen genau funktionieren müssen.



## <a name="design"></a>Entwurf

### <a name="what-third-party-multi-factor-authentication-providers-are-available-for-ad-fs"></a>Welche Multi-Factor Authentication-Anbieter von Drittanbietern sind für AD FS verfügbar?
AD FS bietet einen erweiterbaren Mechanismus für die Integration von Drittanbieter-MFA-Anbietern. Hierfür gibt es kein fest Geleges Zertifizierungsprogramm. Es wird davon ausgegangen, dass der Hersteller vor der Freigabe die erforderlichen Überprüfungen durchgeführt hat. 

Die Liste der Anbieter, die Microsoft benachrichtigt haben, wird bei [MFA-Anbietern für AD FS](../operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)veröffentlicht.  Möglicherweise sind immer Anbieter verfügbar, die wir nicht kennen, und wir aktualisieren die Liste, wie wir Sie darüber erfahren.

### <a name="are-third-party-proxies-supported-with-ad-fs"></a>Werden Drittanbieter Proxys mit AD FS unterstützt?
Ja, Proxys von Drittanbietern können vor dem webanwendungsproxy eingefügt werden, aber jeder Drittanbieter Proxy muss das [MS-adfspip-Protokoll](https://msdn.microsoft.com/library/dn392811.aspx) unterstützen, das anstelle des webanwendungsproxys verwendet werden soll.

Im folgenden finden Sie eine Liste der Anbieter von Drittanbietern, die wir kennen.  Möglicherweise sind immer Anbieter verfügbar, die wir nicht kennen, und wir aktualisieren die Liste, wie wir Sie darüber erfahren.

- [F5-Zugriffsrichtlinien-Manager](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-third-party-integration-13-1-0/12.html#guid-1ee8fbb3-1b33-4982-8bb3-05ae6868d9ee)


### <a name="where-is-the-capacity-planning-sizing-spreadsheet-for-ad-fs-2016"></a>Wo ist das Arbeitsblatt für die Kapazitäts Planungsgröße für AD FS 2016?
Die AD FS 2016-Version der Kalkulations Tabelle kann [hier](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)heruntergeladen werden.
Dies kann auch für AD FS in Windows Server 2012 R2 verwendet werden.

### <a name="how-can-i-ensure-my-ad-fs-and-wap-servers-support-apples-atp-requirements"></a>Wie stelle ich sicher, dass meine AD FS-und WAP-Server die ATP-Anforderungen von Apple unterstützen?

Apple hat eine Reihe von Anforderungen herausgegeben, die als App-Transport Sicherheit (app Transport Security, ATS) bezeichnet werden und AD FS sich auf Aufrufe von IOS-apps auswirken können, die  Sie können sicherstellen, dass Ihre AD FS-und WAP-Server einhalten, indem Sie sicherstellen, dass Sie die [Anforderungen zum Herstellen einer Verbindung über](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)  
Insbesondere sollten Sie überprüfen, ob die AD FS-und WAP-Server TLS 1,2 unterstützen und dass die ausgehandelte Verschlüsselungs Sammlung der TLS-Verbindung eine perfekte vorwärts Prüfung unterstützt.

Sie können SSL 2,0 und 3,0 und die TLS-Version 1,0, 1,1 und 1,2 aktivieren und deaktivieren, indem Sie [SSL-Protokolle in AD FS verwalten](../operations/Manage-SSL-Protocols-in-AD-FS.md).

Um sicherzustellen, dass Ihre AD FS-und WAP-Server nur TLS-Verschlüsselungs Sammlungen aushandeln, die ATP unterstützen, können Sie alle Verschlüsselungs Sammlungen deaktivieren, die nicht in der [Liste der mit ATP kompatiblen](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)Verschlüsselungs Sammlungen enthalten sind.  Verwenden Sie hierzu die Windows- [TLS-PowerShell-Cmdlets](https://technet.microsoft.com/itpro/powershell/windows/tls/index).

## <a name="developer"></a>Entwickler

### <a name="when-generating-an-id_token-with-adfs-for-a-user-authenticated-against-ad-how-is-the-sub-claim-generated-in-the-id_token"></a>Wie wird beim Generieren eines ID mit AD FS für einen Benutzer, der für AD authentifiziert ist, wie der Sub-Anspruch im ID generiert?
Der Wert des "Sub"-Anspruchs ist der Hash von Client-ID + Anker Anspruchs Wert.

### <a name="what-is-the-lifetime-of-the-refresh-tokenaccess-token-when-the-user-logs-in-via-a-remote-claims-provider-trust-over-ws-fedsaml-p"></a>Wie lange ist das Aktualisierungs Token/Zugriffs Token, wenn sich der Benutzer über eine Remote Anspruchs Anbieter-Vertrauensstellung über WS-Fed/SAML-P anmeldet?
Die Gültigkeitsdauer des Aktualisierungs Tokens ist die Lebensdauer des Tokens, das von ADFS von der Remote Anspruchs Anbieter-Vertrauensstellung erhalten wurde. Die Lebensdauer des Zugriffs Tokens ist die Tokengültigkeitsdauer der vertrauenden Seite, für die das Zugriffs Token ausgestellt wird.

### <a name="i-need-to-return-profile-and-email-scopes-as-well-in-addition-to-the-openid-scope-can-i-obtain-additional-information-using-scopes-how-to-do-it-in-ad-fs"></a>Zusätzlich zum OpenID-Bereich muss ich auch Profile-und e-Mail-Bereiche zurückgeben. Kann ich zusätzliche Informationen mithilfe von Bereichen abrufen? Wie gehen Sie in AD FS vor?
Sie können angepasste ID verwenden, um relevante Informationen in der ID selbst hinzuzufügen. Weitere Informationen finden [Sie im Artikel Anpassen von Anspruchs, die in ID ausgegeben werden](../development/Custom-Id-Tokens-in-AD-FS.md).

### <a name="how-to-issue-json-blobs-inside-jwt-tokens"></a>Wie werden JSON-blobblobzeichen in JWT-Token ausgestellt?
Ein spezieller ValueType ("<http://www.w3.org/2001/XMLSchema#json>") und ein Escapezeichen (\x22) wurden in AD FS 2016 hinzugefügt. Bitte das folgende Beispiel für die Ausstellungs Regel und auch die endgültige Ausgabe des Zugriffs Tokens.

Beispiel für eine Ausstellungs Regel:

    => issue(Type = "array_in_json", ValueType = "http://www.w3.org/2001/XMLSchema#json", Value = "{\x22Items\x22:[{\x22Name\x22:\x22Apple\x22,\x22Price\x22:12.3},{\x22Name\x22:\x22Grape\x22,\x22Price\x22:3.21}],\x22Date\x22:\x2221/11/2010\x22}");

Der im Zugriffs Token ausgegebene Anspruch:

    "array_in_json":{"Items":[{"Name":"Apple","Price":12.3},{"Name":"Grape","Price":3.21}],"Date":"21/11/2010"}

### <a name="can-i-pass-resource-value-as-part-of-the-scope-value-like-how-requests-are-done-against-azure-ad"></a>Kann ich den Ressourcen Wert als Teil des Bereichs Werts übergeben, wie z. b. wie Anforderungen gegen Azure AD durchgeführt werden?
Mit AD FS auf Server 2019 können Sie nun den Ressourcen Wert übergeben, der in den Scope-Parameter eingebettet ist. Der Bereichs Parameter kann nun als durch Leerzeichen getrennte Liste organisiert werden, wobei jeder Eintrag als Ressource/Bereich strukturiert ist. Beispiel:  
**< eine gültige Beispiel Anforderung erstellen >**

### <a name="does-ad-fs-support-pkce-extension"></a>Unterstützt AD FS die pkce-Erweiterung?
AD FS in Server 2019 unterstützt den Prüfschlüssel für Code Austausch (pkce) für den OAuth-Autorisierungs Code Grant-Flow.

### <a name="what-permitted-scopes-are-supported-by-ad-fs"></a>Welche zulässigen Bereiche werden von AD FS unterstützt?
- Aza: Wenn die [OAuth 2,0-Protokoll Erweiterungen für Broker Clients](https://docs.microsoft.com/openspecs/windows_protocols/ms-oapxbc/2f7d8875-0383-4058-956d-2fb216b44706) verwendet werden und der Scope-Parameter den Bereich "Aza" enthält, gibt der Server ein neues primäres Aktualisierungs Token aus und legt es im refresh_token-Feld der Antwort fest. Außerdem wird das refresh_token_ expires_in-Feld bis zur Lebensdauer des neuen primären Aktualisierungs Tokens, wenn eine erzwungen wird.
- OpenID: ermöglicht es der Anwendung, die Verwendung des OpenID Connect-Autorisierungs Protokolls anzufordern.
- logon_cert: der logon_cert-Bereich ermöglicht es einer Anwendung, Anmelde Zertifikate anzufordern, die für die interaktive Anmeldung von authentifizierten Benutzern verwendet werden können. Der AD FS Server lässt den access_token-Parameter aus der Antwort aus und stellt stattdessen eine Base64-codierte CMS-Zertifikatskette oder eine SMTP-vollständige PKI-Antwort bereit. Weitere Informationen finden Sie [hier](https://docs.microsoft.com/openspecs/windows_protocols/ms-oapx/32ce8878-7d33-4c02-818b-6c9164cc731e). 
- user_impersonation: der Bereich "user_impersonation" ist erforderlich, um erfolgreich ein Zugriffs Token aus AD FS anzufordern. Ausführliche Informationen zur Verwendung dieses Bereichs finden Sie unter [Erstellen einer Anwendung mit mehreren Stufen mithilfe von "on-Auftrag-of" (OBO) mithilfe von OAuth mit AD FS 2016](../../ad-fs/development/ad-fs-on-behalf-of-authentication-in-windows-server.md).
- vpn_cert: der vpn_cert-Bereich ermöglicht einer Anwendung das Anfordern von VPN-Zertifikaten, die zum Einrichten von VPN-Verbindungen mithilfe der EAP-TLS-Authentifizierung verwendet werden können. Dies wird nicht mehr unterstützt.
- e-Mail: ermöglicht es der Anwendung, einen e-Mail-Anspruch für den angemeldeten Benutzer anzufordern. Dies wird nicht mehr unterstützt. 
- Profil: ermöglicht es der Anwendung, Profil bezogene Ansprüche für den Anmelde Benutzer anzufordern. Dies wird nicht mehr unterstützt. 


## <a name="operations"></a>Vorgänge

### <a name="how-do-i-replace-the-ssl-certificate-for-ad-fs"></a>Gewusst wie das SSL-Zertifikat für AD FS ersetzen?
Das AD FS SSL-Zertifikat ist nicht mit dem AD FS Dienst Kommunikations Zertifikat identisch, das im Snap-in "AD FS-Verwaltung" gefunden wurde.  Um das AD FS SSL-Zertifikat zu ändern, müssen Sie PowerShell verwenden. Befolgen Sie die Anweisungen im folgenden Artikel:

[Verwalten von SSL-Zertifikaten in AD FS und WAP 2016](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)

### <a name="how-can-i-enable-or-disable-tlsssl-settings-for-ad-fs"></a>Wie kann ich TLS/SSL-Einstellungen für AD FS aktivieren oder deaktivieren?
Um SSL-Protokolle und Verschlüsselungs Sammlungen zu deaktivieren oder zu aktivieren, verwenden Sie Folgendes:

[Verwalten von SSL-Protokollen in AD FS](../operations/Manage-SSL-Protocols-in-AD-FS.md)

### <a name="does-the-proxy-ssl-certificate-have-to-be-the-same-as-the-ad-fs-ssl-certificate"></a>Muss das Proxy-SSL-Zertifikat mit dem AD FS SSL-Zertifikat identisch sein?  
Verwenden Sie die folgenden Anleitungen in Bezug auf das Proxy-SSL-Zertifikat und das AD FS SSL-Zertifikat:


- Wenn der Proxy für die Proxy AD FS Anforderungen verwendet wird, die die integrierte Windows-Authentifizierung verwenden, muss das Proxy-SSL-Zertifikat mit dem SSL-Zertifikat des Verbund Servers identisch sein (verwenden Sie denselben Schlüssel).
- Wenn die AD FS-Eigenschaft "extendedschutztokencheck" aktiviert ist (die Standardeinstellung in AD FS), muss das Proxy-SSL-Zertifikat mit dem SSL-Zertifikat des Verbund Servers identisch sein (verwenden Sie denselben Schlüssel).
- Andernfalls kann das Proxy-SSL-Zertifikat über einen anderen Schlüssel als das AD FS SSL-Zertifikat verfügen, muss jedoch dieselben [Anforderungen](../overview/AD-FS-2016-Requirements.md) erfüllen.

### <a name="why-do-i-only-see-a-password-login-on-ad-fs-and-not-my-other-authentication-methods-that-i-have-configured"></a>Warum sehe ich nur eine Kenn Wort Anmeldung auf AD FS und nicht meine anderen Authentifizierungsmethoden, die ich konfiguriert habe? 
AD FS zeigt nur eine einzelne Authentifizierungsmethode auf dem Anmeldebildschirm an, wenn die Anwendung explizit einen bestimmten Authentifizierungs-URI erfordert, der einer konfigurierten und aktivierten Authentifizierungsmethode zugeordnet ist. Dies wird im "WAUTH"-Parameter für WS-Verbund Anforderungen und den "requestedauthnctxref"-Parameter in einer SAML-Protokoll Anforderung weitergeleitet. Daher wird nur die angeforderte Authentifizierungsmethode angezeigt (z. b. Password Login).

Wenn AD FS mit Azure AD verwendet wird, wird von den Anwendungen häufig der prompt = Login-Parameter an Azure AD gesendet. Azure AD übersetzt dies standardmäßig in die Anforderung einer neuen Kenn Wort basierten Anmeldung bei AD FS. Dies ist der häufigste Grund, eine Kenn Wort Anmeldung auf AD FS in Ihrem Netzwerk anzuzeigen oder keine Option zum Anmelden mit Ihrem Zertifikat anzuzeigen. Dies kann problemlos behoben werden, indem Sie in Azure AD Änderungen an den Einstellungen der Verbund Domäne vornehmen. 

Informationen dazu, wie Sie dies konfigurieren, finden Sie [unter Active Directory-Verbunddienste (AD FS) prompt = Unterstützung von Anmelde Parametern](../operations/AD-FS-Prompt-Login.md).

### <a name="how-can-i-change-the-ad-fs-service-account"></a>Wie kann ich das AD FS Dienst Konto ändern?
Um das AD FS Dienst Konto zu ändern, befolgen Sie die Anweisungen unter Verwenden des [PowerShell-Moduls](https://github.com/Microsoft/adfsToolbox/tree/master/serviceAccountModule)AD FS Toolbox-Dienst Kontos.

### <a name="how-can-i-configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>Wie kann ich Browser für die Verwendung der integrierten Windows-Authentifizierung (WIA) mit AD FS konfigurieren?

Weitere Informationen zum Konfigurieren von Browsern finden [Sie unter Konfigurieren von Browsern für die Verwendung der integrierten Windows-Authentifizierung (WIA) mit AD FS](../operations/Configure-AD-FS-Browser-WIA.md).

### <a name="can-i-turn-off-browserssoenabled"></a>Kann ich browserssoaktivierte deaktivieren?
Wenn Sie keine Zugriffs Steuerungs Richtlinien basierend auf dem Gerät auf der AD FS-oder Windows Hello for Business-Zertifikat Registrierung mithilfe von ADFS haben, Sie können browserssoaktivierte deaktivieren. Browserssoaktivierte ermöglicht ADFS, ein PRT (primäres Aktualisierungs Token) von einem Client zu erfassen, der Geräteinformationen enthält. Ohne dass die Geräte Authentifizierung von ADFS auf Windows 10-Geräten nicht funktioniert.

### <a name="how-long-are-ad-fs-tokens-valid"></a>Wie lange sind AD FS Token gültig?

Diese Frage bedeutet häufig, wie lange Benutzer einmaliges Anmelden (Single Sign on, SSO) verwenden, ohne neue Anmelde Informationen eingeben zu müssen, und wie kann ich als Administrator Steuerelement Vorgehen.  Dieses Verhalten und die Konfigurationseinstellungen, die es steuern, werden im Artikel [AD FS Einstellungen für einmaliges Anmelden](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-2016-single-sign-on-settings)beschrieben.

Die Standard Lebensdauer der verschiedenen Cookies und Token sind unten aufgeführt (sowie die Parameter, die die Lebensdauer steuern):

**Registrierte Geräte**

- PRT-und SSO-Cookies: 90 Tage maximal, geregelt von pssolifetimemins. (Das angegebene Gerät wird mindestens alle 14 Tage verwendet, die von "endviceusagewindow" gesteuert werden)

- Aktualisierungs Token: wird basierend auf dem obigen berechnet, um konsistentes Verhalten bereitzustellen.

- access_token: Standardmäßig 1 Stunde, basierend auf der vertrauenden Seite

- ID: identisch mit dem Zugriffs Token

**Nicht registrierte Geräte**

- SSO-Cookies: standardmäßig 8 Stunden, geregelt von ssolifetimemins.  Wenn "angemeldet bleiben" (kmsi) aktiviert ist, beträgt der Standardwert 24 Stunden und kann über "kmsilifetimemins" konfiguriert werden.


- Aktualisierungs Token: standardmäßig 8 Stunden. 24 Stunden mit aktivierter kmsi

- access_token: Standardmäßig 1 Stunde, basierend auf der vertrauenden Seite

- ID: identisch mit dem Zugriffs Token

### <a name="does-ad-fs-support-http-strict-transport-security-hsts"></a>Unterstützt AD FS die http-strikte Transport Sicherheit (hsts)?  

Bei der http-Strict-Transport Sicherheit (hsts) handelt es sich um einen Mechanismus für die Websicherheits Richtlinie, mit dem Angriffe herab Stufungs Angriffe und Cookies für Dienste mit http-und HTTPS-Endpunkten vermieden werden können. Auf diese Weise können Webserver deklarieren, dass Webbrowser (oder andere Benutzer-Agents) nur mit HTTPS und nie über das HTTP-Protokoll interagieren sollen.

Alle AD FS Endpunkte für den Webauthentifizierungs Datenverkehr werden exklusiv über HTTPS geöffnet.  Demzufolge werden von AD FS effektiv die Bedrohungen verringert, die durch den Mechanismus der http Strict-Transport Sicherheitsrichtlinie bereitstellt werden (Entwurfs bedingt gibt es keinen Downgrade auf http, da keine Listener in http vorhanden sind). Außerdem verhindert AD FS, dass Cookies mit HTTP-Protokoll Endpunkten an einen anderen Server gesendet werden, indem alle Cookies mit dem Secure-Flag gekennzeichnet werden.

Daher ist die Implementierung von hsts auf einem AD FS Server nicht erforderlich, da Sie nie herabgestuft werden kann.  Aus Kompatibilitätsgründen erfüllen AD FS Server diese Anforderungen, weil Sie niemals http verwenden können und alle Cookies als sicher gekennzeichnet sind.

Außerdem AD FS 2016 (mit den neuesten Patches) und AD FS 2019-Unterstützung, die den hsts-Header ausgibt. Informationen zur Konfiguration finden Sie unter [Anpassen von http-Sicherheits Antwort Headern mit AD FS](../operations/customize-http-security-headers-ad-fs.md)

### <a name="x-ms-forwarded-client-ip-does-not-contain-the-ip-of-the-client-but-contains-ip-of-the-firewall-in-front-of-the-proxy-where-can-i-get-the-right-ip-of-the-client"></a>X-MS-weitergeleitete Client-IP enthält nicht die IP-Adresse des Clients, sondern enthält die IP-Adresse der Firewall vor dem Proxy. Wo kann ich die richtige IP-Adresse des Clients erhalten?
Es wird nicht empfohlen, die SSL-Beendigung vor WAP durchzuführen. Für den Fall, dass die SSL-Beendigung vor dem WAP erfolgt, enthält das X-MS-weitergeleitete Client-IP die IP-Adresse des Netzwerkgeräts vor WAP. Im folgenden finden Sie eine kurze Beschreibung der verschiedenen IP-bezogenen Ansprüche, die von AD FS unterstützt werden:
 - x-MS-Client-IP: Netzwerk-IP des Geräts, das mit dem STS verbunden ist.  Bei einer extranetanforderung enthält diese immer die IP-Adresse des WAP.
 - x-ms-weitergeleitete Client-IP: Ein mehr wertiger Anspruch, der alle Werte enthält, die von Exchange Online an ADFS weitergeleitet werden, sowie die IP-Adresse des Geräts, das mit dem WAP verbunden ist.
 - Userip: Für extranetanforderungen enthält dieser Anspruch den Wert von "x-ms-weitergeleitet-Client-IP".  Bei Intranetanforderungen enthält dieser Anspruch denselben Wert wie x-MS-Client-IP.

 Außerdem unterstützen Sie in AD FS 2016 (mit den neuesten Patches) und höheren Versionen auch das Erfassen des x-weitergeleiteten-for-Headers. Alle Load Balancer-oder Netzwerkgeräte, die nicht auf Ebene 3 weitergeleitet werden (IP-Adresse beibehalten), sollten die eingehende Client-IP-Adresse dem Industriestandard-Header "x-weitergeleitet" hinzufügen. 

### <a name="i-am-trying-to-get-additional-claims-on-the-user-info-endpoint-but-its-only-returning-subject-how-can-i-get-additional-claims"></a>Ich versuche, zusätzliche Ansprüche für den Benutzer Info-Endpunkt zu erhalten, aber seinen einzigen Betreff. Wie erhalte ich weitere Ansprüche?
Der AD FS userinfo-Endpunkt gibt immer den Antragsteller Anspruch zurück, wie in den OpenID-Standards angegeben. AD FS stellt keine weiteren Ansprüche bereit, die über den userinfo-Endpunkt angefordert werden. Wenn Sie zusätzliche Ansprüche im ID-Token benötigen, finden Sie unter [AD FS benutzerdefinierte ID-Token](../development/custom-id-tokens-in-ad-fs.md).

### <a name="why-do-i-see-a-lot-of-1021-errors-on-my-ad-fs-servers"></a>Warum werden viele 1021-Fehler auf meinen AD FS Servern angezeigt?
Dieses Ereignis wird in der Regel für einen ungültigen Ressourcen Zugriff auf AD FS für die Ressource 00000003-0000-0000-C000-000000000000 protokolliert. Dieser Fehler wird durch ein fehlerhaftes Verhalten des Clients verursacht, bei dem versucht wird, ein Zugriffs Token für den Azure AD Graph-Dienst zu erhalten. Da die Ressource nicht auf AD FS vorhanden ist, führt dies zu der Ereignis-ID 1021 auf den AD FS Servern. Es ist sicher, dass alle Warnungen oder Fehler für die Ressource 00000003-0000-0000-C000-000000000000 auf AD FS ignoriert werden.

### <a name="why-am-i-seeing-a-warning-for-failure-to-add-the-ad-fs-service-account-to-the-enterprise-key-admins-group"></a>Warum wird eine Warnung angezeigt, dass ein Fehler beim Hinzufügen des AD FS Dienst Kontos zur Gruppe "Organisations Schlüssel-Admins" angezeigt wird?
Diese Gruppe wird nur erstellt, wenn ein Windows 2016-Domänen Controller mit der FSMO-PDC-Rolle in der Domäne vorhanden ist. Um den Fehler zu beheben, können Sie die Gruppe manuell erstellen und die unten aufgeführten Schritte befolgen, um die erforderliche Berechtigung zu erteilen, nachdem das Dienst Konto als Mitglied der Gruppe hinzugefügt wurde.
1.  Öffnen Sie **Active Directory-Benutzer und -Computer**.
2.  Klicken Sie im Navigationsbereich mit der **rechten Maustaste auf** Ihren Domänen Namen, und **Klicken Sie auf** Eigenschaften
3.  **Klicken Sie auf** Sicherheit (wenn die Registerkarte Sicherheit fehlt, aktivieren Sie erweiterte Funktionen im Menü Ansicht).
4.  **Klicken Sie auf** Führende. **Klicken Sie auf** Eren. **Klicken Sie auf** Wählen Sie einen Prinzipal aus.
5.  Das Dialogfeld Benutzer, Computer, Dienst Konto oder Gruppe auswählen wird angezeigt.  Geben Sie im Textfeld geben Sie den Namen des zu ausgewähltes Objekts ein den Namen Key Admin Group ein.  Klicken Sie auf „OK“.
6.  Wählen Sie im Listenfeld gilt für die Option untergeordnete **Benutzer Objekte**aus.
7.  Scrollen Sie mithilfe der Scrollleiste zum unteren Rand der Seite, und **Klicken Sie** auf alle löschen.
8.  Wählen Sie im Abschnitt **Eigenschaften** die Option **msDS-keykredentiallink lesen** aus, und **schreiben Sie MSDS-keykredentiallink**.

### <a name="why-does-modern-authentication-from-android-devices-fail-if-the-server-does-not-send-all-the-intermediate-certificates-in-the-chain-with-the-ssl-cert"></a>Warum schlägt die moderne Authentifizierung von Android-Geräten fehl, wenn der Server nicht alle zwischen Zertifikate in der Kette mit dem SSL-Zertifikat sendet?

Verbund Benutzer können die Authentifizierung für die Azure AD von apps durchführen, die die Android-Adal-Bibliothek nicht verwenden. Die APP erhält eine **AuthenticationException** , wenn Sie versucht, die Anmeldeseite anzuzeigen. In Chrome wird die AD FS Anmeldeseite möglicherweise als unsicher bezeichnet.

Android: in allen Versionen und allen Geräten wird das Herunterladen zusätzlicher Zertifikate aus dem Feld " **autorityinformationaccess** " des Zertifikats nicht unterstützt. Dies gilt auch für den Chrome-Browser. Bei allen Server Authentifizierungs Zertifikaten, die zwischen Zertifikate fehlen, tritt dieser Fehler auf, wenn die gesamte Zertifikat Kette nicht von AD FS übermittelt wird.

Eine geeignete Lösung für dieses Problem besteht darin, die AD FS-und WAP-Server so zu konfigurieren, dass die erforderlichen zwischen Zertifikate zusammen mit dem SSL-Zertifikat gesendet werden.

Stellen Sie beim Exportieren des SSL-Zertifikats von einem Computer, der in den persönlichen Speicher des Computers importiert werden soll, der AD FS-und WAP-Server sicher, dass Sie den privaten Schlüssel exportieren, und wählen Sie privater **Informationsaustausch-PKCS #12**aus.

Es ist wichtig, dass das Kontrollkästchen, **Wenn möglich, alle Zertifikate im Zertifikat Pfad einschließen** aktiviert ist, und **alle erweiterten Eigenschaften exportieren**.  

Führen Sie "certlm. msc" auf den Windows-Servern aus, und importieren Sie das *. PFX in den persönlichen Zertifikat Speicher des Computers. Dies bewirkt, dass der Server die gesamte Zertifikatskette an die Adal-Bibliothek übergibt.

>[!NOTE]
> Der Zertifikat Speicher von Netzwerk Lastenausgleich sollte ebenfalls aktualisiert werden, um die gesamte Zertifikatskette einzubeziehen, sofern vorhanden.

### <a name="does-ad-fs-support-head-requests"></a>Unterstützt AD FS Head-Anforderungen?
Der AD FS unterstützt keine HEAD-Anforderungen.  Anwendungen sollten keine HEAD-Anforderungen für AD FS Endpunkte verwenden.  Dies kann zu unerwarteten und/oder verzögerten HTTP-Fehler Antworten führen.  Außerdem werden möglicherweise unerwartete Fehlerereignisse im Ereignisprotokoll AD FS angezeigt.

### <a name="why-am-i-not-seeing-a-refresh-token-when-i-am-logging-in-with-a-remote-idp"></a>Warum sehe ich kein Aktualisierungs Token, wenn ich mich mit einem Remote-IDP anmeldet?
Ein Aktualisierungs Token wird nicht ausgegeben, wenn das von IDP ausgegebene Token eine Validty von weniger als 1 Stunde aufweist. Um sicherzustellen, dass ein Aktualisierungs Token ausgegeben wird, erhöhen Sie die Gültigkeit des vom IDP ausgestellten Tokens auf mehr als eine Stunde.

### <a name="do-we-have-any-way-to-change-rp-token-encryption-algorithm"></a>Haben wir die Möglichkeit, den Verschlüsselungsalgorithmus für die RP-Token zu ändern?
Standardmäßig ist die RP-tokenverschlüsselung auf AES256 festgelegt und kann nicht in einen anderen Wert geändert werden.

### <a name="on-a-mixed-mode-farm-i-get-error-when-trying-to-set-the-new-ssl-certificate-using-set-adfssslcertificate--thumbprint-how-can-i-update-the-ssl-certificate-in-a-mixed-mode-ad-fs-farm"></a>In einer Farm mit gemischtem Modus erhalte ich einen Fehler, wenn ich versuche, das neue SSL-Zertifikat mithilfe von "Set-adfssslcertificate-Thumbprint" festzulegen. Wie kann ich das SSL-Zertifikat in einem AD FS Farm mit gemischtem Modus aktualisieren?
Im gemischten Modus AD FS Farmen als transitiv dienen. Es wird empfohlen, dass Sie bei der Planung entweder ein Rollover des SSL-Zertifikats vor dem Upgradevorgang ausführen oder den Vorgang durchführen und die Farm Verhalten erhöhen, bevor Sie das SSL-Zertifikat aktualisieren. Wenn dies nicht der Fall ist, können Sie mit den folgenden Anweisungen das SSL-Zertifikat aktualisieren. 

Auf WAP-Servern können Sie weiterhin Set-webapplicationproxysslcertificate verwenden. Auf den ADFS-Servern müssen Sie Netsh verwenden. Führen Sie die folgenden Schritte aus:

1. Wählen Sie eine Teilmenge der AD FS 2016-Server für die Wartung aus (z. b. aus dem Lastenausgleich entfernen).
2. Importieren Sie auf den Servern, die in #1 ausgewählt sind, das neue Zertifikat per MMC.
3. Vorhandene Zertifikate löschen

    a. Netsh HTTP DELETE sslcert hostnameport = FS. Configuration. com: 443 b. Netsh HTTP DELETE sslcert hostnameport = localhost: 443 c. Netsh HTTP DELETE sslcert hostnameport = FS. Configuration. com: 49443 verwendet.

4.  Neues Zertifikat hinzufügen

    a. netsh http Add sslcert hostnameport = FS. Configuration. com: 443 CertHash = certthumbprint AppID = {5d89a20c-beab-4389-9447-324788eb944a} certstorename = My SslCtlStoreName = adberstrusteddevices

    b. netsh http Add sslcert hostnameport = localhost: 443 CertHash = certthumbprint AppID = {5d89a20c-beab-4389-9447-324788eb944a} certstorename = My SslCtlStoreName = adberstrusteddevices

    c. netsh http Add sslcert hostnameport = FS. Configuration. com: 49443 verwendet. CertHash = certthumbprint AppID = {5d89a20c-beab-4389-9447-324788eb944a} certstorename = My SslCtlStoreName = adberstrusteddevices

5. AD FS-Dienst auf dem ausgewählten Server neu starten
6. Entfernen einer Teilmenge von WAP-Servern für die Wartung
7. Importieren Sie das neue Zertifikat auf den ausgewählten WAP-Servern über MMC.
8. Festlegen des neuen CERT für WAP mithilfe des Cmdlets

    a. Set-webapplicationproxysslcertificate-Thumbprint "certthumbprint"

9. Dienst auf den ausgewählten WAP-Servern neu starten
10. Versetzen Sie die ausgewählten WAP-und AD FS Server wieder in die Produktionsumgebung.

Führen Sie das Update für den Rest AD FS-und WAP-Server auf ähnliche Weise aus.

### <a name="is-adfs-supported-when-web-application-proxy-wap-servers-are-behind-azure-web-application-firewallwaf"></a>Wird ADFS unterstützt, wenn sich webanwendungsproxy-Server (WAP) hinter der Azure Web Application Firewall (WAF) befinden?
ADFS-und Webanwendungs Server unterstützen jede Firewall, die keine SSL-Beendigung auf dem Endpunkt ausführt. Außerdem verfügen ADFS-/WAP-Server über integrierte Mechanismen, um häufige webangriffe wie z. b. Website übergreifende Skripts, ADFS-Proxy und alle Anforderungen zu erfüllen, die durch das [MS-adfspip-Protokoll](https://msdn.microsoft.com/library/dn392811.aspx)definiert werden.

### <a name="i-am-seeing-an-event-441-a-token-with-a-bad-token-binding-key-was-found-what-should-i-do-to-resolve-this"></a>Ich sehe das Ereignis 441: Ein Token mit einem ungültigen tokenbindungsschlüssel wurde gefunden. " Was soll ich tun, um dieses Problem zu beheben?
In AD FS 2016 wird die tokenbindung automatisch aktiviert, und es werden mehrere bekannte Probleme bei Proxy-und Verbund Szenarien verursacht, die zu diesem Fehler führen. Um dieses Problem zu beheben, führen Sie den folgenden PowerShell-Befehl aus, und entfernen Sie die tokenbindungs

`Set-AdfsProperties -IgnoreTokenBinding $true`

### <a name="i-have-upgraded-my-farm-from-ad-fs-in-windows-server-2016-to-ad-fs-in-windows-server-2019-the-farm-behavior-level-for-the-ad-fs-farm-has-been-successfully-raised-to-2019-but-the-web-application-proxy-configuration-is-still-displayed-as-windows-server-2016"></a>Ich habe meine Farm von AD FS in Windows Server 2016 auf AD FS in Windows Server 2019 aktualisiert. Die Farm Verhaltensebene für die AD FS Farm wurde erfolgreich auf 2019, aber die Konfiguration des webanwendungsproxys wird weiterhin als Windows Server 2016 angezeigt?
Nach einem Upgrade auf Windows Server 2019 wird die Konfigurations Version des webanwendungsproxys weiterhin als Windows Server 2016 angezeigt. Der webanwendungsproxy verfügt nicht über neue versionsspezifische Features für Windows Server 2019. wenn die Farm Verhalten auf AD FS erfolgreich ausgelöst wurde, wird der webanwendungsproxy nach dem Entwurf weiterhin als Windows Server 2016 angezeigt. 
