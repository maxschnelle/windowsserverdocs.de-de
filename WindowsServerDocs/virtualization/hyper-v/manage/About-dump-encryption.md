---
title: Informationen zur Verschlüsselung der dump
description: Beschreibt, wie Dumpdateien zu verschlüsseln und die Problembehandlung bei Verschlüsselung.
ms.prod: windows-server-threshold
manager: dongill
ms.topic: article
author: larsiwer
ms.asset: b78ab493-e7c3-41f5-ab36-29397f086f32
ms.author: kathydav
ms.date: 11/03/2016
ms.openlocfilehash: e0ca8829aa8f93e7543b4183539beade3b4aeb47
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812391"
---
# <a name="about-dump-encryption"></a>Informationen zur Verschlüsselung der dump
Speicherabbildverschlüsselung kann verwendet werden, zum Verschlüsseln von Absturzabbildern und live-Dumps für ein System generiert wird. Die Dumps werden mit der ein symmetrischer Verschlüsselungsschlüssel wird generiert für jede Sicherung verschlüsselt. Dieser Schlüssel selbst wird verschlüsselt mit dem öffentlichen Schlüssel, die vom vertrauenswürdigen Administrator des Hosts (Crash Dumps Verschlüsselung-Schlüsselschutzvorrichtung) angegeben. Dadurch wird sichergestellt, dass nur eine Person mit den passenden privaten Schlüssel zu entschlüsseln und daher Zugriff auf Inhalt des Speicherabbilds. Diese Funktion wird in einem geschützten Fabric genutzt.
Hinweis: Wenn Sie die speicherabbildverschlüsselung konfigurieren, auch deaktivieren Sie Windows-Fehlerberichterstattung. WER kann nicht verschlüsselte Absturzabbilder gelesen werden.

# <a name="configuring-dump-encryption"></a>Konfigurieren die speicherabbildverschlüsselung
## <a name="manual-configuration"></a>Manuelle Konfiguration
Um speicherabbildverschlüsselung mithilfe der Registrierung zu aktivieren, konfigurieren Sie die folgenden Registrierungswerte unter `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl`

| Wertname | Typ | Wert |
| ---------- | ---- | ----- |
| DumpEncryptionEnabled | DWORD | 1 zum Aktivieren der speicherabbildverschlüsselung, 0 zum Deaktivieren der speicherabbildverschlüsselung |
| EncryptionCertificates\Certificate.1::PublicKey | Binär | Öffentliche Schlüssel (RSA, 2048-Bit), die für die Verschlüsselung von Dumps verwendet werden soll. Es muss sich um formatiert [BCRYPT_RSAKEY_BLOB](https://msdn.microsoft.com/library/windows/desktop/aa375531(v=vs.85).aspx). |
| EncryptionCertificates\Certificate.1::Thumbprint | Zeichenfolge | Fingerabdruck des Zertifikats auf automatische Suche der privaten Schlüssel im lokalen Zertifikatspeicher lässt zu, wenn ein Absturzabbild zu entschlüsseln. |


## <a name="configuration-using-script"></a>Konfiguration mithilfe von Skripts
Zur Vereinfachung der Konfiguration einer [Beispielskript](https://github.com/Microsoft/Virtualization-Documentation/tree/live/hyperv-tools/DumpEncryption) ist verfügbar, um die speicherabbildverschlüsselung basierend auf einem öffentlichen Schlüssel aus einem Zertifikat zu aktivieren.

1. In einer vertrauenswürdigen Umgebung: Erstellen Sie ein Zertifikat mit einem 2048-Bit-RSA-Schlüssel und exportieren das öffentliche Zertifikat
2. Auf der Zielhosts: Importieren Sie das öffentliche Zertifikat in den lokalen Zertifikatspeicher
3. Führen Sie das Beispielskript für die Konfiguration 
    ```
    .\Set-DumpEncryptionConfiguration.ps1 -Certificate (Cert:\CurrentUser\My\093568AB328DF385544FAFD57EE53D73EFAAF519) -Force
    ```

# <a name="decrypting-encrypted-dumps"></a>Entschlüsselt verschlüsselten dumps
Um eine vorhandene verschlüsselte Speicherabbilddatei entschlüsseln zu können, müssen Sie zum Herunterladen und installieren das Debuggen für Windows. Dieses Tool enthält KernelDumpDecrypt.exe die verwendet werden kann, um eine verschlüsselte Dumpdatei nicht entschlüsseln.
Wenn das Zertifikat, einschließlich des privaten Schlüssels im Zertifikatspeicher des aktuellen Benutzers vorhanden ist, kann durch Aufrufen die Dumpdatei entschlüsselt werden

```
    KernelDumpDecrypt.exe memory.dmp memory_decr.dmp
```
Nach der Entschlüsselung können Tools wie WinDbg die entschlüsselte Datei öffnen.

# <a name="troubleshooting-dump-encryption"></a>Dump-Encryption-Problembehandlung
Wenn speicherabbildverschlüsselung auf einem System aktiviert ist, jedoch keine Dumpdateien generiert werden, überprüfen Sie auf des Systems `System` Ereignisprotokoll `Kernel-IO` 1207-Ereignis. Wenn speicherabbildverschlüsselung nicht initialisiert werden kann, wird dieses Ereignis wird erstellt, und Dumps werden deaktiviert.

| Detaillierte Fehlermeldung | Schritte, um zu vermeiden |
| ---------------------- | ----------------- |
| Öffentliche Schlüssel oder Fingerabdruck Registrierung fehlt | Überprüfen Sie, ob die beiden Registrierungswerte am erwarteten Speicherort vorhanden ist. |
| Ungültiger, öffentlicher Schlüssel | Stellen Sie sicher, dass der öffentliche Schlüssel gespeichert, die im Registrierungswert öffentlicher Schlüssel, als gespeichert wird [BCRYPT_RSAKEY_BLOB](https://msdn.microsoft.com/library/windows/desktop/aa375531(v=vs.85).aspx). |
| Nicht unterstützte Größe für den öffentlichen Schlüssel | Derzeit werden nur 2048-Bit-RSA-Schlüssel unterstützt. Konfigurieren eines Schlüssels, das dieser Anforderung entspricht. |

Außerdem überprüfen, ob der Wert `GuardedHost` unter `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl\ForceDumpsDisabled` auf einen anderen Wert als 0 festgelegt ist. Dadurch werden Absturzabbilder vollständig deaktiviert. Wenn dies der Fall ist, wird es auf 0 festgelegt.
