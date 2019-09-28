---
title: Problembehandlung beim Host-Überwachungsdienst
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 424b8090-0692-49a6-9dc4-3c0e77d74b80
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: be817a2c06b13af254b80090b9a7488209d4df0a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403527"
---
# <a name="troubleshooting-the-host-guardian-service"></a>Problembehandlung beim Host-Überwachungsdienst

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema werden Lösungen für häufige Probleme beschrieben, die beim Bereitstellen oder betreiben eines HGS-Servers (Host Wächter Service) in einem geschützten Fabric auftreten.
Wenn Sie sich nicht sicher sind, welche Art von Problem Sie haben, versuchen Sie zunächst, die [geschützte Fabric-Diagnose](guarded-fabric-troubleshoot-diagnostics.md) auf Ihren HGS-Servern und Hyper-V-Hosts auszuführen, um die möglichen Gründe einzugrenzen.

## <a name="certificates"></a>Zertifikate

HGS erfordert für den Betrieb mehrere Zertifikate, einschließlich des vom Administrator konfigurierten Verschlüsselungs-und Signatur Zertifikats sowie eines von HGS selbstverwalteten Nachweis Zertifikats.
Wenn diese Zertifikate nicht ordnungsgemäß konfiguriert sind, können von HGS keine Anforderungen von Hyper-V-Hosts bedient werden, die Schlüssel Schutzvorrichtungen für abgeschirmte VMS bestätigen oder entsperren möchten.
In den folgenden Abschnitten werden allgemeine Probleme im Zusammenhang mit auf HGS konfigurierten Zertifikaten behandelt.

### <a name="certificate-permissions"></a>Zertifikat Berechtigungen

HGS müssen in der Lage sein, auf die öffentlichen und privaten Schlüssel der Verschlüsselungs-und Signatur Zertifikate zuzugreifen, die durch den Zertifikat Fingerabdruck zu HGS hinzugefügt werden.
Insbesondere das Gruppen verwaltete Dienst Konto (Group Managed Service Account, GMSA), das den HGS-Dienst ausführt, benötigt Zugriff auf die Schlüssel.
Führen Sie den folgenden Befehl in einer PowerShell-Eingabeaufforderung mit erhöhten Rechten auf Ihrem HGS-Server aus, um den von HGS verwendeten GMSA zu finden:

```powershell
(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName
```

Wie Sie dem GMSA-Konto den Zugriff auf den privaten Schlüssel gewähren, hängt davon ab, wo der Schlüssel gespeichert ist: auf dem Computer als lokale Zertifikat Datei, in einem Hardware Sicherheitsmodul (HSM) oder mithilfe eines benutzerdefinierten Schlüsselspeicher Anbieters von Drittanbietern.

#### <a name="grant-access-to-software-backed-private-keys"></a>Gewähren des Zugriffs auf softwaregestützte private Schlüssel

Wenn Sie ein selbst signiertes Zertifikat oder ein Zertifikat verwenden, das von einer Zertifizierungsstelle ausgestellt wurde, die **nicht** in einem Hardware Sicherheitsmodul oder einem benutzerdefinierten Schlüsselspeicher Anbieter gespeichert ist, können Sie die Berechtigungen für den privaten Schlüssel ändern, indem Sie die folgenden Schritte ausführen:

1. Öffnen Sie den lokalen Zertifikat-Manager (certlm. msc).
2. Erweitern Sie die Option **persönliche > Zertifikate** , und suchen Sie das Signatur-oder Verschlüsselungs Zertifikat, das Sie aktualisieren möchten.
3. Klicken Sie mit der rechten Maustaste auf das Zertifikat, und wählen Sie **Alle Tasks > private Schlüssel verwalten**
4. Klicken Sie auf **Hinzufügen** , um einem neuen Benutzer Zugriff auf den privaten Schlüssel des Zertifikats zu gewähren.
5. Geben Sie in der Objektauswahl den Namen des GMSA-Kontos für die zuvor gefundenen HGS ein, und klicken Sie dann auf **OK**.
6. Stellen Sie sicher, dass GMSA über **Lese** Zugriff auf das Zertifikat verfügt.
7. Klicken Sie auf **OK** , um das Fenster Berechtigung zu schließen.

Wenn Sie HGS auf Server Core ausführen oder den Server remote verwalten, können Sie keine privaten Schlüssel mit dem lokalen Zertifikat-Manager verwalten.
Stattdessen müssen Sie das [PowerShell-Modul für geschützte Fabric-Tools](https://www.powershellgallery.com/packages/GuardedFabricTools) herunterladen, mit dem Sie die Berechtigungen in PowerShell verwalten können.

1. Öffnen Sie eine PowerShell-Konsole mit erhöhten Rechten auf dem Server Core-Computer, oder verwenden Sie PowerShell-Remoting mit einem Konto, das über lokale Administrator Berechtigungen für HGS verfügt.
2. Führen Sie die folgenden Befehle aus, um das PowerShell-Modul für geschützte Fabric-Tools zu installieren und dem GMSA-Konto Zugriff auf den privaten Schlüssel zu gewähren.

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

#### <a name="grant-access-to-hsm-or-custom-provider-backed-private-keys"></a>Gewähren des Zugriffs auf HSM oder benutzerdefinierte private Schlüssel des Anbieters

Wenn die privaten Schlüssel Ihres Zertifikats von einem Hardware Sicherheitsmodul (HSM) oder einem benutzerdefinierten Schlüsselspeicher Anbieter (KSP) unterstützt werden, hängt das Berechtigungs Modell von Ihrem spezifischen Softwareanbieter ab.
Um die besten Ergebnisse zu erzielen, finden Sie auf der Dokumentation oder Support Website Ihres Herstellers Informationen dazu, wie die Berechtigungen für private Schlüssel für ihr bestimmtes Gerät bzw. Ihre Software behandelt werden.

Einige Hardware Sicherheitsmodule unterstützen nicht das Gewähren von Zugriff auf einen privaten Schlüssel für bestimmte Benutzerkonten. Stattdessen wird dem Computer Konto der Zugriff auf alle Schlüssel in einem bestimmten Schlüsselsatz gestattet.
Bei solchen Geräten ist es in der Regel ausreichend, dem Computer den Zugriff auf Ihre Schlüssel zu gewähren, und HGS können diese Verbindung nutzen.

**Tipps für HSMs**

Unten sind die empfohlenen Konfigurationsoptionen aufgeführt, die Sie bei der erfolgreichen Verwendung von HSM-gestützten Schlüsseln mit HGS basierend auf den Erfahrungen von Microsoft und den zugehörigen Partnern unterstützen.
Diese Tipps werden Ihnen zur Verfügung gestellt und sind nicht garantiert, dass Sie zum Zeitpunkt des Lesens korrekt sind. Sie werden auch nicht von den HSM-Herstellern unterstützt.
Wenn Sie weitere Fragen haben, wenden Sie sich an Ihren HSM-Hersteller, um genaue Informationen zu Ihrem speziellen Gerät zu erhalten.

HSM-Marke/-Reihe      | Vorschlag
----------------------|-------------
Gemalto SafeNet       | Stellen Sie sicher, dass die Eigenschaft Schlüssel Verwendung in der Zertifikat Anforderungs Datei auf 0xa0 festgelegt ist, sodass das Zertifikat zum Signieren und Verschlüsseln verwendet werden kann. Außerdem müssen Sie dem GMSA-Konto mit dem lokalen Zertifikat-Manager-Tool *Lese* Zugriff auf den privaten Schlüssel gewähren (siehe die obigen Schritte).
"nCipher nShield"        | Stellen Sie sicher, dass jeder HGS-Knoten Zugriff auf die Security World hat, die Signatur-und Verschlüsselungsschlüssel enthält. Sie müssen keine GMSA-spezifischen Berechtigungen konfigurieren.
Utimaco-kryptoserver | Stellen Sie sicher, dass die Eigenschaft Schlüssel Verwendung in der Zertifikat Anforderungs Datei auf 0x13 festgelegt ist, sodass das Zertifikat für die Verschlüsselung, Entschlüsselung und Signierung verwendet werden kann.

### <a name="certificate-requests"></a>Zertifikat Anforderungen

Wenn Sie eine Zertifizierungsstelle zum Ausstellen Ihrer Zertifikate in einer Public Key-Infrastruktur (PKI)-Umgebung verwenden, müssen Sie sicherstellen, dass Ihre Zertifikat Anforderung die Mindestanforderungen für die Verwendung dieser Schlüssel durch die HGS enthält.

**Signieren von Zertifikaten**

CSR-Eigenschaft | Erforderlicher Wert
-------------|---------------
Algorithmus    | RSA
Schlüsselgröße     | Mindestens 2048 Bits
Schlüsselverwendung    | Signatur/Vorzeichen/DigitalSignature

**Verschlüsselungs Zertifikate**

CSR-Eigenschaft | Erforderlicher Wert
-------------|---------------
Algorithmus    | RSA
Schlüsselgröße     | Mindestens 2048 Bits
Schlüsselverwendung    | Verschlüsselung/Verschlüsselung/DataEncipherment

**Vorlagen für Active Directory Zertifikat Dienste**

Wenn Sie die Zertifikat Vorlagen für die Zertifikat Dienste (Active Directory Certificate Services, ADCs) zum Erstellen der Zertifikate verwenden, empfiehlt es sich, eine Vorlage mit den folgenden Einstellungen zu verwenden:

ADCs-Vorlagen Eigenschaft | Erforderlicher Wert
-----------------------|---------------
Anbieter Kategorie      | Schlüsselspeicheranbieter
Algorithmusname         | RSA
Minimale Schlüsselgröße       | 2\.048
Zweck                | Signatur und Verschlüsselung
Schlüssel Verwendungs Erweiterung    | Digitale Signatur, Schlüssel Verschlüsselung, Datenverschlüsselung ("Verschlüsselung von Benutzerdaten zulassen")


### <a name="time-drift"></a>Zeit Abweichung

Wenn die Zeit Ihres Servers maßgeblich von der von anderen HGS-Knoten oder Hyper-V-Hosts in Ihrem geschützten Fabric abweicht, treten möglicherweise Probleme mit der Gültigkeit des Nachweis Zertifikats des Nachweis Vorgangs auf.
Das Signatur Geber Zertifikat wird im Hintergrund auf HGS erstellt und erneuert und zum Signieren von Integritäts Zertifikaten verwendet, die vom Nachweis Dienst für überwachte Hosts ausgestellt wurden.

Führen Sie den folgenden Befehl an einer PowerShell-Eingabeaufforderung mit erhöhten Rechten aus, um das Signatur Geber Zertifikat zu aktualisieren.

```powershell
Start-ScheduledTask -TaskPath \Microsoft\Windows\HGSServer -TaskName 
AttestationSignerCertRenewalTask
```

Alternativ können Sie die geplante Aufgabe auch manuell ausführen, indem Sie **Taskplaner** (taskschd. msc) öffnen, zu **Taskplaner Bibliothek > Microsoft > Windows > hgsserver** navigieren und die Aufgabe mit dem Namen  **Attestationsignercertrenewaltask**.

## <a name="switching-attestation-modes"></a>Wechseln der Nachweis Modi

Wenn Sie HGS vom TPM-Modus in den Active Directory Modus wechseln oder umgekehrt mithilfe des Cmdlets [Set-hgsserver](https://technet.microsoft.com/library/mt652180.aspx) , kann es bis zu 10 Minuten dauern, bis jeder Knoten in Ihrem HGS-Cluster mit der Erzwingung des neuen Nachweis Modus beginnt.
Dies ist das normale Verhalten.
Es wird empfohlen, dass Sie keine Richtlinien entfernen, die Hosts aus dem vorherigen Nachweis Modus zulassen, bis Sie überprüft haben, ob alle Hosts erfolgreich mit dem neuen Nachweis Modus getestet wurden.

**Bekanntes Problem beim Wechsel von TPM in den AD-Modus**

Wenn Sie Ihren HGS-Cluster im TPM-Modus initialisiert und später in den Active Directory-Modus gewechselt haben, liegt ein bekanntes Problem vor, das verhindert, dass andere Knoten in Ihrem HGS-Cluster in den neuen Nachweis Modus wechseln.
Um sicherzustellen, dass alle HGS-Server den richtigen Nachweis Modus erzwingen, führen Sie `Set-HgsServer -TrustActiveDirectory` **auf jedem Knoten** des HGS-Clusters aus.
Dieses Problem tritt nicht auf, wenn Sie vom TPM-Modus in den AD *-* Modus wechseln und der Cluster ursprünglich im AD-Modus eingerichtet wurde.

Sie können den Nachweis Modus Ihres HGS-Servers durch Ausführen von [Get-hgsserver](https://technet.microsoft.com/library/mt652162.aspx)überprüfen.

## <a name="memory-dump-encryption-policies"></a>Verschlüsselungsrichtlinien für den Speicher Abbild

Wenn Sie versuchen, die Verschlüsselungsrichtlinien für das Speicher Abbild zu konfigurieren und die standardmäßigen HGS-dumprichtlinien (HGS @ no__t-0nodumps, HGS @ no__t-1dumpencryption und HGS @ no__t-2dumpverschlüsseltionkey) oder das dumprichtliniencmdlet (Add-hgsattestationdumppolicy) nicht anzuzeigen, ist dies wahrscheinlich ist das neueste kumulative Update nicht installiert.
[Aktualisieren Sie den HGS-Server](guarded-fabric-manage-hgs.md#patching-hgs) auf das neueste kumulative Windows Update, und [Aktivieren Sie die neuen Nachweis Richtlinien](guarded-fabric-manage-hgs.md#updates-requiring-policy-activation), um dies zu beheben.
Stellen Sie sicher, dass Sie Ihre Hyper-V-Hosts auf das gleiche kumulative Update aktualisieren, bevor Sie die neuen Nachweis Richtlinien aktivieren, da Hosts, auf denen die neuen dumpverschlüsselungs Funktionen nicht installiert sind, möglicherweise nach dem Aktivieren der HGS-Richtlinie fehlschlagen.

## <a name="endorsement-key-certificate-error-messages"></a>Fehlermeldungen für den Endorsement Key-Zertifikat

Beim Registrieren eines Hosts mithilfe des Cmdlets [Add-hgsattestationtpmhost](https://docs.microsoft.com/powershell/module/hgsattestation/add-hgsattestationtpmhost) werden zwei TPM-IDs aus der bereitgestellten Plattform-bezeichnerdatei extrahiert: das Endorsement Key-Zertifikat (ekcert) und der Public Endorsement Key (ekpub).
Das ekcert identifiziert den Hersteller des TPM und stellt sicher, dass das TPM authentisch ist und über die normale Lieferkette gefertigt wird.
Das ekpub identifiziert dieses bestimmte TPM eindeutig und ist eines der Measures, die HGS verwendet, um einem Host Zugriff zum Ausführen von abgeschirmten VMS zu gewähren.

Beim Registrieren eines TPM-Hosts wird eine Fehlermeldung angezeigt, wenn eine der beiden Bedingungen erfüllt ist:
1. Die Plattform-bezeichnerdatei enthält **kein** Endorsement Key-Zertifikat.
2. Die Plattform-bezeichnerdatei enthält ein Endorsement Key-Zertifikat, aber dieses Zertifikat ist auf dem System **nicht vertrauenswürdig** .

Bestimmte TPM-Hersteller enthalten keine ekcerts in ihren TPMs.
Wenn Sie vermuten, dass dies bei Ihrem TPM der Fall ist, vergewissern Sie sich bei Ihrem OEM, dass die TPMs nicht über ein ekcert verfügen sollten, und verwenden Sie das Flag "`-Force`", um den Host manuell bei HGS zu registrieren.
Wenn Ihr TPM über ein ekcert verfügen soll, aber in der Datei mit der Platt Form Kennung nicht gefunden wurde, stellen Sie sicher, dass Sie beim Ausführen von " [Get-platformidentifier](https://docs.microsoft.com/powershell/module/platformidentifier/get-platformidentifier) " auf dem Host eine Administrator-PowerShell-Konsole (erweitert) verwenden.

Wenn Sie die Fehlermeldung erhalten, dass Ihr ekcert nicht vertrauenswürdig ist, stellen Sie sicher, dass Sie [das vertrauenswürdige TPM](guarded-fabric-install-trusted-tpm-root-certificates.md) -Stamm Zertifikat Paket auf jedem HGS-Server installiert haben und dass sich das Stamm Zertifikat für den **TPM-Hersteller auf dem lokalen Computer befindet. t-2rootca-** Speicher. Alle anwendbaren zwischen Zertifikate müssen auch im Trust **dtpm @ no__t-1intermediateca-** Speicher auf dem lokalen Computer installiert werden.
Nachdem Sie die Stamm-und zwischen Zertifikate installiert haben, sollten Sie `Add-HgsAttestationTpmHost` erfolgreich ausführen können.
