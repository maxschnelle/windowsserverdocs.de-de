---
ms.assetid: 1ea2e1be-874f-4df3-bc9a-eb215002da91
title: Konfigurieren der AD FS-Unterstützung für die Authentifizierung mit Benutzerzertifikat
description: ''
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 01/18/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2d819ea036029fbe7cfde9ad5a445db6b2b42c96
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189696"
---
# <a name="configuring-ad-fs-for-user-certificate-authentication"></a>Konfigurieren von AD FS für die Authentifizierung mit Benutzerzertifikat


AD FS kann konfiguriert werden, für die Authentifizierung mit Benutzerzertifikat mithilfe einer der Modi, die in beschriebenen X509 [in diesem Artikel](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md). Diese Funktion kann verwendet werden, [in Azure Active Directory](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/) oder allein, um Clients und Geräten ermöglichen mit bereitgestellt wurde von Benutzerzertifikaten für den Zugriff auf AD FS Ressourcen über das Intranet oder extranet.

## <a name="prerequisites"></a>Vorraussetzungen
- Stellen Sie sicher, dass Ihre Benutzerzertifikate von allen AD FS- und WAP-Servern als vertrauenswürdig eingestuft werden
- Stellen Sie sicher, dass das Stammzertifikat von der Vertrauenskette für Ihre Benutzerzertifikate im NTAuth-Speicher in Active Directory ist
- Wenn AD FS im alternativem Zertifikat-Authentifizierungsmodus verwenden, stellen Sie sicher, dass Ihre AD FS und WAP-Server SSL-Zertifikate, die mit den AD FS-Hostnamen, die mit dem Präfix "Certauth", z. B. "certauth.fs.contoso.com," aufweisen, und diesen Datenverkehr mit diesem Hostnamen ist zulässig. durch die firewall
- Wenn Sie über das extranet-Zertifikatauthentifizierung verwenden möchten, sicherstellen Sie, dass mindestens einen AIA- und mindestens eine CDP oder OCSP-Standort aus der Liste, die in Ihrer Zertifikate angegeben über das Internet zugegriffen werden kann.
- Wenn Sie AD FS für die Azure AD-Zertifikat-Authentifizierung konfigurieren möchten, stellen Sie sicher, dass Sie konfiguriert haben die [Azure AD-Einstellungen](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-get-started#step-2-configure-the-certificate-authorities) und [AD FS-Anspruchsregeln erforderlich](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-ios#requirements) für Zertifikat Aussteller und Seriennummer
- Außerdem muss für Azure AD-Zertifikat-Authentifizierung für Exchange ActiveSync-Clients das Clientzertifikat die routingfähige e-Mail-Adresse von Benutzern in Exchange verfügen online in entweder als Prinzipalname oder der Wert des RFC822-Namens im Feld Alternativer Antragstellername. (Azure Active Directory ordnet den RFC822-Wert, mit dem Proxy-Adresse-Attribut in das Verzeichnis).

## <a name="configure-ad-fs-for-user-certificate-authentication"></a>Konfigurieren von AD FS für die Benutzerauthentifizierung Zertifikat  
- Aktivieren der Authentifizierung mit Benutzerzertifikat als Intranet oder extranet Authentifizierungsmethode in AD FS mit der AD FS-Verwaltungskonsole oder das PowerShell-Cmdlet Set-AdfsGlobalAuthenticationPolicy
- Stellen Sie sicher, dass die gesamte Kette der Vertrauensstellung einschließlich alle Zwischenzertifikate auf jedem AD FS- und WAP-Server installiert ist. Die Zwischenzertifikate sollte in den Speicher des lokalen Computers Zwischenzertifizierungsstellen Behörden auf allen AD FS- und WAP-Servern installiert werden.
- Wenn Sie Ansprüche, die basierend auf Clientzertifikatfelder und Erweiterungen zusätzlich zu EKU verwenden möchten (Anspruchstyp https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku), konfigurieren Sie zusätzliche Anspruch Pass-through-Regeln für die Active Directory Anspruchsanbieter-Vertrauensstellung.  Nachfolgend finden Sie eine vollständige Liste der verfügbaren Zertifikatsspeicher Ansprüche.  
- [Optional] Konfigurieren von zulässigen ausstellenden Zertifizierungsstellen für Clientzertifikate, die mithilfe der Anleitungen unter "Verwaltung vertrauenswürdiger Aussteller zur Clientauthentifizierung" in [in diesem Artikel](https://technet.microsoft.com/library/dn786429(v=ws.11).aspx).

## <a name="configure-seamless-certificate-authentication-for-chrome-browser-on-windows-desktops"></a>Konfigurieren Sie nahtlose Zertifikatauthentifizierung für Chrome-Browser auf Windows-Desktops
Wenn mehrere Zertifikate für Benutzer (z. B. Wi-Fi-Zertifikaten), die auf dem Computer, die den Zweck der Clientauthentifizierung erfüllen vorhanden sind, fordert der Chrome-Browser auf Windows-Desktop den Benutzer das richtige Zertifikat auswählen. Dies kann für den Endbenutzer verwirrend sein. Um diese Funktion zu optimieren, können Sie eine Richtlinie für Chrome, um das richtige Zertifikat für eine bessere benutzererfahrung automatische Auswahl festlegen. Diese Richtlinie kann manuell festlegen, indem Sie eine registrierungsänderung vornehmen oder automatisch über ein Gruppenrichtlinienobjekt (zum Festlegen von Registrierungsschlüsseln) konfiguriert werden. Dies erfordert der Clientzertifikate für den Benutzer, für die Authentifizierung bei AD FS, um unterschiedliche Aussteller in anderen Fällen haben. 

Weitere Informationen zum Konfigurieren dieser für Chrome verwenden Sie Sie [Link](http://www.chromium.org/administrators/policy-list-3#AutoSelectCertificateForUrls).  


## <a name="troubleshooting"></a>Problembehandlung
- Wenn Fehlschlagen von zertifikatanforderungen für die Authentifizierung mit einem HTTP 204 "kein Inhalt über Https:\//certauth.fs.contoso.com"-Antwort, stellen Sie sicher, dass die Stamm- und alle Zwischenzertifizierungsstellen-Zertifikate, auf die vertrauenswürdige Stammzertifizierungsstelle installiert sind, und Speichert den Zwischenzertifizierungsstellen-Zertifikat auf allen Verbundservern.
- Wenn zertifikatanforderungen für die Authentifizierung aus unbekannten Gründen fehlschlagen, exportieren Sie des Clientzertifikats in eine CER-Datei, und führen Sie den Befehl 

`certutil -f -urlfetch -verify certificatefilename.cer`

Stellen Sie sicher, alle CRL und Delta-Zertifikatsperrlisten-Speicherorte auflösen.  Beachten Sie, dass Delta-Zertifikatsperrlisten-Speicherorte auf Basis der Inhalte der Basis-CRL gefunden werden.

## <a name="reference-complete-list-of-user-certificate-claim-types-and-example-values"></a>Referenz: Vollständige Liste der Benutzerzertifikat anspruchtypen und Beispielwerte

|Anspruchstyp|Beispielwert
|-----|-----
|https://schemas.microsoft.com/2012/12/certificatecontext/field/x509version | 3
|https://schemas.microsoft.com/2012/12/certificatecontext/field/signaturealgorithm | sha256RSA
|https://schemas.microsoft.com/2012/12/certificatecontext/field/issuer | CN=entca, DC=domain, DC=contoso, DC=com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/issuername | CN=entca, DC=domain, DC=contoso, DC=com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/notbefore | 12/05/2016 20:50:18
|https://schemas.microsoft.com/2012/12/certificatecontext/field/notafter | 12/05/2017 20:50:18
|https://schemas.microsoft.com/2012/12/certificatecontext/field/subject | E =user@contoso.com, CN = Benutzer, CN = Users, DC = Domain, DC = Contoso, DC = com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/subjectname | E =user@contoso.com, CN = Benutzer, CN = Users, DC = Domain, DC = Contoso, DC = com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/rawdata | {Base64-codierte Daten des digitalen Zertifikats}
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage | DigitalSignature
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage | KeyEncipherment
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/subjectkeyidentifier | 9D11941EC06FACCCCB1B116B56AA97F3987D620A
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/authoritykeyidentifier | KeyID=d6 13 e3 6b bc e5 d8 15 52 0a fd 36 6a d5 0b 51 f3 0b 25 7f
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/certificatetemplatename | Benutzer
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/san | Andere Namen: Prinzipalname =user@contoso.com, RFC822-namens =user@contoso.com
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku | 1.3.6.1.4.1.311.10.3.4


