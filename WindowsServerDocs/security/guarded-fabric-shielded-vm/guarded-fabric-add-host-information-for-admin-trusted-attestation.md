---
title: Fügen Sie die Hostinformationen für Admin-vertrauenswürdiger Nachweis
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 87089ebc-b953-4aa3-96b5-966cf91acb02
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 7949711dbb0f89f5404b491d60938985bfa98c22
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849461"
---
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

# <a name="authorize-hyper-v-hosts-using-admin-trusted-attestation"></a>Autorisieren von Hyper-V-Hosts, die Admin-vertrauenswürdiger Nachweis verwenden

>[!IMPORTANT]
>Admin-vertrauenswürdiger Nachweis (Active Directory-Modus) ist veraltet, beginnend mit Windows Server-2019. Konfigurieren Sie für Umgebungen, in denen ist TPM-Nachweis nicht möglich, [hosten den schlüsselnachweis](guarded-fabric-initialize-hgs-key-mode.md). Host den schlüsselnachweis bietet eine ähnliche Garantie in den Active Directory-Modus, und es ist leichter einzurichten. 


So autorisieren Sie als überwachten Host im AD-Modus 

1. Fügen Sie in der Fabric-Domäne die Hyper-V-Hosts zu einer Sicherheitsgruppe hinzu.
2. Registrieren Sie in der Domäne des Host-Überwachungsdienst die SID der Sicherheitsgruppe mit Host-Überwachungsdienst. 

## <a name="add-the-hyper-v-host-to-a-security-group-and-reboot-the-host"></a>Der Hyper-V-Host zu einer Sicherheitsgruppe hinzugefügt und den Host neu starten

1. Erstellen Sie eine **GLOBAL** Sicherheit in der Fabric-Domäne, und fügen Sie abgeschirmte VMs Hyper-V-Hosts, die ausgeführt werden. 
   Starten Sie den Host aktualisieren ihre Gruppenmitgliedschaft neu.

2. Verwenden Sie Get-ADGroup, um die Sicherheits-ID (SID) der Sicherheitsgruppe zu erhalten, und geben Sie sie an den HGS-Administrator. 

   ```powershell
   Get-ADGroup "Guarded Hosts"
   ```

   ![Get-AdGroup-Befehl mit der Ausgabe](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>Registrieren Sie die SID der Sicherheitsgruppe mit Host-Überwachungsdienst  

1. Rufen Sie die SID der Sicherheitsgruppe für überwachte Hosts von der Fabric-Administrator, und führen Sie den folgenden Befehl, der Sicherheitsgruppe "bei HGS registriert. 
   Führen Sie den Befehl erneut aus, bei Bedarf für zusätzliche Gruppen. 
   Geben Sie einen Anzeigenamen für die Gruppe ein. 
   Es muss nicht mit dem Active Directory Security Group-Namen übereinstimmen. 

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. Führen Sie zum Überprüfen, ob die Gruppe hinzugefügt wurde, [Get-HgsAttestationHostGroup](https://technet.microsoft.com/library/mt652172.aspx). 


