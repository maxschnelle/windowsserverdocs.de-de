---
title: Problembehandlung beim Host-Überwachungsdienst
ms.topic: article
ms.assetid: 424b8090-0692-49a6-9dc4-3c0e77d74b80
manager: dongill
author: rpsqrd
description: Lösungen zu häufigen Problemen bei der Bereitstellung oder dem Betrieb eines Host-Überwachungsdienst-Servers (HGS) in einem geschützten Fabric.
ms.author: ryanpu
ms.date: 10/12/2020
ms.openlocfilehash: 398029ed048ac835d23ffebb954baad13970b538
ms.sourcegitcommit: c56e74743e5ad24b28ae81668668113d598047c6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987294"
---
# <a name="troubleshooting-the-host-guardian-service"></a>Problembehandlung beim Host-Überwachungsdienst

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Artikel werden Lösungen für häufige Probleme beschrieben, die beim Bereitstellen oder betreiben eines HGS-Servers (Host-Überwachungsdienst) in einem geschützten Fabric auftreten.
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
4. Wählen Sie **Hinzufügen** aus, um einem neuen Benutzer Zugriff auf den privaten Schlüssel des Zertifikats zu gewähren.
5. Geben Sie in der Objektauswahl den Namen des GMSA-Kontos für die zuvor gefundenen HGS ein, und klicken Sie dann auf **OK**.
6. Stellen Sie sicher, dass GMSA über **Lese** Zugriff auf das Zertifikat verfügt.
7. Wählen Sie **OK** , um das Berechtigungs Fenster zu schließen.

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
In jedem Fall benötigt das von HGS verwendete GMSA *Lese* Berechtigungen für die privaten Schlüssel für die Verschlüsselung, Signatur und den Kommunikations Zertifikat, damit Signierungs-und Verschlüsselungs Vorgänge durchgeführt werden können.

Einige Hardware Sicherheitsmodule unterstützen nicht das Gewähren von Zugriff auf einen privaten Schlüssel für bestimmte Benutzerkonten. Stattdessen wird dem Computer Konto der Zugriff auf alle Schlüssel in einem bestimmten Schlüsselsatz gestattet.
Bei solchen Geräten ist es in der Regel ausreichend, dem Computer den Zugriff auf Ihre Schlüssel zu gewähren, und HGS können diese Verbindung nutzen.

**Tipps für HSMs**

Unten sind die empfohlenen Konfigurationsoptionen aufgeführt, die Sie bei der erfolgreichen Verwendung von HSM-gestützten Schlüsseln mit HGS basierend auf den Erfahrungen von Microsoft und den zugehörigen Partnern unterstützen.
Diese Tipps werden Ihnen zur Verfügung gestellt und sind nicht garantiert, dass Sie zum Zeitpunkt des Lesens korrekt sind. Sie werden auch nicht von den HSM-Herstellern unterstützt.
Wenn Sie weitere Fragen haben, wenden Sie sich an Ihren HSM-Hersteller, um genaue Informationen zu Ihrem speziellen Gerät zu erhalten.

HSM-Marke/-Reihe      | Vorschlag
----------------------|-------------
Gemalto SafeNet       | Stellen Sie sicher, dass die Eigenschaft Schlüssel Verwendung in der Zertifikat Anforderungs Datei auf 0xa0 festgelegt ist, sodass das Zertifikat zum Signieren und Verschlüsseln verwendet werden kann. Außerdem müssen Sie dem GMSA-Konto mit dem lokalen Zertifikat-Manager-Tool *Lese* Zugriff auf den privaten Schlüssel gewähren (siehe die obigen Schritte).
"nCipher nShield"        | Stellen Sie sicher, dass jeder HGS-Knoten Zugriff auf die Security World hat, die Signatur-und Verschlüsselungsschlüssel enthält. Außerdem müssen Sie ggf. den GMSA *Lese* Zugriff auf den privaten Schlüssel mit dem lokalen Zertifikat-Manager gewähren (siehe die obigen Schritte).
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

Wenn Sie zum Erstellen der Zertifikate Active Directory Certificate Services (ADCs)-Zertifikat Vorlagen verwenden, empfiehlt es sich, eine Vorlage mit den folgenden Einstellungen zu verwenden:

ADCs-Vorlagen Eigenschaft | Erforderlicher Wert
-----------------------|---------------
Anbieter Kategorie      | Schlüsselspeicheranbieter
Algorithmusname         | RSA
Minimale Schlüsselgröße       | 2048
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

Alternativ können Sie die geplante Aufgabe auch manuell ausführen, indem Sie **Taskplaner** (taskschd. msc) öffnen, zu **Taskplaner Bibliothek > Microsoft > Windows > hgsserver** navigieren und die Aufgabe mit dem Namen **attestationsignercertrenewaltask**ausführen.

## <a name="switching-attestation-modes"></a>Wechseln der Nachweis Modi

Wenn Sie HGS vom TPM-Modus in den Active Directory Modus wechseln oder umgekehrt mithilfe des Cmdlets [Set-hgsserver](https://technet.microsoft.com/library/mt652180.aspx) , kann es bis zu 10 Minuten dauern, bis jeder Knoten in Ihrem HGS-Cluster mit der Erzwingung des neuen Nachweis Modus beginnt.
Dies ist das normale Verhalten.
Es wird empfohlen, dass Sie keine Richtlinien entfernen, die Hosts aus dem vorherigen Nachweis Modus zulassen, bis Sie überprüft haben, ob alle Hosts erfolgreich mit dem neuen Nachweis Modus getestet wurden.

**Bekanntes Problem beim Wechsel von TPM in den AD-Modus**

Wenn Sie Ihren HGS-Cluster im TPM-Modus initialisiert und später in den Active Directory Modus gewechselt haben, gibt es ein bekanntes Problem, das verhindert, dass andere Knoten in Ihrem HGS-Cluster in den neuen Nachweis Modus wechseln.
Um sicherzustellen, dass alle HGS-Server den richtigen Nachweis Modus erzwingen, führen `Set-HgsServer -TrustActiveDirectory` Sie **auf jedem Knoten** des HGS-Clusters aus.
Dieses Problem tritt nicht auf, wenn Sie vom TPM-Modus in den AD *-* Modus wechseln und der Cluster ursprünglich im AD-Modus eingerichtet wurde.

Sie können den Nachweis Modus Ihres HGS-Servers durch Ausführen von [Get-hgsserver](https://technet.microsoft.com/library/mt652162.aspx)überprüfen.

## <a name="memory-dump-encryption-policies"></a>Verschlüsselungsrichtlinien für den Speicher Abbild

Wenn Sie versuchen, die Verschlüsselungsrichtlinien für Speicher Abbilder zu konfigurieren und die standardmäßigen HGS-dumprichtlinien (HGS \_ nodumps, HGS \_ dumpencryption und HGS \_ dumpverschlüsselungskey) oder das Cmdlet für die dumprichtlinie (Add-hgsattestationdumppolicy) nicht zu sehen, ist es wahrscheinlich, dass das neueste kumulative Update nicht installiert ist.
[Aktualisieren Sie den HGS-Server](guarded-fabric-manage-hgs.md#patching-hgs) auf das neueste kumulative Windows Update, und [Aktivieren Sie die neuen Nachweis Richtlinien](guarded-fabric-manage-hgs.md#updates-requiring-policy-activation), um dies zu beheben.
Stellen Sie sicher, dass Sie Ihre Hyper-V-Hosts auf das gleiche kumulative Update aktualisieren, bevor Sie die neuen Nachweis Richtlinien aktivieren, da Hosts, auf denen die neuen dumpverschlüsselungs Funktionen nicht installiert sind, möglicherweise nach dem Aktivieren der HGS-Richtlinie fehlschlagen.

## <a name="endorsement-key-certificate-error-messages"></a>Fehlermeldungen für den Endorsement Key-Zertifikat

Beim Registrieren eines Hosts mithilfe des Cmdlets [Add-hgsattestationtpmhost](/powershell/module/hgsattestation/add-hgsattestationtpmhost) werden zwei TPM-IDs aus der bereitgestellten Plattform-bezeichnerdatei extrahiert: das Endorsement Key-Zertifikat (ekcert) und der Public Endorsement Key (ekpub).
Das ekcert identifiziert den Hersteller des TPM und stellt sicher, dass das TPM authentisch ist und über die normale Lieferkette gefertigt wird.
Das ekpub identifiziert dieses bestimmte TPM eindeutig und ist eines der Measures, die HGS verwendet, um einem Host Zugriff zum Ausführen von abgeschirmten VMS zu gewähren.

Beim Registrieren eines TPM-Hosts wird eine Fehlermeldung angezeigt, wenn eine der beiden Bedingungen erfüllt ist:
1. Die Plattform-bezeichnerdatei enthält **kein** Endorsement Key-Zertifikat.
2. Die Plattform-bezeichnerdatei enthält ein Endorsement Key-Zertifikat, aber dieses Zertifikat ist auf dem System **nicht vertrauenswürdig** .

Bestimmte TPM-Hersteller enthalten keine ekcerts in ihren TPMs.
Wenn Sie vermuten, dass dies bei Ihrem TPM der Fall ist, vergewissern Sie sich bei Ihrem OEM, dass Ihre TPMs kein ekcert aufweisen sollten, und verwenden Sie das `-Force` Flag, um den Host manuell bei HGS zu registrieren.
Wenn Ihr TPM über ein ekcert verfügen soll, aber in der Datei mit der Platt Form Kennung nicht gefunden wurde, stellen Sie sicher, dass Sie beim Ausführen von " [Get-platformidentifier](/powershell/module/platformidentifier/get-platformidentifier) " auf dem Host eine Administrator-PowerShell-Konsole (erweitert) verwenden.

Wenn Sie die Fehlermeldung erhalten, dass Ihr ekcert nicht vertrauenswürdig ist, stellen Sie sicher, dass Sie [das vertrauenswürdige TPM](guarded-fabric-install-trusted-tpm-root-certificates.md) -Stamm Zertifikat Paket auf jedem HGS-Server installiert haben und dass das Stamm Zertifikat für den TPM-Hersteller im Trust **dtpm \_ rootca** -Speicher des lokalen Computers vorhanden ist. Alle anwendbaren zwischen Zertifikate müssen auch im Trust **dtpm \_ intermediateca** -Speicher auf dem lokalen Computer installiert werden.
Nachdem Sie die Stamm-und zwischen Zertifikate installiert haben, sollten Sie erfolgreich ausgeführt werden können `Add-HgsAttestationTpmHost` .

## <a name="group-managed-service-account-gmsa-privileges"></a>Berechtigungen für Gruppen verwaltete Dienst Konten (GMSA)

Für das HGS-Dienst Konto (GMSA, das für den Schlüsselschutz Dienst-Anwendungs Pool in IIS verwendet wird) müssen Berechtigungen zum [Generieren von Sicherheits](/windows/security/threat-protection/security-policy-settings/generate-security-audits) Überwachungen erteilt werden, auch bekannt als `SeAuditPrivilege` . Wenn diese Berechtigung fehlt, ist die anfängliche HGS-Konfiguration erfolgreich, und IIS wird gestartet, aber der Schlüsselschutz Dienst ist nicht funktionsfähig und gibt den HTTP-Fehler 500 _("Server Fehler in/KeyProtection-Anwendung") zurück._ Möglicherweise beachten Sie auch die folgenden Warnmeldungen im Anwendungs Ereignisprotokoll.
```
System.ComponentModel.Win32Exception (0x80004005): A required privilege is not held by the client
at Microsoft.Windows.KpsServer.Common.Diagnostics.Auditing.NativeUtility.RegisterAuditSource(String pszSourceName, SafeAuditProviderHandle& phAuditProvider)
at Microsoft.Windows.KpsServer.Common.Diagnostics.Auditing.SecurityLog.RegisterAuditSource(String sourceName)
```
oder
```
Failed to register the security event source.
   at System.Web.HttpApplicationFactory.EnsureAppStartCalledForIntegratedMode(HttpContext context, HttpApplication app)
   at System.Web.HttpApplication.RegisterEventSubscriptionsWithIIS(IntPtr appContext, HttpContext context, MethodInfo[] handlers)
   at System.Web.HttpApplication.InitSpecial(HttpApplicationState state, MethodInfo[] handlers, IntPtr appContext, HttpContext context)
   at System.Web.HttpApplicationFactory.GetSpecialApplicationInstance(IntPtr appContext, HttpContext context)
   at System.Web.Hosting.PipelineRuntime.InitializeApplication(IntPtr appContext)

Failed to register the security event source.
   at Microsoft.Windows.KpsServer.Common.Diagnostics.Auditing.SecurityLog.RegisterAuditSource(String sourceName)
   at Microsoft.Windows.KpsServer.Common.Diagnostics.Auditing.SecurityLog.ReportAudit(EventLogEntryType eventType, UInt32 eventId, Object[] os)
   at Microsoft.Windows.KpsServer.KpsServerHttpApplication.Application_Start()

A required privilege is not held by the client
   at Microsoft.Windows.KpsServer.Common.Diagnostics.Auditing.NativeUtility.RegisterAuditSource(String pszSourceName, SafeAuditProviderHandle& phAuditProvider)
   at Microsoft.Windows.KpsServer.Common.Diagnostics.Auditing.SecurityLog.RegisterAuditSource(String sourceName)
```
Darüber hinaus können Sie feststellen, dass keine der Schlüsselschutz Dienst-Cmdlets (z. b. [Get-hgskeyschutzcertificate](/powershell/module/hgskeyprotection/get-hgskeyprotectioncertificate)) funktionieren und stattdessen Fehler zurückgeben.

Um dieses Problem zu beheben, müssen Sie GMSA das "Generieren von Sicherheits Überwachungen" (SeAuditPrivilege) gewähren. Zu diesem Zweck können Sie entweder lokale Sicherheitsrichtlinien `SecPol.msc` für jeden Knoten des HGS-Clusters oder Gruppenrichtlinie verwenden. Alternativ können Sie mit [SecEdit.exe](/windows-server/administration/windows-commands/secedit) Tool die aktuelle Sicherheitsrichtlinie exportieren, die erforderlichen Änderungen in der Konfigurationsdatei vornehmen (bei der es sich um einen nur-Text handelt) und Sie dann wieder importieren.

> [!NOTE]
> Wenn Sie diese Einstellung konfigurieren, überschreibt die Liste der Sicherheitsprinzipien, die für ein-Privileg definiert sind, die Standardwerte (Sie werden nicht verkettet). Wenn Sie diese Richtlinien Einstellung definieren, achten Sie darauf, dass zusätzlich zu dem von Ihnen hinzugefügten GMSA beide Standard Inhaber dieser Berechtigung (Netzwerkdienst und lokaler Dienst) enthalten sind.
