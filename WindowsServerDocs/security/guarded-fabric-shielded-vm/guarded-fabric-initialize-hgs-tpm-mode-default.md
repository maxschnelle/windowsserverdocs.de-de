---
title: Initialisieren Sie den Host-Überwachungsdienst-Cluster mithilfe von TPM-Modus in einer neuen dedizierten Gesamtstruktur (Standard)
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: f2fb970cdc215df06dd9dee2e20b5466d7e42dcb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447409"
---
# <a name="initialize-the-hgs-cluster-using-tpm-mode-in-a-new-dedicated-forest-default"></a>Initialisieren Sie den Host-Überwachungsdienst-Cluster mithilfe von TPM-Modus in einer neuen dedizierten Gesamtstruktur (Standard)

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

1.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-one.md)]

2.  [!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

3.  Führen Sie [Initialize-HgsServer](https://technet.microsoft.com/library/mt652185.aspx) in einer mit erhöhten Rechten PowerShell-Fenster auf dem ersten Knoten für den Host-Überwachungsdienst. Die Syntax des Cmdlets unterstützt viele verschiedene Eingaben, aber die 2 am häufigsten verwendeten Aufrufe sind unten aufgeführt:

    -   Wenn Sie PFX-Dateien für Ihre Zertifikate für Signierung und Verschlüsselung verwenden, führen Sie die folgenden Befehle aus:

        ```powershell
        $signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
        $encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signingCertPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustTpm
        ```

    -   Wenn Sie nicht exportierbare Zertifikate verwenden, die im lokalen Zertifikatspeicher installiert sind, führen Sie den folgenden Befehl aus. Wenn Sie nicht, dass die Fingerabdrücke der Zertifikate wissen, können Sie Verfügbare Zertifikate auflisten, mit `Get-ChildItem Cert:\LocalMachine\My`.

        ```powershell
        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificateThumbprint '1A2B3C4D5E6F...' -EncryptionCertificateThumbprint '0F9E8D7C6B5A...' -TrustTpm
        ```

4.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-four.md)]

5.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-five.md)]

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Installieren von TPM-Stammzertifikaten](guarded-fabric-install-trusted-tpm-root-certificates.md)
  