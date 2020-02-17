---
ms.assetid: acc9101b-841c-4540-8b3c-62a53869ef7a
title: AD FS – FAQ
description: Häufig gestellte Fragen zu Active Directory-Verbunddienste (AD FS)
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 04/17/2019
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 48d93f515a5f3e5f8ce2c3ff9a1b40f300ca57ed
ms.sourcegitcommit: c5709021aa98abd075d7a8f912d4fd2263db8803
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2020
ms.locfileid: "76265742"
---
# <a name="ad-fs-frequently-asked-questions-faq"></a>AD FS – Häufig gestellte Fragen (FAQ)


In der folgenden Dokumentation finden Sie Informationen zu häufig gestellten Fragen im Zusammenhang mit Active Directory-Verbunddienste (Active Directory Federation Services, AD FS).  Das Dokument wurde in Gruppen unterteilt, die auf der Art der Frage basieren.

## <a name="deployment"></a>Bereitstellung

### <a name="how-can-i-upgrademigrate-from-previous-versions-of-ad-fs"></a>Wie kann ich ein Upgrade/eine Migration von früheren AD FS-Versionen durchführen?
Sie können AD FS mit einer der folgenden Versionen aktualisieren:


- Windows Server 2012 R2 AD FS zu Windows Server 2016 AD FS oder höher. Beachten Sie, dass die Methodik identisch ist, wenn Sie von Windows Server 2016 AD FS auf Windows Server 2019 AD FS aktualisieren. 
    - [Aktualisieren auf AD FS unter Windows Server 2016 unter Verwendung einer WID-Datenbank](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)
    - [Aktualisieren auf AD FS unter Windows Server 2016 unter Verwendung einer SQL-Datenbank](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL.md)
- Windows Server 2012 AD FS zu Windows Server 2012 R2 AD FS
    - [Migrieren zu AD FS unter Windows Server 2012 R2](https://technet.microsoft.com/library/dn486815.aspx)
- AD FS 2.0 zu Windows Server 2012 AD FS
    - [Migrieren zu AD FS unter Windows Server 2012](https://technet.microsoft.com/library/jj647765.aspx)
- AD FS 1.x zu AD FS 2.0
    - [Upgrade von AD FS 1.x auf AD FS 2.0](https://technet.microsoft.com/library/ff678035.aspx)

Wenn ein Upgrade von AD FS 2.0 oder 2.1 (Windows Server 2008 R2 oder Windows Server 2012) erforderlich ist, müssen Sie die mitgelieferten Skripts (in „C:\Windows\ADFS“) verwenden.

### <a name="why-does-ad-fs-installation-require-a-reboot-of-the-server"></a>Warum ist für die AD FS-Installation ein Neustart des Servers erforderlich?

Die HTTP/2-Unterstützung wurde in Windows Server 2016 hinzugefügt, aber HTTP/2 kann nicht für die Authentifizierung mit Clientzertifikat verwendet werden.  Weil in vielen AD FS-Szenarien die Authentifizierung mit Clientzertifikat genutzt wird und eine große Anzahl von Clients eine Wiederholung von Anforderungen mit HTTP/1.1 nicht unterstützt, werden bei der AD FS-Farmkonfiguration die HTTP-Einstellungen des lokalen Servers auf HTTP/1.1 neu konfiguriert.  Dazu ist ein Neustart des Servers erforderlich.  

### <a name="is-using-windows-2016-wap-servers-to-publish-the-ad-fs-farm-to-the-internet-without-upgrading-the-back-end-ad-fs-farm-supported"></a>Wird es unterstützt, wenn WAP-Server unter Windows 2016 zum Veröffentlichen der AD FS-Farm im Internet verwendet werden, ohne dass ein Upgrade der AD FS-Back-End-Farm durchgeführt wird?
Ja, diese Konfiguration wird unterstützt, allerdings würden darin keine neuen AD FS 2016-Features unterstützt.  Diese Konfiguration soll während der Migrationsphase von AD FS 2012 R2 zu AD FS 2016 temporär sein und sollte nicht über einen längeren Zeitraum bereitgestellt werden.

### <a name="is-it-possible-to-deploy-ad-fs-for-office-365-without-publishing-a-proxy-to-office-365"></a>Ist es möglich, AD FS für Office 365 bereitzustellen, ohne einen Proxy für Office 365 zu veröffentlichen?
Ja, das wird unterstützt. Allerdings als ein Nebeneffekt.

1. Sie müssen die Aktualisierung von Tokensignaturzertifikaten manuell verwalten, weil Azure AD auf die Verbundmetadaten nicht zugreifen kann. Weitere Informationen zum manuellen Aktualisieren des Tokensignaturzertifikats finden Sie unter [Erneuern von Verbundzertifikaten für Office 365 und Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs).
2. Sie können keine Legacyauthentifizierungsflows (z. B. den ExO-Proxy-Authentifizierungsflow) nutzen.

### <a name="what-are-load-balancing-requirements-for-ad-fs-and-wap-servers"></a>Was sind die Anforderungen an den Lastenausgleich für AD FS- und WAP-Server?

AD FS ist ein statusfreies System. Daher ist der Lastenausgleich bei Anmeldungen ziemlich einfach. Im Folgenden sind die wichtigsten Empfehlungen für Lastenausgleichssysteme aufgeführt.


- Lastenausgleichsmodule sollten NICHT mit IP-Affinität konfiguriert werden. Dadurch kann eine Teilmenge Ihrer Server in bestimmten Exchange Online-Szenarien übermäßig geladen werden.
- Lastenausgleichsmodule DÜRFEN die HTTPS-Verbindungen nicht beenden und keine neue Verbindung mit dem AD FS-Server erneut initiieren.
- Lastenausgleichsmodule SOLLTEN sicherstellen, dass die IP-Adresse zum Herstellen einer Verbindung im HTTP-Paket beim Senden an AD FS als Quell-IP-Adresse übersetzt wird. Wenn ein Lastenausgleichsmodul die Quell-IP-Adresse nicht im HTTP-Paket senden kann, MUSS das Modul die IP-Adresse dem Header „ x-forwarded-for“ hinzufügen (oder sie anfügen). Diese Vorgehensweise ist für die korrekte Verarbeitung bestimmter IP-bezogener Features (gesperrte IP-Adresse, intelligente Extranetsperre,...) erforderlich und könnte bei nicht ordnungsgemäßer Konfiguration zu eingeschränkter Sicherheit führen.
- Lastenausgleichsmodule SOLLTEN SNI unterstützen. Wenn dies nicht der Fall ist, sorgen Sie dafür, dass AD FS so konfiguriert wird, dass HTTPS-Bindungen zur Verarbeitung von Nicht-SNI-fähigen Clients erstellt werden.
- Lastenausgleichsmodule SOLLTEN über den HTTP-Integritätstestendpunkt von AD FS ermitteln, ob die AD FS- oder WAP-Server ausgeführt werden. Wenn kein „200 OK“ zurückgegeben wird, sollten die Module die betreffenden Server ausschließen.

### <a name="what-multi-forest-configurations-are-supported-by-ad-fs"></a>Welche Konfigurationen mit mehreren Gesamtstrukturen werden von AD FS unterstützt?

AD FS unterstützt eine Konfiguration mit mehreren Gesamtstrukturen und basiert auf dem zugrunde liegenden AD DS-Vertrauensstellungsnetzwerk, um Benutzer über mehrere vertrauenswürdige Bereiche hinweg zu authentifizieren. Wir empfehlen dringend bidirektionale Gesamtstruktur-Vertrauensstellungen, da dies ein einfacheres Setup ist und so sichergestellt werden kann, dass das Vertrauensstellung-Subsystem einwandfrei und ohne Probleme funktioniert. Darüber hinaus gilt:

- Bei einer unidirektionalen Gesamtstruktur-Vertrauensstellung, z. B. einer DMZ-Gesamtstruktur mit Partneridentitäten, empfehlen wir, AD FS in der CORP-Gesamtstruktur bereitzustellen und die DMZ-Gesamtstruktur als eine weitere Anspruchsanbieter-Vertrauensstellung zu behandeln, die über LDAP verbunden ist. In diesem Fall funktioniert die integrierte Windows-Authentifizierung für die Benutzer der DMZ-Gesamtstruktur nicht, und die Benutzer müssen eine Kennwortauthentifizierung durchführen, da dies der einzige unterstützte Mechanismus für LDAP ist. Wenn Sie diese Option nicht nutzen können, müssten Sie ein weiteres AD FS in der DMZ-Gesamtstruktur einrichten und es als Anspruchsanbieter-Vertrauensstellung im AD FS in der CORP-Gesamtstruktur hinzufügen. Benutzer müssen eine Startbereichsermittlung durchführen, doch sowohl die integrierte Windows-Authentifizierung als auch die Kennwortauthentifizierung werden funktionieren. Nehmen Sie entsprechende Änderungen an den Ausstellungsregeln in AD FS in der DMZ-Gesamtstruktur vor, da AD FS in der CORP-Gesamtstruktur keine zusätzlichen Benutzerinformationen über den Benutzer aus der DMZ-Gesamtstruktur erhalten kann.
- Obwohl Vertrauensstellungen auf Domänenebene unterstützt werden und funktionieren können, wird dringend empfohlen, zu einem Vertrauensmodell auf Gesamtstrukturebene zu wechseln. Außerdem müssten Sie sicherstellen, dass das UPN-Routing und die NetBIOS-Namensauflösung von Namen fehlerfrei funktionieren müssen.

>[!NOTE]  
>Wenn bei einer bidirektionalen Vertrauenskonfiguration optionale Authentifizierung verwendet wird, stellen Sie sicher, dass dem Aufrufer für das Zieldienstkonto die Berechtigung „allow to authenticate“ (zur Authentifizierung zulassen) erteilt wird. 


## <a name="design"></a>Entwurf

### <a name="what-third-party-multi-factor-authentication-providers-are-available-for-ad-fs"></a>Welche Mehrstufige-Authentifizierung-Anbieter (Multi-Factor Authentication, MFA) von Drittanbietern sind für AD FS verfügbar?
AD FS bietet einen erweiterbaren Mechanismus zum Integrieren der MFA-Anbieter von Drittanbietern. Hierfür gibt es kein festgelegtes Zertifizierungsprogramm. Es wird davon ausgegangen, dass der Hersteller die erforderlichen Überprüfungen vor der Freigabe durchgeführt hat. 

Die Liste der Anbieter, die Microsoft benachrichtigt haben, wird unter [MFA-Anbieter für AD FS](../operations/Configure-Additional-Authentication-Methods-for-AD-FS.md) veröffentlicht.  Es kann immer Anbieter geben, von denen wir nichts wissen, und wir werden die Liste aktualisieren, sobald wir etwas über diese Anbieter erfahren.

### <a name="are-third-party-proxies-supported-with-ad-fs"></a>Werden Drittanbieter-Proxys mit AD FS unterstützt?
Ja, Proxys von Drittanbietern können vor dem Webanwendungsproxy eingefügt werden, aber jeder Drittanbieter-Proxy muss das [MS-ADFSPIP-Protokoll](https://msdn.microsoft.com/library/dn392811.aspx) unterstützen, das anstelle des Webanwendungsproxys zu verwenden ist.

Nachstehend finden Sie eine Liste der uns bekannten Drittanbieter.  Es kann immer Anbieter geben, von denen wir nichts wissen, und wir werden die Liste aktualisieren, sobald wir etwas über diese Anbieter erfahren.

- [F5-Zugriffsrichtlinien-Manager](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-third-party-integration-13-1-0/12.html#guid-1ee8fbb3-1b33-4982-8bb3-05ae6868d9ee)


### <a name="where-is-the-capacity-planning-sizing-spreadsheet-for-ad-fs-2016"></a>Wo ist das Arbeitsblatt zur Dimensionierung der Kapazitätsplanung für AD FS 2016?
Die AD FS 2016-Version des Arbeitsblatts kann [hier](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)heruntergeladen werden.
Sie kann auch für AD FS in Windows Server 2012 R2 verwendet werden.

### <a name="how-can-i-ensure-my-ad-fs-and-wap-servers-support-apples-atp-requirements"></a>Wie kann ich sicherstellen, dass meine AD FS- und WAP-Server die ATP-Anforderungen von Apple unterstützen?

Apple hat eine Reihe von Anforderungen herausgegeben, die als „App-Transportsicherheit“ (App Transport Security, ATS) bezeichnet werden und sich auf Aufrufe aus iOS-Apps auswirken können, die sich bei AD FS authentifizieren.  Sie können dafür sorgen, dass Ihre AD FS- und WAP-Server diesem entsprechen, indem Sie sicherstellen, dass die Server die [Anforderungen zum Herstellen einer Verbindung mithilfe von ATS](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57) unterstützen.  
Insbesondere sollten Sie überprüfen, ob Ihre AD FS- und WAP-Server TLS 1.2 unterstützen und ob die ausgehandelte Verschlüsselungssammlung der TLS-Verbindung Perfect Forward Secrecy (PFS) unterstützen wird.

Sie können SSL 2.0 und 3.0 sowie die TLS-Versionen 1.0, 1.1 und 1.2 anhand der Informationen unter [Verwalten von SSL-Protokollen in AD FS](../operations/Manage-SSL-Protocols-in-AD-FS.md) aktivieren und deaktivieren.

Um sicherzustellen, dass Ihre AD FS- und WAP-Server nur TLS-Verschlüsselungssammlungen aushandeln, die ATP unterstützen, können Sie alle Sammlungen deaktivieren, die in der [Liste der ATP-kompatiblen Verschlüsselungssammlungen](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57) nicht enthalten sind.  Verwenden Sie dazu die [Windows TLS PowerShell-Cmdlets](https://technet.microsoft.com/itpro/powershell/windows/tls/index).

## <a name="developer"></a>Entwickler

### <a name="when-generating-an-id_token-with-adfs-for-a-user-authenticated-against-ad-how-is-the-sub-claim-generated-in-the-id_token"></a>Wie wird beim Generieren eines ID-Tokens (id_token) mit AD FS für einen Benutzer, der für AD authentifiziert ist, der „sub“-Anspruch in diesem Token generiert?
Der Wert des „sub“-Anspruchs ist der Hash von Client-ID + Ankeranspruchswert.

### <a name="what-is-the-lifetime-of-the-refresh-tokenaccess-token-when-the-user-logs-in-via-a-remote-claims-provider-trust-over-ws-fedsaml-p"></a>Wie lange ist die Lebensdauer des Aktualisierungstokens/Zugriffstokens, wenn sich der Benutzer über eine Vertrauensstellung mit Remote-Anspruchsanbieter und WS-Fed/SAML-P anmeldet?
Die Lebensdauer des Aktualisierungstokens ist die Lebensdauer des Tokens, das AD FS von dieser Vertrauensstellung erhalten hat. Die Lebensdauer des Zugriffstokens ist die Tokenlebensdauer der vertrauenden Seite, für die das Token ausgegeben wird.

### <a name="i-need-to-return-profile-and-email-scopes-as-well-in-addition-to-the-openid-scope-can-i-obtain-additional-information-using-scopes-how-to-do-it-in-ad-fs"></a>Ich muss zusätzlich zum OpenId-Bereich auch Profil und E-Mail-Bereiche zurückgeben. Kann ich weitere Informationen unter Verwendung von Bereichen abrufen? Wie geht das in AD FS?
Sie können das angepasste ID-Token (id_token) verwenden, um relevante Informationen im Token selbst hinzuzufügen. Weitere Informationen finden Sie im Artikel [Customize claims to be emitted in id_token](../development/Custom-Id-Tokens-in-AD-FS.md) (Anpassen von Ansprüchen, die im ID-Token ausgegeben werden müssen).

### <a name="how-to-issue-json-blobs-inside-jwt-tokens"></a>Wie werden JSON-Blobs in JWT-Token ausgestellt?
Dafür wurden ein spezieller ValueType („<http://www.w3.org/2001/XMLSchema#json>“) und ein Escapezeichen (\x22) in AD FS 2016 hinzugefügt. Sehen Sie sich das nachstehende Beispiel für die Ausstellungsregel und auch die endgültige Ausgabe des Zugriffstokens an.

Beispiel für eine Ausstellungsregel:

    => issue(Type = "array_in_json", ValueType = "http://www.w3.org/2001/XMLSchema#json", Value = "{\x22Items\x22:[{\x22Name\x22:\x22Apple\x22,\x22Price\x22:12.3},{\x22Name\x22:\x22Grape\x22,\x22Price\x22:3.21}],\x22Date\x22:\x2221/11/2010\x22}");

Der im Zugriffstoken ausgegebene Anspruch:

    "array_in_json":{"Items":[{"Name":"Apple","Price":12.3},{"Name":"Grape","Price":3.21}],"Date":"21/11/2010"}

### <a name="can-i-pass-resource-value-as-part-of-the-scope-value-like-how-requests-are-done-against-azure-ad"></a>Kann ich den Ressourcenwert als Teil des Bereichswerts übergeben, so wie Anforderungen für Azure AD durchgeführt werden?
Bei AD FS unter Windows Server 2019 können Sie jetzt den im Bereichsparameter eingebetteten Ressourcenwert übergeben. Der Bereichsparameter kann jetzt als eine durch Leerzeichen getrennte Liste organisiert werden, wobei jeder Eintrag als Ressource/Bereich strukturiert ist. Beispiel:  
**<eine gültige Beispielanforderung erstellen>**

### <a name="does-ad-fs-support-pkce-extension"></a>Unterstützt AD FS die PKCE-Erweiterung?
AD FS unter Windows Server 2019 unterstützt die Erweiterung „Proof Key for Code Exchange“ (PKCE) für den OAuth Authorization Code Grant-Datenfluss.

### <a name="what-permitted-scopes-are-supported-by-ad-fs"></a>Welche zulässigen Bereiche werden von AD FS unterstützt?
- aza – Wenn Sie [OAuth 2.0-Protokollerweiterungen für Broker-Clients](https://docs.microsoft.com/openspecs/windows_protocols/ms-oapxbc/2f7d8875-0383-4058-956d-2fb216b44706) verwenden und der Bereichsparameter den Bereich „aza“ enthält, gibt der Server ein neues primäres Aktualisierungstoken aus und legt es im Feld „refresh_token“ der Antwort fest. Außerdem wird im Feld „refresh_token_expires_in“ die Lebensdauer für das Token festgelegt, wenn diese erzwungen wird.
- openid – Ermöglicht es der Anwendung, die Verwendung des „OpenID Connect“-Autorisierungsprotokolls anzufordern.
- logon_cert – Der Bereich „logon_cert“ ermöglicht einer Anwendung das Anfordern von Anmeldezertifikaten, die für die interaktive Anmeldung authentifizierter Benutzer verwendet werden können. Der AD FS-Server lässt den Parameter „access_token“ in der Antwort aus und stellt stattdessen eine Base64-codierte CMS-Zertifikatskette oder eine CMC-vollständige PKI-Antwort bereit. Weitere Details können Sie [hier](https://docs.microsoft.com/openspecs/windows_protocols/ms-oapx/32ce8878-7d33-4c02-818b-6c9164cc731e) finden. 
- user_impersonation – Der Bereich „user_impersonation“ ist erforderlich, um ein „on-behalf-of“-Zugriffstoken von AD FS erfolgreich anzufordern. Ausführliche Informationen zur Verwendung dieses Bereichs finden Sie unter [Build a multi-tiered application using On-Behalf-Of (OBO) using OAuth with AD FS 2016](../../ad-fs/development/ad-fs-on-behalf-of-authentication-in-windows-server.md) (Erstellen einer Anwendung mit mehreren Ebenen mithilfe von „On-Behalf-Of“ (OBO) unter Verwendung von OAuth mit AD FS 2016).
- vpn_cert – Der Bereich „vpn_cert“ ermöglicht einer Anwendung das Anfordern von VPN-Zertifikaten, die verwendet werden können, um VPN-Verbindungen mithilfe der EAP-TLS-Authentifizierung herzustellen. Dies wird nicht mehr unterstützt.
- email – Ermöglicht es der Anwendung, einen E-Mail-Anspruch für den angemeldeten Benutzer anzufordern. Dies wird nicht mehr unterstützt. 
- profile – Ermöglicht es der Anwendung, profilbezogene Ansprüche für den angemeldeten Benutzer anzufordern. Dies wird nicht mehr unterstützt. 


## <a name="operations"></a>Betrieb

### <a name="how-do-i-replace-the-ssl-certificate-for-ad-fs"></a>Wie ersetze ich das SSL-Zertifikat für AD FS?
Das AD FS SSL-Zertifikat ist nicht identisch mit dem Zertifikat für die AD FS-Dienstkommunikation, das im Snap-in „AD FS-Verwaltung“ enthalten ist.  Zum Ändern des AD FS SSL-Zertifikats müssen Sie PowerShell verwenden. Führen Sie dazu die Schritte in folgendem Artikel aus:

[Verwalten von SSL-Zertifikaten in AD FS und WAP 2016](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)

### <a name="how-can-i-enable-or-disable-tlsssl-settings-for-ad-fs"></a>Wie kann ich TLS/SSL-Einstellungen für AD FS aktivieren oder deaktivieren?
Zum Deaktivieren oder Aktivieren von SSL-Protokollen und -Verschlüsselungssammlungen verwenden Sie Folgendes:

[Verwalten von SSL-Protokollen in AD FS](../operations/Manage-SSL-Protocols-in-AD-FS.md)

### <a name="does-the-proxy-ssl-certificate-have-to-be-the-same-as-the-ad-fs-ssl-certificate"></a>Muss das Proxy-SSL-Zertifikat mit dem AD FS SSL-Zertifikat identisch sein?  
Verwenden Sie die folgenden Anleitungen im Hinblick auf das SSL-Proxyzertifikat und das AD FS SSL-Zertifikat:


- Wenn der Proxy für AD FS-Anforderungen eingesetzt wird, die die integrierte Windows-Authentifizierung verwenden, muss das Proxy-SSL-Zertifikat mit dem SSL-Zertifikat des Verbundservers identisch sein (verwenden Sie denselben Schlüssel).
- Wenn die AD FS-Eigenschaft „ExtendedProtectionTokenCheck“ aktiviert ist (die Standardeinstellung in AD FS), muss das Proxy-SSL-Zertifikat mit dem SSL-Zertifikat des Verbundservers identisch sein (verwenden Sie denselben Schlüssel).
- Andernfalls kann das Proxy-SSL-Zertifikat einen anderen Schlüssel als das AD FS SSL-Zertifikat haben, muss aber dieselben [Anforderungen](../overview/AD-FS-2016-Requirements.md) erfüllen.

### <a name="why-do-i-only-see-a-password-login-on-ad-fs-and-not-my-other-authentication-methods-that-i-have-configured"></a>Warum zeigt mir AD FS nur eine Kennwortanmeldung und nicht die anderen von mir konfigurierten Authentifizierungsmethoden an? 
AD FS zeigt im Anmeldebildschirm nur eine einzige Authentifizierungsmethode an, wenn die Anwendung explizit einen bestimmten Authentifizierungs-URI erfordert, der einer konfigurierten und aktivierten Authentifizierungsmethode zugeordnet ist. Dies wird bei WS-Verbund-Anforderungen im Parameter „wauth“ und in einer SAML-Protokollanforderung im Parameter „RequestedAuthnCtxRef“ übermittelt. Deshalb wird nur die angeforderte Authentifizierungsmethode angezeigt (z. B. Anmeldung mit Kennwort).

Wenn AD FS bei Azure AD verwendet wird, senden Anwendungen normalerweise den Parameter „prompt=login“ an Azure AD. Azure AD übersetzt dies standardmäßig, um ein neues Kennwort anzufordern, das auf der Anmeldung bei AD FS basiert. Dies ist der häufigste Grund dafür, dass eine Kennwortanmeldung bei AD FS in Ihrem Netzwerk angezeigt oder eine Option zur Anmeldung mit Ihrem Zertifikat nicht angezeigt wird. Dies kann problemlos behoben werden, indem Sie in Azure AD eine Änderung an den Einstellungen der Verbunddomäne vornehmen. 

Informationen dazu, wie dies konfiguriert wird, finden Sie unter [Active Directory Federation Services prompt=login parameter support](../operations/AD-FS-Prompt-Login.md) (Unterstützung in Active Directory-Verbunddienste (AD FS) für den Parameter „prompt=login“).

### <a name="how-can-i-change-the-ad-fs-service-account"></a>Wie kann ich das AD FS-Dienstkonto ändern?
Führen Sie zum Ändern des AD FS-Dienstkontos die Anleitungen aus, bei denen die Toolbox [Service Account Powershell Module](https://github.com/Microsoft/adfsToolbox/tree/master/serviceAccountModule) (Dienstkonto „PowerShell-Modul“) verwendet wird.

### <a name="how-can-i-configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>Wie kann ich Browser für die Verwendung der integrierten Windows-Authentifizierung (Windows Integrated Authentication, WIA) mit AD FS konfigurieren?

Informationen zum Konfigurieren von Browsern finden Sie unter [Konfigurieren von Browsern zur Verwendung der integrierten Windows-Authentifizierung (WIA) mit AD FS](../operations/Configure-AD-FS-Browser-WIA.md).

### <a name="can-i-turn-off-browserssoenabled"></a>Kann ich „BrowserSsoEnabled“ deaktivieren?
Wenn Sie keine Zugriffssteuerungsrichtlinien, die auf dem Gerät in AD FS basieren, oder keine Windows Hello for Business-Zertifikatregistrierung mithilfe von AD FS haben, können Sie „BrowserSsoEnabled“ deaktivieren. „BrowserSsoEnabled“ ermöglicht es AD FS, ein PRT (Primary Refresh Token, Primäres Aktualisierungstoken) von einem Client zu erfassen, der Geräteinformationen enthält. Ohne diese Geräteauthentifizierung funktioniert AD FS nicht auf Windows 10-Geräten.

### <a name="how-long-are-ad-fs-tokens-valid"></a>Wie lange sind AD FS-Token gültig?

Diese Frage bedeutet oft: „Wie lange ist für Benutzer einmaliges Anmelden (Single Sign on, SSO) möglich, ohne dass sie neue Anmeldinformationen eingeben müssen, und wie kann ich das als Administrator steuern?“  Dieses Verhalten und die Konfigurationseinstellungen zur entsprechenden Steuerung werden im Artikel [AD FS: Einstellungen für einmaliges Anmelden](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-2016-single-sign-on-settings) beschrieben.

Die Standardlebensdauern der verschiedenen Cookies und Token (sowie die Parameter zur Steuerung der Lebensdauern) sind unten aufgeführt :

**Registrierte Geräte**

- PRT- und SSO-Cookies: Maximal 90 Tage, gesteuert durch „PSSOLifeTimeMins“. (Das bereitgestellte Gerät wird mindestens alle 14 Tage verwendet, und dies wird durch „DeviceUsageWindow“ gesteuert.)

- Aktualisierungstoken: Wird basierend auf den vorstehenden Angaben berechnet, um ein einheitliches Verhalten zu bieten.

- access_token: Standardmäßig 1 Stunde, basierend auf der vertrauenden Seite.

- id_token: identisch mit access_token

**Nicht registrierte Geräte**

- SSO-Cookies: Standardmäßig 8 Stunden, gesteuert durch „SSOLifetimeMins“.  Wenn „Angemeldet bleiben“ (Keep Me Signed in, KMSI) aktiviert ist, beträgt die Standarddauer 24 Stunden, und dies kann über „KMSILifetimeMins“ konfiguriert werden.


- Aktualisierungstoken: Standardmäßig 8 Stunden. 24 Stunden bei aktiviertem Schlüsselverwaltungsdienst.

- access_token: Standardmäßig 1 Stunde, basierend auf der vertrauenden Seite.

- id_token: identisch mit access_token

### <a name="does-ad-fs-support-http-strict-transport-security-hsts"></a>Unterstützt AD FS das Feature HTTP Strict Transport Security (HSTS)?  

HTTP Strict Transport Security (HSTS) ist ein Richtlinienmechanismus für Websicherheit, mit dessen Hilfe Angriffe zur Herabstufung des Protokolls und Cookieübernahme für Dienste reduziert werden, die sowohl über HTTP- als auch über HTTPS-Endpunkte verfügen. Auf diese Weise können Webserver deklarieren, dass Webbrowser (oder andere dementsprechende Benutzer-Agents) nur mit HTTPS und niemals über das HTTP-Protokoll interagieren sollten.

Alle AD FS-Endpunkte für den Webauthentifizierungsdatenverkehr werden ausschließlich über HTTPS geöffnet.  Folglich reduziert AD FS effektiv die Bedrohungen, die durch den Mechanismus der Richtlinie HTTP Strict Transport Security geboten werden (entwurfsbedingt erfolgt keine Herabstufung auf HTTP, da es in HTTP keine Listener gibt). Außerdem verhindert AD FS, dass Cookies mit HTTP-Protokollendpunkten an einen anderen Server gesendet werden, indem alle Cookies mit dem Secure-Flag gekennzeichnet werden.

Deshalb ist die Implementierung von HSTS auf einem AD FS-Server nicht erforderlich, weil er nie herabgestuft werden kann.  Aus Kompatibilitätsgründen erfüllen AD FS-Server diese Anforderungen, weil sie niemals HTTP verwenden können und alle Cookies als sicher gekennzeichnet sind.

Darüber hinaus unterstützen AD FS 2016 (mit den neuesten Patches) und AD FS 2019 die Ausgabe des HSTS-Headers. Informationen zur dafür erforderlichen Konfiguration finden Sie unter [Anpassen der HTTP-Sicherheitsantwortheader mit AD FS](../operations/customize-http-security-headers-ad-fs.md).

### <a name="x-ms-forwarded-client-ip-does-not-contain-the-ip-of-the-client-but-contains-ip-of-the-firewall-in-front-of-the-proxy-where-can-i-get-the-right-ip-of-the-client"></a>„X-ms-forwarded-client-ip“ enthält nicht die IP-Adresse des Clients; enthalten ist aber die IP-Adresse der Firewall vor dem Proxy. Wo kann ich die richtige IP-Adresse für den Client abrufen?
Es wird davon abgeraten, SSL vor WAP zu beenden. Wenn SSL vor dem WAP beendet wird, enthält „X-ms-forwarded-client-ip“ die IP-Adresse des Netzwerkgeräts vor WAP. Im Folgenden finden Sie eine kurze Beschreibung der verschiedenen IP-bezogenen Ansprüche, die von AD FS unterstützt werden:
 - x-ms-client-ip: Netzwerk-IP-Adresse des Geräts, das mit dem STS verbunden ist.  Eine Extranetanforderung enthält immer die IP-Adresse des WAP.
 - x-ms-forwarded-client-ip: Ein mehrwertiger Anspruch, der alle von Exchange Online an AD FS weitergeleiteten Werte sowie die IP-Adresse des Geräts enthält, das mit dem WAP verbunden ist.
 - Userip: Bei Extranetanforderungen enthält dieser Anspruch den Wert von „x-ms-forwarded-client-ip“.  Bei Intranetanforderungen enthält dieser Anspruch denselben Wert wie „x-ms-client-ip“.

 Außerdem wird in AD FS 2016 (mit den neuesten Patches) und höheren Versionen auch das Erfassen des Headers „x-forwarded-for“ unterstützt. Ein Lastenausgleichsmodul oder Netzwerkgerät, das nicht auf Ebene 3 weitergeleitet wird (IP-Adresse wird beibehalten), sollte die eingehende Client-IP-Adresse dem Header nach Branchenstandard „x-forwarded-for“ hinzufügen. 

### <a name="i-am-trying-to-get-additional-claims-on-the-user-info-endpoint-but-its-only-returning-subject-how-can-i-get-additional-claims"></a>Ich versuche, zusätzliche Ansprüche auf dem Benutzerinformationsendpunkt abzurufen, doch er gibt nur den Antragsteller zurück. Wie kann ich weitere Ansprüche abrufen?
Der AD FS-Benutzerinformationsendpunkt gibt – wie in den OpenID-Standards festgelegt – immer den Antragstelleranspruch zurück. AD FS stellt keine zusätzlichen Ansprüche bereit, die über den UserInfo-Endpunkt angefordert werden. Wenn Sie zusätzliche Ansprüche im ID-Token benötigen, lesen Sie [Benutzerdefinierte ID-Token in AD FS](../development/custom-id-tokens-in-ad-fs.md).

### <a name="why-do-i-see-a-lot-of-1021-errors-on-my-ad-fs-servers"></a>Warum werden auf meinen AD FS-Servern viele Fehler des Typs „1021“ angezeigt?
Dieses Ereignis wird normalerweise bei einem ungültigen Ressourcenzugriff auf AD FS für die Ressource „00000003-0000-0000-c000-000000000000“ protokolliert. Dieser Fehler wird durch ein fehlerhaftes Verhalten des Clients verursacht, wenn er versucht, ein Zugriffstoken für den Azure AD Graph-Dienst abzurufen. Da die Ressource in AD FS nicht vorhanden ist, führt dies auf den AD FS-Servern zur Ereignis-ID 1021. Es ist sicher, etwaige Warnungen oder Fehler für die Ressource „00000003-0000-0000-C000-000000000000“ in AD FS zu ignorieren.

### <a name="why-am-i-seeing-a-warning-for-failure-to-add-the-ad-fs-service-account-to-the-enterprise-key-admins-group"></a>Warum wird eine Warnung angezeigt, dass beim Hinzufügen des AD FS-Dienstkontos zur Gruppe “Enterprise Key Admins“ ein Fehler aufgetreten ist?
Diese Gruppe wird nur erstellt, wenn ein Windows 2016-Domänencontroller mit der FSMO-PDC-Rolle in der Domäne vorhanden ist. Zur Behebung des Fehlers können Sie die Gruppe manuell erstellen und die nachstehenden Schritte ausführen, um die erforderliche Berechtigung zu erteilen, nachdem Sie das Dienstkonto als Gruppenmitglied hinzugefügt haben.
1.  Öffnen Sie **Active Directory-Benutzer und -Computer**.
2.  Klicken Sie im Navigationsbereich **mit der rechten Maustaste** auf Ihren Domänennamen, und **klicken** Sie dann auf „Eigenschaften“.
3.  **Klicken** Sie auf „Sicherheit“ (wenn die Registerkarte „Sicherheit“ nicht vorhanden ist, aktivieren Sie über das Menü „Ansicht“ die Option „Erweiterte Funktionen“).
4.  **Klicken** Sie auf „Erweitert“. **Klicken** Sie auf „Hinzufügen“. **Klicken** Sie auf „Prinzipal auswählen“.
5.  Das Dialogfeld „Benutzer, Computer, Dienstkonto oder Gruppe auswählen“ wird geöffnet.  Geben Sie im Textfeld „Geben Sie den zu verwendenden Objektnamen ein“ den Namen „Key Admin-Gruppe“ ein.  Klicken Sie auf OK.
6.  Wählen Sie im Listenfeld „Gilt für“ die Option **Nachgeordnete Benutzerobjekte** aus.
7.  Scrollen Sie mit der Bildlaufleiste zum unteren Bereich der Seite, und **klicken** Sie auf „Alle löschen“.
8.  Wählen Sie im Abschnitt **Eigenschaften** die Optionen **msDS-KeyCredentialLink lesen** und **msDS-KeyCredentialLink schreiben** aus.

### <a name="why-does-modern-authentication-from-android-devices-fail-if-the-server-does-not-send-all-the-intermediate-certificates-in-the-chain-with-the-ssl-cert"></a>Warum schlägt die moderne Authentifizierung von Android-Geräten fehl, wenn der Server nicht alle Zwischenzertifikate in der Kette mit dem SSL-Zertifikat sendet?

Bei Verbundbenutzern kann die Authentifizierung bei Azure AD für Apps, die die Android-ADAL-Bibliothek nutzen, fehlschlagen. Bei der App tritt ein **AuthenticationException**-Fehler auf, wenn Sie die Anmeldeseite anzuzeigen versucht. In Chrome wird die AD FS-Anmeldeseite möglicherweise als unsicher bezeichnet.

Android unterstützt – in allen Versionen und auf allen Geräten – nicht das Herunterladen zusätzlicher Zertifikate über das Feld **authorityInformationAccess** des Zertifikats. Dies gilt auch für den Chrome-Browser. Bei jedem Serverauthentifizierungszertifikat, bei dem Zwischenzertifikate fehlen, tritt dieser Fehler auf, wenn die gesamte Zertifikatskette nicht von AD FS übergeben wird.

Eine geeignete Lösung für dieses Problem besteht darin, die AD FS-und WAP-Server so zu konfigurieren, dass die erforderlichen Zwischenzertifikate zusammen mit dem SSL-Zertifikat gesendet werden.

Sorgen Sie beim Exportieren des SSL-Zertifikats von einem Computer, der in den persönlichen Computerspeicher des/der AD FS- und WAP-Server(s) importiert werden soll, dafür, dass Sie den privaten Schlüssel exportieren und **Privater Informationsaustausch – PKCS #12** auswählen.

Es ist wichtig, das Kontrollkästchen **Wenn möglich, alle Zertifikate im Zertifizierungspfad einbeziehen** sowie **Alle erweiterten Eigenschaften exportieren** zu aktivieren.  

Führen Sie „certlm.msc“ auf den Windows-Servern aus, und importieren Sie die *.PFX in den Zertifikatspeicher „Persönlich“ des Computers. Dies bewirkt, dass der Server die gesamte Zertifikatskette an die ADAL-Bibliothek übergibt.

>[!NOTE]
> Der Zertifikatspeicher von Netzwerklastenausgleichsmodulen sollte ebenfalls aktualisiert werden, um die gesamte Zertifikatskette einzubeziehen (sofern vorhanden).

### <a name="does-ad-fs-support-head-requests"></a>Unterstützt AD FS HEAD-Anforderungen?
AD FS unterstützt keine HEAD-Anforderungen.  Anwendungen sollten keine HEAD-Anforderungen für AD FS-Endpunkte verwenden.  Dies kann nämlich zu unerwarteten und/oder verzögerten HTTP-Fehlerantworten führen.  Außerdem werden möglicherweise im AD FS-Ereignisprotokoll unerwartete Fehlerereignisse angezeigt.

### <a name="why-am-i-not-seeing-a-refresh-token-when-i-am-logging-in-with-a-remote-idp"></a>Warum wird kein Aktualisierungstoken angezeigt, wenn ich mich mit einem Remote-IdP anmelde?
Es wird kein Aktualisierungstoken ausgegeben, wenn das von IdP ausgegebene Token weniger als 1 Stunde gültig ist. Wenn Sie sicherstellen möchten, dass ein Aktualisierungstoken ausgegeben wird, verlängern Sie die Gültigkeit des vom IdP ausgestellten Tokens auf mehr als 1 Stunde.

### <a name="do-we-have-any-way-to-change-rp-token-encryption-algorithm"></a>Gibt es eine Möglichkeit zum Ändern des Verschlüsselungsalgorithmus für das RP-Token?
Die RP-Tokenverschlüsselung ist standardmäßig auf „AES256“ festgelegt und kann nicht auf einen anderen Wert geändert werden.

### <a name="on-a-mixed-mode-farm-i-get-error-when-trying-to-set-the-new-ssl-certificate-using-set-adfssslcertificate--thumbprint-how-can-i-update-the-ssl-certificate-in-a-mixed-mode-ad-fs-farm"></a>In einer Farm mit gemischtem Modus wird ein Fehler angezeigt, wenn ich versuche, das neue SSL-Zertifikat mit „Set-AdfsSslCertificate -Thumbprint“ festzulegen. Wie kann ich das SSL-Zertifikat in eine AD FS-Farm im gemischtem Modus aktualisieren?
AD FS-Farmen im gemischtem Modus sollen nur als vorübergehender Status dienen. Es wird empfohlen, dass Sie während Ihrer Planung entweder ein Rollover des SSL-Zertifikats vor dem Upgradevorgang ausführen oder erst den Vorgang beenden und die Farmverhaltensebene erhöhen, bevor Sie das SSL-Zertifikat aktualisieren. Wenn das nicht geschehen ist, können Sie mit den nachstehenden Anweisungen das SSL-Zertifikat aktualisieren. 

Auf WAP-Servern können Sie „Set-WebApplicationProxySslCertificate“ weiterhin verwenden. Auf den AD FS-Servern müssen Sie Netsh verwenden. Führen Sie die nachstehend aufgeführten Schritte aus:

1. Eine Teilmenge von AD FS 2016-Servern zu Wartungszwecken auswählen (z. B. zum Entfernen aus dem Lastenausgleich)
2. Das neue Zertifikat auf den in #1 ausgewählten Servern über MMC importieren
3. Die vorhandenen Zertifikate löschen

    ein. netsh http delete sslcert hostnameport=fs.contoso.com:443 b. netsh http delete sslcert hostnameport=localhost:443 c. netsh http delete sslcert hostnameport=fs.contoso.com:49443

4.  Das neue Zertifikat hinzufügen

    ein. netsh http add sslcert hostnameport=fs.contoso.com:443 certhash=CERTTHUMBPRINT appid={5d89a20c-beab-4389-9447-324788eb944a} certstorename=MY sslctlstorename=AdfsTrustedDevices

    b. netsh http add sslcert hostnameport=localhost:443 certhash=CERTTHUMBPRINT appid={5d89a20c-beab-4389-9447-324788eb944a} certstorename=MY sslctlstorename=AdfsTrustedDevices

    c. netsh http add sslcert hostnameport=fs.contoso.com:49443 certhash=CERTTHUMBPRINT appid={5d89a20c-beab-4389-9447-324788eb944a} certstorename=MY sslctlstorename=AdfsTrustedDevices

5. Den AD FS-Dienst auf dem ausgewählten Server neu starten
6. Eine Teilmenge von WAP-Servern zu Wartungszwecken entfernen
7. Das neue Zertifikat auf den ausgewählten WAP-Servern über MMC importieren
8. Das neue Zertifikat für WAP mithilfe des Cmdlets festlegen

    ein. Set-WebApplicationProxySslCertificate -Thumbprint „CERTTHUMBPRINT“

9. Neustarten des Diensts auf den ausgewählten WAP-Servern
10. Versetzen Sie die ausgewählten WAP- und AD FS-Server zurück in die Produktionsumgebung.

Führen Sie das Update auf den restlichen AD FS- und WAP-Servern in ähnlicher Weise aus.

### <a name="is-adfs-supported-when-web-application-proxy-wap-servers-are-behind-azure-web-application-firewallwaf"></a>Wird AD FS unterstützt, wenn sich WAP-Server (Webanwendungsproxy) hinter der Azure-Webanwendungsfirewall (Web Application Firewall, WAF) befinden?
AD FS- und Webanwendungsserver unterstützen jede Firewall, die keine SSL-Beendigung auf dem Endpunkt ausführt. Darüber hinaus verfügen AD FS-/WAP-Server über integrierte Mechanismen, um häufige Webangriffe wie z. B. websiteübergreifende Skripts, auf AD FS-Proxy zu verhindern und alle Anforderungen zu erfüllen, die durch das [MS-ADFSPIP-Protokoll](https://msdn.microsoft.com/library/dn392811.aspx) definiert wurden.

### <a name="i-am-seeing-an-event-441-a-token-with-a-bad-token-binding-key-was-found-what-should-i-do-to-resolve-this"></a>Es wird angezeigt „Event 441: A token with a bad token binding key was found.“ (Ereignis 441: Ein Token mit einem ungültigen Tokenbindungsschlüssel wurde gefunden.) Was soll ich tun, um dieses Problem zu beheben?
In AD FS 2016 wird die Tokenbindung automatisch aktiviert. Das verursacht mehrere bekannte Probleme bei Proxy- und Verbundszenarien, die schließlich zu diesem Fehler führen. Führen Sie zum Beheben dieses Problems den folgenden PowerShell-Befehl aus, und entfernen Sie die Unterstützung für das Bindungstoken.

`Set-AdfsProperties -IgnoreTokenBinding $true`

### <a name="i-have-upgraded-my-farm-from-ad-fs-in-windows-server-2016-to-ad-fs-in-windows-server-2019-the-farm-behavior-level-for-the-ad-fs-farm-has-been-successfully-raised-to-2019-but-the-web-application-proxy-configuration-is-still-displayed-as-windows-server-2016"></a>Ich habe meine Farm von AD FS in Windows Server 2016 auf AD FS in Windows Server 2019 aktualisiert. Die Farmverhaltensebene für die AD FS-Farm wurde erfolgreich auf 2019 erhöht, aber die Konfiguration des Webanwendungsproxys wird weiterhin als Windows Server 2016 angezeigt – warum?
Nach einem Upgrade auf Windows Server 2019 wird die Konfigurationsversion des Webanwendungsproxys weiterhin als Windows Server 2016 angezeigt. Der Webanwendungsproxy verfügt über keine neuen versionsspezifischen Features für Windows Server 2019. Wenn die Farmverhaltensebene in AD FS erfolgreich erhöht wurde, wird der Proxy entwurfsbedingt weiterhin als Windows Server 2016 angezeigt.

### <a name="can-i-estimate-the-size-of-the-adfsartifactstore-before-enabling-esl"></a>Kann ich die Größe von „ADFSArtifactStore“ vor dem Aktivieren von ESL schätzen?
Bei aktiviertem ESL verfolgt AD FS die Kontoaktivität und die bekannten Speicherorte für Benutzer in der ADFSArtifactStore-Datenbank nach. Die Größe dieser Datenbank wird relativ zur Anzahl der nachverfolgten Benutzer und bekannten Standorte skaliert. Beim Planen der Aktivierung von ESL können Sie die Größenzunahme für die ADFSArtifactStore-Datenbank auf eine Rate von bis zu 1 GB pro 100.000 Benutzer schätzen. Wenn die AD FS-Farm die interne Windows-Datenbank (Windows Internal Database, WID) verwendet, ist der Standardspeicherort für die Datenbankdateien „C:\Windows\WID\Data“. Um das Auffüllen dieses Laufwerks zu verhindern, stellen Sie sicher, dass mindestens 5 GB freier Speicherplatz verfügbar sind, bevor Sie ESL aktivieren. Planen Sie zusätzlich zum Datenträgerspeicher, dass der gesamte Prozessspeicher nach der Aktivierung von ESL um bis zu weitere 1 GB RAM für Benutzerauffüllungen von maximal 500.000 größer wird.
