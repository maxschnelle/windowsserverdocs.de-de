---
ms.assetid: a3f50046-5d48-43d3-b0f8-ac2346b15285
title: Verwalten von SSL-Zertifikaten in AD FS und WAP in WindowsServer 2016
description: Verwalten von SSL-Zertifikaten in AD FS und WAP in WindowsServer 2016
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/02/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5156b3ad357ab8edb5e08a89a459beaf9b8c9b1a
ms.sourcegitcommit: ca7dc3d56a33924ae5fe0e9ffb1274da6dc4e54d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/03/2017
---
# <a name="managing-ssl-certificates-in-ad-fs-and-wap-in-windows-server-2016"></a>Verwalten von SSL-Zertifikaten in AD FS und WAP in WindowsServer 2016

>Gilt für: Windows Server 2016

Dieser Artikel beschreibt, wie Sie ein neues SSL-Zertifikat für Ihre AD FS und WAP-Server bereitstellen.

>[!NOTE]
>Die empfohlene Vorgehensweise für das SSL-Zertifikat für eine AD FS-Farm in Zukunft zu ersetzen ist die Verwendung von Azure AD Connect.  Weitere Informationen finden Sie unter [aktualisieren Sie das SSL-Zertifikat für eine Farm mit Active Directory-Verbunddienste (AD FS)](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectfed-ssl-update)

## <a name="obtaining-your-ssl-certificates"></a>Abrufen von SSL-Zertifikate
Für Produktions-AD FS-Farmen wird öffentlich vertrauenswürdiges SSL-Zertifikat empfohlen. Dies wird in der Regel durch übermitteln ein Zertifikat signieren zertifikatsignieranforderung (CSR) an einen dritten, öffentliche Zertifikatanbieter abgerufen. Es gibt eine Vielzahl von Möglichkeiten zum Generieren der CSR, einschließlich der von Windows 7 oder höher PC. Der Anbieter sollte die Dokumentation für diese verfügen.

- Stellen Sie sicher, dass das Zertifikat erfüllt die [AD FS und Web Application Proxy-SSL-zertifikatanforderungen](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

### <a name="how-many-certificates-are-needed"></a>Wie viele Zertifikate erforderlich sind
Es wird empfohlen, dass Sie ein gemeinsames SSL-Zertifikat für alle AD FS und Web Application Proxy Server verwenden. Detaillierte Anforderungen finden Sie in das Dokument [AD FS und Web Application Proxy-SSL-zertifikatanforderungen](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

### <a name="ssl-certificate-requirements"></a>SSL-Zertifikatanforderungen
Anforderungen, z. B. den Namen, Stamm-Vertrauensstellung und Erweiterungen finden Sie im Dokument [AD FS und Web Application Proxy-SSL-zertifikatanforderungen](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

## <a name="replacing-the-ssl-certificate-for-ad-fs"></a>Ersetzen die SSL-Zertifikats für AD FS
> [!NOTE]
> Das AD FS-SSL-Zertifikat ist nicht identisch mit AD FS dienstkommunikationszertifikat finden Sie in der AD FS-Verwaltungs-Snap-In. Um das AD FS-SSL-Zertifikat zu ändern, müssen Sie mithilfe von PowerShell.

Ermitteln Sie zunächst, welches Zertifikat binding Modus den AD FS-Servern ausgeführt werden: Standard-Authentifizierung zertifikatbindung oder anderen Client TLS Bindungsmodus.

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-default-certificate-authentication-binding-mode"></a>Ersetzen das SSL-Zertifikat für AD FS unter im Zertifikat Bindung Authentifizierungsmodus
AD FS in der Standardeinstellung führt eine gerätezertifikatauthentifizierung auf Port 443 und benutzerzertifikatauthentifizierung Port 49443 verwendet (oder eine konfigurierbare Port, der nicht 443).
Verwenden Sie in diesem Modus das Powershell-Cmdlet Set-AdfsSslCertificate, um das SSL-Zertifikat zu verwalten.

Führen Sie die folgenden Schritte aus:

1. Zunächst müssen Sie das Zertifikat erhalten haben. Dies erfolgt i. d. r. durch ein Zertifikat signieren zertifikatsignieranforderung (CSR) an einen dritten, öffentliche Zertifikatanbieter übermitteln. Es gibt eine Vielzahl von Möglichkeiten zum Generieren der CSR, einschließlich der von Windows 7 oder höher PC. Der Anbieter sollte die Dokumentation für diese verfügen.

    * Stellen Sie sicher, dass das Zertifikat erfüllt die [AD FS und Web Application Proxy-SSL-zertifikatanforderungen](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

1. Nachdem Sie die Antwort von Ihrem Zertifikatanbieter erhalten haben, importieren Sie es auf den lokalen Computerspeicher auf jedem AD FS und Web Application Proxy Server.

1. Auf der **primären** AD FS-Server das folgende Cmdlet verwenden, um das neue SSL-Zertifikat zu installieren

```powershell
Set-AdfsSslCertificate -Thumbprint '<thumbprint of new cert>'
```

Der Fingerabdruck des Zertifikats kann durch Ausführen dieses Befehls finden:

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>Zusätzliche Hinweise

* Das Cmdlet "Set-AdfsSslCertificate" ist ein Cmdlet mit mehreren Knoten. Dies bedeutet, dass sie nur vom primären ausführen und alle Knoten in der Farm werden aktualisiert. Dies ist neu in Server 2016. Auf Server 2012 R2 mussten Sie Set-AdfsSslCertificate auf jedem Server ausführen.
* Das Cmdlet "Set-AdfsSslCertificate" muss nur auf dem primären Server ausgeführt werden. Der primäre Server verfügt über Server 2016 ausgeführt werden und Verhalten Farmebene zu 2016 ausgelöst werden soll.
* Das Cmdlet "Set-AdfsSslCertificate" wird die PowerShell-Remoting verwendet, die anderen AD FS-Server konfigurieren, stellen Sie sicher, dass Port 5985 (TCP) auf den anderen Knoten geöffnet ist.
* Das Cmdlet "Set-AdfsSslCertificate" wird der Adfssrv principal auf die privaten Schlüssel des SSL-Zertifikats Leseberechtigungen. Diesen Prinzipal stellt den AD FS-Dienst. Es ist nicht erforderlich, um die AD FS-Dienst lesen Zugriff auf die privaten Schlüssel des SSL-Zertifikats zu gewähren.

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-alternate-tls-binding-mode"></a>Ersetzen die SSL-Zertifikats für AD FS alternativen TLS-Bindung im Modus ausgeführt wird
Wenn in anderen Client Bindungsmodus TLS konfiguriert ist, führt AD FS gerätezertifikatauthentifizierung auf Port 443 und benutzerzertifikatauthentifizierung Port 443 auch auf einem anderen Hostnamen. Der Hostname des Benutzer-Zertifikat wird der AD FS Hostname vorangestellt "Certauth", z. B. "certauth.fs.contoso.com".
Verwenden Sie in diesem Modus das Powershell-Cmdlet Set-AdfsAlternateTlsClientBinding, um das SSL-Zertifikat zu verwalten. Dies wird nicht nur die alternativen Client TLS-Bindung, sondern alle Bindungen, die auf denen AD FS das SSL-Zertifikat wird verwaltet.

Führen Sie die folgenden Schritte aus:

1. Zunächst müssen Sie das Zertifikat erhalten haben. Dies erfolgt i. d. r. durch ein Zertifikat signieren zertifikatsignieranforderung (CSR) an einen dritten, öffentliche Zertifikatanbieter übermitteln. Es gibt eine Vielzahl von Möglichkeiten zum Generieren der CSR, einschließlich der von Windows 7 oder höher PC. Der Anbieter sollte die Dokumentation für diese verfügen.

    * Stellen Sie sicher, dass das Zertifikat erfüllt die [AD FS und Web Application Proxy-SSL-zertifikatanforderungen](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

1. Nachdem Sie die Antwort von Ihrem Zertifikatanbieter erhalten haben, importieren Sie es auf den lokalen Computerspeicher auf jedem AD FS und Web Application Proxy Server.

1. Auf der **primären** AD FS-Server das folgende Cmdlet verwenden, um das neue SSL-Zertifikat zu installieren

```powershell
Set-AdfsAlternateTlsClientBinding -Thumbprint '<thumbprint of new cert>'
```

Der Fingerabdruck des Zertifikats kann durch Ausführen dieses Befehls finden:

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>Zusätzliche Hinweise

* Das Cmdlet "Set-AdfsAlternateTlsClientBinding" ist ein Cmdlet mit mehreren Knoten. Dies bedeutet, dass sie nur vom primären ausführen und alle Knoten in der Farm werden aktualisiert.
* Das Cmdlet "Set-AdfsAlternateTlsClientBinding" muss nur auf dem primären Server ausgeführt werden. Der primäre Server verfügt über Server 2016 ausgeführt werden und Verhalten Farmebene zu 2016 ausgelöst werden soll.
* Das Cmdlet "Set-AdfsAlternateTlsClientBinding" wird die PowerShell-Remoting verwendet, die anderen AD FS-Server konfigurieren, stellen Sie sicher, dass Port 5985 (TCP) auf den anderen Knoten geöffnet ist.
* Das Cmdlet "Set-AdfsAlternateTlsClientBinding" wird der Adfssrv principal auf die privaten Schlüssel des SSL-Zertifikats Leseberechtigungen. Diesen Prinzipal stellt den AD FS-Dienst. Es ist nicht erforderlich, um die AD FS-Dienst lesen Zugriff auf die privaten Schlüssel des SSL-Zertifikats zu gewähren.

## <a name="replacing-the-ssl-certificate-for-the-web-application-proxy"></a>Ersetzen das SSL-Zertifikat für den Webanwendungsproxy
Zum Konfigurieren der standardmäßigen zertifikatbindung Authentifizierung oder die anderen Client TLS Bindungsmodus auf dem drahtlosen Zugriffspunkt können wir das Cmdlet "Set-WebApplicationProxySslCertificate" verwenden.
Ersetzen Sie das Web Application Proxy-SSL-Zertifikat auf **jedes** Web Application Proxy Server verwenden Sie das folgende Cmdlet, um das neue SSL-Zertifikat zu installieren:

```powershell
Set-WebApplicationProxySslCertificate '<thumbprint of new cert>'
```

Wenn die oben genannten Cmdlet fehlschlägt, weil das alte Zertifikat bereits abgelaufen ist, neu konfigurieren Sie, des Proxys mit den folgenden Cmdlets:

```powershell
$cred = Get-Credential
```

Geben Sie die Anmeldeinformationen eines Benutzers Domäne, lokaler Administrator auf dem AD FS-server

```powershell
Install-WebApplicationProxy -FederationServiceTrustCredential $cred -CertificateThumbprint '<thumbprint of new cert>' -FederationServiceName 'fs.contoso.com'
```

## <a name="additional-references"></a>Weitere Verweise  
* [AD FS-Unterstützung für alternative hostnamenbindung für zertifikatbasierte Authentifizierung](../operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)
* [AD FS und das Zertifikat von Schlüsselspezifikationen Eigenschaft Informationen](../technical-reference/AD-FS-and-KeySpec-Property.md)
