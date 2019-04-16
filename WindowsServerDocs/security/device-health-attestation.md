---
title: "Integritätsnachweis für Geräte"
H1: na
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology:
- techgroup-security
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e7b77a4-1c6a-4c21-8844-0df89b63f68d
author: brianlic-msft
ms.date: 10/12/2016
ms.openlocfilehash: d304ee3456f8db1e5b202c1d9221d1374a5251be
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="device-health-attestation"></a>Integritätsnachweis für Geräte

>Gilt für: Windows Server 2016

In Windows10, Version 1507 eingeführte, enthalten (Device Health Attestation, DHA) Folgendes:

-   Integriert in Windows10 Mobile Device Management (MDM) Framework ausgerichtet [Open Mobile Alliance (OMA) Standards](http://openmobilealliance.org/).

-   Unterstützt Geräte, die ein Modul TPM (Trusted Platform) in einer Firmware oder einem diskreten Format bereitgestellt haben.

-   Ermöglicht Unternehmen das Sicherheitsniveau ihrer Organisation auf Heraufstufen und -bescheinigte Sicherheit, unter minimaler oder ohne Auswirkungen auf die Betriebskosten.

Ab Windows Server2016 können Sie jetzt den DHA-Dienst als Serverrolle in Ihrer Organisation ausführen. Verwenden Sie in diesem Thema finden Sie Informationen zum Installieren und Konfigurieren der Integritätsnachweis für Geräte-Serverrolle.

## <a name="overview"></a>(Übersicht)

Sie können DHA verwenden, zum Bewerten der Integrität für Geräte:
  
-   Windows10 und Windows10 Mobile Geräte, die TPM 1.2 oder 2.0 unterstützen.  
-   Lokale Geräte, die mithilfe von Active Directory mit Internetzugriff, Geräte, die verwaltet werden, wird mithilfe von Active Directory ohne Internetzugriff von Azure Active Directory oder eine Hybridbereitstellung mithilfe von Active Directory und Azure Active Directory verwalteten Geräte verwaltet werden.


### <a name="dha-service"></a>DHA-Dienst

Der DHA-Dienst überprüft die TPM- und PCR-Protokolle für ein Gerät und stellt dann einen DHA-Bericht. Microsoft bietet den DHA-Dienst auf drei Arten:

- **DHA-Clouddienst** ein von Microsoft verwalteter DHA-Dienst, der frei, Geo-Lastenausgleich und für den Zugriff aus verschiedenen Weltregionen optimiert ist.

- **DHA lokalen Dienst** eine neue Serverrolle in Windows Server2016 eingeführt wurde. Sie steht kostenlos für Kunden, die eine Windows Server2016-Lizenz verfügen.

- **DHA-Azure-Clouddienst** virtueller Host in Microsoft Azure. Dazu benötigen Sie einen virtuellen Host und Lizenzen für den lokalen DHA-Dienst.

Der DHA-Dienst mit MDM-Lösungen integriert und bietet Folgendes: 

-   Kombinieren der Informationen, die sie von Geräten (über vorhandene Geräteverwaltungs-Kommunikationskanäle) mit dem DHA-Bericht erhalten
-   Stellen Sie einen sichereren und vertrauenswürdigeren sicherheitsentscheidung basierend auf hardwarebescheinigten und -geschützten Daten

Hier ist ein Beispiel, das zeigt, wie Sie DHA nutzen können, können Sie das Sicherheitsniveau für die Ressourcen Ihrer Organisation auslösen.

1. Sie erstellen eine Richtlinie, die die folgenden Startkonfiguration/-Attribute überprüft:
  - Sicherer Start
  - BitLocker
  - ELAM
2. Die MDM-Lösung erzwingt diese Richtlinie und löst eine auf den DHA-Berichtsdaten basierende Korrekturmaßnahme aus.  Beispielsweise könnten sie Folgendes überprüfen:
  - Der sichere Start aktiviert wurde, das Gerät lud vertrauenswürdigen, der authentischen Code und das Windows-Startladeprogramm wurde nicht manipuliert.
  - Vertrauenswürdiger Start überprüfte erfolgreich die digitale Signatur des Windows-Kernels und die Komponenten, die geladen wurden, während das Gerät gestartet.
  - Kontrollierter Start erstellte einen TPM-geschützten Audit-Trail, der Remote überprüft werden konnte.
  - BitLocker aktiviert wurde und dass sie die Daten geschützt, wenn das Gerät ausgeschaltet wurde deaktiviert.
  - ELAM wurde in frühen startphasen aktiviert und überwacht die Laufzeit.
  
#### <a name="dha-cloud-service"></a>DHA-Clouddienst

Der DHA-Clouddienst bietet folgende Vorteile:

-   Überprüfung der TCG- und PCR-gerätestartprotokolle, die von einem Gerät empfängt, die bei einer MDM-Lösung registriert ist. 
-   Erstellt eine manipulationssicheren und Berichts (DHA-Bericht), die beschreibt, wie das Gerät Basis von Daten gestartet, die gesammelt und durch TPM-Chip des Geräts geschützt. 
-   Bietet den DHA-Bericht an den MDM-Server, der den Bericht in einem geschützten Kommunikationskanal angefordert.

#### <a name="dha-on-premises-service"></a>Lokalen DHA-Dienst

Der lokale DHA-Dienst bietet alle Funktionen, die von der DHA-Clouddienst angeboten werden.  Darüber hinaus ermöglicht er Kunden:

 - Optimieren der Leistung durch Ausführen der DHA-Dienst in Ihrem eigenen Rechenzentrum
 - Stellen Sie sicher, dass der DHA-Bericht nicht Ihr Netzwerk verlässt

#### <a name="dha-azure-cloud-service"></a>DHA-Azure-Cloud-Dienst

Dieser Dienst bietet die gleiche Funktionalität wie der lokale DHA-Dienst, mit dem Unterschied, dass der DHA-Azure-Clouddienst als virtueller Host in Microsoft Azure ausgeführt wird.

### <a name="dha-validation-modes"></a>DHA-validierungsmodi

Sie können den lokalen DHA-Dienst für die Ausführung im Ekcert- oder AIKCert-Validierungsmodus einrichten. Wenn der DHA-Dienst einen Bericht ausgibt, wird angezeigt, ob er im Aikcert- oder EKCert-Validierungsmodus ausgegeben wurde. Aikcert- und EKCert-Validierungsmodus bieten die gleiche Sicherheitsgarantie, solange die EKCert-Zertifikatkette auf dem neuesten Stand gehalten wird.

#### <a name="ekcert-validation-mode"></a>EKCert-Validierungsmodus

EKCert-Validierungsmodus ist optimiert für Geräte in Unternehmen, die nicht mit dem Internet verbunden sind. Führen Sie die Geräte, die Verbindung mit einem DHA-Dienst, der im EKCert-Validierungsmodus ausgeführt wird **nicht** haben direkten Zugriff auf das Internet.

Wenn DHA im EKCert-Validierungsmodus ausgeführt wird, hängt es ein Unternehmen verwalteten Vertrauenskette, die gelegentlich (ca. 5 - 10 Mal pro Jahr) aktualisiert werden soll. 

Microsoft veröffentlicht aggregierte Pakete von vertrauenswürdigen Stammzertifizierungsstellen und Zwischenzertifizierungsstellen für genehmigte TPM-Hersteller (wie sie verfügbar sind) in einem öffentlich zugänglichen Archiv im CAB-Archiv. Sie müssen den Feed herunterladen, die Integrität überprüfen und installieren Sie es auf dem Server mit der Integritätsnachweis für Geräte.

Ein beispielarchiv ist [https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab](https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab).

#### <a name="aikcert-validation-mode"></a>AIKCert-Validierungsmodus

AIKCert-Validierungsmodus ist optimiert für betriebsumgebungen, die Zugriff auf das Internet verfügen. Geräte, die Verbindung mit einem DHA-Dienst, der im AIKCert-Validierungsmodus ausgeführt wird, benötigen direkten Zugriff auf das Internet und können ein AIK-Zertifikat von Microsoft erhalten. 

## <a name="install-and-configure-the-dha-service-on-windows-server-2016"></a>Installieren und Konfigurieren des DHA-Diensts unter Windows Server2016

Verwenden Sie die folgenden Abschnitten, um DHA auf Windows Server2016 installiert und konfiguriert abzurufen.

### <a name="prerequisites"></a>Erforderliche Komponenten

Damit einrichten und einen lokalen DHA-Dienst überprüft haben, müssen Sie folgende Aktionen ausführen:

- Ein Server mit Windows Server2016.
- (mindestens) Windows10-Clientgeräte mit einem TPM (Version 1.2 oder 2.0), die klar/bereit mit den neuesten Windows Insider ist zu erstellen.
- Entscheiden Sie, wenn Sie beabsichtigen, im Ekcert- oder AIKCert-Validierungsmodus ausführen.
- Die folgenden Zertifikate:
  - **DHA-SSL-Zertifikat** ein x. 509-SSL-Zertifikat, das eine Enterprise trusted Root mit einem exportierbaren privaten Schlüssel verkettet ist. Dieses Zertifikat schützt DHA-Datenkommunikation im Transit einschließlich Server-zu-Server (DHA-Dienst und MDM-Server) und einen Server für die Clientkommunikation (DHA-Dienst und ein Windows10-Gerät).
  - **DHA-Signaturzertifikat** ein x. 509-Zertifikat, das eine Enterprise trusted Root mit einem exportierbaren privaten Schlüssel verkettet ist. Der DHA-Dienst verwendet dieses Zertifikat zum digitalen Signieren. 
  - **DHA-Verschlüsselungszertifikat** ein x. 509-Zertifikat, das eine Enterprise trusted Root mit einem exportierbaren privaten Schlüssel verkettet ist. Der DHA-Dienst verwendet dieses Zertifikat auch für die Verschlüsselung. 


### <a name="install-windows-server-2016"></a>Installieren von Windows Server 2016

Installieren Sie Windows Server2016 mithilfe Ihrer bevorzugten Installationsmethode, wie z.B. Windows-Bereitstellungsdienste oder Ausführen des Installationsprogramms von startbaren Medien, einem USB-Laufwerk oder im lokalen Dateisystem. Ist dies das erste Mal den lokalen DHA-Dienst konfigurieren, installieren Sie Windows Server2016 mit der **Desktopdarstellung** -Installationsoption.

### <a name="add-the-device-health-attestation-server-role"></a>Die Integritätsnachweis für Geräte-Serverrolle hinzufügen

Sie können die Geräteintegrität-Serverrolle und ihre Abhängigkeiten mithilfe von Server-Manager installieren. 

Nachdem Sie Windows Server2016 installiert haben, wird das Gerät wird neu gestartet, und Server-Manager geöffnet. Wenn der Server-Manager nicht automatisch gestartet wird, klicken Sie auf **starten**, und klicken Sie dann auf **Server-Manager**.

1.  Klicken Sie auf **Hinzufügen von Rollen und Features**.
2.  Auf der **vor dem Beginn** auf **Weiter**.
3.  Auf der **Installationstyp auswählen** auf **rollenbasierte oder featurebasierte Installation**, und klicken Sie dann auf **Weiter**.
4.  Auf der **Zielserver auswählen** auf **wählen Sie einen Server aus dem Serverpool**, wählen Sie den Server, und klicken Sie dann auf **Weiter**.
5.  Auf der **Serverrollen auswählen** Seite der **Geräteintegrität** Kontrollkästchen.
6.  Klicken Sie auf **Features hinzufügen** So installieren Sie andere erforderliche Rollendienste und Features.
7.  Klicken Sie auf **Weiter**.
8.  Auf der **Features auswählen** auf **Weiter**.
9.  Auf der **Webserverrolle (IIS)** auf **Weiter**.
10. Auf der **Rollendienste auswählen** auf **Weiter**.
11. Auf der **Dienst zum Integritätsnachweis** auf **Weiter**.
12. Auf der **Installationsauswahl bestätigen** auf **installieren**.
13. Wenn die Installation abgeschlossen ist, klicken Sie auf **schließen**.

### <a name="install-the-signing-and-encryption-certificates"></a>Installieren Sie die Zertifikate für Signierung und Verschlüsselung

Installieren Sie die Zertifikate für Signierung und Verschlüsselung mithilfe des folgenden Windows PowerShell-Skripts. Weitere Informationen zu den Fingerabdruck, finden Sie unter [wie: Rufen Sie den Fingerabdruck eines Zertifikats](https://msdn.microsoft.com/library/ms734695.aspx).

```
$key = Get-ChildItem Cert:\LocalMachine\My | Where-Object {$_.Thumbprint -like "<thumbprint>"}
$keyname = $key.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
$keypath = $env:ProgramData + "\Microsoft\Crypto\RSA\MachineKeys\" + $keyname
icacls $keypath /grant <username>`:R
  
#<thumbprint>: Certificate thumbprint for encryption certificate or signing certificate
#<username>: Username for web service app pool, by default IIS_IUSRS
```

### <a name="install-the-trusted-tpm-roots-certificate-package"></a>Installieren des vertrauenswürdigen TPM-stammzertifikatpakets

Zum Installieren des vertrauenswürdigen TPM-stammzertifikatpakets müssen Sie es extrahieren, ggf. Zertifikatketten, die nicht von Ihrer Organisation als vertrauenswürdig eingestuft werden entfernen und setup.cmd führen.

#### <a name="download-the-trusted-tpm-roots-certificate-package"></a>Herunterladen des vertrauenswürdigen TPM-stammzertifikatpakets

Bevor Sie das Zertifikatspaket installieren, können Sie die aktuelle Liste der vertrauenswürdigen TPM-Stammzertifizierungsstellen aus [https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab](https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab).

> **Wichtig:** vor der Installation des Pakets, stellen Sie sicher, dass es von Microsoft digital signiert ist.

#### <a name="extract-the-trusted-certificate-package"></a>Extrahieren Sie das Paket vertrauenswürdiges Zertifikat
Extrahieren Sie das vertrauenswürdige zertifikatpaket durch Ausführen der folgenden Befehle ein.
```
mkdir .\TrustedTpm
expand -F:* .\TrustedTpm.cab .\TrustedTpm
```

#### <a name="remove-the-trust-chains-for-tpm-vendors-that-are-not-trusted-by-your-organization-optional"></a>Entfernen der Zertifikatketten für TPM-Hersteller, die *nicht* vertrauenswürdige von Ihrer Organisation (Optional)

Löschen Sie die Ordner für alle Zertifikatketten TPM-Anbieter, die nicht von Ihrer Organisation als vertrauenswürdig eingestuft werden.

> **Hinweis:** Wenn AIK-Zertifikat-Modus verwenden, ist der Microsoft-Ordner zum Überprüfen von Microsoft ausgestellten AIK-Zertifikate erforderlich.

#### <a name="install-the-trusted-certificate-package"></a>Installieren Sie das Paket vertrauenswürdiges Zertifikat
Installieren Sie das vertrauenswürdige zertifikatpaket durch Ausführen des Setupskripts aus der CAB-Datei.

```
.\setup.cmd
```

### <a name="configure-the-device-health-attestation-service"></a>Konfigurieren Sie den Dienst Integritätsnachweis für Geräte

Sie können Windows PowerShell verwenden, konfigurieren Sie den lokalen DHA-Dienst.

```
Install-DeviceHealthAttestation -EncryptionCertificateThumbprint <encryption> -SigningCertificateThumbprint <signing> -SslCertificateStoreName My -SslCertificateThumbprint <ssl> -SupportedAuthenticationSchema "<schema>"

#<encryption>: Thumbprint of the encryption certificate
#<signing>: Thumbprint of the signing certificate
#<ssl>: Thumbprint of the SSL certificate
#<schema>: Comma-delimited list of supported schemas including AikCertificate, EkCertificate, and AikPub
```

### <a name="configure-the-certificate-chain-policy"></a>Konfigurieren der Zertifikatketten-Richtlinie

Konfigurieren der Zertifikatketten-Richtlinie durch Ausführen des folgenden Windows PowerShell-Skripts.

```
$policy = Get-DHASCertificateChainPolicy
$policy.RevocationMode = "NoCheck"
Set-DHASCertificateChainPolicy -CertificateChainPolicy $policy
```

## <a name="dha-management-commands"></a>DHA-Verwaltungsbefehle

Hier sind einige Windows PowerShell-Beispiele, mit denen Sie den DHA-Dienst verwalten können.

### <a name="configure-the-dha-service-for-the-first-time"></a>Konfigurieren Sie den DHA-Dienst zum ersten Mal

```
Install-DeviceHealthAttestation -SigningCertificateThumbprint "<HEX>" -EncryptionCertificateThumbprint "<HEX>" -SslCertificateThumbprint "<HEX>" -Force
```

### <a name="remove-the-dha-service-configuration"></a>Entfernen der DHA-Dienstkonfiguration

```
Uninstall-DeviceHealthAttestation -RemoveSslBinding -Force
```
### <a name="get-the-active-signing-certificate"></a>Abrufen des aktiven Signaturzertifikats

```
Get-DHASActiveSigningCertificate
```
### <a name="set-the-active-signing-certificate"></a>Festlegen des aktiven Signaturzertifikats

```
Set-DHASActiveSigningCertificate -Thumbprint "<hex>" -Force
```

> **Hinweis:** dieses Zertifikat muss bereitgestellt werden, auf dem Server mit der DHA-Dienst der **LocalMachine\My** Zertifikatspeicher. Wenn das aktive Signaturzertifikat festgelegt ist, wird das vorhandene aktive Signaturzertifikat in die Liste der inaktiven Signaturzertifikate verschoben.

### <a name="list-the-inactive-signing-certificates"></a>Liste der inaktiven Signaturzertifikate
```
Get-DHASInactiveSigningCertificates
```

### <a name="remove-any-inactive-signing-certificates"></a>Entfernen Sie beliebiger inaktiver Signaturzertifikate
```
Remove-DHASInactiveSigningCertificates -Force
Remove-DHASInactiveSigningCertificates  -Thumbprint "<hex>" -Force
```

> **Hinweis:** nur *eine* inaktives Zertifikat (beliebigen Typs) kann zu einem beliebigen Zeitpunkt im Dienst vorhanden. Zertifikate sollten aus der Liste der inaktiven Zertifikate entfernt werden, sobald sie nicht mehr benötigt werden.

### <a name="get-the-active-encryption-certificate"></a>Abrufen des aktiven Verschlüsselungszertifikats

```
Get-DHASActiveEncryptionCertificate
```

### <a name="set-the-active-encryption-certificate"></a>Festlegen des aktiven Verschlüsselungszertifikats

```
Set-DHASActiveEncryptionCertificate -Thumbprint "<hex>" -Force
```

Das Zertifikat muss bereitgestellt werden, auf dem Gerät in der **LocalMachine\My** Zertifikatspeicher. 

Wenn das aktive Verschlüsselungszertifikat festgelegt ist, wird das vorhandene aktive Verschlüsselungszertifikat in die Liste der inaktiven Verschlüsselungszertifikate verschoben.

### <a name="list-the-inactive-encryption-certificates"></a>Liste der inaktiven Verschlüsselungszertifikate

```
Get-DHASInactiveEncryptionCertificates
```
### <a name="remove-any-inactive-encryption-certificates"></a>Entfernen Sie beliebiger inaktiver Verschlüsselungszertifikate

```
Remove-DHASInactiveEncryptionCertificates -Force
Remove-DHASInactiveEncryptionCertificates -Thumbprint "<hex>" -Force 
```

### <a name="get-the-x509chainpolicy-configuration"></a>Abrufen der X509ChainPolicy-Konfiguration 

```
Get-DHASCertificateChainPolicy
```
### <a name="change-the-x509chainpolicy-configuration"></a>Ändern der X509ChainPolicy-Konfiguration

```
$certificateChainPolicy = Get-DHASInactiveEncryptionCertificates
$certificateChainPolicy.RevocationFlag = <X509RevocationFlag>
$certificateChainPolicy.RevocationMode = <X509RevocationMode>
$certificateChainPolicy.VerificationFlags = <X509VerificationFlags>
$certificateChainPolicy.UrlRetrievalTimeout = <TimeSpan>
Set-DHASCertificateChainPolicy = $certificateChainPolicy
```

## <a name="dha-service-reporting"></a>DHA-dienstberichterstellung

Im folgenden finden eine Liste von Fehlermeldungen, die durch den DHA-Dienst, um die MDM-Lösung gemeldet werden: 

- **200** HTTP OK. Das Zertifikat wird zurückgegeben.
- **400** ungültige Anforderung. Ungültiges Anforderungsformat, ungültiges Integritätszertifikat, Zertifikatsignatur nicht übereinstimmen, ungültiges Integritätsnachweisblob oder ein ungültiges Integritätsstatusblob. Die Antwort enthält auch eine Meldung mit einem Fehlercode und eine Fehlermeldung angezeigt, die für die Diagnose verwendet werden, kann im Antwortschema beschrieben.
- **500** Interner Serverfehler. Dies kann passieren, wenn Probleme auftreten, die verhindern, dass den Dienst Zertifikate ausstellt.
- **503** Einschränkung lehnt Anforderungen ab, um eine Überlastung des Servers zu verhindern. 
