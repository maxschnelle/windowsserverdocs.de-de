---
title: Initialisieren des HGS-Clusters mit dem AD-Modus in einer geschützten Gesamtstruktur
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: c69561f7d17bb1d36d90fc66cf4c1a196072fc72
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402365"
---
# <a name="initialize-the-hgs-cluster-using-ad-mode-in-an-existing-bastion-forest"></a>Initialisieren des HGS-Clusters mit dem AD-Modus in einer vorhandenen geschützten Gesamtstruktur

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016


>[!IMPORTANT]
>Der admin-Trusted Nachweis (AD-Modus) ist ab Windows Server 2019 veraltet. Für Umgebungen, in denen ein TPM-Nachweis nicht möglich ist, konfigurieren Sie den [Host Schlüssel](guarded-fabric-initialize-hgs-key-mode-bastion.md)Nachweis. Der Host Schlüssel Nachweis bietet eine ähnliche Garantie für den AD-Modus und ist einfacher einzurichten. 

Active Directory Domain Services wird auf dem Computer installiert, sollte jedoch nicht konfiguriert bleiben.

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)] 

Bevor Sie fortfahren, stellen Sie sicher, dass Sie die Cluster Objekte für den Host-Überwachungsdienst vorab bereitgestellt haben, und gewähren Sie dem angemeldeten Benutzer die **vollständige Kontrolle** über die VCO-und CNO-Objekte in Active Directory.
Der Name des virtuellen Computer Objekts muss an den Parameter "`-HgsServiceName`" und der Cluster Name an den Parameter "`-ClusterName`" übergeben werden.

> [!TIP]
> Überprüfen Sie die AD-Domänen Controller, um sicherzustellen, dass Ihre Cluster Objekte auf alle DCS repliziert wurden

Wenn Sie PFX-basierte Zertifikate verwenden, führen Sie auf dem HGS-Server die folgenden Befehle aus:

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustActiveDirectory
```

Wenn Sie Zertifikate verwenden, die auf dem lokalen Computer installiert sind (z. b. HSM-gestützte Zertifikate und nicht exportierbare Zertifikate), verwenden Sie stattdessen die Parameter "`-SigningCertificateThumbprint`" und "`-EncryptionCertificateThumbprint`".

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Konfigurieren des Fabric-DNS](guarded-fabric-configuring-fabric-dns-ad.md)

