---
title: Konfigurieren von DNS-Weiterleitung und domänenvertrauensstellung
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 3f9083d749ba9251ba47ecb64b7cb3d7c6290f1d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443769"
---
# <a name="configure-dns-forwarding-in-the-hgs-domain-and-a-one-way-trust-with-the-fabric-domain"></a>Konfigurieren von DNS-Weiterleitung in die Host-Überwachungsdienst-Domäne und eine unidirektionale Vertrauensstellung mit der Fabric-Domäne

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

>[!IMPORTANT]
>AD-Modus ist veraltet, beginnend mit Windows Server-2019. Konfigurieren Sie für Umgebungen, in denen ist TPM-Nachweis nicht möglich, [hosten den schlüsselnachweis](guarded-fabric-initialize-hgs-key-mode.md). Host den schlüsselnachweis bietet eine ähnliche Garantie in den Active Directory-Modus, und es ist leichter einzurichten. 

Verwenden Sie die folgenden Schritte aus, um DNS-Weiterleitung eingerichtet und eine unidirektionale Vertrauensstellung mit der Fabric-Domäne herstellen. Diese Schritte, damit der Host-Überwachungsdienst, suchen Sie das Fabric Domänencontroller und Überprüfen der Gruppenmitgliedschaft von Hyper-V-Hosts.

1.  Führen Sie den folgenden Befehl in einer mit erhöhten Rechten PowerShell-Sitzung zum Konfigurieren von DNS-Weiterleitung an. Ersetzen Sie durch den Namen der Fabric-Domäne "Fabrikam.com", und geben Sie die IP-Adressen der DNS-Server in der Fabric-Domäne. Zeigen Sie auf mehr als ein DNS-Server, um eine höhere Verfügbarkeit.

    ```powershell
    Add-DnsServerConditionalForwarderZone -Name "fabrikam.com" -ReplicationScope "Forest" -MasterServers <DNSserverAddress1>, <DNSserverAddress2>
    ```

2.  Um eine unidirektionale Gesamtstruktur-Vertrauensstellung zu erstellen, führen Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten aus:

    Ersetzen Sie dies `bastion.local` durch den Namen der Domäne des Host-Überwachungsdienst und `fabrikam.com` mit dem Namen der Domäne ein Fabric. Geben Sie das Kennwort für den Administrator der Domäne ein Fabric.

        netdom trust bastion.local /domain:fabrikam.com /userD:fabrikam.com\Administrator /passwordD:<password> /add

## <a name="next-step"></a>Nächster Schritt 

> [!div class="nextstepaction"]
> [Konfigurieren von HTTPS](guarded-fabric-configure-hgs-https.md)
