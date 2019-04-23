---
title: Problembehandlung für die Host-Überwachungsdienst
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 424b8090-0692-49a6-9dc4-3c0e77d74b80
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: 2dc9a612fa9760a6ca5f05efe1c287fd0872a1d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861251"
---
# <a name="troubleshooting-the-host-guardian-service"></a>Problembehandlung für die Host-Überwachungsdienst

> Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema wird beschrieben, Lösungen für häufige Probleme beim Bereitstellen oder einen Server (Host Guardian Service, HGS) in einem geschützten Fabric ausgeführt wird.
Wenn Sie die Art des Problems, erste führen nicht genau wissen, sind die [überwachten Fabric-Diagnose](guarded-fabric-troubleshoot-diagnostics.md) bewirkt, dass auf Ihrem Host-Überwachungsdienst-Server und Hyper-V-Hosts, um das Potenzial einzugrenzen.

## <a name="certificates"></a>Zertifikate

Host-Überwachungsdiensts erforderlich mehrere Zertifikate angewendet werden, einschließlich der Verschlüsselung-Administrator konfiguriert, und Signieren Zertifikat als auch ein nachweiszertifikat Host-Überwachungsdienst selbst verwaltet.
Wenn diese Zertifikate nicht ordnungsgemäß konfiguriert sind, wird-Host-Überwachungsdiensts in der Lage, die Anforderungen von Hyper-V-Hosts zu bestätigen oder zu entsperrenden Schlüsselschutzvorrichtungen für abgeschirmte VMs möchte.
Die folgenden Abschnitte enthalten allgemeine Probleme im Zusammenhang mit Zertifikaten, die auf dem Host-Überwachungsdienst konfiguriert.

### <a name="certificate-permissions"></a>Zertifikatberechtigungen

Host-Überwachungsdienst müssen die öffentlichen und privaten Schlüssel von der Verschlüsselung und Signaturzertifikate Host-Überwachungsdienst hinzugefügt, durch den Fingerabdruck des Zertifikats zugreifen können.
Insbesondere die gruppenverwalteten Dienstkonten (gMSA), die der Host-Überwachungsdienst-Dienst ausgeführt wird, benötigt Zugriff auf die Schlüssel.
Um das gruppenverwaltete Dienstkonto ein, die Host-Überwachungsdiensts zu suchen, führen Sie den folgenden Befehl in einer PowerShell-Eingabeaufforderung mit erhöhten Rechten auf dem Host-Überwachungsdienst-Server:

```powershell
(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName
```

Wie Sie dem gMSA-Konto Zugriff auf den privaten Schlüssel gewähren abhängig, in dem der Schlüssel gespeichert ist: auf dem Computer wie eine lokale Zertifikatdatei, auf ein Hardwaresicherheitsmodul (HSM) oder über einen benutzerdefinierten Drittanbieter-Schlüsselspeicher-Anbieter.

#### <a name="grant-access-to-software-backed-private-keys"></a>Gewähren des Zugriffs auf private Schlüssel Software-Backup

Wenn Sie ein selbstsigniertes Zertifikat oder ein Zertifikat von einer Zertifizierungsstelle, die verwenden **nicht** in ein Hardwaresicherheitsmodul oder eine benutzerdefinierte Schlüsselspeicheranbieter gespeichert werden, können Sie die Berechtigungen für den privaten Schlüssel anhand Ändern der folgende Schritte durch:

1. Öffnen Sie das lokale Zertifikat-Manager (certlm.msc)
2. Erweitern Sie **persönliche > Zertifikate** und suchen Sie nach der Signierung oder Verschlüsselung Zertifikat, das Sie aktualisieren möchten.
3. Klicken Sie mit der rechten Maustaste auf das Zertifikat, und wählen Sie **alle Aufgaben > Privatschlüssel verwalten**.
4. Klicken Sie auf **hinzufügen** um einen neuen Benutzer den Zugriff auf die Certiciate den privaten Schlüssel zu gewähren.
5. Geben Sie in der Objektauswahl der gMSA-Kontoname für Host-Überwachungsdienst finden Sie weiter oben, und klicken Sie dann **OK**.
6. Stellen Sie sicher, das gruppenverwaltete Dienstkonto wurde **lesen** Zugriff auf das Zertifikat.
7. Klicken Sie auf **OK** Berechtigung Fenster schließen.

Wenn Sie Host-Überwachungsdienst auf Server Core ausgeführt werden oder den Server remote verwalten, werden Sie nicht private Schlüssel mit dem lokalen Zertifikat-Manager verwalten können.
Stattdessen müssen Sie zum Herunterladen der [überwachten Fabric-Tools-PowerShell-Modul](https://www.powershellgallery.com/packages/GuardedFabricTools) wird, mit denen Sie die Berechtigungen in PowerShell verwalten.

1. Öffnen Sie eine mit erhöhten Rechten PowerShell-Konsole auf dem Server Core-Computer, oder verwenden Sie PowerShell-Remoting mit einem Konto mit Berechtigungen als lokaler Administrator auf dem Host-Überwachungsdienst.
2. Führen Sie die folgenden Befehle zum Installieren des überwachten Fabric-Tools-PowerShell-Moduls, und gewähren Sie dem gMSA Zugriff auf den privaten Schlüssel.

```powershell
$certificateThumbprint = '<ENTER CERTIFICATE THUMBPRINT HERE>'

# Install the Guarded Fabric Tools module, if necessary
Install-Module -Name GuardedFabricTools -Repository PSGallery

# Import the module into the current session
Import-Module -Name GuardedFabricTools

# Get the certificate object
$cert = Get-Item "Cert:\LocalMachine\My\$certificateThumbprint"

# Get the gMSA account name
$gMSA = (Get-IISAppPool -Name KeyProtection).ProcessModel.UserName

# Grant the gMSA read access to the certificate
$cert.Acl = $cert.Acl | Add-AccessRule $gMSA Read Allow
```

#### <a name="grant-access-to-hsm-or-custom-provider-backed-private-keys"></a>Gewähren des Zugriffs auf das HSM oder benutzerdefinierte Anbieter gestützte private Schlüssel verwenden

Wenn der private Schlüssel des Zertifikats durch ein Hardwaresicherheitsmodul (HSM) oder einen benutzerdefinierten Schlüsselspeicheranbieter (KSP) gesichert sind, ist das Berechtigungsmodell bestimmte Softwareanbieter abhängig.
Finden Sie in der Dokumentation des Herstellers oder support-Website für Informationen dazu, wie private Schlüssel Berechtigungen behandelt werden für Ihre spezifischen Gerätesoftware, für die besten Ergebnisse.

Einige Hardwaresicherheitsmodulen unterstützen nicht die bestimmter Benutzerkonten Zugriff auf einen privaten Schlüssel gewähren. Stattdessen können sie den Computerzugriff auf alle Schlüssel in einem bestimmten Schlüssel Satz.
Für solche Geräte reicht es normalerweise den Computerzugriff auf Ihre Schlüssel zu gewähren, und Host-Überwachungsdienst ist in der Lage, diese Verbindung nutzen.

**Tipps für die HSMs**

Im folgenden finden Sie empfohlene Konfiguration-Optionen für das erfolgreiche Verwendung HSM-gesicherten Schlüsseln mit Host-Überwachungsdienst basierend auf von Microsoft und seinen Partnern Erfahrungen.
Diese Tipps sind der Einfachheit halber bereitgestellt und werden nicht unbedingt zum Zeitpunkt des Lesens korrekt zu sein, und sie durch die HSM-Hersteller unterstützt werden.
Wenden Sie sich an den HSM-Hersteller, genaue Informationen, die das jeweilige Gerät zu, wenn Sie weitere Fragen haben.

HSM-Marke/Serien      | Vorschlag
----------------------|-------------
Gemalto SafeNet       | Stellen Sie sicher, dass die Schlüssel-Usage-Eigenschaft in die Datei zur zertifikatanforderung 0xa0 und festgelegt ist das Zertifikat zum Signieren und Verschlüsseln verwendet werden können. Darüber hinaus müssen Sie das gMSA-Konto gewähren *lesen* Zugriff auf den privaten Schlüssel mit dem lokalen Zertifikat-Manager-Tool (siehe oben genannten Schritte).
Thales nShield        | Stellen Sie sicher, dass jeder Host-Überwachungsdienst-Knoten auf die Security World, die die Signierung und Verschlüsselung Schlüssel zugreifen. Sie müssen sich nicht um gMSA-spezifischen Berechtigungen zu konfigurieren.
Utimaco CryptoServers | Stellen Sie sicher, dass die Schlüssel-Usage-Eigenschaft in die Datei zur zertifikatanforderung auf 0 x 13, festgelegt ist, können das Zertifikat für die Verschlüsselung, Entschlüsselung und Signatur verwendet werden.

### <a name="certificate-requests"></a>Zertifikatanforderungen

Wenn Sie Ihre Zertifikate in einer Umgebung mit public Key-Infrastruktur (PKI) ausstellen eine Zertifizierungsstelle verwenden, müssen Sie sicherstellen, dass Ihre zertifikatanforderung die Mindestanforderungen für die HGS Nutzung für die Schlüssel enthält.

**Signieren von Zertifikaten**

CSR-Eigenschaft | Erforderlicher Wert
-------------|---------------
Algorithmus    | RSA
Schlüsselgröße     | Mindestens 2048 Bit
Schlüsselverwendung    | Signatur/SSO/DigitalSignature

**Verschlüsselungszertifikate**

CSR-Eigenschaft | Erforderlicher Wert
-------------|---------------
Algorithmus    | RSA
Schlüsselgröße     | Mindestens 2048 Bit
Schlüsselverwendung    | Verschlüsselung/verschlüsselt/DataEncipherment

**Vorlagen für die Active Directory-Zertifikatdienste**

Wenn Sie Zertifikatvorlagen für die Active Directory-Zertifikatdienste (ADCS) verwenden, erstellen Sie verwenden die Zertifikate, die Sie es empfiehlt eine Vorlage mit den folgenden Einstellungen:

AD CS-Template-Eigenschaft | Erforderlicher Wert
-----------------------|---------------
Anbieterkategorie      | Schlüsselspeicheranbieter
Name des Algorithmus         | RSA
Minimale Schlüsselgröße       | 2.048
Zweck                | Signatur und Verschlüsselung
Erweiterte Schlüsselverwendung    | Digitale Signatur, Schlüsselverschlüsselung, Data Encipherment ("Allow Verschlüsseln von Benutzerdaten")


### <a name="time-drift"></a>Zeitunterschied

Wenn die Uhrzeit des Servers erheblich von der, die von anderen HGS-Knoten oder den Hyper-V-Hosts in Ihrer geschützten Fabric abweicht, können Sie mit dem Nachweis Signaturgeber die Gültigkeit des Zertifikats Probleme auftreten.
Das signaturgeberzertifikat Nachweis wird erstellt und im Hintergrund auf den Host-Überwachungsdienst erneuert und wird verwendet, um Integritätszertifikate für überwachte Hosts ausgestellt werden, durch die Attestation-Dienst anmelden.

Um das signaturgeberzertifikat Nachweis zu aktualisieren, führen Sie den folgenden Befehl in einer PowerShell-Eingabeaufforderung mit erhöhten Rechten aus.

```powershell
Start-ScheduledTask -TaskPath \Microsoft\Windows\HGSServer -TaskName 
AttestationSignerCertRenewalTask
```

Alternativ können Sie die geplante Aufgabe manuell ausführen, durch Öffnen **Taskplaner** (taskschd.msc), navigieren zu **Aufgabenplanungsbibliothek > Microsoft > Windows > HGSServer** und Ausführen der Aufgabe mit dem Namen **AttestationSignerCertRenewalTask**.

## <a name="switching-attestation-modes"></a>Nachweismodi wechseln

Wenn Sie Host-Überwachungsdienst von TPM-Modus wechseln, mit Active Directory-Modus oder umgekehrt über die [Set-HgsServer](https://technet.microsoft.com/library/mt652180.aspx) -Cmdlet, dauert möglicherweise bis zu 10 Minuten für jeden Knoten in Ihrem Host-Überwachungsdienst-Cluster, starten Sie den neuen nachweismodus erzwingen.
Dies ist normal.
Es wird empfohlen, dass Sie keine Richtlinien, die Hosts aus den vorherigen nachweismodus ermöglicht, bis Sie sichergestellt haben, dass alle Hosts erfolgreich mit den neuen nachweismodus bestätigen sind entzogen.

**Bekanntes Problem beim Wechseln von TPM zu AD-Modus**

Wenn Sie Ihr HGS-Cluster im TPM-Modus und höher Switch Active Directory-Modus initialisiert wird, besteht ein bekanntes Problem, das kann keine anderen Knoten im Cluster-Host-Überwachungsdiensts von einem Umschalten auf den neuen nachweismodus.
Um sicherzustellen, dass alle HGS-Server den richtigen nachweismodus erzwingen, führen Sie `Set-HgsServer -TrustActiveDirectory` **auf jedem Knoten** des Host-Überwachungsdienst-Clusters.
Dieses Problem gilt nicht, wenn Sie vom TPM-Modus in den Active Directory-Modus wechseln *und* der Cluster wurde ursprünglich im AD-Modus eingerichtet.

Sie können den nachweismodus des Host-Überwachungsdienst-Servers überprüfen, indem Sie mit [Get-HgsServer](https://technet.microsoft.com/library/mt652162.aspx).

## <a name="memory-dump-encryption-policies"></a>Memory Dump-Verschlüsselungsrichtlinien

Wenn Sie versuchen, die Richtlinien des Serverarbeitsspeichers Dump-Verschlüsselung zu konfigurieren und werden nicht angezeigt wird der Standard-Host-Überwachungsdienst dump Richtlinien (Host-Überwachungsdienst\_NoDumps, Host-Überwachungsdienst\_DumpEncryption und Host-Überwachungsdienst\_DumpEncryptionKey) oder das Speicherabbild Richtlinie Cmdlet ( Add-HgsAttestationDumpPolicy), ist es wahrscheinlich, dass Sie nicht das neueste kumulative Update installiert haben.
Um dies zu korrigieren [aktualisieren Sie Ihr HGS-Server](guarded-fabric-manage-hgs.md#patching-hgs) auf das neueste kumulative Windows Update und [aktivieren Sie die neuen Richtlinien für den Nachweis](guarded-fabric-manage-hgs.md#updates-requiring-policy-activation).
Stellen Sie sicher, dass Sie den Hyper-V-Hosts das kumulative Update vor dem Aktivieren der neuen Nachweis-Richtlinien, aktualisieren, wie Hosts, die nicht über die neuen Dump Verschlüsselungsfunktionen installiert verfügen wahrscheinlich Nachweis fehl, sobald die Host-Überwachungsdienst-Richtlinie aktiviert ist.

## <a name="endorsement-key-certificate-error-messages"></a>Endorsement Key-Zertifikat-Fehlermeldungen

Beim Registrieren eines Hosts mithilfe der [hinzufügen-HgsAttestationTpmHost](https://docs.microsoft.com/powershell/module/hgsattestation/add-hgsattestationtpmhost) -Cmdlet zwei TPM-Bezeichner aus der angegebenen Plattform-ID-Datei extrahiert werden: der Endorsement Key-Zertifikat (EKcert) und dem öffentlichen Endorsement Key (EKpub).
Der EKcert identifiziert den Hersteller des TPM zusicherungen, dass das TPM, authentifiziert und über der normalen Lieferkette produzierten ist bereitstellen.
Die EKpub dieses spezielle TPM identifiziert eindeutig und ist einer der Maßnahmen, die Host-Überwachungsdienst verwendet wird, um einem Host, dass der Zugriff zum Ausführen von abgeschirmten VMs zu gewähren.

Sie erhalten eine Fehlermeldung bei einen TPM-Host registrieren, wenn eine der beiden Bedingungen erfüllt sind:
1. Die Plattform-ID-Datei **nicht** enthalten einen Endorsement Key-Zertifikat
2. Die Plattform-ID-Datei enthält einen Endorsement Key-Zertifikat, aber das Zertifikat ist **nicht vertrauenswürdig** auf Ihrem System

Bestimmte TPM-Hersteller enthalten keine EKcerts in ihre TPMs.
Wenn Sie vermuten, dass dies der Fall mit TPM ist, vergewissern Sie sich mit Ihren OEM, dass Ihre TPMs sollte kein EKcert und verwenden Sie die `-Force` Flag manuell den Host bei HGS registriert.
Wenn Ihr TPM eine EKcert müssen, aber eine nicht, in der Plattform-ID-Datei gefunden wurde, sicherzustellen, dass Sie eine Administrator (erhöht) PowerShell-Konsole bei der Ausführung [Get-PlatformIdentifier](https://docs.microsoft.com/powershell/module/platformidentifier/get-platformidentifier) auf dem Host.

Wenn Sie den Fehler, dass Ihre EKcert nicht vertrauenswürdig ist, stellen Sie sicher, [installiert das vertrauenswürdige TPM Zertifikate Stammpaket](guarded-fabric-install-trusted-tpm-root-certificates.md) auf jedem Host-Überwachungsdienst-Server und, das Stammzertifikat für den TPM-Anbieter auf dem lokalen Computer die vorhandenist **TrustedTPM\_Stammzertifizierungsstelle** zu speichern. Alle anwendbaren Zwischenzertifikate müssen auch für die Installation in der **TrustedTPM\_Zwischenzertifizierungsstelle** auf dem lokalen Computer zu speichern.
Nach der Installation die Stamm- und Zwischenzertifikate werden Sie ausführen können `Add-HgsAttestationTpmHost` erfolgreich.
