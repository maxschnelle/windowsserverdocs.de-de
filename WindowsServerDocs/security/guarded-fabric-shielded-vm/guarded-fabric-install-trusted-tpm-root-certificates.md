---
title: Installieren Sie vertrauenswürdige TPM-Stamm Zertifikate.
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 06/27/2019
ms.openlocfilehash: 04beb3f517df090393690a871a12015cf0bed163
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971317"
---
# <a name="install-trusted-tpm-root-certificates"></a>Installieren Sie vertrauenswürdige TPM-Stamm Zertifikate.

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Wenn Sie HGS für die Verwendung des TPM-Attestation konfigurieren, müssen Sie auch HGS so konfigurieren, dass Sie den Anbietern der TPMs auf Ihren Servern vertrauen.
Durch diesen zusätzlichen Überprüfungsprozess wird sichergestellt, dass nur echte vertrauenswürdige TPMs ihre HGS überzeugen können.
Wenn Sie versuchen, ein nicht vertrauenswürdiges TPM bei zu registrieren `Add-HgsAttestationTpmHost` , erhalten Sie eine Fehlermeldung, die darauf hinweist, dass der TPM-Anbieter nicht vertrauenswürdig ist.

Um den TPMs zu vertrauen, müssen die Stamm-und zwischen Signatur Zertifikate, die zum Signieren des Endorsement Key in den TPMs Ihres Servers verwendet werden, auf HGS installiert werden.
Wenn Sie in Ihrem Daten Center mehr als ein TPM-Modell verwenden, müssen Sie möglicherweise verschiedene Zertifikate für jedes Modell installieren.
HGS sehen sich die Zertifikat Speicher "TrustedTPM_RootCA" und "TrustedTPM_IntermediateCA" für die herstellerzertifikate an.

> [!NOTE]
> Die TPM-herstellerzertifikate unterscheiden sich von den standardmäßig in Windows installierten Stamm-und zwischen Zertifikaten, die von TPM-Anbietern verwendet werden.

Eine Sammlung vertrauenswürdiger TPM-Stamm-und zwischen Zertifikate wird von Microsoft zur einfacheren Veröffentlichung veröffentlicht.
Mithilfe der nachfolgenden Schritte können Sie diese Zertifikate installieren.
Wenn Ihre TPM-Zertifikate nicht im folgenden Paket enthalten sind, wenden Sie sich an den TPM-Hersteller oder den OEM-Server, um die Stamm-und zwischen Zertifikate für ihr bestimmtes TPM-Modell zu erhalten.

Wiederholen Sie die folgenden Schritte auf **jedem HGS-Server**:

1.  Laden Sie das neueste Paket aus herunter [https://go.microsoft.com/fwlink/?linkid=2097925](https://go.microsoft.com/fwlink/?linkid=2097925) .

2.  Überprüfen Sie die Signatur der CAB-Datei, um ihre Echtheit sicherzustellen. Fahren Sie nicht fort, wenn die Signatur ungültig ist.

    ```powershell
    Get-AuthenticodeSignature .\TrustedTpm.cab
    ```

    Hier ist eine Beispielausgabe angegeben:

    ```
    Directory: C:\Users\Administrator\Downloads

    SignerCertificate                         Status                                 Path
    -----------------                         ------                                 ----
    0DD6D4D4F46C0C7C2671962C4D361D607E370940  Valid                                  TrustedTpm.cab
    ```

2.  Erweitern Sie die CAB-Datei.

    ```
    mkdir .\TrustedTPM
    expand.exe -F:* <Path-To-TrustedTpm.cab> .\TrustedTPM
    ```

3.  Standardmäßig installiert das Konfigurationsskript Zertifikate für jeden TPM-Anbieter. Wenn Sie nur Zertifikate für Ihren spezifischen TPM-Hersteller importieren möchten, löschen Sie die Ordner für TPM-Anbieter, die von Ihrer Organisation nicht als vertrauenswürdig eingestuft werden.

4.  Installieren Sie das vertrauenswürdige Zertifikat Paket durch Ausführen des Setup Skripts im erweiterten Ordner.

    ```
    cd .\TrustedTPM
    .\setup.cmd
    ```

Wenn Sie neue Zertifikate hinzufügen oder diese bei einer früheren Installation absichtlich übersprungen haben, wiederholen Sie einfach die oben beschriebenen Schritte auf jedem Knoten in Ihrem HGS-Cluster.
Vorhandene Zertifikate bleiben vertrauenswürdig, aber der vertrauenswürdigen TPM-Speicher werden neue Zertifikate in der erweiterten CAB-Datei hinzugefügt.

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Konfigurieren des Fabric-DNS](guarded-fabric-configuring-fabric-dns-tpm.md)



