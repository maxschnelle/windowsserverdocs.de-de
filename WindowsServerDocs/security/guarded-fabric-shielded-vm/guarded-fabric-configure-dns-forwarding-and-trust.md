---
title: Konfigurieren der DNS-Weiterleitung und der Vertrauensstellung
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 5d8ffe82065caeee27c5d13f5243f13addc6c325
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386737"
---
# <a name="configure-dns-forwarding-in-the-hgs-domain-and-a-one-way-trust-with-the-fabric-domain"></a>Konfigurieren der DNS-Weiterleitung in der HGS-Domäne und einer unidirektionalen Vertrauensstellung mit der Fabric-Domäne

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

>[!IMPORTANT]
>Der AD-Modus ist ab Windows Server 2019 veraltet. Für Umgebungen, in denen ein TPM-Nachweis nicht möglich ist, konfigurieren Sie den [Host Schlüssel](guarded-fabric-initialize-hgs-key-mode.md)Nachweis. Der Host Schlüssel Nachweis bietet eine ähnliche Garantie für den AD-Modus und ist einfacher einzurichten. 

Führen Sie die folgenden Schritte aus, um die DNS-Weiterleitung einzurichten und eine unidirektionale Vertrauensstellung mit der Fabric-Domäne einzurichten. Diese Schritte ermöglichen es dem HGS, die Fabric-Domänen Controller zu finden und die Gruppenmitgliedschaft der Hyper-V-Hosts zu überprüfen.

1.  Führen Sie den folgenden Befehl in einer PowerShell-Sitzung mit erhöhten Rechten aus, um die DNS-Weiterleitung Ersetzen Sie fabrikam.com durch den Namen der Fabric-Domäne, und geben Sie die IP-Adressen der DNS-Server in der Fabric-Domäne ein. Zeigen Sie auf mehr als einen DNS-Server, um eine höhere Verfügbarkeit zu erhalten.

    ```powershell
    Add-DnsServerConditionalForwarderZone -Name "fabrikam.com" -ReplicationScope "Forest" -MasterServers <DNSserverAddress1>, <DNSserverAddress2>
    ```

2.  Führen Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten aus, um eine unidirektionale Vertrauensstellung zu erstellen:

    Ersetzen Sie `bastion.local` durch den Namen der HGS-Domäne und `fabrikam.com` durch den Namen der Fabric-Domäne. Geben Sie das Kennwort für einen Administrator der Fabric-Domäne an.

        netdom trust bastion.local /domain:fabrikam.com /userD:fabrikam.com\Administrator /passwordD:<password> /add

## <a name="next-step"></a>Nächster Schritt 

> [!div class="nextstepaction"]
> [Konfigurieren von HTTPS](guarded-fabric-configure-hgs-https.md)
