---
title: Erfassen von TPM-Modus Informationen, die vom Host-Überwachungsdiensts erforderlich
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 915b1338-5085-481b-8904-75d29e609e93
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 12/12/2018
ms.openlocfilehash: 82171eee10a06cad6bb3ac30e8f771086975c242
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841661"
---
# <a name="authorize-guarded-hosts-using-tpm-based-attestation"></a>Autorisieren von überwachten Hosts über TPM-basierten Nachweis

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

TPM-Modus verwendet, eine TPM-ID (auch als eine Plattform Bezeichner oder ein Endorsement Key bezeichnet \[EKpub\]) zu beginnen, ermitteln, ob es sich bei ein bestimmter Host autorisiert ist, als "geschützt". In diesem Modus Nachweis verwendet Messwerte für die Integrität von Sicherer Start "und" Code, um sicherzustellen, dass der angegebener Hyper-V-Host befindet sich in einem ordnungsgemäßen Zustand, und nur vertrauenswürdigen Code ausgeführt wird. In der Reihenfolge für den Nachweis zu verstehen, was ist, und ist nicht fehlerfrei müssen Sie die folgenden Elemente erfasst:

1.  TPM-Bezeichner (EKpub)

    -  Diese Informationen sind nur für jeden Hyper-V-host

2.  TPM-Baseline (startmessungen)

    -  Dies gilt für alle Hyper-V-Hosts, die für die gleiche Klasse der Hardware ausgeführt werden soll.

3.  Codeintegritätsrichtlinie (einer Positivliste der zulässigen Binärdateien)

    -  Dies gilt für alle Hyper-V-Hosts, die allgemeine Hardware- und Softwarekonfiguration aufweisen

Es wird empfohlen, dass Sie den geplanten und CI-Richtlinie von einem Host"Verweis" erfassen, die repräsentativ für jede eindeutige Klasse von Hyper-V-Hardware-Konfiguration in Ihrem Rechenzentrum. Ab Windows Server-Version 1709, sind CI-Beispielrichtlinien am C:\Windows\schemas\CodeIntegrity\ExamplePolicies enthalten. 

## <a name="versioned-attestation-policies"></a>Mit versionsverwaltung durch das Attestation-Richtlinien

Windows Server-2019 führt eine neue Methode für den Nachweis, dem Namen *v2-Nachweis*, wobei ein TPM-Zertifikat vorhanden, damit die EKPub-Host-Überwachungsdienst hinzufügen sein muss. Die v1-Nachweis-Methode, die in Windows Server 2016 verwendet konnten Sie überschreiben diese sicherheitsprüfung durch Angabe des - Force-Flag beim Ausführen der hinzufügen-HgsAttestationTpmHost oder andere TPM-Nachweis-Cmdlets, um die Artefakte zu erfassen. Ab Windows Server-2019, v2-Nachweis wird standardmäßig verwendet, und Sie müssen das PolicyVersion - v1-Flag angeben, wenn Add-HgsAttestationTpmHost ausführen, müssen Sie ein TPM ohne Zertifikat zu registrieren. Die - Force Flag nicht mit v2-Nachweis funktioniert. 

Ein Host kann nur bestätigen lassen, ob alle Elemente (EKPub + TPM Baseline + Codeintegritätsrichtlinie) die gleiche Version von nachweisen. V2-Nachweis zuerst versucht wird, und schlägt dies fehl, wird die v1-Nachweis verwendet. Dies bedeutet, wenn Sie eine TPM-ID zu registrieren, indem Sie die v1-Nachweis verwenden möchten, müssen Sie auch das PolicyVersion - v1-Flag, um die v1-Nachweis verwenden, wenn Sie die TPM-Baseline zu erfassen, und erstellen Sie die CI-Richtlinie angeben. Wenn der TPM-Baseline und der codeintegritätsrichtlinie mithilfe von v2-Nachweis erstellt wurden, und klicken Sie dann später Sie einen überwachten Host ohne ein TPM-Zertifikat hinzufügen müssen, müssen Sie jedes Artefakt mit dem Flag für die v1 - Spezifikation neu zu erstellen. 

## <a name="capture-the-tpm-identifier-platform-identifier-or-ekpub-for-each-host"></a>Erfassen Sie den TPM-Bezeichner (Plattformbezeichner oder EKpub) für jeden host

1.  Die Fabric-Domäne Vergewissern Sie sich das TPM auf jedem Host ist zur Verwendung bereit – das heißt, das TPM initialisiert wird und des Besitzes abgerufen. Sie können den Status des TPM überprüfen, öffnen die TPM-Verwaltungskonsole (tpm.msc) oder durch Ausführen **Get-Tpm** in einer Windows PowerShell-Fenster mit erhöhten Rechten. Wenn Ihr TPM nicht in der **bereit** aufweist, müssen Sie initialisiert, und legen Sie den Besitz. Dies kann erfolgen in der TPM-Verwaltungskonsole oder durch Ausführen **Initialize Tpm**.

2.  Führen Sie für jeden überwachten Host den folgenden Befehl in einer mit erhöhten Rechten Windows PowerShell-Konsole, um seine EKpub zu erhalten. Für `<HostName>`, ersetzen Sie den eindeutigen Hostnamen mit etwas gut geeignet, um das Identifizieren von diesem Host – kann es sich seinem Hostnamen oder den Namen von einem Fabric Inventory-Dienst (falls verfügbar). Der Einfachheit halber benennen Sie die Datei mithilfe der Name des Hosts.

    ```powershell
    (Get-PlatformIdentifier -Name '<HostName>').InnerXml | Out-file <Path><HostName>.xml -Encoding UTF8
    ```
3.  Wiederholen Sie die vorherigen Schritte für jeden Host, der einem bewachten Host, wird Sie sicher, dass jede XML-Datei einen eindeutigen Namen geben werden soll.

4.  Geben Sie die resultierenden XML-Dateien für dem HGS-Administrator.

5.  Öffnen Sie in der Domäne des Host-Überwachungsdienst eine mit erhöhten Rechten aus Windows PowerShell-Konsole auf einem Host-Überwachungsdienst-Server, und führen Sie den folgenden Befehl aus. Wiederholen Sie den Befehl für jede XML-Dateien.

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
    ```

    > [!NOTE]
    > Wenn Sie ein Fehler auftritt, wenn Sie eine TPM-ID in Bezug auf ein nicht vertrauenswürdiges Endorsement Key-Zertifikat (EKCert) hinzufügen, stellen Sie sicher, dass die [vertrauenswürdige Stammzertifikate TPM wurden hinzugefügt,](guarded-fabric-install-trusted-tpm-root-certificates.md) auf den Host-Überwachungsdienst-Knoten.
    > Darüber hinaus verwenden einige TPM-Hersteller EKCerts nicht.
    > Sie können überprüfen, ob ein EKCert nicht vorhanden, ist durch die XML-Datei in einem Editor wie Editor öffnen und eine Fehlermeldung, die keine EKCert gesucht wurde gefunden.
    > Wenn dies der Fall ist, und Sie vertrauen, dass das TPM auf Ihrem Computer authentifiziert ist, können Sie die `-Force` Parameter Host-Überwachungsdienst die Host-ID hinzu. In Windows Server-2019, müssen Sie auch die `-PolicyVersion v1` Parameter bei Verwendung `-Force`. Dies erstellt eine Richtlinie auf dem Verhalten von Windows Server 2016 und erfordert, dass Sie mit `-PolicyVersion v1` beim Registrieren der codeintegritätsrichtlinie und auch die TPM-Baseline.

## <a name="create-and-apply-a-code-integrity-policy"></a>Erstellen und Anwenden einer codeintegritätsrichtlinie

Eine codeintegritätsrichtlinie trägt dazu bei, dass nur die ausführbaren Dateien, denen, die Sie vertrauen für die Ausführung auf einem Host, ausgeführt werden dürfen. Die Ausführung sind Malware und andere ausführbare Dateien außerhalb der vertrauenswürdigen ausführbarer Dateien verhindert.

Einzelnen überwachten Hosts müssen eine codeintegritätsrichtlinie angewendet, um abgeschirmte VMs im TPM-Modus ausführen. Sie geben die genaue anwendungssteuerungscode-Integritätsrichtlinien, denen, die Sie vertrauen, indem sie Host-Überwachungsdienst hinzugefügt. Anwendungssteuerungscode-Integritätsrichtlinien können konfiguriert werden, um die Richtlinie blockiert jegliche Software, die nicht mit der Richtlinie entsprechen, oder einfach prüfen (Protokoll ein Ereignis, wenn die Software nicht in der Richtlinie definierte ausgeführt wird) zu erzwingen. 

Ab Windows Server-Version 1709, sind die anwendungssteuerungscode-Integritätsrichtlinien Beispiel in Windows auf C:\Windows\schemas\CodeIntegrity\ExamplePolicies enthalten. Es werden zwei Richtlinien für Windows Server empfohlen:

- **AllowMicrosoft**: Können alle Dateien, die von Microsoft signiert. Diese Richtlinie wird empfohlen, für serveranwendungen wie SQL oder Exchange, oder wenn der Server von Agents von Microsoft veröffentlichten überwacht wird.
- **DefaultWindows_Enforced**: Ermöglicht nur die Dateien, die im Lieferumfang von Windows und gestattet keine anderen Anwendungen, die von Microsoft, wie z. B. Office veröffentlicht. Diese Richtlinie empfiehlt sich für Server, der nur integrierte Serverrollen und Features wie z. B. Hyper-V ausgeführt werden. 

Es wird empfohlen, dass Sie zuerst erstellen die codeintegritätsrichtlinie in im Überwachungsmodus (Protokollierung), um festzustellen, ob etwas fehlt, und die Richtlinie für produktionsworkloads Host erzwingt. 

Bei Verwendung der [New-CIPolicy](https://docs.microsoft.com/powershell/module/configci/new-cipolicy?view=win10-ps) Cmdlet, um Ihre eigenen generieren codeintegritätsrichtlinie an, Sie müssen entscheiden, die regelebenen verwenden. Es wird empfohlen, eine primäre Maß **Verleger** mit Fallback zu **Hash**, wodurch die meisten digital signierte Software aktualisiert werden, ohne die CI-Richtlinie zu ändern.
Neuer Software, die von demselben Herausgeber geschrieben kann auch auf dem Server installiert werden, ohne die CI-Richtlinie zu ändern.
Ausführbare Dateien, die nicht digital signiert sind werden hashcodiert – Updates für diese Dateien erfordert, dass Sie eine neue CI-Richtlinie erstellen.
Weitere Informationen zu den verfügbaren Richtlinienebenen Regel CI, finden Sie unter [bereitstellen anwendungssteuerungscode-Integritätsrichtlinien: Richtlinien und Dateiregeln](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create#windows-defender-application-control-policy-rules) und Cmdlet-Hilfe.

1.  Generieren Sie eine neue codeintegritätsrichtlinie, auf dem Host Verweis. Die folgenden Befehle erstellen eine Richtlinie auf die **Verleger** Ebene mit Fallback auf **Hash**. Klicken Sie dann konvertiert die XML-Datei in das Binärdateiformat ein, die Windows-Host-Überwachungsdienst müssen angewendet und messen die codeintegritätsrichtlinie bzw.

    ```powershell
    New-CIPolicy -Level Publisher -Fallback Hash -FilePath 'C:\temp\HW1CodeIntegrity.xml' -UserPEs

    ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\HW1CodeIntegrity.xml' -BinaryFilePath 'C:\temp\HW1CodeIntegrity.p7b'
    ```

    >[!NOTE]
    >Der obige Befehl erstellt eine CI-Richtlinie nur Überwachungsmodus aktiviert. Nicht autorisierte Binärdateien aus, die auf dem Host ausgeführt wird nicht blockiert. Sie sollten nur erzwungene Richtlinien in der Produktion verwenden.

2.  Halten Sie Ihre Code Integrity-Richtliniendatei (XML-Datei), in dem Sie diese leicht finden können. Sie benötigen zum Bearbeiten dieser Datei später, um die codeintegritätsrichtlinie oder der Merge in zukünftigen Updates, die am System vorgenommenen Änderungen zu erzwingen.

3.  Die CI-Richtlinie auf Ihrem Host Verweis anwenden:

    1.  Kopieren Sie die binäre CI-Richtliniendatei (HW1CodeIntegrity.p7b) am folgenden Speicherort auf Ihrem referenzhost (der Dateiname muss genau übereinstimmen):<br>
        **C:\\Windows\\System32\\CodeIntegrity\\SIPolicy.p7b**

    2.  Starten Sie den Host aus, um die Richtlinie anzuwenden.

3.  Testen Sie die codeintegritätsrichtlinie, durch Ausführen einer typischen arbeitsauslastung. Dazu kann beispielsweise ausgeführte virtuelle Computer, alle Fabric-Verwaltungs-Agents, die backup-Agents oder Tools auf dem Computer zur Problembehandlung. Überprüfen Sie, ob Code Integrity Verstöße und aktualisieren Sie Ihrer CI-Richtlinie bei Bedarf zu.

4.  Ändern Sie die CI-Richtlinie erzwungenen Modus, indem Sie die folgenden Befehle ausführen, für die aktualisierten XML-Datei für die CI-Richtlinie.

    ```powershell
    Set-RuleOption -FilePath 'C:\temp\HW1CodeIntegrity.xml' -Option 3 -Delete

    ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\HW1CodeIntegrity.xml' -BinaryFilePath 'C:\temp\HW1CodeIntegrity_enforced.p7b'
    ```

5.  Wenden Sie die CI-Richtlinie auf alle Hosts (mit identischer Hardware und Software-Konfiguration) mit den folgenden Befehlen:

    ```powershell
    Copy-Item -Path '<Path to HW1CodeIntegrity\_enforced.p7b>' -Destination 'C:\Windows\System32\CodeIntegrity\SIPolicy.p7b'

    Restart-Computer
    ```

    >[!NOTE]
    >Seien Sie vorsichtig beim Anwenden von CI-Richtlinien auf Hosts und beim Aktualisieren von Software auf diesen Computern. Alle Kernelmodus-Treiber, die mit der CI-Richtlinie nicht konform sind können verhindern, dass den Computer gestartet wurde. 

6.  Geben Sie die binäre Datei (in diesem Beispiel HW1CodeIntegrity\_enforced.p7b) für den HGS-Administrator.

7.  Kopieren Sie in der Domäne des Host-Überwachungsdienst die codeintegritätsrichtlinie in ein HGS-Server, und führen Sie den folgenden Befehl aus.

    Für `<PolicyName>`, geben Sie einen Namen für die CI-Richtlinie, die den Typ des Hosts beschreibt es gilt. Eine bewährte Methode ist, um den Namen nach dem Hersteller/Modell des Computers und keine spezielle Software-Konfiguration, die darauf ausgeführt.<br>Für `<Path>`, geben Sie den Pfad und Dateinamen, der die codeintegritätsrichtlinie.

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
    ```

## <a name="capture-the-tpm-baseline-for-each-unique-class-of-hardware"></a>Erfassen Sie die TPM-Baseline für jede eindeutige Gruppe von hardware

Eine TPM-Baseline ist erforderlich für jede eindeutige Hardware in Ihrem Datencenter-Fabric. Verwenden Sie einen "Verweis-Host" erneut aus. 

1. Auf dem Host Verweis sicher, dass die Hyper-V-Rolle und das Feature Hyper-V-Unterstützung für Host-Überwachungsdiensts installiert sind.

    >[!WARNING]
    >Das Feature Hyper-V-Unterstützung für Host-Überwachungsdiensts ermöglicht die Virtualisierung basierende Schutz der Integrität des Codes, die möglicherweise bei einigen Geräten nicht kompatibel sind. Es wird dringend empfohlen, diese Konfiguration in Ihrem Lab testen, bevor Sie dieses Feature aktivieren. Andernfalls kann es zu unerwarteten Fehlern und sogar zu Datenverlusten oder zu einem Bluescreen (STOP-Fehler) kommen.

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```
        
2. Wenn die Basisrichtlinie erfassen möchten, führen Sie den folgenden Befehl in einer Windows PowerShell-Konsole mit erhöhten Rechten.
        
    ```powershell
    Get-HgsAttestationBaselinePolicy -Path 'HWConfig1.tcglog'
    ```

    >[!NOTE]
    >Sie benötigen, verwenden Sie die **- SkipValidation** Flag, wenn der Verweis-Host keinen sicheren Start aktiviert, ein IOMMU vorhanden, aktivierter Virtualisierungsbasierter Sicherheit und ausgeführt wird oder eine codeintegritätsrichtlinie angewendet. Diese Überprüfungen sollen Sie die Mindestanforderungen für eine abgeschirmte VM auf dem Host ausgeführten aufmerksam zu machen. Mit dem Flag - SkipValidation ändert sich nicht auf die Ausgabe des Cmdlets aus. Es werbetour lediglich die Fehler.

3.  Geben Sie die TPM-Baseline (TCGlog-Datei) für dem HGS-Administrator.

4.  Kopieren Sie in der Domäne des Host-Überwachungsdienst die TCGlog-Datei auf einem Host-Überwachungsdienst-Server, und führen Sie den folgenden Befehl aus. In der Regel werden Sie benennen Sie die Richtlinie nach dem die Klasse der Hardware, den sie darstellt (z. B. "Hersteller-Modell-Revision").

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

## <a name="next-step"></a>Nächster Schritt

>[!div class="nextstepaction"]
[Nachweis bestätigen](guarded-fabric-confirm-hosts-can-attest-successfully.md)
