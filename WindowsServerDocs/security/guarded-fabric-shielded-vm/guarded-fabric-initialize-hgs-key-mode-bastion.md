---
title: Initialisieren des HGS-Clusters mithilfe des Schlüssel Modus in einer geschützten Gesamtstruktur
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 45f0f587c17e90251da2632f034fe03e2dc1c083
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856653"
---
# <a name="initialize-the-hgs-cluster-using-key-mode-in-an-existing-bastion-forest"></a>Initialisieren des HGS-Clusters mithilfe des Schlüssel Modus in einer vorhandenen geschützten Gesamtstruktur

> Gilt für: Windows Server 2019
> 
> [!div class="step-by-step"]
> [«Installieren von HGS in einer neuen](guarded-fabric-install-hgs-in-a-bastion-forest.md) Gesamtstruktur
> [Erstellen eines Host Schlüssels»](guarded-fabric-create-host-key.md)

Active Directory Domain Services wird auf dem Computer installiert, sollte jedoch nicht konfiguriert bleiben.

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)] 

Bevor Sie fortfahren, stellen Sie sicher, dass Sie die Cluster Objekte für den Host-Überwachungsdienst vorab bereitgestellt haben, und gewähren Sie dem angemeldeten Benutzer die **vollständige Kontrolle** über die VCO-und CNO-Objekte in Active Directory.
Der Name des virtuellen Computer Objekts muss an den `-HgsServiceName`-Parameter übergeben werden, und der Cluster Name muss an den `-ClusterName`-Parameter übergeben werden.

> [!TIP]
> Überprüfen Sie die AD-Domänen Controller, um sicherzustellen, dass Ihre Cluster Objekte auf alle DCS repliziert wurden

Wenn Sie PFX-basierte Zertifikate verwenden, führen Sie auf dem HGS-Server die folgenden Befehle aus:

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustHostKey
```

Wenn Sie Zertifikate verwenden, die auf dem lokalen Computer installiert sind (z. b. HSM-gestützte Zertifikate und nicht exportierbare Zertifikate), verwenden Sie stattdessen die Parameter "`-SigningCertificateThumbprint`" und "`-EncryptionCertificateThumbprint`".

