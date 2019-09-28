---
title: Erfassen der von HGS benötigten Informationen zum TPM-Modus
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 915b1338-5085-481b-8904-75d29e609e93
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 04/01/2019
ms.openlocfilehash: ba67cb80a405cd1c6d368a52798e3dec4d9861cb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403513"
---
# <a name="authorize-guarded-hosts-using-tpm-based-attestation"></a>Autorisieren von überwachten Hosts mithilfe von TPM-basiertem Nachweis

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Der TPM-Modus verwendet einen TPM-Bezeichner (auch als Platt Form Bezeichner oder Endorsement Key \[ekpub @ no__t-1 bezeichnet), um zu bestimmen, ob ein bestimmter Host als "geschützt" autorisiert ist. Bei diesem Nachweis werden sichere Start-und Code Integritäts Messungen verwendet, um sicherzustellen, dass sich ein bestimmter Hyper-V-Host in einem fehlerfreien Zustand befindet und nur vertrauenswürdiger Code ausgeführt wird. Damit der Nachweis weiß, was nicht fehlerfrei ist, müssen Sie die folgenden Artefakte erfassen:

1.  TPM-Bezeichner (ekpub)

    -  Diese Informationen sind für jeden Hyper-V-Host eindeutig.

2.  TPM-Baseline (Start Messungen)

    -  Dies gilt für alle Hyper-V-Hosts, die auf derselben Hardware Klasse ausgeführt werden.

3.  Code Integritätsrichtlinie (eine Whitelist zulässiger Binärdateien)

    -  Dies gilt für alle Hyper-V-Hosts, die gemeinsame Hardware und Software gemeinsam verwenden.

Es wird empfohlen, die Baseline-und CI-Richtlinie von einem "Verweis Host" zu erfassen, der für jede eindeutige Klasse der Hyper-V-Hardwarekonfiguration innerhalb Ihres Rechenzentrums repräsentativ ist. Ab Windows Server, Version 1709, sind die CI-Beispiel Richtlinien unter c:\windows\schemas\codeintegrity\examplepoliciesenthalten. 

## <a name="versioned-attestation-policies"></a>Nachweis Richtlinien mit Versions Angabe

In Windows Server 2019 wird eine neue Methode für den Nachweis namens " *v2*-Nachweis" eingeführt, in der ein TPM-Zertifikat vorhanden sein muss, um die ekpub-Datei zu HGS hinzuzufügen. Mit der in Windows Server 2016 verwendeten v1-Nachweismethode konnten Sie diese Sicherheitsüberprüfung außer Kraft setzen, indem Sie das Flag "-Force" angeben, wenn Sie "Add-hgsattestationtpmhost" oder andere TPM-Nachweis-Cmdlets ausführen, um die Artefakte zu erfassen. Ab Windows Server 2019 wird der V2-Nachweis standardmäßig verwendet, und Sie müssen das Flag "-PolicyVersion v1" angeben, wenn Sie "Add-hgsattestationtpmhost" ausführen müssen, wenn Sie ein TPM ohne Zertifikat registrieren müssen. Das Flag-Force funktioniert nicht mit dem V2-Nachweis. 

Ein Host kann nur überzeugen, ob für alle Artefakte (ekpub + TPM-Baseline und CI-Richtlinie) dieselbe Version des Nachweis verwendet wird. Der V2-Nachweis wird zuerst ausprobiert, und wenn dies nicht möglich ist, wird der v1-Nachweis verwendet. Dies bedeutet Folgendes: Wenn Sie eine TPM-ID mithilfe des v1-Nachweis registrieren müssen, müssen Sie auch das Flag "-PolicyVersion v1" angeben, um den v1-Nachweis zu verwenden, wenn Sie die TPM-Baseline erfassen und die CI-Richtlinie erstellen. Wenn die TPM-Baseline und die CI-Richtlinie mit dem V2-Nachweis erstellt wurden und Sie später einen überwachten Host ohne TPM-Zertifikat hinzufügen müssen, müssen Sie jedes artefaktelement mit dem Flag "-PolicyVersion v1" neu erstellen. 

## <a name="capture-the-tpm-identifier-platform-identifier-or-ekpub-for-each-host"></a>Erfassen Sie den TPM-Bezeichner (Platt Form Bezeichner oder ekpub) für jeden Host.

1.  Stellen Sie in der Fabric-Domäne sicher, dass das TPM auf den einzelnen Hosts zur Verwendung bereit ist, d. h., das TPM ist initialisiert, und der Besitz wurde abgerufen. Sie können den Status des TPM überprüfen, indem Sie die TPM-Verwaltungskonsole (TPM. msc) öffnen oder **Get-TPM** in einem Windows PowerShell-Fenster mit erhöhten Rechten ausführen. Wenn das TPM nicht den Status **bereit** aufweist, müssen Sie es initialisieren und dessen Besitz festlegen. Dies kann in der TPM-Verwaltungskonsole oder durch Ausführen von **Initialize-TPM**erfolgen.

2.  Führen Sie auf jedem überwachten Host den folgenden Befehl in einer Windows PowerShell-Konsole mit erhöhten Rechten aus, um die ekpub-Datei abzurufen. Ersetzen Sie für `<HostName>` den eindeutigen Hostnamen durch einen geeigneten Hostnamen, der zum Identifizieren dieses Hosts geeignet ist. dabei kann es sich um den Hostnamen oder den von einem Fabric-Inventur Dienst (falls verfügbar) verwendeten Namen handeln. Benennen Sie die Ausgabedatei unter Verwendung des Host namens.

    ```powershell
    (Get-PlatformIdentifier -Name '<HostName>').InnerXml | Out-file <Path><HostName>.xml -Encoding UTF8
    ```
3.  Wiederholen Sie die vorherigen Schritte für jeden Host, der zu einem überwachten Host werden soll, und stellen Sie sicher, dass jede XML-Datei einen eindeutigen Namen erhält

4.  Stellen Sie die resultierenden XML-Dateien für den HGS-Administrator bereit.

5.  Öffnen Sie in der HGS-Domäne eine Windows PowerShell-Konsole mit erhöhten Rechten auf einem HGS-Server, und führen Sie den folgenden Befehl aus. Wiederholen Sie den Befehl für jede der XML-Dateien.

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
    ```

    > [!NOTE]
    > Wenn beim Hinzufügen eines TPM-Bezeichners zu einem nicht vertrauenswürdigen Endorsement Key-Zertifikat (ekcert) ein Fehler auftritt, stellen Sie sicher, dass die [vertrauenswürdigen TPM](guarded-fabric-install-trusted-tpm-root-certificates.md) -Stamm Zertifikate dem HGS-Knoten hinzugefügt wurden.
    > Darüber hinaus verwenden einige TPM-Anbieter keine ekcerts.
    > Sie können überprüfen, ob ein ekcert fehlt, indem Sie die XML-Datei in einem Editor wie z. b. Editor öffnen und auf eine Fehlermeldung mit dem Hinweis, dass kein ekcert gefunden wurde, prüfen.
    > Wenn dies der Fall ist und Sie sich darauf verlassen, dass das TPM auf dem Computer authentisch ist, können Sie den `-Force`-Parameter verwenden, um den Host Bezeichner zu HGS hinzuzufügen. In Windows Server 2019 müssen Sie auch den `-PolicyVersion v1`-Parameter verwenden, wenn Sie `-Force` verwenden. Dadurch wird eine Richtlinie erstellt, die dem Verhalten von Windows Server 2016 entspricht, und Sie müssen beim Registrieren der CI-Richtlinie und der TPM-Baseline auch `-PolicyVersion v1` verwenden.

## <a name="create-and-apply-a-code-integrity-policy"></a>Erstellen und Anwenden einer Code Integritätsrichtlinie

Mit einer Code Integritätsrichtlinie kann sichergestellt werden, dass nur die ausführbaren Dateien, denen Sie Vertrauen, auf einem Host ausgeführt werden dürfen, ausgeführt werden dürfen. Schadsoftware und andere ausführbare Dateien außerhalb der vertrauenswürdigen ausführbaren Dateien können nicht ausgeführt werden.

Für jeden überwachten Host muss eine Code Integritätsrichtlinie angewendet werden, damit abgeschirmte VMS im TPM-Modus ausgeführt werden können. Sie geben die exakten Code Integritäts Richtlinien an, denen Sie Vertrauen, indem Sie Sie zu HGS hinzufügen. Code Integritäts Richtlinien können konfiguriert werden, um die Richtlinie zu erzwingen, jegliche Software zu blockieren, die die Richtlinie nicht einhält, oder einfach ein Ereignis zu überwachen (protokollieren, wenn Software, die nicht in der Richtlinie definiert ist). 

Ab Windows Server, Version 1709, sind Beispielcode Integritäts Richtlinien in Windows unter c:\windows\schemas\codeintegrity\examplepoliciesenthalten. Für Windows Server werden zwei Richtlinien empfohlen:

- **Allowmicrosoft**: Ermöglicht alle Dateien, die von Microsoft signiert wurden. Diese Richtlinie wird für Server Anwendungen, z. b. SQL oder Exchange, empfohlen, oder wenn der Server von Agents überwacht wird, die von Microsoft veröffentlicht wurden.
- **DefaultWindows_Enforced**: Ermöglicht nur Dateien, die in Windows enthalten sind und keine anderen von Microsoft veröffentlichten Anwendungen, wie z. b. Office, zulässt. Diese Richtlinie wird für Server empfohlen, auf denen nur integrierte Server Rollen und Features wie z. b. Hyper-V ausgeführt werden. 

Es wird empfohlen, zuerst die CI-Richtlinie im Überwachungsmodus (Protokollierungs Modus) zu erstellen, um festzustellen, ob Sie etwas hat, und dann die Richtlinie für Host produktionsworkloads zu erzwingen. 

Wenn Sie das Cmdlet " [New-cipolicy](https://docs.microsoft.com/powershell/module/configci/new-cipolicy?view=win10-ps) " verwenden, um eine eigene Code Integritätsrichtlinie zu generieren, müssen Sie die zu verwendenden Regel Ebenen festlegen. Wir empfehlen eine primäre Ebene des **Verlegers** mit Fall Back auf **Hash**, sodass die meisten digital signierten Software aktualisiert werden kann, ohne die CI-Richtlinie zu ändern.
Neue Software, die vom selben Verleger geschrieben wird, kann auch auf dem Server installiert werden, ohne dass die CI-Richtlinie geändert wird.
Ausführbare Dateien, die nicht digital signiert sind, werden Hashwerte aufweisen: bei Updates für diese Dateien müssen Sie eine neue CI-Richtlinie erstellen.
Weitere Informationen zu den verfügbaren CI-Richtlinien Regel Ebenen finden Sie unter Bereitstellen von [Code Integritäts Richtlinien: Richtlinien Regeln und Datei Regeln](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create#windows-defender-application-control-policy-rules) und Cmdlet-Hilfe.

1.  Generieren Sie auf dem Referenz Host eine neue Code Integritätsrichtlinie. Die folgenden Befehle erstellen eine Richtlinie auf **Verleger** Ebene mit Fall Back auf **Hash**. Anschließend wird die XML-Datei in das Binärdatei Format konvertiert, und HGS müssen die CI-Richtlinie anwenden bzw. messen.

    ```powershell
    New-CIPolicy -Level Publisher -Fallback Hash -FilePath 'C:\temp\HW1CodeIntegrity.xml' -UserPEs

    ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\HW1CodeIntegrity.xml' -BinaryFilePath 'C:\temp\HW1CodeIntegrity.p7b'
    ```

    >[!NOTE]
    >Der obige Befehl erstellt eine CI-Richtlinie nur im Überwachungsmodus. Nicht autorisierte Binärdateien können nicht auf dem Host ausgeführt werden. Sie sollten nur erzwungene Richtlinien in der Produktionsumgebung verwenden.

2.  Behalten Sie die Datei mit der Code Integritätsrichtlinie (XML-Datei) bei, wo Sie Sie leicht finden können. Sie müssen diese Datei zu einem späteren Zeitpunkt bearbeiten, um die CI-Richtlinie zu erzwingen oder Änderungen von zukünftigen Updates, die im System vorgenommen wurden, zusammenzuführen.

3.  Anwenden der CI-Richtlinie auf den Verweis Host:

    1.  Führen Sie den folgenden Befehl aus, um den Computer zur Verwendung Ihrer CI-Richtlinie zu konfigurieren. Sie können die CI-Richtlinie auch mit [Gruppenrichtlinie](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-windows-defender-application-control-policies-using-group-policy) oder [System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/guarded-deploy-host?view=sc-vmm-2019#manage-and-deploy-code-integrity-policies-with-vmm)bereitstellen.

        ```powershell
        Invoke-CimMethod -Namespace root/Microsoft/Windows/CI -ClassName PS_UpdateAndCompareCIPolicy -MethodName Update -Arguments @{ FilePath = "C:\temp\HW1CodeIntegrity.p7b" }
        ```

    2.  Starten Sie den Host neu, um die Richtlinie anzuwenden.

3.  Testen Sie die Code Integritätsrichtlinie, indem Sie eine typische Arbeitsauslastung ausführen. Hierzu zählen u. a. die Ausführung von VMS, fabricverwaltungs-Agents, Sicherungs-Agents oder Tools zur Problembehandlung auf dem Computer. Überprüfen Sie, ob Code Integritäts Verletzungen vorliegen, und aktualisieren Sie ggf. die CI-Richtlinie.

4.  Ändern Sie die CI-Richtlinie in den erzwungenen Modus, indem Sie die folgenden Befehle für die aktualisierte CI-Richtlinien-XML-Datei ausführen

    ```powershell
    Set-RuleOption -FilePath 'C:\temp\HW1CodeIntegrity.xml' -Option 3 -Delete

    ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\HW1CodeIntegrity.xml' -BinaryFilePath 'C:\temp\HW1CodeIntegrity_enforced.p7b'
    ```

5.  Wenden Sie die CI-Richtlinie auf alle Ihre Hosts (mit identischer Hardware-und Softwarekonfiguration) mithilfe der folgenden Befehle an:

    ```powershell
    Invoke-CimMethod -Namespace root/Microsoft/Windows/CI -ClassName PS_UpdateAndCompareCIPolicy -MethodName Update -Arguments @{ FilePath = "C:\temp\HW1CodeIntegrity.p7b" }
    
    Restart-Computer
    ```

    >[!NOTE]
    >Seien Sie vorsichtig, wenn Sie CI-Richtlinien auf Hosts anwenden und Software auf diesen Computern aktualisieren. Alle Kernelmodustreiber, die nicht mit der CI-Richtlinie kompatibel sind, können verhindern, dass der Computer gestartet wird. 

6.  Stellen Sie die Binärdatei (in diesem Beispiel HW1CodeIntegrity @ no__t-0enforced. p7b) dem HGS-Administrator bereit.

7.  Kopieren Sie in der HGS-Domäne die Code Integritätsrichtlinie auf einen HGS-Server, und führen Sie den folgenden Befehl aus.

    Geben Sie für `<PolicyName>` einen Namen für die CI-Richtlinie ein, die den Hosttyp beschreibt, auf den Sie angewendet wird. Eine bewährte Vorgehensweise besteht darin, den Namen nach dem Make/Model Ihres Computers und allen darauf laufenden speziellen Software Konfigurationen zu benennen.<br>Geben Sie für `<Path>` den Pfad und den Dateinamen der Code Integritätsrichtlinie an.

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
    ```

## <a name="capture-the-tpm-baseline-for-each-unique-class-of-hardware"></a>Erfassen der TPM-Baseline für jede eindeutige Hardware Klasse

Eine TPM-Baseline ist für jede eindeutige Hardware Klasse in Ihrer Rechenzentrums Struktur erforderlich. Verwenden Sie erneut einen "Verweis Host". 

1. Stellen Sie auf dem Referenz Host sicher, dass die Hyper-v-Rolle und die Hyper-v-Unterstützung des Host-Überwachungs Diensts installiert sind.

    >[!WARNING]
    >Die Hyper-V-Unterstützung des Host-Überwachungs Diensts ermöglicht den virtualisierungsbasierten Schutz der Code Integrität, der möglicherweise mit einigen Geräten nicht kompatibel ist. Wir empfehlen dringend, diese Konfiguration in Ihrem Lab zu testen, bevor Sie diese Funktion aktivieren. Andernfalls kann es zu unerwarteten Fehlern und sogar zu Datenverlusten oder zu einem Bluescreen (STOP-Fehler) kommen.

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```
        
2. Führen Sie den folgenden Befehl in einer Windows PowerShell-Konsole mit erhöhten Rechten aus, um die Baseline-Richtlinie aufzuzeichnen.
        
    ```powershell
    Get-HgsAttestationBaselinePolicy -Path 'HWConfig1.tcglog'
    ```

    >[!NOTE]
    >Sie müssen das Flag " **-skipvalidation** " verwenden, wenn auf dem Referenz Host kein sicherer Start aktiviert ist, ein IOMMU vorhanden ist, die virtualisierungsbasierte Sicherheit aktiviert ist und ausgeführt wird, oder eine Code Integritätsrichtlinie angewendet wird. Diese Überprüfungen sind so konzipiert, dass Sie die Mindestanforderungen für das Ausführen einer abgeschirmten VM auf dem Host kennen. Wenn Sie das Flag "-skipvalidation" verwenden, wird die Ausgabe des Cmdlets nicht geändert. die Fehler werden lediglich mit einem Fehler verursacht.

3.  Stellen Sie die TPM-Baseline (tcglog-Datei) für den HGS-Administrator bereit.

4.  Kopieren Sie in der HGS-Domäne die Datei tcglog auf einen HGS-Server, und führen Sie den folgenden Befehl aus. In der Regel benennen Sie die Richtlinie nach der Klasse der Hardware, die Sie repräsentiert (z. b. "Hersteller Modell Revision").

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Bestätigen des Nachweises](guarded-fabric-confirm-hosts-can-attest-successfully.md)
