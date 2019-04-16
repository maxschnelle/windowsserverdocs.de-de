---
ms.assetid: 1ea2e1be-874f-4df3-bc9a-eb215002da91
title: "Konfigurieren von AD FS-Unterstützung für die Zertifikatauthentifizierung für Benutzer"
description: 
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 01/18/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.service: active-directory
ms.technology: identity-adfs
ms.openlocfilehash: 9941d4dd997e857874aceddc920ec7f9d8944a81
ms.sourcegitcommit: d351cdbb0bf2533d6db35626ebbc4924b3834309
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/23/2018
---
# <a name="configuring-ad-fs-for-user-certificate-authentication"></a>Konfigurieren von AD FS für die Zertifikatauthentifizierung für Benutzer

>Gilt für: Windows Server 2016, Windows Server2012 R2

AD FS kann konfiguriert werden, für die benutzerzertifikatauthentifizierung verwenden einen der Modi in beschrieben X509 [in diesem Artikel](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md). Diese Funktion verwendet werden kann [mit Azure Active Directory](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/) oder eigenständig, zum Aktivieren von Clients und Geräten mit bereitgestellt Benutzerzertifikate für den Zugriff auf AD FS Ressourcen im Intranet oder extranet.

## <a name="prerequisites"></a>Erforderliche Komponenten
- Stellen Sie sicher, dass Ihre Benutzerzertifikate alle AD FS und WAP-Server als vertrauenswürdig eingestuft werden
- Stellen Sie sicher, dass das Stammzertifikat der Vertrauenskette für Ihre Benutzerzertifikate im NTAuth-Speicher in Active Directory ist
- Wenn AD FS alternatives Zertifikat Authentifizierungsmodus verwenden, stellen Sie sicher, dass Ihre AD FS und WAP-Server SSL-Zertifikate verfügen, die den AD FS-Hostnamen mit dem Präfix "Certauth", z. B. "certauth.fs.contoso.com," enthalten und diesen Datenverkehr mit diesem Hostnamen zugeordnet ist zulässig, durch die firewall
- Über das extranet der Zertifikatauthentifizierung, sicher, dass mindestens ein AIA und mindestens eine CDP oder OCSP Speicherort aus der Liste, angegeben in Ihre Zertifikate aus dem Internet zugegriffen werden kann.
- Wenn Sie AD FS für Azure AD-Clientzertifikatauthentifizierung konfigurieren, stellen Sie sicher, dass Sie konfiguriert haben die [Azure AD-Einstellungen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-certificate-based-authentication-get-started#step-2-configure-the-certificate-authorities) und [AD FS Anspruchsregeln erforderlich](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-certificate-based-authentication-ios#requirements) für Zertifikate Aussteller und Seriennummer
- Auch muss für Azure AD-Zertifikatauthentifizierung für Exchange ActiveSync-Clients das Clientzertifikat Benutzer Routingfähigen E-Mail-Adresse in Exchange verfügen online in den Prinzipal Namen oder den Wert des Alternativer Antragstellername RFC822 Namens. (Azure Active Directory wird den Wert RFC822 Proxyadresse-Attribut im Verzeichnis.)

## <a name="configure-ad-fs-for-user-certificate-authentication"></a>Konfigurieren von AD FS für die Zertifikatauthentifizierung für Benutzer  
- Die aktivieren Sie Zertifikatauthentifizierung als Intranet oder extranet Authentifizierungsmethode in AD FS, mit der AD FS-Verwaltungskonsole oder das PowerShell-Cmdlet Set-AdfsGlobalAuthenticationPolicy Benutzer
- Stellen Sie sicher, dass die gesamte Kette der Vertrauensstellung einschließlich alle Zwischenzertifizierungsstellen-Zertifikate auf jedem AD FS und WAP-Server installiert ist. Die Zwischenzertifizierungsstellen-Zertifikate sollte in den lokalen Computer Zwischenzertifizierungsstellen Speicher für alle AD FS und WAP-Server installiert werden.
- Wenn Sie Ansprüche basierend auf Zertifikatfelder und Erweiterungen neben EKU (Anspruchstyp https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku) verwenden möchten, konfigurieren Sie zusätzliche Anspruch Pass-Through-Regeln für die Active Directory-Anspruchsanbieter-Vertrauensstellung.  Nachfolgend finden Sie eine vollständige Liste der verfügbaren Zertifikat Ansprüche.  
- [Optional] Konfigurieren von zulässigen ausstellenden Zertifizierungsstellen für Clientzertifikate, die mit den Richtlinien unter "Verwaltung vertrauenswürdiger Aussteller zur Clientauthentifizierung" in [in diesem Artikel](https://technet.microsoft.com/en-us/library/dn786429(v=ws.11).aspx).

## <a name="configure-seamless-certificate-authentication-for-chrome-browser-on-windows-desktops"></a>Konfigurieren Sie eine nahtlose Authentifizierung per Clientzertifikat für Chrome-Browser für Windows-Desktops
Wenn mehrere Zertifikate (z.B. WLAN-Zertifikate) auf dem Computer, die im Rahmen der Authentifizierung des Clients entsprechen verfügbar sind, fordert der Chrome-Browser auf Windows-Desktop den Benutzer das richtige Zertifikat auswählen. Dies kann für den Benutzer verwirrend sein. Um diese Erfahrung zu optimieren, können Sie eine Richtlinie für Chrome das richtige Zertifikat für eine bessere Benutzererfahrung automatische Auswahl festlegen. Diese Richtlinie kann nur eine registrierungsänderung manuell festlegen oder automatisch über ein Gruppenrichtlinienobjekt (zum Festlegen von Registrierungsschlüsseln) konfiguriert werden. Dies erfordert Ihre Benutzer Clientzertifikate für die Authentifizierung mit AD FS unterschiedliche Aussteller in anderen Fällen haben. 

Weitere Informationen zum Konfigurieren von dies für Chrome verwenden Sie Sie [Link](http://www.chromium.org/administrators/policy-list-3#AutoSelectCertificateForUrls).  


## <a name="troubleshooting"></a>Problembehandlung
- Wenn zertifikatanforderungen für die Authentifizierung mit einer "Nicht von https://certauth.fs.contoso.com Content" HTTP 204-Antwort Fehler auftreten, stellen Sie sicher, dass die Stamm- und alle Zwischenzertifizierungsstellen-Zertifikate, bzw. installiert sind, auf die vertrauenswürdige Stammzertifizierungsstelle und zwischen-ZS Zertifikatspeichern auf allen Verbundservern.
- Wenn Zertifikatanforderungen für die Authentifizierung für aus unbekannten Gründen fehlschlagen, exportieren Sie das Clientzertifikat in eine CER-Datei, und führen Sie den Befehl 

`certutil -f -urlfetch -verify certificatefilename.cer`

Stellen Sie sicher, alle Zertifikatsperrlisten und Delta-Zertifikatsperrlisten-Speicherorte auflösen.  Beachten Sie, dass Delta-Zertifikatsperrlisten-Speicherorte basierend auf den Inhalt von der Basis-Zertifikatsperrliste gefunden werden.

## <a name="reference-complete-list-of-user-certificate-claim-types-and-example-values"></a>Referenz: Die vollständige Liste der Benutzerzertifikat geltend machen, Typen und Beispielwerte

|Typ des Anspruchs|Beispiel für einen Wert
|-----|-----
|https://schemas.microsoft.com/2012/12/certificatecontext/field/x509version | 3
|https://schemas.microsoft.com/2012/12/certificatecontext/field/signaturealgorithm | sha256RSA
|https://schemas.microsoft.com/2012/12/certificatecontext/field/issuer | CN = OrgZert, DC = Domain, DC = Contoso, DC = com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/issuername | CN = OrgZert, DC = Domain, DC = Contoso, DC = com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/notbefore | 12/05/2016 20:50:18
|https://schemas.microsoft.com/2012/12/certificatecontext/field/notafter | 12/05/2017 20:50:18
|https://schemas.microsoft.com/2012/12/certificatecontext/field/subject | E =user@contoso.com, CN = Benutzer, CN = Users, DC = Domain, DC = Contoso, DC = com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/subjectname | E =user@contoso.com, CN = Benutzer, CN = Users, DC = Domain, DC = Contoso, DC = com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/rawdata | {Base64-codierte Daten des digitalen Zertifikats}
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage | DigitalSignature
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage | KeyEncipherment
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/subjectkeyidentifier | 9D11941EC06FACCCCB1B116B56AA97F3987D620A
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/authoritykeyidentifier | Schlüssel-ID = d6 13 e3 6 b bc e5 d8 15 52 0a fd 36 6a d5 0 b 51 f3 0 b 25 7f
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/certificatetemplatename | Benutzer
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/san | Andere Namen: Principal Name =user@contoso.com, RFC822 Name =user@contoso.com
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku | 1.3.6.1.4.1.311.10.3.4


