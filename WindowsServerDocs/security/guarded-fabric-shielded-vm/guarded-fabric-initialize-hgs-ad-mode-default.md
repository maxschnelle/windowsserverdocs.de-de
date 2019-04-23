---
title: Initialisieren Sie den Host-Überwachungsdienst-Cluster mithilfe von AD-Modus in einer neuen dedizierten Gesamtstruktur (Standard)
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 4ef70ab9ce8150a9a3ed774d6df407da097880e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865671"
---
# <a name="initialize-the-hgs-cluster-using-ad-mode-in-a-new-dedicated-forest-default"></a>Initialisieren Sie den Host-Überwachungsdienst-Cluster mithilfe von AD-Modus in einer neuen dedizierten Gesamtstruktur (Standard)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

>[!IMPORTANT]
>Admin-vertrauenswürdiger Nachweis (Active Directory-Modus) ist veraltet, beginnend mit Windows Server-2019. Konfigurieren Sie für Umgebungen, in denen ist TPM-Nachweis nicht möglich, [hosten den schlüsselnachweis](guarded-fabric-initialize-hgs-key-mode-default.md). Host den schlüsselnachweis bietet eine ähnliche Garantie in den Active Directory-Modus, und es ist leichter einzurichten. 

1.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-one.md)] 
2.  [!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

3.  Führen Sie [Initialize-HgsServer](https://technet.microsoft.com/library/mt652185.aspx) in einer mit erhöhten Rechten PowerShell-Fenster auf dem ersten Knoten für den Host-Überwachungsdienst. Die Syntax des Cmdlets unterstützt viele verschiedene Eingaben, aber die 2 am häufigsten verwendeten Aufrufe sind unten aufgeführt:

    -   Wenn Sie PFX-Dateien für Ihre Zertifikate für Signierung und Verschlüsselung verwenden, führen Sie die folgenden Befehle aus:

        ```powershell
        $signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
        $encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signingCertPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustActiveDirectory
        ```

    -   Wenn Sie nicht exportierbare Zertifikate verwenden, die im lokalen Zertifikatspeicher installiert sind, führen Sie den folgenden Befehl aus. Wenn Sie nicht, dass die Fingerabdrücke der Zertifikate wissen, können Sie Verfügbare Zertifikate auflisten, mit `Get-ChildItem Cert:\LocalMachine\My`.

        ```powershell
        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificateThumbprint '1A2B3C4D5E6F...' -EncryptionCertificateThumbprint '0F9E8D7C6B5A...' --TrustActiveDirectory
        ```

4.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-four.md)]  

5.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-five.md)]

## <a name="next-step"></a>Nächster Schritt

>[!div class="nextstepaction"]
[Konfigurieren Sie DNS-fabric](guarded-fabric-configuring-fabric-dns-ad.md)