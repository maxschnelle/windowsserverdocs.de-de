---
title: Hinzufügen von Hostinformationen für den Administrator vertrauenswürdigen Nachweis
ms.topic: article
ms.assetid: 87089ebc-b953-4aa3-96b5-966cf91acb02
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: abc01dbb691843d199169bd654afaa5cf06bbb87
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971437"
---
# <a name="authorize-hyper-v-hosts-using-admin-trusted-attestation"></a>Autorisieren von Hyper-V-Hosts mithilfe von Administrator vertrauenswürdigem Nachweis

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

> [!IMPORTANT]
> Der admin-Trusted Nachweis (AD-Modus) ist ab Windows Server 2019 veraltet. Für Umgebungen, in denen ein TPM-Nachweis nicht möglich ist, konfigurieren Sie den [Host Schlüssel](guarded-fabric-initialize-hgs-key-mode.md)Nachweis. Der Host Schlüssel Nachweis bietet eine ähnliche Garantie für den AD-Modus und ist einfacher einzurichten.


So autorisieren Sie einen überwachten Host im AD-Modus:

1. Fügen Sie die Hyper-V-Hosts in der Fabric-Domäne einer Sicherheitsgruppe hinzu.
2. Registrieren Sie in der HGS-Domäne die SID der Sicherheitsgruppe bei HGS.

## <a name="add-the-hyper-v-host-to-a-security-group-and-reboot-the-host"></a>Hinzufügen des Hyper-V-Hosts zu einer Sicherheitsgruppe und Neustarten des Hosts

1. Erstellen Sie eine **globale** Sicherheitsgruppe in der Fabric-Domäne, und fügen Sie Hyper-V-Hosts hinzu, auf denen geschützte VMS ausgeführt werden.
   Starten Sie die Hosts neu, um deren Gruppenmitgliedschaft zu aktualisieren.

2. Verwenden Sie Get-adgroup zum Abrufen der Sicherheits-ID (SID) der Sicherheitsgruppe, und stellen Sie Sie für den HGS-Administrator bereit.

   ```powershell
   Get-ADGroup "Guarded Hosts"
   ```

   ![Befehl "Get-adgroup" mit Ausgabe](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>Registrieren der SID der Sicherheitsgruppe bei HGS

1. Rufen Sie die SID der Sicherheitsgruppe für geschützte Hosts vom Fabric-Administrator ab, und führen Sie den folgenden Befehl aus, um die Sicherheitsgruppe bei HGS zu registrieren.
   Führen Sie den Befehl bei Bedarf erneut für weitere Gruppen aus.
   Geben Sie einen anzeigen Amen für die Gruppe an.
   Er muss nicht mit dem Namen der Active Directory Sicherheitsgruppe identisch sein.

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. Führen [Sie Get-hgsattestationhostgroup](https://technet.microsoft.com/library/mt652172.aspx)aus, um zu überprüfen, ob die Gruppe hinzugefügt wurde.


