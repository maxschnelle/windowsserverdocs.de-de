---
ms.assetid: a3f50046-5d48-43d3-b0f8-ac2346b15285
title: Verwalten von SSL-Zertifikaten in AD FS und WAP in Windows Server 2016
description: Verwalten von SSL-Zertifikaten in AD FS und WAP in Windows Server 2016
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/02/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b832756e123bee0223738ee804ac3a4db2371e84
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855293"
---
# <a name="managing-ssl-certificates-in-ad-fs-and-wap-in-windows-server-2016"></a>Verwalten von SSL-Zertifikaten in AD FS und WAP in Windows Server 2016



In diesem Artikel wird beschrieben, wie Sie ein neues SSL-Zertifikat für Ihre AD FS-und WAP-Server bereitstellen.

>[!NOTE]
>Die empfohlene Vorgehensweise, um das SSL-Zertifikat für eine AD FS-Farm zu ersetzen, besteht in der Verwendung von Azure AD Connect.  Weitere Informationen finden Sie [unter Aktualisieren des SSL-Zertifikats für eine Active Directory-Verbunddienste (AD FS)-Farm (AD FS)](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectfed-ssl-update) .

## <a name="obtaining-your-ssl-certificates"></a>Abrufen der SSL-Zertifikate
Für Produktions AD FS Farmen wird ein öffentlich vertrauenswürdiges SSL-Zertifikat empfohlen. Dies wird in der Regel durch übermitteln einer Zertifikat Signier Anforderung (Certificate Signing Request, CSR) an einen öffentlichen Zertifikat Anbieter eines Drittanbieters erreicht. Es gibt eine Vielzahl von Möglichkeiten, die CSR zu generieren, einschließlich von einem Computer mit Windows 7 oder höher. Der Anbieter sollte über eine Dokumentation verfügen.

- Stellen Sie sicher, dass das Zertifikat die [SSL-Zertifikat Anforderungen für AD FS-und Webanwendung](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

### <a name="how-many-certificates-are-needed"></a>Erforderliche Anzahl von Zertifikaten
Es wird empfohlen, ein gemeinsames SSL-Zertifikat für alle AD FS-und webanwendungsproxy-Server zu verwenden. Ausführliche Informationen finden Sie im Dokument [AD FS und SSL-Zertifikat Anforderungen für den webanwendungsproxy](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

### <a name="ssl-certificate-requirements"></a>SSL-Zertifikatanforderungen
Informationen zu Anforderungen einschließlich Benennung, Stamm der Vertrauensstellung und Erweiterungen finden Sie in den Dokumenten [AD FS und SSL-Zertifikat Anforderungen des webanwendungspro](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

## <a name="replacing-the-ssl-certificate-for-ad-fs"></a>Ersetzen des SSL-Zertifikats für AD FS
> [!NOTE]
> Das AD FS SSL-Zertifikat ist nicht identisch mit dem Zertifikat für die AD FS-Dienstkommunikation, das im Snap-in „AD FS-Verwaltung“ enthalten ist. Um das AD FS SSL-Zertifikat zu ändern, müssen Sie PowerShell verwenden.

Legen Sie zunächst fest, in welchem Zertifikat Bindungs Modus Ihre AD FS Server ausgeführt werden: Standard Zertifikat-Authentifizierungs Bindung oder alternativer Client-TLS-Bindungs Modus.

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-default-certificate-authentication-binding-mode"></a>Ersetzen des SSL-Zertifikats für AD FS, das im standardmäßigen Zertifikat Authentifizierungs Bindungs Modus ausgeführt wird
AD FS standardmäßig die Authentifizierung von Geräte Zertifikaten an Port 443 und die Benutzerzertifikat Authentifizierung an Port 49443 (oder einem konfigurierbaren Port, der nicht 443 ist) ausführt.
Verwenden Sie in diesem Modus das PowerShell-Cmdlet Set-adfssslcertificate, um das SSL-Zertifikat zu verwalten.

Führen Sie die unten beschriebenen Schritte aus.

1. Zunächst müssen Sie das neue Zertifikat abrufen. Dies erfolgt in der Regel durch übermitteln einer Zertifikat Signier Anforderung (Certificate Signing Request, CSR) an einen öffentlichen Zertifikat Anbieter eines Drittanbieters. Es gibt eine Vielzahl von Möglichkeiten, die CSR zu generieren, einschließlich von einem Computer mit Windows 7 oder höher. Der Anbieter sollte über eine Dokumentation verfügen.

    * Stellen Sie sicher, dass das Zertifikat die [SSL-Zertifikat Anforderungen für AD FS-und Webanwendung](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

1. Nachdem Sie die Antwort von Ihrem Zertifikat Anbieter erhalten haben, importieren Sie Sie auf jedem AD FS-und webanwendungsproxy-Server in den Speicher des lokalen Computers.

1. Verwenden Sie auf dem **primären** AD FS Server das folgende Cmdlet, um das neue SSL-Zertifikat zu installieren.

```powershell
Set-AdfsSslCertificate -Thumbprint '<thumbprint of new cert>'
```

Sie können den Zertifikat Fingerabdruck durch Ausführen des folgenden Befehls finden:

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>Weitere Hinweise

* Beim Cmdlet "Set-ADF ssslcertificate" handelt es sich um ein Cmdlet mit mehreren Knoten. Dies bedeutet, dass Sie nur vom primären Replikat ausgeführt werden muss und alle Knoten in der Farm aktualisiert werden. Dies ist neu in Server 2016. Auf Server 2012 R2 mussten Sie Set-adfssslcertificate auf jedem Server ausführen.
* Das Set-adfssslcertificate-Cmdlet muss nur auf dem primären Server ausgeführt werden. Auf dem primären Server muss Server 2016 ausgeführt werden, und die Ebene des Farm Verhaltens muss auf 2016.
* Das Cmdlet "Set-adfssslcertificate" verwendet PowerShell-Remoting, um die anderen AD FS Server zu konfigurieren. Stellen Sie sicher, dass Port 5985 (TCP) auf den anderen Knoten geöffnet ist.
* Mit dem Cmdlet "Set-adfssslcertificate" erhält der adfssrv-Prinzipal Leseberechtigungen für die privaten Schlüssel des SSL-Zertifikats. Dieser Prinzipal stellt den AD FS Dienstanbieter dar. Es ist nicht notwendig, dem AD FS-Dienst Konto Lesezugriff auf die privaten Schlüssel des SSL-Zertifikats zu gewähren.

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-alternate-tls-binding-mode"></a>Ersetzen des SSL-Zertifikats für AD FS, die im alternativen TLS-Bindungs Modus ausgeführt werden
Wenn Sie im alternativen Client-TLS-Bindungs Modus konfiguriert ist, werden AD FS die Gerätezertifikat Authentifizierung an Port 443 und die Benutzerzertifikat Authentifizierung an Port 443 auch unter einem anderen Hostnamen durchführen. Der Hostname des Benutzer Zertifikats ist der AD FS Hostname, dem "certauth" vorausgeht, z. b. "certauth.fs.contoso.com".
Verwenden Sie in diesem Modus das PowerShell-Cmdlet Set-adfsalternatetlsclientbinding, um das SSL-Zertifikat zu verwalten. Dadurch wird nicht nur die Alternative Client-TLS-Bindung verwaltet, sondern auch alle anderen Bindungen, für die AD FS das SSL-Zertifikat festlegt.

Führen Sie die unten beschriebenen Schritte aus.

1. Zunächst müssen Sie das neue Zertifikat abrufen. Dies erfolgt in der Regel durch übermitteln einer Zertifikat Signier Anforderung (Certificate Signing Request, CSR) an einen öffentlichen Zertifikat Anbieter eines Drittanbieters. Es gibt eine Vielzahl von Möglichkeiten, die CSR zu generieren, einschließlich von einem Computer mit Windows 7 oder höher. Der Anbieter sollte über eine Dokumentation verfügen.

    * Stellen Sie sicher, dass das Zertifikat die [SSL-Zertifikat Anforderungen für AD FS-und Webanwendung](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

1. Nachdem Sie die Antwort von Ihrem Zertifikat Anbieter erhalten haben, importieren Sie Sie auf jedem AD FS-und webanwendungsproxy-Server in den Speicher des lokalen Computers.

1. Verwenden Sie auf dem **primären** AD FS Server das folgende Cmdlet, um das neue SSL-Zertifikat zu installieren.

```powershell
Set-AdfsAlternateTlsClientBinding -Thumbprint '<thumbprint of new cert>'
```

Sie können den Zertifikat Fingerabdruck durch Ausführen des folgenden Befehls finden:

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>Weitere Hinweise

* Das Cmdlet "Set-ADF salternatetlsclientbinding" ist ein Cmdlet mit mehreren Knoten. Dies bedeutet, dass Sie nur vom primären Replikat ausgeführt werden muss und alle Knoten in der Farm aktualisiert werden.
* Das Set-adfsalternatetlsclientbinding-Cmdlet muss nur auf dem primären Server ausgeführt werden. Auf dem primären Server muss Server 2016 ausgeführt werden, und die Ebene des Farm Verhaltens muss auf 2016.
* Das Cmdlet "Set-adfsalternatetlsclientbinding" verwendet PowerShell-Remoting, um die anderen AD FS Server zu konfigurieren. Stellen Sie sicher, dass Port 5985 (TCP) auf den anderen Knoten geöffnet ist.
* Mit dem Cmdlet "Set-adfsalternatetlsclientbinding" erhält der adfssrv-Prinzipal Leseberechtigungen für die privaten Schlüssel des SSL-Zertifikats. Dieser Prinzipal stellt den AD FS Dienstanbieter dar. Es ist nicht notwendig, dem AD FS-Dienst Konto Lesezugriff auf die privaten Schlüssel des SSL-Zertifikats zu gewähren.

## <a name="replacing-the-ssl-certificate-for-the-web-application-proxy"></a>Ersetzen des SSL-Zertifikats für den webanwendungsproxy
Zum Konfigurieren der standardmäßigen Zertifikat Authentifizierungs Bindung oder des alternativen Client-TLS-Bindungs Modus auf dem WAP können wir das Cmdlet Set-webapplicationproxysslcertificate verwenden.
Verwenden Sie zum Ersetzen des SSL-Zertifikats für den webanwendungsproxy auf **jedem** webanwendungsproxy-Server das folgende Cmdlet zum Installieren des neuen SSL-Zertifikats

```powershell
Set-WebApplicationProxySslCertificate -Thumbprint '<thumbprint of new cert>'
```

Wenn das obige Cmdlet fehlschlägt, weil das alte Zertifikat bereits abgelaufen ist, konfigurieren Sie den Proxy mithilfe der folgenden Cmdlets neu:

```powershell
$cred = Get-Credential
```

Geben Sie die Anmelde Informationen eines Domänen Benutzers ein, der auf dem AD FS Server als lokaler Administrator angemeldet ist.

```powershell
Install-WebApplicationProxy -FederationServiceTrustCredential $cred -CertificateThumbprint '<thumbprint of new cert>' -FederationServiceName 'fs.contoso.com'
```

## <a name="additional-references"></a>Weitere Verweise  
* [AD FS: Unterstützung der alternativen Hostnamenbindung für die Zertifikatauthentifizierung](../operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)
* [Eigenschaften Informationen für die AD FS-und Zertifikat KeySpec](../technical-reference/AD-FS-and-KeySpec-Property.md)
