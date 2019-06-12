---
title: Erstellen Sie einen Hostschlüssel, und fügen sie Sie Host-Überwachungsdienst hinzu
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 0526831fb0648e7f8f6fb1a081180f2e2aa9f09f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447490"
---
# <a name="create-a-host-key-and-add-it-to-hgs"></a>Erstellen Sie einen Hostschlüssel, und fügen sie Sie Host-Überwachungsdienst hinzu

>Gilt für: Windows Server 2019


In diesem Thema wird beschrieben, wie zum Vorbereiten von Hyper-V-Hosts werden von überwachten Hosts, die mit der Host den schlüsselnachweis (Schlüssel-Modus) werden. Sie müssen ein paar Host erstellen (oder ein vorhandenes Zertifikat verwenden) und Host-Überwachungsdienst, der öffentliche Teil des Schlüssels hinzu.

## <a name="create-a-host-key"></a>Erstellen Sie einen Hostschlüssel

1.  Installieren Sie Windows Server-2019 auf dem Hyper-V-Hostcomputer an.
2.  Installieren Sie die Hyper-V und Hyper-V-Unterstützung für Host-Überwachungsdiensts Funktionen:

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ``` 

3.  Generieren Sie einen Hostschlüssel automatisch, oder wählen Sie ein vorhandenes Zertifikat. Wenn Sie ein benutzerdefiniertes Zertifikat verwenden, müssen sie mindestens einen 2048-Bit-RSA-Schlüssel, die Clientauthentifizierungs-EKU und die Schlüsselverwendung digitale Signatur.

    ```powershell
    Set-HgsClientHostKey
    ```

    Alternativ können Sie einen Fingerabdruck angeben, wenn Sie Ihr eigenes Zertifikat verwenden möchten. 
    Dies kann nützlich sein, wenn ein Zertifikat auf mehreren Computern freigeben, oder verwenden ein Zertifikat an einem TPM noch ein HSM gebunden werden soll. Hier ist ein Beispiel zum Erstellen eines TPM-Bound-Zertifikats (der verhindert, dass der private Schlüssel gestohlen und auf einem anderen Computer verwendet und erfordert nur ein TPM 1.2):

    ```powershell
    $tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
    Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
    ```

4.  Abrufen der öffentliche Hälfte des Schlüssels, der für den HGS-Server bereitstellen. Sie können das folgende Cmdlet verwenden oder das Zertifikat, das an anderer Stelle gespeicherten enthält finden Sie eine .cer-Datei mit den öffentlichen Teil des Schlüssels. Beachten Sie, dass wir nur das Speichern und überprüfen den öffentlichen Schlüssel auf dem Host-Überwachungsdienst. Wir behalten keine Zertifikatinformationen hinzuzufügen, und überprüfen wir das Datum Kette oder Ablauf des Zertifikats.

    ```powershell
    Get-HgsClientHostKey -Path "C:\temp\$env:hostname-HostKey.cer"
    ```

5.  Kopieren Sie die CER-Datei auf Ihren Host-Überwachungsdienst-Server.

## <a name="add-the-host-key-to-the-attestation-service"></a>Fügen Sie den Hostschlüssel mit dem Attestation-Dienst

Dieser Schritt erfolgt auf dem Host-Überwachungsdienst-Server und ermöglicht es dem Host zum Ausführen geschützter VMs. Es wird empfohlen, dass Sie legen Sie den Namen auf den vollqualifizierten Domänennamen oder Ressourcenbezeichner des Hostcomputers, sodass Sie problemlos auf welchem Host den Schlüssel verweisen können, die auf installiert ist.

```powershell
Add-HgsAttestationHostKey -Name MyHost01 -Path "C:\temp\MyHost01-HostKey.cer"
``` 

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Bestätigen Sie, dass die Hosts nachweisen können, erfolgreich](guarded-fabric-confirm-hosts-can-attest-successfully.md)

## <a name="see-also"></a>Siehe auch

- [Bereitstellen von Host-Überwachungsdienst für überwachte Hosts und abgeschirmten VMs](guarded-fabric-deploying-hgs-overview.md)
