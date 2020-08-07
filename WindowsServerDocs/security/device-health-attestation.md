---
title: Integritätsnachweis für Geräte
ms.topic: article
ms.assetid: 8e7b77a4-1c6a-4c21-8844-0df89b63f68d
author: brianlic-msft
ms.author: brianlic
ms.date: 10/12/2016
ms.openlocfilehash: 8ed6e2aafeeca0486bdb45019ba879e391af9934
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936732"
---
# <a name="device-health-attestation"></a>Integritätsnachweis für Geräte

>Gilt für: Windows Server 2016

Der mit Windows 10, Version 1507, eingeführte Integritätsnachweis für Geräte (Device Health Attestation, DHA) weist folgende Merkmale auf:

-    Integration in Windows 10 Mobile Device Management-Framework (MDM, Mobile Geräteverwaltung) in Ausrichtung mit [Open Mobile Alliance Standards (OMA)](http://openmobilealliance.org/).

-    Unterstützung von Geräten, die über eine in einer Firmware oder einem diskreten Format bereitgestellte Trusted Module Platform (TPM) verfügen.

-    Ermöglicht Unternehmen, mit minimalem oder keinem Einfluss auf die Betriebskosten das Sicherheitsniveau ihrer Organisation auf hardwareüberwachte und -bescheinigte Sicherheit anzuheben.

Ab Windows Server 2016 können Sie den DHA-Dienst als Serverrolle in Ihrer Organisation ausführen. Nutzen Sie dieses Thema, um das Installieren und Konfigurieren der DHA-Serverrolle zu lernen.

## <a name="overview"></a>Übersicht

Mit DHA können Sie den Integritätsnachweis für Geräte führen für:

-    Windows 10 und mobile Geräte unter Windows 10, die TPM 1.2 oder 2.0 unterstützen.
-    Lokale Geräte, die von Active Directory mit Internetzugriff verwaltet werden, Geräte, die von Active Directory ohne Internetzugriff verwaltet werden, Geräte, die von Azure Active Directory oder einer Hybridbereitstellung sowohl mit Active Directory als auch Azure Active Directory verwaltet werden.


### <a name="dha-service"></a>DHA-Dienst

Der DHA-Dienst überprüft die TPM- und PCR-Protokolle für ein Gerät und generiert dann einen DHA-Bericht. Microsoft bietet den DHA-Dienst auf drei Arten an:

- **DHA-Clouddienst**: Ein von Microsoft verwalteter DHA-Dienst, der frei, einem geografischen Lastenausgleich unterzogen und für den Zugriff aus verschiedenen Weltregionen optimiert ist.

- **Lokaler DHA-Dienst**: Eine neue, mit Windows Server 2016 eingeführte Serverrolle. Er ist kostenlos für Kunden, die über eine Windows Server 2016-Lizenz verfügen.

- **DHA-Azure-Clouddienst**: Ein virtueller Host in Microsoft Azure. Zu diesem Zweck benötigen Sie einen virtuellen Host und Lizenzen für den lokalen DHA-Dienst.

Der DHA-Dienst ist in MDM-Lösungen integriert und bietet Folgendes:

-    Kombinieren der Informationen, die sie von Geräten (über vorhandene Geräteverwaltungs-Kommunikationskanäle) mit dem DHA-Bericht erhalten
-    Treffen einer sichereren und vertrauenswürdigeren Sicherheitsentscheidung auf Basis der hardwarebescheinigten und -geschützten Daten

Hier ist ein Beispiel, das zeigt, wie Sie DHA nutzen können, um das Sicherheitsniveau für die Ressourcen Ihrer Organisation anzuheben.

1. Sie erstellen eine Richtlinie, die die folgende(n) Startkonfiguration/-attribute überprüft:
   - Sicherer Start
   - BitLocker
   - ELAM
2. Die MDM-Lösung erzwingt diese Richtlinie und löst eine auf den DHA-Berichtsdaten basierende Korrekturmaßnahme aus.  Beispielsweise könnte sie Folgendes überprüfen:
   - Der sichere Start wurde aktiviert, das Gerät lud vertrauenswürdigen, authentischen Code, und das Windows-Startladeprogramm wurde nicht manipuliert.
   - Vertrauenswürdiger Start überprüfte erfolgreich die digitale Signatur des Windows-Kernels und die Komponenten, die geladen wurden, während das Gerät startete.
   - Kontrollierter Start erstellte einen TPM-geschützten Audit-Trail, der remote überprüft werden konnte.
   - BitLocker wurde aktiviert und schützte die Daten, als das Gerät ausgeschaltet wurde.
   - ELAM wurde in frühen Startphasen aktiviert und überwacht die Laufzeit.

#### <a name="dha-cloud-service"></a>DHA-Clouddienst

Der DHA-Clouddienst bietet folgende Vorteile:

-    Überprüfung der TCG- und PCR-Gerätestartprotokolle, die er von einem Gerät empfängt, das mit einer MDM-Lösung registriert ist.
-    Erstellen eines manipulationssicheren Berichts (DHA-Bericht), der beschreibt, wie das Gerät auf der Basis von Daten startete, die von einem TPM-Chip des Geräts gesammelt und geschützt wurden.
-    Übermitteln des DHA-Berichts an den MDM-Server, der den Bericht in einem geschützten Kommunikationskanal angefordert hat.

#### <a name="dha-on-premises-service"></a>Lokaler DHA-Dienst

Der lokale DHA-Dienst bietet alle Funktionen, die auch der DHA-Clouddienst bietet.  Außerdem ermöglicht er Kunden Folgendes:

 - Optimieren der Leistung durch Ausführung des DHA-Diensts in Ihrem eigenen Rechenzentrum
 - Sicherstellen, dass der DHA-Bericht nicht Ihr Netzwerk verlässt

#### <a name="dha-azure-cloud-service"></a>DHA-Azure-Clouddienst

Dieser Dienst bietet die gleiche Funktionalität wie der lokale DHA-Dienst, mit der Ausnahme, dass der DHA-Azure-Clouddienst als virtueller Host in Microsoft Azure ausgeführt wird.

### <a name="dha-validation-modes"></a>DHA-Validierungsmodi

Sie können den lokalen DHA-Dienst entweder zur Ausführung im EKCert- oder AIKCert-Validierungsmodus einrichten. Wenn der DHA-Dienst einen Bericht ausgibt, wird angezeigt, ob er im AIKCert- oder EKCert-Validierungsmodus ausgegeben wurde. AIKCert- und EKCert-Validierungsmodus bieten die gleiche Sicherheitsgarantie, solange die EKCert-Zertifikatkette auf dem neuesten Stand gehalten wird.

#### <a name="ekcert-validation-mode"></a>EKCert-Validierungsmodus

Der EKCert-Validierungsmodus ist optimiert für Geräte in Unternehmen, die nicht mit dem Internet verbunden sind. Geräte, die eine Verbindung mit einem DHA-Dienst herstellen, der im EKCert-Validierungsmodus ausgeführt wird, haben **keinen** direkten Zugriff auf das Internet.

Wenn DHA im EKCert-Validierungsmodus ausgeführt wird, hängt DHA von einer unternehmensverwalteten Zertifikatkette ab, die gelegentlich (ca. 5 - 10 Mal pro Jahr) aktualisiert werden muss.

Microsoft veröffentlicht aggregierte Pakete von vertrauenswürdigen Stammzertifizierungsstellen und Zwischenzertifizierungsstellen für genehmigte TPM-Hersteller (sobald sie verfügbar sind) in einem öffentlich zugänglichen Archiv im CAB-Archiv. Sie müssen den Feed herunterladen, die Integrität überprüfen und das Zertifikat auf dem Server installieren, der den Integritätsnachweis für Geräte ausführt.

Ein Beispiel Archiv ist [https://go.microsoft.com/fwlink/?linkid=2097925](https://go.microsoft.com/fwlink/?linkid=2097925) .

#### <a name="aikcert-validation-mode"></a>AIKCert-Validierungsmodus

Der AIKCert-Validierungsmodus ist optimiert für Betriebsumgebungen, die über Zugriff auf das Internet verfügen. Geräte, die eine Verbindung mit einem DHA-Dienst herstellen, der im AIKCert-Validierungsmodus ausgeführt wird, müssen direkten Zugriff auf das Internet haben und können ein AIK-Zertifikat von Microsoft bekommen.

## <a name="install-and-configure-the-dha-service-on-windows-server-2016"></a>Installieren und Konfigurieren des DHA-Diensts unter Windows Server 2016

Verwenden Sie die folgenden Abschnitte, um DHA unter Windows Server 2016 zu installieren und konfigurieren.

### <a name="prerequisites"></a>Voraussetzungen

Um einen lokalen DHA-Dienst einzurichten und zu überprüfen, benötigen Sie Folgendes:

- Einen Server, auf dem Windows Server 2016 ausgeführt wird.
- (Mindestens) ein Windows 10-Clientgerät mit einer TPM (Version 1.2 oder 2.0), das sich im Zustand „klar/bereit“ befindet und den aktuellen Windows Insider-Build ausführt.
- Entscheiden Sie sich zwischen einer Ausführung im EKCert- oder AIKCert-Validierungsmodus.
- Die folgenden Zertifikate stehen zur Verfügung:
  - **DHA-SSL-Zertifikat**: Ein x.509-SSL-Zertifikat, das über eine Enterprise Trusted Root mit einem exportierbaren privaten Schlüssel verkettet ist. Dieses Zertifikat schützt DHA-Datenkommunikation im Transit einschließlich Server-zu-Server-Kommunikation (DHA-Dienst und MDM-Server) und Server-zu-Client-Kommunikation (DHA-Dienst und ein Windows 10-Gerät).
  - **DHA-Signaturzertifikat**: Ein x.509-Zertifikat, das über eine Enterprise Trusted Root mit einem exportierbaren privaten Schlüssel verkettet ist. Der DHA-Dienst verwendet dieses Zertifikat zum digitalen Signieren.
  - **DHA-Verschlüsselungszertifikat**: Ein x.509-Zertifikat, das über eine Enterprise Trusted Root mit einem exportierbaren privaten Schlüssel verkettet ist. Der DHA-Dienst verwendet dieses Zertifikat auch zur Verschlüsselung.


### <a name="install-windows-server-2016"></a>Installieren von Windows Server 2016

Installieren Sie Windows Server 2016 mithilfe Ihrer bevorzugten Installationsmethode, wie z.B. Windows-Bereitstellungsdienste, oder Ausführen des Installationsprogramms von startbaren Medien, einem USB-Laufwerk oder dem lokalen Dateisystem. Wenn Sie jetzt zum ersten Mal den lokalen DHA-Dienst konfigurieren, sollten Sie Windows Server 2016 mit der Installationsoption **Desktopdarstellung** installieren.

### <a name="add-the-device-health-attestation-server-role"></a>Hinzufügen der Serverrolle „Integritätsnachweis für Geräte“

Sie können die Serverrolle „Integritätsnachweis für Geräte“ und ihre Abhängigkeiten mithilfe des Server-Managers installieren.

Nachdem Sie Windows Server 2016 installiert haben, wird das Gerät neu gestartet und der Server-Manager geöffnet. Wenn der Server-Manager nicht automatisch startet, klicken Sie auf **Start** und dann auf **Server-Manager**.

1.    Klicken Sie auf **Rollen und Features hinzufügen**.
2.    Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.
3.    Klicken Sie auf der Seite **Installationstyp auswählen** auf **Rollenbasierte oder featurebasierte Installation**, und klicken Sie anschließend auf **Weiter**.
4.    Klicken Sie auf der Seite **Zielserver auswählen** auf **Einen Server aus dem Serverpool auswählen**, treffen Sie Ihre Wahl, und klicken Sie dann auf **Weiter**.
5.    Aktivieren Sie auf der Seite **Serverrollen auswählen** das Kontrollkästchen **Integritätsnachweis für Geräte**.
6.    Klicken Sie auf **Features hinzufügen**, um andere erforderliche Rollendienste und Features zu installieren.
7.    Klicken Sie auf **Weiter**.
8.    Klicken Sie auf der Seite **Features auswählen** auf **Weiter**.
9.    Klicken Sie auf der Seite **Webserverrolle (IIS)** auf **Weiter**.
10.    Klicken Sie auf der Seite **Rollendienste auswählen** auf **Weiter**.
11.    Klicken Sie auf der Seite **Integritätsnachweis für Geräte** auf **Weiter**.
12.    Klicken Sie auf der Seite **Installationsauswahl bestätigen** auf **Installieren**.
13.    Klicken Sie nach dem Abschluss der Installation auf **Schließen**.

### <a name="install-the-signing-and-encryption-certificates"></a>Installieren der Signatur- und Verschlüsselungszertifikate

Installieren Sie mit dem folgenden Windows PowerShell-Skript die Signatur- und Verschlüsselungszertifikate. Weitere Informationen zum Fingerabdruck finden Sie unter Gewusst [wie: Abrufen des Fingerabdrucks eines Zertifikats](https://msdn.microsoft.com/library/ms734695.aspx).

```
$key = Get-ChildItem Cert:\LocalMachine\My | Where-Object {$_.Thumbprint -like "<thumbprint>"}
$keyname = $key.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
$keypath = $env:ProgramData + "\Microsoft\Crypto\RSA\MachineKeys\" + $keyname
icacls $keypath /grant <username>`:R

#<thumbprint>: Certificate thumbprint for encryption certificate or signing certificate
#<username>: Username for web service app pool, by default IIS_IUSRS
```

### <a name="install-the-trusted-tpm-roots-certificate-package"></a>Installieren des vertrauenswürdigen TPM-Stammzertifikatpakets

Um das vertrauenswürdige TPM-Stammzertifikatpaket zu installieren, müssen Sie es extrahieren, ggf. Zertifikatketten entfernen, die von Ihrer Organisation nicht als vertrauenswürdig eingestuft werden, und „setup.cmd“ ausführen.

#### <a name="download-the-trusted-tpm-roots-certificate-package"></a>Herunterladen des vertrauenswürdigen TPM-Stammzertifikatpakets

Vor der Installation des Zertifikat Pakets können Sie die aktuelle Liste der vertrauenswürdigen TPM-Stämme von herunterladen [https://go.microsoft.com/fwlink/?linkid=2097925](https://go.microsoft.com/fwlink/?linkid=2097925) .

> **Wichtig:** Stellen Sie vor der Installation des Pakets sicher, dass es von Microsoft digital signiert ist.

#### <a name="extract-the-trusted-certificate-package"></a>Extrahieren des vertrauenswürdigen Zertifikatpakets
Extrahieren Sie das vertrauenswürdige Zertifikatspaket durch Ausführen der folgenden Befehle.
```
mkdir .\TrustedTpm
expand -F:* .\TrustedTpm.cab .\TrustedTpm
```

#### <a name="remove-the-trust-chains-for-tpm-vendors-that-are-not-trusted-by-your-organization-optional"></a>Entfernen der Zertifikatketten für TPM-Hersteller, die von Ihrer Organisation *nicht* als vertrauenswürdig eingestuft werden (optional)

Löschen Sie die Ordner für alle Zertifikatketten von TPM-Herstellern, die von Ihrer Organisation nicht als vertrauenswürdig eingestuft werden.

> **Hinweis:** Im AIK-Zertifikatmodus ist der Microsoft-Ordner zum Überprüfen der von Microsoft ausgestellten AIK-Zertifikate erforderlich.

#### <a name="install-the-trusted-certificate-package"></a>Installieren des vertrauenswürdigen Zertifikatpakets
Installieren Sie das vertrauenswürdige Zertifikatpaket durch Ausführen des Setupskripts aus der CAB-Datei.

```
.\setup.cmd
```

### <a name="configure-the-device-health-attestation-service"></a>Konfigurieren des Integritätsnachweises für Geräte

Sie können Windows PowerShell verwenden, um den lokalen DHA-Dienst zu konfigurieren.

```
Install-DeviceHealthAttestation -EncryptionCertificateThumbprint <encryption> -SigningCertificateThumbprint <signing> -SslCertificateStoreName My -SslCertificateThumbprint <ssl> -SupportedAuthenticationSchema "<schema>"

#<encryption>: Thumbprint of the encryption certificate
#<signing>: Thumbprint of the signing certificate
#<ssl>: Thumbprint of the SSL certificate
#<schema>: Comma-delimited list of supported schemas including AikCertificate, EkCertificate, and AikPub
```

### <a name="configure-the-certificate-chain-policy"></a>Konfigurieren der Zertifikatketten-Richtlinie

Konfigurieren Sie die Zertifikatketten-Richtlinie durch Ausführen des folgenden Windows PowerShell-Skripts.

```
$policy = Get-DHASCertificateChainPolicy
$policy.RevocationMode = "NoCheck"
Set-DHASCertificateChainPolicy -CertificateChainPolicy $policy
```

## <a name="dha-management-commands"></a>DHA-Verwaltungsbefehle

Hier finden Sie einige Windows PowerShell-Beispiele, die Ihnen helfen können, den DHA-Dienst zu verwalten.

### <a name="configure-the-dha-service-for-the-first-time"></a>Erstmaliges Konfigurieren des DHA-Diensts

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

> **Hinweis:** Dieses Zertifikat muss auf dem Server bereitgestellt werden, der den DHA-Dienst im Zertifikatspeicher **LocalMachine\My** ausführt. Wenn das aktive Signaturzertifikat festgelegt ist, wird das vorhandene aktive Signaturzertifikat in die Liste der inaktiven Signaturzertifikate verschoben.

### <a name="list-the-inactive-signing-certificates"></a>Liste der inaktiven Signaturzertifikate
```
Get-DHASInactiveSigningCertificates
```

### <a name="remove-any-inactive-signing-certificates"></a>Entfernen beliebiger inaktiver Signaturzertifikate
```
Remove-DHASInactiveSigningCertificates -Force
Remove-DHASInactiveSigningCertificates  -Thumbprint "<hex>" -Force
```

> **Hinweis:** Nur *ein* inaktives Zertifikat (beliebigen Typs) kann zu einem beliebigen Zeitpunkt im Dienst vorhanden sein. Zertifikate sollten aus der Liste der inaktiven Zertifikate entfernt werden, sobald sie nicht mehr benötigt werden.

### <a name="get-the-active-encryption-certificate"></a>Abrufen des aktiven Verschlüsselungszertifikats

```
Get-DHASActiveEncryptionCertificate
```

### <a name="set-the-active-encryption-certificate"></a>Festlegen des aktiven Verschlüsselungszertifikats

```
Set-DHASActiveEncryptionCertificate -Thumbprint "<hex>" -Force
```

Das Zertifikat muss auf dem Gerät im Zertifikatspeicher **LocalMachine\My** bereitgestellt werden.

Wenn das aktive Verschlüsselungszertifikat festgelegt ist, wird das vorhandene aktive Verschlüsselungszertifikat in die Liste der inaktiven Verschlüsselungszertifikate verschoben.

### <a name="list-the-inactive-encryption-certificates"></a>Liste der inaktiven Verschlüsselungszertifikate

```
Get-DHASInactiveEncryptionCertificates
```
### <a name="remove-any-inactive-encryption-certificates"></a>Entfernen beliebiger inaktiver Verschlüsselungszertifikate

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

## <a name="dha-service-reporting"></a>DHA-Dienstberichterstellung

Im Folgenden finden Sie eine Liste der Meldungen des DHA-Diensts an die MDM-Lösung:

- **200** HTTP OK. Das Zertifikat wird zurückgegeben.
- **400** ungültige Anforderung. Ungültiges Anforderungsformat, ungültiges Integritätszertifikat, keine Übereinstimmung bei Zertifikatsignatur, ungültiges Integritätsnachweisblob oder ungültiges Integritätsstatusblob. Die Antwort enthält auch, wie im Antwortschema beschrieben, eine Nachricht mit einem Fehlercode und eine Fehlermeldung, die für die Diagnose verwendet werden kann.
- **500** interner Server Fehler. Dies kann geschehen, wenn Probleme auftreten, die verhindern, dass der Dienst Zertifikate ausstellt.
- **503** Einschränkung lehnt Anforderungen ab, um eine Überlastung des Servers zu verhindern.
