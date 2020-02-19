---
title: Problembehandlung beim Host-Überwachungsdienst
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 80ea38f4-4de6-4f85-8188-33a63bb1cf81
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 09/25/2019
ms.openlocfilehash: ec885670ca6808e89c63848781c4ff3dc27799b8
ms.sourcegitcommit: 2a15de216edde8b8e240a4aa679dc6d470e4159e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/19/2020
ms.locfileid: "77465604"
---
# <a name="troubleshooting-guarded-hosts"></a>Problembehandlung für geschützte Hosts

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema werden Lösungen für häufige Probleme beschrieben, die beim Bereitstellen oder betreiben eines geschützten Hyper-V-Hosts in Ihrem geschützten Fabric auftreten.
Wenn Sie sich nicht sicher sind, welche Art von Problem Sie haben, versuchen Sie zunächst, die [geschützte Fabric-Diagnose](guarded-fabric-troubleshoot-diagnostics.md) auf Ihren Hyper-V-Hosts auszuführen, um die möglichen Gründe einzugrenzen.

## <a name="guarded-host-feature"></a>Überwachte Host Funktion

Wenn Probleme mit dem Hyper-v-Host auftreten, stellen Sie zunächst sicher, dass die **Hyper-v-Unterstützung des Host** -Überwachungs Diensts installiert ist.
Ohne dieses Feature fehlen dem Hyper-V-Host einige wichtige Konfigurationseinstellungen und Software, mit denen er den Nachweis durchlaufen und abgeschirmte VMS bereitstellen kann.

Verwenden Sie Server-Manager, oder führen Sie den folgenden Befehl in einem PowerShell-Fenster mit erhöhten Rechten aus:

```powershell
Get-WindowsFeature HostGuardian
```

Wenn das Feature nicht installiert ist, installieren Sie es mit dem folgenden PowerShell-Befehl:

```powershell
Install-WindowsFeature HostGuardian -Restart
```

## <a name="attestation-failures"></a>Nachweis Fehler

Wenn ein Host den Nachweis nicht mit dem Host-Überwachungsdienst übergibt, ist es nicht möglich, abgeschirmte VMS auszuführen.
Die Ausgabe von [Get-hgsclientconfiguration](https://technet.microsoft.com/library/dn914500.aspx) auf diesem Host zeigt Informationen darüber an, warum bei diesem Host ein Fehler aufgetreten ist.

In der folgenden Tabelle werden die Werte erläutert, die ggf. im Feld **attestationstatus** und mögliche nächste Schritte angezeigt werden können.

Attestationstatus         | Erklärung
--------------------------|------------
Abgelaufen                   | Der Host hat den Nachweis zuvor übermittelt, das ausgegebene Integritäts Zertifikat ist jedoch abgelaufen. Stellen Sie sicher, dass die Host-und HGS-Zeit synchronisiert sind.
Insecurehostconfiguration | Der Host hat den Nachweis nicht bestanden, weil er nicht den Nachweis Richtlinien entsprach, die auf HGS konfiguriert sind. Weitere Informationen finden Sie in der Tabelle attestationsubstatus.
NotConfigured             | Der Host ist nicht für die Verwendung eines HGS für den Nachweis und den Schlüsselschutz konfiguriert. Stattdessen ist Sie für den lokalen Modus konfiguriert. Wenn sich dieser Host in einem geschützten Fabric befindet, verwenden Sie [Set-hgsclientconfiguration](https://technet.microsoft.com/library/dn914494.aspx) , um die URLs für Ihren HGS-Server bereitzustellen.
Bestanden                    | Der Host hat den Nachweis übermittelt.
Transiendterror            | Der letzte Nachweis Versuch ist aufgrund eines Netzwerk-, Dienst-oder anderen temporären Fehlers fehlgeschlagen. Wiederholen Sie den letzten Vorgang.
Tpmerror                  | Der Host konnte den letzten Nachweis Versuch aufgrund eines Fehlers mit dem TPM nicht durchführen. Weitere Informationen finden Sie in den TPM-Protokollen.
Unauthorizedhost          | Der Host hat den Nachweis nicht bestanden, weil er nicht zum Ausführen von abgeschirmten VMS autorisiert ist. Stellen Sie sicher, dass der Host zu einer Sicherheitsgruppe gehört, die von HGS als vertrauenswürdig eingestuft wird
Unbekannt                   | Der Host hat noch nicht versucht, HGS zu bestätigen.

Wenn **attestationstatus** als **insecurehostconfiguration**gemeldet wird, werden im Feld **attestationsubstatus** ein oder mehrere Gründe aufgefüllt.
In der folgenden Tabelle werden die möglichen Werte für attestationsubstatus und Tipps zum Beheben des Problems erläutert.

Attestationsubstatus       | Bedeutung und Vorgehensweise
---------------------------|-------------------------------
BitLocker                  | Das Betriebssystem Volume des Hosts wird nicht von BitLocker verschlüsselt. Um dieses Problem zu beheben, [Aktivieren Sie BitLocker](https://technet.microsoft.com/itpro/windows/keep-secure/bitlocker-basic-deployment) auf dem Betriebssystem Volume, oder [Deaktivieren Sie die BitLocker-Richtlinie auf HGS](guarded-fabric-manage-hgs.md#review-attestation-policies).
Codeintegritypolicy        | Der Host ist nicht für die Verwendung einer Code Integritätsrichtlinie konfiguriert oder verwendet keine Richtlinie, die vom HGS-Server als vertrauenswürdig eingestuft wird. Stellen Sie sicher, dass eine Code Integritätsrichtlinie konfiguriert wurde, dass der Host neu gestartet wurde und die Richtlinie beim HGS-Server registriert ist. Weitere Informationen finden Sie unter [Erstellen und Anwenden einer Code Integritätsrichtlinie](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#create-and-apply-a-code-integrity-policy).
Dumpsenabled               | Der Host ist so konfiguriert, dass Absturz Abbilder oder Live-Speicher Abbilder zugelassen werden, was von ihren HGS-Richtlinien nicht zulässig ist. Um dieses Problem zu beheben, deaktivieren Sie Abbilder auf dem Host.
Dumpencryption             | Der Host ist so konfiguriert, dass Absturz Abbilder oder Live-Speicher Abbilder zugelassen werden, aber diese Abbilder nicht verschlüsselt werden. Deaktivieren Sie entweder Abbilder auf dem Host, oder konfigurieren Sie die [dumpverschlüsselung](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption).
Dumpverschlüsselungskey          | Der Host ist so konfiguriert, dass er Dumps zulässt und verschlüsselt, verwendet aber kein Zertifikat, das HGS bekannt ist, um Sie zu verschlüsseln. Um dieses Problem zu beheben, [Aktualisieren Sie den Verschlüsselungsschlüssel](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption) für die Sicherung auf dem Host, oder [registrieren Sie den Schlüssel bei HGS](guarded-fabric-manage-hgs.md#authorizing-new-guarded-hosts).
Voll Start                   | Der Host wurde aus dem Ruhezustand oder dem Ruhezustand fortgesetzt. Starten Sie den Host neu, damit ein sauberer, vollständiger Start ermöglicht wird.
Ruhe Zustands fähig         | Der Host ist so konfiguriert, dass er den Ruhezustand zulässt, ohne die Ruhe Zustands Datei zu verschlüsseln, was von ihren HGS-Richtlinien nicht zulässig ist. Deaktivieren Sie den Ruhezustand, starten Sie den Host neu, oder konfigurieren Sie die [dumpverschlüsselung](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption).
Hypervisorenforcedcodeintegritypolicy | Der Host ist nicht für die Verwendung einer durch Hypervisor erzwungenen Code Integritätsrichtlinie konfiguriert. Überprüfen Sie, ob die Code Integrität vom Hypervisor aktiviert, konfiguriert und erzwungen wird. Weitere Informationen finden Sie im [Device Guard-Bereitstellungs Handbuch](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-deploy-code-integrity-policies) .
IOMMU                      | Die virtualisierungsbasierten Sicherheitsfeatures des Hosts sind nicht so konfiguriert, dass ein IOMMU-Gerät zum Schutz vor Angriffen für den direkten Speicherzugriff erforderlich ist, wie dies für Ihre HGS-Richtlinien erforderlich ist. Vergewissern Sie sich, dass der Host über ein IOMMU verfügt, dass er aktiviert ist und dass Device Guard so konfiguriert ist, dass beim Starten von VSB der [DMA-Schutz erforderlich](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-enable-virtualization-based-security#enable-virtualization-based-security-vbs-and-device-guard) ist.
Pagefileencryption         | Die Verschlüsselung der Auslagerungs Datei ist auf dem Host nicht aktiviert. Um dieses Problem zu beheben, führen Sie `fsutil behavior set encryptpagingfile 1` aus, um die Verschlüsselung der Datei zu aktivieren Weitere Informationen finden Sie unter "f"- [Verhalten](https://technet.microsoft.com/library/cc785435.aspx).
SecureBoot                 | Der sichere Start ist auf diesem Host nicht aktiviert oder verwendet nicht die Microsoft-Vorlage für den sicheren Start. [Aktivieren Sie den sicheren Start](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/disabling-secure-boot#enable_secure_boot) mit der Microsoft Secure Boot-Vorlage, um dieses Problem zu beheben.
Securebootsettings         | Die TPM-Baseline auf diesem Host entspricht keiner der von HGS als vertrauenswürdig eingestuft. Dies kann vorkommen, wenn Ihre UEFI-Start-, dbx-, Debug-oder benutzerdefinierten Richtlinien für den sicheren Start durch die Installation neuer Hardware oder Software geändert werden. Wenn Sie die aktuelle Hardware, Firmware und Softwarekonfiguration dieses Computers als vertrauenswürdig einstufen, können Sie [eine neue TPM-Baseline erfassen](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#capture-the-tpm-baseline-for-each-unique-class-of-hardware) und [bei HGS registrieren](guarded-fabric-manage-hgs.md#authorizing-new-guarded-hosts).
Tcglogverifizierung         | Das TCG-Protokoll (TPM-Baseline) kann nicht abgerufen oder überprüft werden. Dies kann auf ein Problem mit der Firmware des Hosts, dem TPM oder anderen Hardwarekomponenten hinweisen. Wenn der Host für den PXE-Start konfiguriert ist, bevor Windows gestartet wird, kann auch ein veraltetes net Start Programm (NBP) diesen Fehler verursachen. Stellen Sie sicher, dass alle NBPs auf dem neuesten Stand sind, wenn PXE-Start aktiviert ist.
Virtualsecuremode          | Auf dem Host werden keine virtualisierungsbasierten Sicherheitsfunktionen ausgeführt. Stellen Sie sicher, dass VSB aktiviert ist und dass Ihr System den konfigurierten [Sicherheitsfeatures der Plattform](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-enable-virtualization-based-security#validate-enabled-device-guard-hardware-based-security-features)entspricht. Weitere Informationen zu den VSB-Anforderungen finden Sie in der [Device Guard-Dokumentation](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide) .

## <a name="modern-tls"></a>Modernes TLS

Wenn Sie eine Gruppenrichtlinie bereitgestellt oder den Hyper-V-Host anderweitig konfiguriert haben, um die Verwendung von TLS 1,0 zu verhindern, kann der Fehler "der Host-Überwachungsdienst Client konnte eine Schlüssel Schutzvorrichtung im Auftrag eines aufrufenden Prozesses nicht entpacken" beim Versuch, eine abgeschirmte VM zu starten, angezeigt werden.
Dies ist auf ein Standardverhalten in .NET 4,6 zurückzuführen, bei dem die standardmäßige TLS-Version des Systems beim Aushandeln unterstützter TLS-Versionen mit dem HGS-Server nicht berücksichtigt wird.

Um dieses Verhalten zu umgehen, führen Sie die folgenden beiden Befehle aus, um .net so zu konfigurieren, dass die standardmäßigen TLS-Versionen für alle .net-apps verwendet werden.

```cmd
reg add HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319 /v SystemDefaultTlsVersions /t REG_DWORD /d 1 /f /reg:64
reg add HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319 /v SystemDefaultTlsVersions /t REG_DWORD /d 1 /f /reg:32
```

> [!WARNING]
> Die Standardeinstellung für die TLS-Version des Systems wirkt sich auf alle .net-apps auf Ihrem Computer aus. Stellen Sie sicher, dass Sie die Registrierungsschlüssel in einer isolierten Umgebung testen, bevor Sie Sie auf den Produktions Computern bereitstellen.

Weitere Informationen zu .NET 4,6 und TLS 1,0 finden Sie unter [Lösen des TLS 1,0-Problems, 2. Edition](https://docs.microsoft.com/security/solving-tls1-problem).
