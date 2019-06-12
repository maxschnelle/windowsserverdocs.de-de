---
title: Initialisieren Sie den Host-Überwachungsdienst-Cluster mithilfe von Schlüssel-Modus in einer geschützten Gesamtstruktur
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: e785ee17bf68c07d965816480baa0d59062fc434
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447421"
---
# <a name="initialize-the-hgs-cluster-using-key-mode-in-an-existing-bastion-forest"></a>Initialisieren Sie den Host-Überwachungsdienst-Cluster, die mithilfe von Modus-Taste in einer vorhandenen geschützten Gesamtstruktur

> Gilt für: Windows Server 2019
> 
> [!div class="step-by-step"]
> [«Installieren Sie die Host-Überwachungsdienst in einer neuen Gesamtstruktur](guarded-fabric-install-hgs-in-a-bastion-forest.md)
> [erstellen Hostschlüssel»](guarded-fabric-create-host-key.md)

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

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustHostKey
```

Wenn Sie Zertifikate installiert sind, auf dem lokalen Computer (z. B. HSM-gesicherten Zertifikate und nicht exportierbare Zertifikate) verwenden, verwenden Sie die `-SigningCertificateThumbprint` und `-EncryptionCertificateThumbprint` Parameter stattdessen.

