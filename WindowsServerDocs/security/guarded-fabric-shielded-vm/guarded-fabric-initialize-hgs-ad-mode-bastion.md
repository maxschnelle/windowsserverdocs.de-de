---
title: Initialisieren Sie den Host-Überwachungsdienst-Cluster mithilfe von AD-Modus in einer geschützten Gesamtstruktur
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 98003745823cf780a38487dff997798ebef12fc9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870091"
---
# <a name="initialize-the-hgs-cluster-using-ad-mode-in-an-existing-bastion-forest"></a>Initialisieren Sie den Host-Überwachungsdienst-Cluster mithilfe von AD-Modus in einer vorhandenen geschützten Gesamtstruktur

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016


>[!IMPORTANT]
>Admin-vertrauenswürdiger Nachweis (Active Directory-Modus) ist veraltet, beginnend mit Windows Server-2019. Konfigurieren Sie für Umgebungen, in denen ist TPM-Nachweis nicht möglich, [hosten den schlüsselnachweis](guarded-fabric-initialize-hgs-key-mode-bastion.md). Host den schlüsselnachweis bietet eine ähnliche Garantie in den Active Directory-Modus, und es ist leichter einzurichten. 

Active Directory Domain Services auf dem Computer installiert werden, aber nicht konfigurierte bleiben sollen.

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)] 

Bevor Sie fortfahren, stellen Sie sicher, dass Sie vorab Ihre Clusterobjekte für die Host-Überwachungsdienst bereitgestellten und dem angemeldeten Benutzer erteilt **Vollzugriff** über die Objekte VCO und CNO in Active Directory.
Den Namen des virtuellen Computers-Objekt übergeben werden muss die `-HgsServiceName` Parameter und den Namen des Clusters, um die `-ClusterName` Parameter.

> [!TIP]
> Überprüfen Sie haben Ihre Active Directory-Domänencontroller, um sicherzustellen, dass die Clusterobjekte auf allen Domänencontrollern vor dem Fortfahren repliziert werden.

Wenn Sie PFX-Zertifikate verwenden, führen Sie die folgenden Befehle auf dem Host-Überwachungsdienst-Server:

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustActiveDirectory
```

Wenn Sie Zertifikate installiert sind, auf dem lokalen Computer (z. B. HSM-gesicherten Zertifikate und nicht exportierbare Zertifikate) verwenden, verwenden Sie die `-SigningCertificateThumbprint` und `-EncryptionCertificateThumbprint` Parameter stattdessen.

## <a name="next-step"></a>Nächster Schritt

>[!div class="nextstepaction"]
[Konfigurieren Sie DNS-fabric](guarded-fabric-configuring-fabric-dns-ad.md)

