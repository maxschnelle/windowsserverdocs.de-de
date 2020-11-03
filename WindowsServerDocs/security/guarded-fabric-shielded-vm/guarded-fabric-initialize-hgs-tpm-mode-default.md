---
title: Initialisieren des HGS-Clusters mit dem TPM-Modus in einer neuen dedizierten Gesamtstruktur (Standard)
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 2a89ffb238b631fc24035f2b18a57c614003c644
ms.sourcegitcommit: 8c0a419ae5483159548eb0bc159f4b774d4c3d85
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235827"
---
# <a name="initialize-the-hgs-cluster-using-tpm-mode-in-a-new-dedicated-forest-default"></a>Initialisieren des HGS-Clusters mit dem TPM-Modus in einer neuen dedizierten Gesamtstruktur (Standard)

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

1.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-one.md)]

2.  [!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

3.  Führen Sie [Initialize-hgsserver](https://docs.microsoft.com/powershell/module/hgsserver/initialize-hgsserver) in einem PowerShell-Fenster mit erhöhten Rechten auf dem ersten HGS-Knoten aus. Die Syntax dieses Cmdlets unterstützt viele verschiedene Eingaben, aber die zwei häufigsten Aufrufe sind unten aufgeführt:

    -   Wenn Sie PFX-Dateien für Ihre Signatur-und Verschlüsselungs Zertifikate verwenden, führen Sie die folgenden Befehle aus:

        ```powershell
        $signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
        $encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signingCertPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustTpm
        ```

    -   Wenn Sie nicht exportierbare Zertifikate verwenden, die im lokalen Zertifikat Speicher installiert sind, führen Sie den folgenden Befehl aus. Wenn Sie die Fingerabdrücke ihrer Zertifikate nicht kennen, können Sie die verfügbaren Zertifikate auflisten, indem Sie Ausführen `Get-ChildItem Cert:\LocalMachine\My` .

        ```powershell
        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificateThumbprint '1A2B3C4D5E6F...' -EncryptionCertificateThumbprint '0F9E8D7C6B5A...' -TrustTpm
        ```

4.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-four.md)]

5.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-five.md)]

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Installieren von TPM-Stammzertifikaten](guarded-fabric-install-trusted-tpm-root-certificates.md)
