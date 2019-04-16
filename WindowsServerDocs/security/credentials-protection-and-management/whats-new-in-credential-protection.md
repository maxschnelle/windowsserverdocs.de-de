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
ms.openlocfilehash: 0556c606b987a69eae663b0196467f532d5a307a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="whats-new-in-credential-protection"></a>Neues in den Schutz von Anmeldeinformationen

## <a name="credential-guard-for-signed-in-user"></a>Überwachung von Anmeldeinformationen für den angemeldeten Benutzer

Ab Windows10, Version 1507, verwenden Sie Kerberos oder NTLM virtualisierungsbasierte Sicherheit Kerberos und NTLM geheime Schlüssel, der die Sitzung angemeldeten Benutzer zu schützen. 

Ab Windows10, Version 1511, Anmeldeinformations-Manager wird virtualisierungsbasierte Sicherheit zum Schutz von gespeicherter Anmeldeinformationen von Typ von Anmeldeinformationen verwendet. Angemeldeten Anmeldeinformationen und gespeicherte Anmeldeinformationen werden nicht mit einem Remotehost mit Remotedesktop übergeben werden. Credential Guard kann ohne UEFI-Sperre aktiviert werden.

Ab Windows10, Version 1607, ist die isolierten Benutzermodus mit Hyper-V enthalten, damit es nicht mehr separat für Credential Guard-Bereitstellung installiert ist.

[Weitere Informationen zu Credential Guard](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/credential-guard).


## <a name="remote-credential-guard-for-signed-in-user"></a>Remote Credential Guard für den angemeldeten Benutzer

Ab Windows10, Version 1607, schützt Remote Credential Guard Anmeldeinformationen des angemeldeten Benutzers bei Verwendung von Remotedesktop durch die Kerberos und NTLM-Schlüssel auf dem Client-Gerät zu schützen. Für den Remotehost Netzwerkressourcen wie der Benutzer zu bewerten erfordern Authentifizierungsanfragen das Clientgerät Kennwörter verwenden.

Ab Windows10, Version 1703, schützt Remote Credential Guard angegebenen Benutzeranmeldeinformationen bei Verwendung von Remotedesktop.

[Erfahren Sie mehr über Remote Credential Guard](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/remote-credential-guard).

## <a name="domain-protections"></a>Domäne Schutzmaßnahmen

Domäne Schutzmaßnahmen erforderlich Active Directory-Domäne.

### <a name="domain-joined-device-support-for-authentication-using-public-key"></a>Unterstützung für Geräte Domäne für die Authentifizierung mit öffentlichen Schlüssel

Mit Windows10, Version 1507 und Windows Server2016 ab, wenn eine Domäne eingebundenen Gerät seinen gebundenen öffentlichen Schlüssel mit einem Windows Server2016-Domänencontroller (DC) registrieren kann, kann das Gerät dann mit dem öffentlichen Schlüssel mithilfe der PKINIT Kerberos-Authentifizierung auf einem Windows Server2016-Domänencontroller authentifizieren.

Ab Windows Server2016, unterstützen KDCs unter Verwendung von Schlüssel-Kerberos-Authentifizierung.  

[Weitere Informationen zu den public Key-Unterstützung für die Domäne eingebundene Geräte & Kerberos Key Vertrauensstellung](https://technet.microsoft.com/en-us/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication).

### <a name="pkinit-freshness-extension-support"></a>Unterstützung von PKINIT Aktualität

Ab Windows10, Version 1507 und Windows Server2016, werden Kerberos-Clients die PKInit Aktualität-Erweiterung für öffentliche Schlüssel Basis-Anmeldungen versucht. 

Ab Windows Server2016, können die PKInit Aktualität Erweiterung KDCs unterstützen.  Standardmäßig werden KDCs PKInit Aktualität Erweiterung nicht angeboten. 

[Erfahren Sie mehr über die Unterstützung von PKINIT Aktualität](https://technet.microsoft.com/en-us/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication).

### <a name="rolling-public-key-only-users-ntlm-secrets"></a>Zurücksetzen der öffentliche Schlüssel nur NTLM geheimen Schlüssel des Benutzers

Ab Windows Server2016-Domänenfunktionsebene (DFL), können Domänencontroller unterstützen, einen öffentlichen Schlüssel nur NTLM geheimen Schlüssel des Benutzers veröffentlichen. Dieses Feature ist in der unteren DFLs Quellspeicherort.

> [!WARNING] 
> Hinzufügen eines Domänencontrollers zu einer Domäne mit parallelen NTLM geheime Schlüssel aktiviert, bevor der Domänencontroller mit mindestens vom 8.November2016 aktualisiert wurde Wartung ausgeführt wird das Risiko, dass der Domänencontroller abstürzt. 

Konfiguration: Für neue Domänen ist dieses Feature standardmäßig aktiviert. Für vorhandene Domänen müssen sie in der Active Directory-Verwaltungscenter konfiguriert werden: 

1. Active Directory Administrative Center Maustaste auf die Domäne auf der linken Seite und wählen **Eigenschaften**.

    ![Eigenschaften von Domänen](../media/Credentials-Protection-And-Management/domain-properties.png)
    
2. Wählen Sie **Aktivieren der geheime Schlüssel ablaufende NTLM, für Benutzer, die Verwendung von Microsoft Passport oder einer Smartcard für die interaktive Anmeldung erforderlich sind während der Anmeldung parallelen**.

    ![Autoroll ablaufende NTLM geheime Schlüssel](../media/Credentials-Protection-And-Management/autoroll-ntlm.png)

3. Klicken Sie auf **OK**. 

### <a name="allowing-network-ntlm-when-user-is-restricted-to-specific-domain-joined-devices"></a>Netzwerk NTLM zulassen, wenn Benutzer auf bestimmte Geräte in einer Domäne beschränkt ist

Ab Windows Server 2016-Domänenfunktionsebene (DFL), DCs kann ermöglicht Netzwerk NTLM unterstützen, wenn ein Benutzer auf bestimmte Geräte in einer Domäne ist. Dieses Feature ist nicht in der unteren DFLs verfügbar.

Konfiguration: Klicken Sie auf die Authentifizierungsrichtlinie auf **Netzwerkauthentifizierung NTLM zulassen, wenn der Benutzer auf beschränkt ist, ausgewählte Geräte**. 

[Erfahren Sie mehr über Authentifizierungsrichtlinien](https://technet.microsoft.com/en-us/windows-server-docs/security/credentials-protection-and-management/authentication-policies-and-authentication-policy-silos).
