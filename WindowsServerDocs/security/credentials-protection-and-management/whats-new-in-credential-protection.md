---
title: Neues in den Schutz von Anmeldeinformationen
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b0b5180-f65a-43ac-8ef3-66014116f297
author: gitmichiko
ms.author: michikos
manager: dongill
ms.date: 03/06/2017
ms.openlocfilehash: 475b6a0b24b811008ee213c1604d98d9aa9eb092
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447034"
---
# <a name="whats-new-in-credential-protection"></a>Neues in den Schutz von Anmeldeinformationen

## <a name="credential-guard-for-signed-in-user"></a>Credential Guard für den angemeldeten Benutzer

Ab Windows 10, Version 1507 verwenden Kerberos und NTLM virtualisierungsbasierte Sicherheit zum Schutz von Kerberos und NTLM-Geheimnissen von der anmeldesitzung für den angemeldeten Benutzer. 

Ab Windows 10, Version 1511 verwendet Credential Manager virtualisierungsbasierte Sicherheit, um die gespeicherte Anmeldeinformationen der Typ der Anmeldeinformationen zu schützen. Angemeldet von Anmeldeinformationen und gespeicherte Anmeldeinformationen werden nicht mit einem Remotehost mithilfe von Remotedesktop übergeben werden. Ohne UEFI-Sperre kann Credential Guard aktiviert werden.

Ab Windows 10, Version 1607 ist die isolierten Benutzermodus in Hyper-V enthalten, damit es nicht mehr separat für die Bereitstellung des Credential Guard installiert ist.

[Weitere Informationen zu Credential Guard](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard).


## <a name="remote-credential-guard-for-signed-in-user"></a>Remote Credential Guard für den angemeldeten Benutzer

Remote Credential Guard, die ab Windows 10, Version 1607, schützt die Anmeldeinformationen des angemeldeten Benutzers, bei Verwendung von Remotedesktop, indem Sie die Kerberos- und NTLM geheimen Schlüssel, auf dem Clientgerät zu schützen. Für den remote-Host zum Bewerten von Netzwerkressourcen als der Benutzer anfordern, dass authentifizierungsanforderungen Client die geheimen Schlüssel zu verwenden.

Remote Credential Guard, die ab Windows 10, Version 1703, schützt die angegebenen Anmeldeinformationen, bei Verwendung von Remotedesktop.

[Erfahren Sie mehr über Remote Credential Guard](https://technet.microsoft.com/itpro/windows/keep-secure/remote-credential-guard).

## <a name="domain-protections"></a>Domäne Schutzmaßnahmen

Domäne Schutz erfordern Active Directory-Domäne.

### <a name="domain-joined-device-support-for-authentication-using-public-key"></a>Zur Domäne gehörenden Gerät-Unterstützung für die Authentifizierung mit öffentlichen Schlüssel

Mit Windows 10 Version 1507 und Windows Server 2016 ab, wenn eine Domäne eingebundenes Gerät gebundenen öffentlichen Schlüssel mit einem Windows Server 2016-Domänencontroller (DC) registrieren kann, kann das Gerät mit dem öffentlichen Schlüssel, die mithilfe von Kerberos PKINIT authentifiziert Authentifizierung bei einem Windows Server 2016-Domänencontroller.

Ab Windows Server 2016 unterstützen KDCs Authentifizierung unter Verwendung von Kerberos-Schlüssel.  

[Erfahren Sie mehr über die public Key-Unterstützung für die Domäne eingebundene Geräte & Schlüssel Kerberos-Vertrauensstellung](https://technet.microsoft.com/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication).

### <a name="pkinit-freshness-extension-support"></a>Unterstützung von PKINIT Aktualität

Ab Windows 10, Version 1507 und Windows Server 2016, versucht Kerberos-Clients die PKInit Aktualität-Erweiterung für öffentlichen Schlüssel basiert anmelden. 

Ab Windows Server 2016 können KDCs PKInit Aktualität Erweiterung unterstützen.  Standardmäßig bietet KDCs nicht die Erweiterung der PKInit-Aktualität. 

[Erfahren Sie mehr über die Unterstützung von PKINIT Aktualität](https://technet.microsoft.com/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication).

### <a name="rolling-public-key-only-users-ntlm-secrets"></a>Nur Benutzer des öffentlichen Schlüssels des NTLM-Geheimnisse parallelen

Ab Windows Server 2016-Domänenfunktionsebene (DFL) können DCs unterstützen, ein eine einzige Benutzer des öffentlichen Schlüssels des NTLM-Geheimnisse. Dieses Feature ist darin in niedrigeren DFLs.

> [!WARNING] 
> Hinzufügen eines Domänencontrollers zu einer Domäne mit rollierenden NTLM-Geheimnisse, die aktiviert werden, bevor der Domänencontroller mit mindestens vom 8. November 2016 aktualisiert wurde Wartung ausgeführt wird das Risiko der Domänencontroller abstürzt. 

Konfiguration: Für neue Domänen ist dieses Feature standardmäßig aktiviert. Für vorhandene Domänen müssen sie in den Active Directory-Verwaltungscenter konfiguriert werden: 

1. Maustaste auf die Domäne im linken Bereich auf, aus dem Active Directory Administrative Center, und wählen **Eigenschaften**.

    ![Domäneneigenschaften](../media/Credentials-Protection-And-Management/domain-properties.png)

2. Wählen Sie **aktivieren ablaufende NTLM geheimer Schlüssel, für Benutzer, die Verwendung von Microsoft Passport oder eine Smartcard für die interaktive Anmeldung erforderlich sind bei der parallelen**.

    ![Autoroll ablaufende NTLM Geheimnisse](../media/Credentials-Protection-And-Management/autoroll-ntlm.png)

3. Klicken Sie auf **OK**. 

### <a name="allowing-network-ntlm-when-user-is-restricted-to-specific-domain-joined-devices"></a>Lässt die NTLM bei der Benutzer auf bestimmte Domäne eingebundene Geräte beschränkt ist

Ab WindowsServer 2016-Domänenfunktionsebene (DFL), DCs unterstützen und ermöglicht Netzwerk NTLM, wenn ein Benutzer beschränkt, die Domäne eingebundenen Geräten ist. Dieses Feature ist in der unteren DFLs nicht verfügbar.

Konfiguration: Klicken Sie auf die Authentifizierungsrichtlinie auf **Netzwerkauthentifizierung NTLM zulassen, wenn der Benutzer auf beschränkt ist ausgewählten Geräte**. 

[Weitere Informationen zu Authentifizierungsrichtlinien](https://technet.microsoft.com/windows-server-docs/security/credentials-protection-and-management/authentication-policies-and-authentication-policy-silos).
