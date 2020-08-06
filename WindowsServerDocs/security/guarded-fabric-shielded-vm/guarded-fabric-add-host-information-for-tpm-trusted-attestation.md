---
title: Hinzufügen von Hostinformationen für den TPM-vertrauenswürdigen Nachweis
ms.prod: windows-server
ms.topic: article
ms.assetid: f0aa575b-b34e-4f6c-8416-ed3e398e0ad2
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 06/21/2019
ms.openlocfilehash: cfc1d0d2b99a79e6c1deb013fab350e3abc6167c
ms.sourcegitcommit: acfdb7b2ad283d74f526972b47c371de903d2a3d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87769668"
---
# <a name="add-host-information-for-tpm-trusted-attestation"></a>Hinzufügen von Hostinformationen für den TPM-vertrauenswürdigen Nachweis

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Für den TPM-Modus erfasst der Fabric-Administrator drei Arten von Hostinformationen, die jeweils der HGS-Konfiguration hinzugefügt werden müssen:

- Eine TPM-Kennung (ekpub) für jeden Hyper-V-Host
- Code Integritäts Richtlinien, eine weiße Liste zulässiger Binärdateien für die Hyper-V-Hosts
- Eine TPM-Baseline (Start Messungen), die eine Gruppe von Hyper-V-Hosts darstellt, die auf derselben Hardware Klasse ausgeführt werden

Nachdem der Fabric-Administrator die Informationen erfasst hat, fügen Sie ihn der HGS-Konfiguration hinzu, wie im folgenden Verfahren beschrieben.

1. Rufen Sie die XML-Dateien ab, die die ekpub-Informationen enthalten, und kopieren Sie Sie auf einen HGS-Server. Es wird eine XML-Datei pro Host vorhanden sein. Führen Sie dann in einer Windows PowerShell-Konsole mit erhöhten Rechten auf einem HGS-Server den folgenden Befehl aus. Wiederholen Sie den Befehl für jede der XML-Dateien.

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
    ```

    > [!NOTE]
    > Wenn beim Hinzufügen eines TPM-Bezeichners zu einem nicht vertrauenswürdigen Endorsement Key-Zertifikat (ekcert) ein Fehler auftritt, stellen Sie sicher, dass die [vertrauenswürdigen TPM](guarded-fabric-install-trusted-tpm-root-certificates.md) -Stamm Zertifikate dem HGS-Knoten hinzugefügt wurden.
    > Darüber hinaus verwenden einige TPM-Anbieter keine ekcerts.
    > Sie können überprüfen, ob ein ekcert fehlt, indem Sie die XML-Datei in einem Editor wie z. b. Editor öffnen und auf eine Fehlermeldung mit dem Hinweis, dass kein ekcert gefunden wurde, prüfen.
    > Wenn dies der Fall ist und Sie sich darauf verlassen, dass das TPM auf dem Computer authentisch ist, können Sie `-Force` diese Sicherheitsüberprüfung mit dem Flag außer Kraft setzen und die Host Kennung zu HGS hinzufügen.

2. Abrufen der Code Integritätsrichtlinie, die der Fabric-Administrator für die Hosts erstellt hat, im Binärformat ( \* . p7b). Kopieren Sie die Datei auf einen HGS-Server. Führen Sie dann den folgenden Befehl aus.

    `<PolicyName>`Geben Sie unter einen Namen für die CI-Richtlinie ein, die den Hosttyp beschreibt, auf den Sie angewendet wird. Eine bewährte Vorgehensweise besteht darin, den Namen nach dem Make/Model Ihres Computers und allen darauf laufenden speziellen Software Konfigurationen zu benennen.<br>Geben Sie für `<Path>` den Pfad und den Dateinamen der Code Integritätsrichtlinie an.

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
    ```

    > [!NOTE]
    > Wenn Sie eine Code Integritätsrichtlinie mit Vorzeichen verwenden, registrieren Sie eine nicht signierte Kopie derselben Richtlinie mit HGS.
    > Die Signatur der Code Integritäts Richtlinien wird zum Steuern der Aktualisierung der Richtlinie verwendet, jedoch nicht auf dem Host-TPM und kann daher nicht von HGS bestätigt werden.

3. Abrufen der TCG-Protokolldatei, die der Fabric-Administrator von einem Referenz Host aufgezeichnet hat. Kopieren Sie die Datei auf einen HGS-Server. Führen Sie dann den folgenden Befehl aus. In der Regel benennen Sie die Richtlinie nach der Klasse der Hardware, die Sie repräsentiert (z. b. "Hersteller Modell Revision").

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

Dadurch wird der Prozess der Konfiguration eines HGS-Clusters für den TPM-Modus abgeschlossen. Der Fabric-Administrator muss möglicherweise zwei URLs von HGS bereitstellen, bevor die Konfiguration für die Hosts abgeschlossen werden kann. Um diese URLs zu erhalten, führen Sie auf einem HGS [-Server Get-hgsserver](https://docs.microsoft.com/powershell/module/hgsserver/get-hgsserver?view=win10-ps)aus.

## <a name="next-step"></a>Nächster Schritt

> [Bestätigen des Nachweises](guarded-fabric-confirm-hosts-can-attest-successfully.md)
