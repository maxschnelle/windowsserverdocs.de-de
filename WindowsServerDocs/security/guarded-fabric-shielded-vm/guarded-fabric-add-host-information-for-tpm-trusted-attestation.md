---
title: Fügen Sie die Hostinformationen für den TPM-vertrauenswürdiger Nachweis
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: f0aa575b-b34e-4f6c-8416-ed3e398e0ad2
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 06/21/2019
ms.openlocfilehash: 99be11bfec02924f93d9f759676e1eea364daa18
ms.sourcegitcommit: 545dcfc23a81943e129565d0ad188263092d85f6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2019
ms.locfileid: "67407639"
---
>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

### <a name="add-host-information-for-tpm-trusted-attestation"></a>Fügen Sie die Hostinformationen für den TPM-vertrauenswürdiger Nachweis

Für den TPM-Modus, der fabricadministrator drei Arten von Hostinformationen erfasst jede muss der Host-Überwachungsdienst-Konfiguration hinzugefügt werden:

- Ein TPM-Bezeichner (EKpub) für jeden Hyper-V-host
- Anwendungssteuerungscode-Integritätsrichtlinien, eine Positivliste der zulässigen Binärdateien für die Hyper-V-hosts
- Eine TPM-Baseline (startmessungen), die einen Satz von Hyper-V darstellt hostet, für die gleiche Klasse der Hardware ausgeführt werden.

Nach dem Fabric-Administrator erfasst die Informationen, wie im folgenden Verfahren beschrieben, die Host-Überwachungsdienst-Konfiguration hinzufügen.

1. Rufen Sie die XML-Dateien, die die EKpub-Informationen enthalten, und kopieren Sie sie an einen Host-Überwachungsdienst-Server. Es wird eine XML-Datei für den Host vorhanden sein. Klicken Sie dann in einer Windows PowerShell-Konsole mit erhöhten Rechten auf einem Host-Überwachungsdienst-Server, führen Sie den folgenden Befehl aus. Wiederholen Sie den Befehl für jede XML-Dateien.

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
    ```

    > [!NOTE]
    > Wenn Sie ein Fehler auftritt, wenn Sie eine TPM-ID in Bezug auf ein nicht vertrauenswürdiges Endorsement Key-Zertifikat (EKCert) hinzufügen, stellen Sie sicher, dass die [vertrauenswürdige Stammzertifikate TPM wurden hinzugefügt,](guarded-fabric-install-trusted-tpm-root-certificates.md) auf den Host-Überwachungsdienst-Knoten.
    > Darüber hinaus verwenden einige TPM-Hersteller EKCerts nicht.
    > Sie können überprüfen, ob ein EKCert nicht vorhanden, ist durch die XML-Datei in einem Editor wie Editor öffnen und eine Fehlermeldung, die keine EKCert gesucht wurde gefunden.
    > Wenn dies der Fall ist, und Sie vertrauen, dass das TPM auf Ihrem Computer authentifiziert ist, können Sie die `-Force` Flag, um diese sicherheitsprüfung zu überschreiben und Host-Überwachungsdienst die Host-ID hinzugefügt.

2. Die codeintegritätsrichtlinie, die Fabric-Administrator erstellt für die Hosts, im Binärformat zu erhalten (\*p7b). Kopieren sie auf einem Host-Überwachungsdienst-Server. Führen Sie dann den folgenden Befehl aus.

    Für `<PolicyName>`, geben Sie einen Namen für die CI-Richtlinie, die den Typ des Hosts beschreibt es gilt. Eine bewährte Methode ist, um den Namen nach dem Hersteller/Modell des Computers und keine spezielle Software-Konfiguration, die darauf ausgeführt.<br>Für `<Path>`, geben Sie den Pfad und Dateinamen, der die codeintegritätsrichtlinie.

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
    ```
    
    > [!NOTE]
    > Bei Verwendung eine signierten codeintegritätsrichtlinie, registrieren Sie eine nicht signierte Kopie derselben Richtlinie mit Host-Überwachungsdienst.
    > Die Signatur anwendungssteuerungscode-Integritätsrichtlinien wird verwendet, um Updates für die Richtlinie zu steuern, aber nicht mit dem Host TPM gemessen wird und kann nicht aus diesem Grund von Host-Überwachungsdienst auf nachgewiesen werden.

3. Rufen Sie die TCGlog-Datei, die der fabricadministrator erfasst, von einem Host Verweis. Kopieren Sie die Datei auf einem Host-Überwachungsdienst-Server. Führen Sie dann den folgenden Befehl aus. In der Regel werden Sie benennen Sie die Richtlinie nach dem die Klasse der Hardware, den sie darstellt (z. B. "Hersteller-Modell-Revision").

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

Dies schließt den Prozess der Konfiguration eines Host-Überwachungsdienst-Clusters für den TPM-Modus. Der Fabric-Administrator möglicherweise zwei URLs von Host-Überwachungsdienst bereitstellen, bevor die Konfiguration für die Hosts abgeschlossen werden kann. Um diese URLs, auf einem Host-Überwachungsdienst-Server erhalten, führen [Get-HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/get-hgsserver?view=win10-ps).

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Bestätigen des Nachweises](guarded-fabric-confirm-hosts-can-attest-successfully.md)
