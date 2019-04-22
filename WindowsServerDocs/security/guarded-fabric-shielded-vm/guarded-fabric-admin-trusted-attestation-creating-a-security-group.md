---
title: Erstellen Sie eine Sicherheitsgruppe für überwachte Hosts und die Gruppe bei HGS registriert
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: ba547dff862a283b68ff105a14b14ed367891745
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816341"
---
# <a name="create-a-security-group-for-guarded-hosts-and-register-the-group-with-hgs"></a>Erstellen Sie eine Sicherheitsgruppe für überwachte Hosts und die Gruppe bei HGS registriert

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

>[!IMPORTANT]
>AD-Modus ist veraltet, beginnend mit Windows Server-2019. Konfigurieren Sie für Umgebungen, in denen ist TPM-Nachweis nicht möglich, [hosten den schlüsselnachweis](guarded-fabric-initialize-hgs-key-mode.md). Host den schlüsselnachweis bietet eine ähnliche Garantie in den Active Directory-Modus, und es ist leichter einzurichten. 


Dieses Thema beschreibt die fortgeschrittene Schritte zur Vorbereitung von Hyper-V-Hosts werden von überwachten Hosts, die mit der Admin-vertrauenswürdiger Nachweis (Active Directory-Modus). Vor dem Ausführen dieser Schritte führen Sie die Schritte im [konfigurieren die Fabric-DNS für Hosts, die überwachten Hosts werden](guarded-fabric-configuring-fabric-dns-ad.md).


## <a name="create-a-security-group-and-add-hosts"></a>Erstellen einer Sicherheitsgruppe und Hinzufügen von hosts

1. Erstellen Sie ein neues **GLOBAL** Sicherheit in der Fabric-Domäne, und fügen Sie abgeschirmte VMs Hyper-V-Hosts, die ausgeführt werden. Starten Sie den Host aktualisieren ihre Gruppenmitgliedschaft neu.

2. Verwenden Sie Get-ADGroup, um die Sicherheits-ID (SID) der Sicherheitsgruppe zu erhalten, und geben Sie sie an den HGS-Administrator. 

    ```powershell
    Get-ADGroup "Guarded Hosts"
    ```

    ![Get-AdGroup-Befehl mit der Ausgabe](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>Registrieren Sie die SID der Sicherheitsgruppe mit Host-Überwachungsdienst  

1. Führen Sie den folgenden Befehl, der Sicherheitsgruppe "bei HGS registriert, auf einem Host-Überwachungsdienst-Server. 
   Führen Sie den Befehl erneut aus, bei Bedarf für zusätzliche Gruppen. 
   Geben Sie einen Anzeigenamen für die Gruppe ein. 
   Es muss nicht mit dem Active Directory Security Group-Namen übereinstimmen. 

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. Führen Sie zum Überprüfen, ob die Gruppe hinzugefügt wurde, [Get-HgsAttestationHostGroup](https://technet.microsoft.com/library/mt652172.aspx). 

## <a name="next-step"></a>Nächster Schritt

>[!div class="nextstepaction"]
[Nachweis bestätigen](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="see-also"></a>Siehe auch

- [Bereitstellen von Host-Überwachungsdienst für überwachte Hosts und abgeschirmten VMs](guarded-fabric-deploying-hgs-overview.md)
