---
title: Erstellen einer Sicherheitsgruppe für geschützte Hosts und Registrieren der Gruppe bei HGS
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: efcf148356910a250a06ee9165c544c96226e10e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971417"
---
# <a name="create-a-security-group-for-guarded-hosts-and-register-the-group-with-hgs"></a>Erstellen einer Sicherheitsgruppe für geschützte Hosts und Registrieren der Gruppe bei HGS

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

> [!IMPORTANT]
> Der AD-Modus ist ab Windows Server 2019 veraltet. Für Umgebungen, in denen ein TPM-Nachweis nicht möglich ist, konfigurieren Sie den [Host Schlüssel](guarded-fabric-initialize-hgs-key-mode.md)Nachweis. Der Host Schlüssel Nachweis bietet eine ähnliche Garantie für den AD-Modus und ist einfacher einzurichten.

In diesem Thema werden die Zwischenschritte zum Vorbereiten von Hyper-V-Hosts auf überwachte Hosts mithilfe von Administrator vertrauenswürdigem Nachweis (AD-Modus) beschrieben. Bevor Sie diese Schritte ausführen, führen Sie die Schritte unter [Konfigurieren des Fabric-DNS für Hosts aus, die zu überwachte Hosts](guarded-fabric-configuring-fabric-dns-ad.md)werden.


## <a name="create-a-security-group-and-add-hosts"></a>Erstellen einer Sicherheitsgruppe und Hinzufügen von Hosts

1. Erstellen Sie eine neue **globale** Sicherheitsgruppe in der Fabric-Domäne, und fügen Sie Hyper-V-Hosts hinzu, auf denen geschützte VMS ausgeführt werden. Starten Sie die Hosts neu, um deren Gruppenmitgliedschaft zu aktualisieren.

2. Verwenden Sie Get-adgroup zum Abrufen der Sicherheits-ID (SID) der Sicherheitsgruppe, und stellen Sie Sie für den HGS-Administrator bereit.

    ```powershell
    Get-ADGroup "Guarded Hosts"
    ```

    ![Befehl "Get-adgroup" mit Ausgabe](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>Registrieren der SID der Sicherheitsgruppe bei HGS

1. Führen Sie auf einem HGS-Server den folgenden Befehl aus, um die Sicherheitsgruppe bei HGS zu registrieren.
   Führen Sie den Befehl bei Bedarf erneut für weitere Gruppen aus.
   Geben Sie einen anzeigen Amen für die Gruppe an.
   Er muss nicht mit dem Namen der Active Directory Sicherheitsgruppe identisch sein.

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. Führen [Sie Get-hgsattestationhostgroup](https://technet.microsoft.com/library/mt652172.aspx)aus, um zu überprüfen, ob die Gruppe hinzugefügt wurde.

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Bestätigen des Nachweises](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="additional-references"></a>Weitere Verweise

- [Bereitstellen des Host-Überwachungsdiensts für überwachte Hosts und abgeschirmte VMs](guarded-fabric-deploying-hgs-overview.md)
