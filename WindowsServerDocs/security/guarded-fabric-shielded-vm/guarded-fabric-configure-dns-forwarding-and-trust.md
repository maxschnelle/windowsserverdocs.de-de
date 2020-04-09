---
title: Konfigurieren der DNS-Weiterleitung und der Vertrauensstellung
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 6d6ad10dacf9c667069ecd43f38473a3f20bc781
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856853"
---
# <a name="configure-dns-forwarding-in-the-hgs-domain-and-a-one-way-trust-with-the-fabric-domain"></a>Konfigurieren der DNS-Weiterleitung in der HGS-Domäne und einer unidirektionalen Vertrauensstellung mit der Fabric-Domäne

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

>[!IMPORTANT]
>Der AD-Modus ist ab Windows Server 2019 veraltet. Für Umgebungen, in denen ein TPM-Nachweis nicht möglich ist, konfigurieren Sie den [Host Schlüssel](guarded-fabric-initialize-hgs-key-mode.md)Nachweis. Der Host Schlüssel Nachweis bietet eine ähnliche Garantie für den AD-Modus und ist einfacher einzurichten. 

Führen Sie die folgenden Schritte aus, um die DNS-Weiterleitung einzurichten und eine unidirektionale Vertrauensstellung mit der Fabric-Domäne einzurichten. Diese Schritte ermöglichen es dem HGS, die Fabric-Domänen Controller zu finden und die Gruppenmitgliedschaft der Hyper-V-Hosts zu überprüfen.

1.  Führen Sie den folgenden Befehl in einer PowerShell-Sitzung mit erhöhten Rechten aus, um die DNS-Weiterleitung Ersetzen Sie fabrikam.com durch den Namen der Fabric-Domäne, und geben Sie die IP-Adressen der DNS-Server in der Fabric-Domäne ein. Zeigen Sie auf mehr als einen DNS-Server, um eine höhere Verfügbarkeit zu erhalten.

    ```powershell
    Add-DnsServerConditionalForwarderZone -Name "fabrikam.com" -ReplicationScope "Forest" -MasterServers <DNSserverAddress1>, <DNSserverAddress2>
    ```

2.  Führen Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten aus, um eine unidirektionale Vertrauensstellung zu erstellen:

    Ersetzen Sie `bastion.local` durch den Namen der HGS-Domäne, und `fabrikam.com` Sie durch den Namen der Fabric-Domäne. Geben Sie das Kennwort für einen Administrator der Fabric-Domäne an.

        netdom trust bastion.local /domain:fabrikam.com /userD:fabrikam.com\Administrator /passwordD:<password> /add

## <a name="next-step"></a>Nächster Schritt 

> [!div class="nextstepaction"]
> [Konfigurieren von HTTPS](guarded-fabric-configure-hgs-https.md)
