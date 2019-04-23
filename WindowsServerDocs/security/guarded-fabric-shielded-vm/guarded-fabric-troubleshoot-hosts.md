---
title: Problembehandlung für die Host-Überwachungsdienst
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 80ea38f4-4de6-4f85-8188-33a63bb1cf81
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 7fe01039b47c36d940973fba97d25c401f5af8a7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851371"
---
# <a name="troubleshooting-guarded-hosts"></a>Problembehandlung bei überwachten Hosts

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema wird beschrieben, Lösungen für häufige Probleme beim Bereitstellen oder einen überwachten Hyper-V-Host in Ihrer geschützten Fabric ausgeführt wird.
Wenn Sie die Art des Problems, erste führen nicht sicher sind die [überwachten Fabric-Diagnose](guarded-fabric-troubleshoot-diagnostics.md) bewirkt, dass auf den Hyper-V-Hosts das Potenzial eingrenzen.

## <a name="guarded-host-feature"></a>Überwachten Host-Funktion

Wenn Sie Probleme mit Ihrem Hyper-V-Host auftreten, stellen Sie zunächst sicher, die die **Hyper-V-Unterstützung für Host-Überwachungsdiensts** -Funktion installiert ist.
Ohne diese Funktion des Hyper-V-Hosts werden einige wichtige Konfigurationseinstellungen fehlen, und Software, mit denen sie zum Übergeben von Nachweis und Bereitstellen von abgeschirmten VMs.

Um festzustellen, ob das Feature installiert ist, verwenden Sie Server-Manager, oder führen Sie den folgenden Befehl in einem PowerShell-Fenster mit erhöhten Rechten aus:

```powershell
Get-WindowsFeature HostGuardian
```

Wenn das Feature nicht installiert ist, installieren Sie es mit dem folgenden PowerShell-Befehl ein:

```powershell
Install-WindowsFeature HostGuardian -Restart
```

## <a name="attestation-failures"></a>Nachweis-Fehler

Wenn ein Host Nachweis mit Host-Überwachungsdienst nicht bestanden hat, werden kann nicht abgeschirmte VMs ausgeführt.
Die Ausgabe des [Get-HgsClientConfiguration](https://technet.microsoft.com/library/dn914500.aspx) auf diesem Host wird werden Informationen zu Warum Nachweis auf diesem Host fehlgeschlagen ist.

In der folgenden Tabelle werden die Werte erläutert, die in angezeigt werden, können die **AttestationStatus** Feld und mögliche nächste Schritte beschrieben, falls zutreffend.

AttestationStatus         | Erläuterung
--------------------------|------------
Abgelaufen                   | Der Host übergeben Nachweis zuvor, aber das Integritätszertifikat, die, das es ausgestellt wurde, ist abgelaufen. Stellen Sie sicher, den Host und HGS-Zeit synchronisiert werden.
InsecureHostConfiguration | Der Host nicht einen Nachweis erbringen, da er nicht mit den Nachweis-Richtlinien konfiguriert, auf dem Host-Überwachungsdienst übereinstimmt. Weitere Informationen finden Sie in der Tabelle AttestationSubStatus.
NotConfigured             | Der Host ist nicht konfiguriert, um eine Host-Überwachungsdienst für Nachweis- und Schlüsselschutz verwenden. Es wird stattdessen im lokalen Modus, konfiguriert. Wenn dieser Host in einem geschützten Fabric ist, verwenden Sie [Set-HgsClientConfiguration](https://technet.microsoft.com/library/dn914494.aspx) mit den URLs für den Host-Überwachungsdienst-Server bereitstellen.
Übergeben                    | Der Host, der Nachweis übergeben wird.
TransientError            | Fehler bei der letzte Versuch für den Nachweis aufgrund einer Netzwerk-, Dienst oder anderer vorübergehender Fehler. Wiederholen Sie den letzten Vorgang aus.
TpmError                  | Der Host konnte seine letzten Nachweis Versuch aufgrund eines Fehlers mit TPM nicht abgeschlossen werden. Weitere Informationen finden Sie in der TPM-Protokolle.
UnauthorizedHost          | Der Host nicht einen Nachweis erbringen, weil sie nicht zum Ausführen geschützter VMs autorisiert wurde. Stellen Sie sicher, dass der Host gehört, zu einer Sicherheitsgruppe, die vom Host-Überwachungsdiensts zum Ausführen geschützter VMs als vertrauenswürdig eingestuft.
Unbekannt                   | Der Host hat nicht versucht, noch bei HGS zu bestätigen.


Bei der **AttestationStatus** wird gemeldet, als **InsecureHostConfiguration**, eine oder mehrere Gründe werden aufgefüllt werden, der **AttestationSubStatus** Feld.
In der folgenden Tabelle erläutert die möglichen Werte für AttestationSubStatus und Tipps zum Beheben des Problems.

AttestationSubStatus       | Was es bedeutet und was zu tun ist
---------------------------|-------------------------------
BitLocker                  | Host BS-Volume ist nicht mit BitLocker verschlüsselt. Um dies zu beheben [Aktivieren von BitLocker](https://technet.microsoft.com/itpro/windows/keep-secure/bitlocker-basic-deployment) auf dem Betriebssystemvolume oder [deaktivieren Sie die BitLocker-Richtlinie auf den Host-Überwachungsdienst](guarded-fabric-manage-hgs.md#review-attestation-policies).
CodeIntegrityPolicy        | Der Host nicht für die Verwendung eine codeintegritätsrichtlinie konfiguriert oder wird nicht mithilfe einer Richtlinie, die von der HGS-Server als vertrauenswürdig eingestuft. Stellen Sie sicher, eine codeintegritätsrichtlinie konfiguriert wurde, die der Host neu gestartet wurde, und die Richtlinie für den HGS-Server registriert ist. Weitere Informationen finden Sie unter [erstellen und anwenden eine codeintegritätsrichtlinie](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#create-and-apply-a-code-integrity-policy).
DumpsEnabled               | Der Host wird konfiguriert um Absturzabbilder zuzulassen oder zu live Speicherabbilder, Ihre Richtlinien für die Host-Überwachungsdienst nicht zulässig ist. Deaktivieren Sie dieses Problem lösen, Absturzabbilder auf dem Host ein.
DumpEncryption             | Der Host ist konfiguriert, um Absturzabbilder zu ermöglichen oder live-speicherauslastung sichert, aber diese Abbilder nicht verschlüsselt. Deaktivieren Sie die Abbilder auf dem Host oder [konfigurieren speicherabbildverschlüsselung](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption).
DumpEncryptionKey          | Der Host zum Zulassen und Verschlüsseln von Dumps konfiguriert ist, aber es verwendet ein Zertifikat, das bekannt, dass der Host-Überwachungsdienst nicht verschlüsseln. Um dies zu beheben [Aktualisieren des Verschlüsselungsschlüssels Dump](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption) auf dem Host oder [des Schlüssels bei HGS registriert](guarded-fabric-manage-hgs.md#authorizing-new-guarded-hosts).
FullBoot                   | Der Host wurde von einem Energiesparmodus oder Ruhezustand fortgesetzt. Starten Sie den Host aus, um einen sauberen, vollständige-Start zu ermöglichen.
HibernationEnabled         | Der Host ist konfiguriert, um den Ruhezustand zu ermöglichen, birgt die Ruhezustanddatei, was Ihren HGS-Richtlinien nicht zulässig ist. Deaktivieren Sie den Ruhezustand, und starten Sie den Host oder [konfigurieren speicherabbildverschlüsselung](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption).
HypervisorEnforcedCodeIntegrityPolicy | Der Host ist nicht konfiguriert, um eine Hypervisor erzwungenen codeintegritätsrichtlinie zu verwenden. Überprüfen Sie, ob die Codeintegrität ist aktiviert, konfiguriert und durch den Hypervisor erzwungen. Finden Sie unter den [Device Guard-Bereitstellungshandbuch](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-deploy-code-integrity-policies) für Weitere Informationen.
Iommu                      | Die virtualisierungsbasierte Sicherheit Features des Hosts sind nicht konfiguriert, um ein Gerät unterstützt für den Schutz vor Angriffen von Direct Memory Access, gemäß Ihren Richtlinien für die Host-Überwachungsdiensts erforderlich. Überprüfen Sie, ob der Host verfügt über eine IOMMU, die es aktiviert ist, und diese Device Guard besteht aus [so konfiguriert, dass die DMA-Schutzfunktionen](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-enable-virtualization-based-security#enable-virtualization-based-security-vbs-and-device-guard) beim Starten von VBS.
PagefileEncryption         | Seite dateiverschlüsselung wird auf dem Host nicht aktiviert. Führen Sie zum Beheben dieses Problems `fsutil behavior set encryptpagingfile 1` dateiverschlüsselung Seite zu aktivieren. Weitere Informationen finden Sie unter [Fsutil-Verhalten](https://technet.microsoft.com/library/cc785435.aspx).
SecureBoot                 | Sicherer Start ist entweder nicht auf diesem Host aktiviert ist oder nicht mithilfe der Vorlage für sicheren Start von Microsoft. [Aktivieren des sicheren Starts](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/disabling-secure-boot#enable_secure_boot) mit der Microsoft sicherer Start-Vorlage, um dieses Problem zu beheben.
SecureBootSettings         | Die TPM-Baseline auf diesem Host stimmt nicht mit einer der dieser Host-Überwachungsdienst vertrauenswürdig überein. Dies kann auftreten, wenn Ihre UEFI-Start Behörden, die DBX-Variable, Debug-Flag oder benutzerdefinierte Richtlinien für sicheren Start durch die Installation von neuer Hardware oder Software geändert werden. Wenn Sie die aktuelle Hardware, Firmware und Software-Konfiguration von diesem Computer vertrauen, können Sie [erfassen Sie eine neue TPM-Baseline](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#capture-the-tpm-baseline-for-each-unique-class-of-hardware) und [registrieren Sie ihn beim Host-Überwachungsdienst](guarded-fabric-manage-hgs.md#authorizing-new-guarded-hosts).
TcgLogVerification         | TCG-Protokoll (TPM-Baseline) kann nicht abgerufen oder überprüft werden. Dies kann ein Problem mit der hostfirmware, das TPM oder andere Hardwarekomponenten bedeuten. Wenn Sie Ihren Host für die PXE-Start versucht, vor dem Start von Windows konfiguriert ist, kann eine veraltete Net Start Programm (NBP) dieser Fehler auch verursacht. Stellen Sie sicher, dass alle Netzwerkstartprogramme auf dem neuesten Stand sind, wenn PXE-Start aktiviert ist.
VirtualSecureMode          | Sicherheit auf Basis der Virtualisierungsfunktionen sind auf dem Host nicht ausgeführt. Stellen Sie sicher, VBS aktiviert ist und dass Ihr System konfigurierten erfüllt [Sicherheitsfunktionen Plattform](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-enable-virtualization-based-security#validate-enabled-device-guard-hardware-based-security-features). Wenden Sie sich an den [Dokumentation zu Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide) für Weitere Informationen zu VBS-Anforderungen.
