---
ms.assetid: a3f50046-5d48-43d3-b0f8-ac2346b15285
title: Verwalten von SSL-Zertifikaten in AD FS und WAP in Windows Server 2016
description: Verwalten von SSL-Zertifikaten in AD FS und WAP in Windows Server 2016
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/02/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9bae831da9d247c423c2874a5928b7f811ef65dc
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188711"
---
# <a name="managing-ssl-certificates-in-ad-fs-and-wap-in-windows-server-2016"></a>Verwalten von SSL-Zertifikaten in AD FS und WAP in Windows Server 2016



In diesem Artikel wird beschrieben, wie Sie ein neues SSL-Zertifikat in Ihren AD FS und WAP-Servern bereitstellen.

>[!NOTE]
>Die empfohlene Methode zum Ersetzen des SSL-Zertifikats für eine AD FS-Farm in Zukunft ist die Verwendung von Azure AD Connect.  Weitere Informationen finden Sie unter [aktualisieren Sie das SSL-Zertifikat für eine Farm Active Directory-Verbunddienste (AD FS)](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectfed-ssl-update)

## <a name="obtaining-your-ssl-certificates"></a>Die SSL-Zertifikate abrufen
Für Produktions-AD FS-Farmen empfiehlt sich ein öffentlich vertrauenswürdiges SSL-Zertifikat. Dies wird in der Regel durch die Übermittlung von einem Zertifikat signieren zertifikatsignieranforderung (CSR) an Dritte weiter, öffentlicher Zertifikatanbieter abgerufen. Es gibt eine Vielzahl von Möglichkeiten, um die CSR-Datei, einschließlich der von einem Windows 7 oder höher PC zu generieren. Ihr Anbieter sollte es sich um Dokumentation für diese verfügen.

- Stellen Sie sicher, dass das Zertifikat erfüllt die [AD FS und Web Application Proxy-SSL-zertifikatanforderungen](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

### <a name="how-many-certificates-are-needed"></a>Wie viele Zertifikate erforderlich sind
Es wird empfohlen, dass Sie ein gemeinsames SSL-Zertifikat auf allen AD FS- und Webanwendungsproxy-Server verwenden. Details zu den Anforderungen finden Sie in das Dokument [AD FS und Web Application Proxy-SSL-zertifikatanforderungen](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

### <a name="ssl-certificate-requirements"></a>SSL-Zertifikatanforderungen
Anforderungen, die z.B. die Benennung, Stamm der Trust- und -Erweiterungen finden Sie im Dokument [AD FS und Web Application Proxy-SSL-zertifikatanforderungen](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

## <a name="replacing-the-ssl-certificate-for-ad-fs"></a>Ersetzen die SSL-Zertifikats für AD FS
> [!NOTE]
> Das AD FS-SSL-Zertifikat ist nicht identisch mit AD FS dienstkommunikationszertifikat finden Sie in das AD FS-Verwaltungs-Snap-in. Um das AD FS-SSL-Zertifikat zu ändern, müssen Sie PowerShell verwenden.

Bestimmen Sie zunächst, welches Zertifikat Bindungsmodus Ihre AD FS-Server ausgeführt werden: standardbindung für Zertifikat-Authentifizierung oder anderen Client TLS-Bindungsmodus.

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-default-certificate-authentication-binding-mode"></a>Ersetzen die SSL-Zertifikats für AD FS-Ausführung im standardmäßigen zertifikatsauthentifizierungsmodus Bindung
AD FS standardmäßig führt das Gerät Zertifikatauthentifizierung über Port 443 und Authentifizierung mit Benutzerzertifikat über Port 49443 (oder einen konfigurierbaren Port, der nicht 443).
Verwenden Sie in diesem Modus wird das Powershell-Cmdlet Set-AdfsSslCertificate, um das SSL-Zertifikat zu verwalten.

Führen Sie die unten beschriebenen Schritte aus.

1. Zunächst müssen Sie das neue Zertifikat zu erhalten. Dies erfolgt normalerweise durch die Übermittlung von einem Zertifikat signieren zertifikatsignieranforderung (CSR) an Dritte weiter, public Certificate-Anbieter. Es gibt eine Vielzahl von Möglichkeiten, um die CSR-Datei, einschließlich der von einem Windows 7 oder höher PC zu generieren. Ihr Anbieter sollte es sich um Dokumentation für diese verfügen.

    * Stellen Sie sicher, dass das Zertifikat erfüllt die [AD FS und Web Application Proxy-SSL-zertifikatanforderungen](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

1. Nachdem Sie die Antwort von Ihrem Zertifikatanbieter erhalten haben, importieren Sie sie auf den lokalen Computerspeicher auf jedem AD FS- und Webanwendungsproxy-Server.

1. Auf der **primären** AD FS-Server verwenden Sie das folgende Cmdlet, um das neue SSL-Zertifikat zu installieren.

```powershell
Set-AdfsSslCertificate -Thumbprint '<thumbprint of new cert>'
```

Der Fingerabdruck des Zertifikats finden Sie diesen Befehl ausführen:

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>Zusätzliche Hinweise

* Das Cmdlet "Set-AdfsSslCertificate" ist ein Cmdlet mit mehreren Knoten. Dies bedeutet, dass es nur vom primären Replikat ausgeführt und alle Knoten in der Farm aktualisiert werden. Dies ist neu in Server 2016. Auf Server 2012 R2 mussten Sie Set-AdfsSslCertificate auf jedem Server ausführen.
* Das Cmdlet "Set-AdfsSslCertificate" muss nur auf dem primären Server ausgeführt werden. Der primäre Server Server 2016 ausgeführt werden muss, und die Farmen mit Verhaltensebene auf 2016 ausgelöst werden soll.
* Das Cmdlet Set-AdfsSslCertificate verwendet PowerShell-Remoting auf andere AD FS-Servern konfigurieren, stellen Sie sicher, dass Port 5985 (TCP) in den anderen Knoten geöffnet ist.
* Das Cmdlet "Set-AdfsSslCertificate" wird die Adfssrv Dienstprinzipal Leseberechtigungen auf die privaten Schlüssel des SSL-Zertifikats gewährt. Dieser Prinzipal steht für den AD FS-Dienst. Es ist nicht erforderlich, die AD FS-Dienst-Konto Lesezugriff auf die privaten Schlüssel des SSL-Zertifikats zu erteilen.

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-alternate-tls-binding-mode"></a>Ersetzen die SSL-Zertifikats für AD FS im alternativen TLS-Bindung-Modus ausgeführt wird
In anderen Client TLS-Bindung-Modus konfiguriert ist, führt beim AD FS Device-Zertifikatauthentifizierung über Port 443 und Authentifizierung mit Benutzerzertifikat an Port 443 auch auf einen anderen Hostnamen. Der Hostname für das Zertifikat ist der AD FS-Hostname vorangestellt "Certauth", z. B. "certauth.fs.contoso.com".
Verwenden Sie in diesem Modus wird das Powershell-Cmdlet Set-AdfsAlternateTlsClientBinding, um das SSL-Zertifikat zu verwalten. Dadurch werden verwaltet, nicht nur die alternativen Client TLS-Bindung, sondern alle Bindungen, die auf denen AD FS das SSL-Zertifikat und legt sie fest.

Führen Sie die unten beschriebenen Schritte aus.

1. Zunächst müssen Sie das neue Zertifikat zu erhalten. Dies erfolgt normalerweise durch die Übermittlung von einem Zertifikat signieren zertifikatsignieranforderung (CSR) an Dritte weiter, public Certificate-Anbieter. Es gibt eine Vielzahl von Möglichkeiten, um die CSR-Datei, einschließlich der von einem Windows 7 oder höher PC zu generieren. Ihr Anbieter sollte es sich um Dokumentation für diese verfügen.

    * Stellen Sie sicher, dass das Zertifikat erfüllt die [AD FS und Web Application Proxy-SSL-zertifikatanforderungen](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

1. Nachdem Sie die Antwort von Ihrem Zertifikatanbieter erhalten haben, importieren Sie sie auf den lokalen Computerspeicher auf jedem AD FS- und Webanwendungsproxy-Server.

1. Auf der **primären** AD FS-Server verwenden Sie das folgende Cmdlet, um das neue SSL-Zertifikat zu installieren.

```powershell
Set-AdfsAlternateTlsClientBinding -Thumbprint '<thumbprint of new cert>'
```

Der Fingerabdruck des Zertifikats finden Sie diesen Befehl ausführen:

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>Zusätzliche Hinweise

* Das Cmdlet "Set-AdfsAlternateTlsClientBinding" ist ein Cmdlet mit mehreren Knoten. Dies bedeutet, dass es nur vom primären Replikat ausgeführt und alle Knoten in der Farm aktualisiert werden.
* Das Cmdlet "Set-AdfsAlternateTlsClientBinding" muss nur auf dem primären Server ausgeführt werden. Der primäre Server Server 2016 ausgeführt werden muss, und die Farmen mit Verhaltensebene auf 2016 ausgelöst werden soll.
* Das Cmdlet Set-AdfsAlternateTlsClientBinding verwendet PowerShell-Remoting auf andere AD FS-Servern konfigurieren, stellen Sie sicher, dass Port 5985 (TCP) in den anderen Knoten geöffnet ist.
* Das Cmdlet "Set-AdfsAlternateTlsClientBinding" wird die Adfssrv Dienstprinzipal Leseberechtigungen auf die privaten Schlüssel des SSL-Zertifikats gewährt. Dieser Prinzipal steht für den AD FS-Dienst. Es ist nicht erforderlich, die AD FS-Dienst-Konto Lesezugriff auf die privaten Schlüssel des SSL-Zertifikats zu erteilen.

## <a name="replacing-the-ssl-certificate-for-the-web-application-proxy"></a>Ersetzen das SSL-Zertifikat für den Webanwendungsproxy
Zum Konfigurieren der standardbindung für Zertifikat-Authentifizierung oder die TLS-Bindungsmodus alternativen Client auf dem drahtlosen Zugriffspunkt können wir das Cmdlet "Set-WebApplicationProxySslCertificate" verwenden.
Ersetzen Sie die Web Application Proxy-SSL-Zertifikat auf **jedes** Webanwendungs-Proxyserver verwenden das folgende Cmdlet, um das neue SSL-Zertifikat zu installieren:

```powershell
Set-WebApplicationProxySslCertificate '<thumbprint of new cert>'
```

Wenn das oben aufgeführte Cmdlet schlägt fehl, da das alte Zertifikat bereits abgelaufen ist, Konfigurieren des Proxys mit den folgenden Cmdlets neu:

```powershell
$cred = Get-Credential
```

Geben Sie die Anmeldeinformationen eines Domänenbenutzers, lokaler Administrator auf dem AD FS-server

```powershell
Install-WebApplicationProxy -FederationServiceTrustCredential $cred -CertificateThumbprint '<thumbprint of new cert>' -FederationServiceName 'fs.contoso.com'
```

## <a name="additional-references"></a>Weitere Verweise  
* [AD FS: Unterstützung der alternativen Hostnamenbindung für die Zertifikatauthentifizierung](../operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)
* [AD FS und Zertifikat KeySpec-Eigenschaft Informationen](../technical-reference/AD-FS-and-KeySpec-Property.md)
