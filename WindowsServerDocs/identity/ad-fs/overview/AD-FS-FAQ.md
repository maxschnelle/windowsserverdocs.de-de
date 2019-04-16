---
ms.assetid: acc9101b-841c-4540-8b3c-62a53869ef7a
title: "AD FS 2016 – HÄUFIG GESTELLTE FRAGEN"
description: "Häufig gestellte Fragen für AD FS 2016"
author: jenfieldmsft
ms.author: billmath
manager: femila
ms.date: 03/06/2018
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 313447d2c92c15505434ec5c39898ca84aef46db
ms.sourcegitcommit: 556361fe7c73c75d6cdc46a67dc88679fbe89c61
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="ad-fs-frequently-asked-questions-faq"></a>AD FS-häufig gestellte Fragen (FAQ)

>Gilt für: Windows Server 2016

Die folgende Dokumentation ist ein Haus auf häufig gestellte Fragen in Bezug auf Active Directory Federation Services.  Das Dokument wurde basierend auf den Typ der Frage in Gruppen aufgeteilt.

## <a name="deployment"></a>Bereitstellung 

### <a name="how-can-i-upgrademigrate-from-previous-versions-of-ad-fs"></a>Wie kann ich Upgrade/von früheren Versionen von AD FS migrieren
Sie können mithilfe einer der folgenden AD FS aktualisieren:


- Windows Server2012 R2 AD FS zu Windows Server2016 AD FS
    - [Upgrade von ADFS in Windows Server2016 mithilfe einer WID-Datenbank](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)
    - [Upgrade von ADFS in Windows Server2016 mithilfe einer SQL-Datenbank](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL.md)
- Windows Server2012 AD FS to Windows Server2012 R2 AD FS
    - [Migrieren Sie zu AD FS unter Windows Server2012 R2](https://technet.microsoft.com/library/dn486815.aspx)
- AD FS 2.0 zu Windows Server2012 AD FS
    - [Migrieren Sie zu AD FS unter Windows Server 2012](https://technet.microsoft.com/library/jj647765.aspx)
- AD FS 1.x, um die AD FS 2.0 
    - [Ein Upgrade von AD FS 1.x, um die AD FS 2.0](https://technet.microsoft.com/library/ff678035.aspx)

Wenn Sie ein Upgrade von AD FS 2.0 oder 2.1 (Windows Server2008 R2 oder Windows Server2012) ausführen möchten, müssen Sie den in-Box-Skripts (im C:\Windows\ADFS) verwenden.

### <a name="why-does-ad-fs-installation-require-a-reboot-of-the-server"></a>Warum ist die AD FS-Installation einen Neustart des Servers erforderlich?

HTTP/2-Unterstützung in Windows Server2016 hinzugefügt wurde, aber HTTP/2 nicht für die Authentifizierung per Clientzertifikat verwendet werden.  Da viele Szenarien für AD FS Verwendung der Authentifizierung per Clientzertifikat und eine größere Anzahl von Clients führen keine Unterstützung für wiederholen machen-Anforderungen mit HTTP/1.1, AD FS-Farm Konfiguration neu konfiguriert des lokalen Servers HTTP-Einstellungen auf HTTP/1.1.  Dies erfordert einen Neustart des Servers.  

### <a name="is-using-windows-2016-wap-servers-to-publish-the-ad-fs-farm-to-the-internet-without-upgrading-the-back-end-ad-fs-farm-supported"></a>Ist Windows2016 WAP-Servern mithilfe die AD FS-Farm mit dem Internet zu veröffentlichen, ohne dass eine Aktualisierung der Back-End-AD FS-Farm unterstützt?
Ja, wird diese Konfiguration unterstützt, jedoch keine neuen Features für AD FS 2016 in dieser Konfiguration unterstützt werden würde.  Diese Konfiguration gilt als temporäre während der Migration von AD FS 2012 R2 AD FS 2016 und für einen längeren Zeitraum nicht bereitgestellt werden.

## <a name="design"></a>Design

### <a name="what-third-party-multi-factor-authentication-providers-are-available-for-ad-fs"></a>Welche Multi-Factor Authentication-Anbieter von Drittanbietern sind für AD FS verfügbar? 
Es folgt eine Liste der Drittanbieter-Anbieter, denen wir kennen.  Möglicherweise gibt es immer Anbieter zur Verfügung, wir wissen nicht zu, und wir die Liste aktualisieren werden, wie wir diese Informationen.

- [Gemalto Identitäts- & Sicherheitsdienste](http://www.gemalto.com/identity)
- [InWebo Enterprise Authentication-Dienst](http://www.inwebo.com/)
- [Melden Sie sich Personen MFA-API-Connector](https://www.loginpeople.com)
- [RSA SecurID Authentication Agent für Microsoft Active Directory-Verbunddienste](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)
- [SafeNet Authentifizierung (SAS)-Dienst-Agent für AD FS](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)
- [Swisscom Mobile-ID-Authentifizierungsdienst](http://swisscom.ch/mid)
- [Symantec-Überprüfung und ID-Schutzdienst (VIP)](http://www.symantec.com/vip-authentication-service) 

### <a name="are-third-party-proxies-supported-with-ad-fs"></a>Werden Drittanbieter-Proxys werden mit AD FS unterstützt?
Ja, vor the Web Application Proxy können von Drittanbietern Proxys platziert werden, aber Drittanbieter-Proxy muss unterstützen die [MS-ADFSPIP Protokoll](https://msdn.microsoft.com/library/dn392811.aspx) anstelle der Web Application Proxy verwendet werden.

### <a name="what-third-party-proxies-are-available-for-ad-fs-that-support-ms-adfspip"></a>Welche Drittanbieter-Proxys für AD FS verfügbar sind, die MS-ADFSPIP unterstützen?

Es folgt eine Liste der Drittanbieter-Anbieter, denen wir kennen.  Möglicherweise gibt es immer Anbieter zur Verfügung, wir wissen nicht zu, und wir die Liste aktualisieren werden, wie wir diese Informationen.

- [F5 Access-Richtlinien-Manager](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-third-party-integration-13-1-0/12.html#guid-1ee8fbb3-1b33-4982-8bb3-05ae6868d9ee)

### <a name="where-is-the-capacity-planning-sizing-spreadsheet-for-ad-fs-2016"></a>Wo ist die Kapazität Dimensionierung für AD FS 2016 planen?
Die AD FS 2016-Version der Kalkulationstabelle heruntergeladen werden kann [hier](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx).
Dies kann auch für AD FS unter Windows Server2012 R2 verwendet werden.

### <a name="how-can-i-ensure-my-ad-fs-and-wap-servers-support-apples-atp-requirements"></a>Wie kann ich meine AD FS und WAP-Server-Unterstützung von Apple ATP Anforderungen sicherstellen?

Apple stellt eine Reihe von Anforderungen, die App Transport Security (ATS), die Aufrufe von iOS-Apps auswirken können, die Authentifizierung bei AD FS aufgerufen.  Sie können sicherstellen, dass Ihre AD FS und WAP-Servern entsprechen, indem Sie sicherstellen, dass sie unterstützen die [Anforderungen für das Herstellen einer Verbindung mit ATS](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57).  
Insbesondere sollten Sie sicherstellen, dass Ihre AD FS und WAP-Server TLS 1.2 unterstützen und die TLS-Verbindung ausgehandelte Verschlüsselungssammlung unterstützt, die mit perfect forward Secrecy.

Sie können aktivieren und Deaktivieren von SSL 2.0 und 3.0 und TLS Version 1.0, 1.1 und 1.2 mit [verwalten SSL-Protokolle in AD FS](../operations/Manage-SSL-Protocols-in-AD-FS.md).

Um sicherzustellen, dass Ihre AD FS und WAP Server aushandeln nur TLS-Verschlüsselungssammlungen, die ATP unterstützen, können Sie alle Verschlüsselungssammlungen ab, die nicht in Deaktivieren der [Liste der kompatiblen Verschlüsselungssammlungen ATP](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57).  Verwenden Sie hierzu die [Windows TLS-PowerShell-Cmdlets](https://technet.microsoft.com/itpro/powershell/windows/tls/index). 


## <a name="operations"></a>Vorgänge

### <a name="how-do-i-replace-the-ssl-certificate-for-ad-fs"></a>Wie ersetzen kann ich das SSL-Zertifikat für AD FS? 
Das AD FS-SSL-Zertifikat ist nicht identisch mit AD FS dienstkommunikationszertifikat finden Sie in der AD FS-Verwaltungs-Snap-In.  Um das AD FS-SSL-Zertifikat zu ändern, müssen Sie mithilfe von PowerShell. Folgen Sie den Anweisungen im folgenden Artikel:

[Verwalten von SSL-Zertifikaten in AD FS und WAP 2016](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)

### <a name="how-can-i-enable-or-disable-tlsssl-settings-for-ad-fs"></a>Wie kann ich aktivieren oder Deaktivieren von TLS/SSL-Einstellungen für AD FS
Verwenden Sie zum Deaktivieren oder Aktivieren von SSL-Protokolle und Verschlüsselungssuiten, folgende Schritteaus:

[Verwalten von SSL-Protokolle in AD FS](../operations/Manage-SSL-Protocols-in-AD-FS.md)

### <a name="does-the-proxy-ssl-certificate-have-to-be-the-same-as-the-ad-fs-ssl-certificate"></a>Verfügt die Proxy-SSL-Zertifikat des AD FS-SSL-Zertifikats identisch sein?  
Verwenden Sie die folgende Richtlinien in Bezug auf die Proxy-SSL-Zertifikat und das AD FS-SSL-Zertifikat:


- Wenn der Proxy, um verwendet wird müssen AD FS-Proxy-Anfragen, die integrierte Windows-Authentifizierung, die Proxy-SSL-Zertifikat verwenden identisch sein (mit dem gleichen Schlüssel) das SSL-Zertifikat Föderation
- Wenn die AD FS-Eigenschaft, die "ExtendedProtectionTokenCheck" ist (die Standardeinstellung in AD FS) aktiviert ist, muss die Proxy-SSL-Zertifikat identisch sein (verwenden Sie den gleichen Schlüssel) das SSL-Zertifikat Föderation
- Andernfalls die Proxy-SSL-Zertifikat kann einen anderen Schlüssel aus dem AD FS-SSL-Zertifikat verfügen, aber erfüllt die gleiche [Anforderungen](../overview/AD-FS-2016-Requirements.md)

### <a name="how-can-i-configure-promptlogin-behavior-for-ad-fs"></a>Wie kann ich die Eingabeaufforderung konfigurieren Anmeldung Verhalten für AD FS =?
Informationen zum Konfigurieren der Aufforderung = Anmeldung, finden Sie unter [Active Directory Federation Services auffordern = Anmelde-Parameter Unterstützung](../operations/AD-FS-Prompt-Login.md).

### <a name="how-can-i-configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>Wie kann ich Browser Windows integrierte Authentifizierung (WIA) mit AD FS konfigurieren?

Informationen zum Konfigurieren von Browsern finden Sie unter [konfigurieren Browser, um Windows integrierte Authentifizierung (WIA) mit AD FS verwenden](../operations/Configure-AD-FS-Browser-WIA.md).


### <a name="how-long-are-ad-fs-tokens-valid"></a>Wie lange sind die AD FS-Token gültig?

Häufig bedeutet, dass diese Frage "wie lange Benutzer erhalte für einmaliges Anmelden (SSO) ohne neue Anmeldeinformationen eingeben zu müssen, und wie kann ich als Administrator, die steuern?"  Dieses Verhalten und die Konfigurationseinstellungen, die steuern, in diesem Artikel beschriebenen [hier](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/ad-fs-2016-single-sign-on-settings).

Die Standardwerte für die Gültigkeitsdauer der verschiedenen Cookies und Token sind unten aufgeführt, (sowie die Parameter, die bestimmen, die Lebensdauer):

**Registrierte Geräte**

- Druck und SSO Cookies: 90Tage maximale, unterliegt PSSOLifeTimeMins. (Bereitgestellten Gerät wird mindestens alle 14Tage verwendet, die durch DeviceUsageWindow gesteuert wird)

- Aktualisieren von Token: berechnet anhand der oben genannten einheitliches Verhalten bereitstellen

- Access_Token: 1 Stunde standardmäßig basierend auf die vertrauende Seite

- ID_Token: wie Zugriffstoken

**Nicht registrierte Geräte**

- SSO Cookies: 8 Stunden in der Standardeinstellung unterliegt SSOLifetimeMins.  Wenn beibehalten, die ich angemeldet (KMSI) aktiviert ist, wird standardmäßig 24 Stunden und konfigurierbar über KMSILifetimeMins.


- Aktualisieren von Token: standardmäßig acht Stunden. 24 Stunden mit KMSI aktiviert

- Access_Token: 1 Stunde standardmäßig basierend auf die vertrauende Seite

- ID_Token: wie Zugriffstoken

### <a name="does-ad-fs-support-http-strict-transport-security-hsts"></a>Unterstützt die AD FS-HTTP-Strict Transport Security (HSTS)?  

HTTP Strict Transport Security (HSTS) handelt es sich um eine Web-Richtlinie Sicherheitsmechanismus Dies trägt zu verringern, Protokoll Downgrade-Angriffe und Cookie-Missbrauch für Dienste, die HTTP- und HTTPS-Endpunkte haben. Es kann Webserver zu deklarieren, dass Webbrowser (oder andere leitete Benutzer-Agents) nur mit HTTPS und nie über die HTTP-Protokoll interagieren soll.

Alle AD FS-Endpunkte für Web-Authentifizierungsdatenverkehr werden ausschließlich über HTTPS geöffnet.  AD FS reduziert daher effektiv die Bedrohungen, bei denen HTTP-Strict Transport Security Policy Mechanismus (ist es kein Downgrade HTTP gab es keine Listener in HTTP). Darüber hinaus verhindert, dass AD FS Cookies auf einen anderen Server mit HTTP-Protokoll-Endpunkten gesendet werden, indem Sie alle Cookies mit dem sicheren Flag markiert.

Aus diesem Grund ist implementieren HSTS auf einem AD FS-Server nicht erforderlich, da es nie herabgestuft werden kann.  Zur Einhaltung von Vorschriften werden die folgenden Anforderungen von AD FS-Server erfüllen, da sie nie HTTP verwenden können, und alle Cookies sicheren gekennzeichnet sind.

### <a name="x-ms-forwarded-client-ip-does-not-contain-the-ip-of-the-client-but-contains-ip-of-the-firewall-in-front-of-the-proxy-where-can-i-get-the-right-ip-of-the-client"></a>X-ms-weitergeleitet-Client-IP-enthält IP-Adresse der Firewall vor der Proxy jedoch enthält nicht die IP-Adresse des dem Client. Wo finde ich die richtige IP-Adresse des dem Client?
Es wird nicht empfohlen, SSL-Tunnelabschluss vor WAP tun. Für den Fall, dass SSL-Tunnelabschluss vor dem drahtlosen Zugriffspunkt abgeschlossen ist, wird die X-ms-weitergeleitet-Client-IP-die IP-Adresse des das Netzwerkgerät vor WAP enthalten. Im Folgenden ist eine kurze Beschreibung der verschiedenen IP-Ansprüche in Bezug, die von AD FS unterstützt werden:
 - X-ms-Client-Ip: Netzwerk IP-Adresse des Geräts, das mit der STS verbunden.  Bei einer Extranet-Anforderung enthält diese immer die IP-Adresse des dem drahtlosen Zugriffspunkt.
 - X-ms-weitergeleitet-Client-Ip: mehrwertige Anspruch die enthält alle Werte an AD FS durch Exchange Online und die IP-Adresse des Geräts, das Verbindung mit dem drahtlosen Zugriffspunkt weitergeleitet.
 - Userip: Für Extranet-Anforderungen werden diesem Anspruch den Wert der X-ms-weitergeleitet-Client-IP-enthalten.  Für Intranet-Anforderungen wird diesem Anspruch den gleichen Wert wie X-ms-Client-IP-enthalten.

### <a name="i-am-trying-to-get-additional-claims-on-the-user-info-endpoint-but-its-only-returning-subject-how-can-i-get-additional-claims"></a>Ich versuche, um zusätzliche Ansprüche auf dem Endpunkt der Benutzer Informationen zu erhalten, aber es wird nur zurückgegeben, Betreff. Wie erhalte ich zusätzliche Ansprüche?
Der AD FS-Endpunkt Userinfo gibt immer den Betreff Anspruch gemäß den Standards OpenID zurück. AD FS bietet keine zusätzliche Ansprüche, die über den Endpunkt UserInfo angefordert. Wenn Sie zusätzliche Ansprüche in Tokens ID benötigen, finden Sie unter [benutzerdefinierte ID Token in AD FS](../development/custom-id-tokens-in-ad-fs.md).

### <a name="why-do-i-see-alot-of-1021-errors-on-my-ad-fs-servers"></a>Warum sehe ich auf Meine AD FS-Server viele 1021 Fehler?
Dieses Ereignis wird in der Regel für eine ungültige Zugriff auf Ressourcen auf AD FS für die Ressource 00000003-0000-0000-c000-000000000000 protokolliert. Dieser Fehler wird durch eine fehlerhafte Verhalten des Clients verursacht, in denen versucht wird, ein Zugriffstoken für den Dienst von Azure AD-Diagramm abzurufen. Da die Ressource nicht auf AD FS vorhanden ist, führt dies im Ereignis-ID 1021 auf die AD FS-Server. Es ist Warn- oder Fehlermeldungen für die Ressource 00000003-0000-0000-c000-000000000000 von AD FS ignoriert. 

### <a name="why-am-i-seeing-a-warning-for-failure-to-add-the-ad-fs-service-account-to-the-enterprise-key-admins-group"></a>Warum sehe ich eine Warnung für Fehler bei der Gruppe der Unternehmensadministratoren Schlüssel der AD FS-Dienstkonto hinzu?
Diese Gruppe wird nur erstellt, wenn ein Windows2016-Domänencontroller mit der PDC-FSMO-Rolle in der Domäne vorhanden ist. Um den Fehler zu beheben, können Sie die Gruppe manuell erstellen und befolgen Sie die unten, um nach dem Hinzufügen des Dienstkontos als Mitglied der Gruppe die Berechtigung zu erteilen.
1.  Öffnen **Active Directory-Benutzer und -Computer**. 
2.  **Mit der rechten Maustaste** Ihren Domänennamen im Navigationsbereich und **klicken Sie auf** Eigenschaften.
3.  **Klicken Sie auf** Sicherheit (fehlt die Registerkarte "Sicherheit", aktivieren Sie erweiterte Funktionen aus dem Menü "Ansicht").
4.  **Klicken Sie auf** erweitert. **Klicken Sie auf** hinzufügen. **Klicken Sie auf** Prinzipal auswählen.
5.  Das Dialogfeld Benutzer, Computer, Dienstkonto oder Gruppe angezeigt wird.  Geben Sie im Feld Geben Sie die zu verwendenden Objektnamen Textfeld Schlüssel administrativen Gruppe.  Klicken Sie auf OK.
6.  Wählen Sie in das Listenfeld, **Nachfolger Benutzerobjekte**.
7.  Verwenden die Bildlaufleiste, scrollen Sie zum unteren Rand der Seite und **klicken Sie auf** alle löschen.
8.  In der **Eigenschaften** Abschnitt **Lesen des MsDS-KeyCredentialLink** und **schreiben MsDS-KeyCrendentialLink**.

### <a name="why-does-modern-authentication-from-android-devices-fail-if-the-server-does-not-send-all-the-intermediate-certificates-in-the-chain-with-the-ssl-cert"></a>Warum fehl moderne von Android-Geräte, wenn der Server nicht alle Zwischenzertifizierungsstellen-Zertifikate in der Kette mit dem SSL-Zertifikat sendet?

Verbundbenutzer können Authentifizierung mit Azure AD für Apps auftreten, die den Android ADAL Bibliothek fehlerhaften verwenden. Die App erhalten eine **AuthenticationException** wenn er versucht, die Anmeldeseite angezeigt. In der AD FS-Chrom kann Anmeldeseite als unsicher aufgerufen werden.

Android – für alle Versionen und alle Geräte – unterstützt keine herunterladen zusätzliche Zertifikate von der **AuthorityInformationAccess** Feld des Zertifikats. Dies gilt auch für Chrome-Browsers zur Verfügung. Alle Serverauthentifizierungszertifikat, die Zwischenzertifizierungsstellen-Zertifikate nicht angezeigt wird, wird dieser Fehler führen, wenn die gesamte Zertifikatkette nicht von AD FS übergeben wird. 

Eine richtige Lösung für dieses Problem wird so konfigurieren Sie die AD FS und WAP-Server, um die erforderlichen Zwischenzertifizierungsstellen-Zertifikate und das SSL-Zertifikat zu senden. 

Stellen Sie beim Exportieren des SSL-Zertifikats von einem Computer, auf den persönlichen Speicher des Computers, der AD FS und WAP-Server importiert werden so exportieren Sie den privaten Schlüssel, und wählen Sie **privater Informationsaustausch – PKCS 12**. 

Es ist wichtig, dass das Kontrollkästchen **, wenn möglich, alle Zertifikate im Zertifizierungspfad einbeziehen** aktiviert ist, sowie **alle erweiterte Eigenschaften exportieren**. 

Führen Sie certlm.msc auf Windows-Servern und importieren Sie die *. PFX in persönlichen Zertifikatspeicher des Computers. Dadurch wird den Server die gesamte Zertifikatkette der ADAL Bibliothek übergeben. 

>[!NOTE]
> Zertifikat Store des Netzwerks Lastenausgleichsmodule sollten ebenfalls aktualisiert werden die gesamte Zertifikatkette, falls vorhanden

### <a name="does-ad-fs-support-head-requests"></a>Unterstützt die AD FS HEAD-Anfragen?
AD FS unterstützt HEAD-Anfragen nicht.  Anwendungen sollten nicht HEAD-Anforderungen anhand der AD FS-Endpunkte verwenden.  Dadurch kann HTTP-Fehlerseiten, die unerwartete und/oder verzögert werden.  Darüber hinaus können Sie unerwartete Fehlerereignisse im AD FS-Ereignisprotokoll finden Sie unter.

### <a name="why-am-i-not-seeing-a-refresh-token-when-i-am-logging-in-with-a-remote-idp"></a>Warum sehe ich die keinen Aktualisierungstoken ich die Anmeldung mit einem Remote-IdP bin?
Ein Aktualisierungstoken wird nicht ausgegeben, wenn der IdP ausgestellte Token eine Validty von weniger als 1 Stunde hat. Um sicherzustellen, dass ein Aktualisierungstoken ausgestellt wurde, erhöhen Sie die Gültigkeit der IdP auf mehr als 1 Stunde ausgestellte Token.
