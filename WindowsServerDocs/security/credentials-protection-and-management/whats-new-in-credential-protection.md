---
title: Neues beim Schutz von Anmelde Informationen
description: Windows Server-Sicherheit
ms.prod: windows-server
ms.technology: security-credential-protection
ms.topic: article
ms.assetid: 1b0b5180-f65a-43ac-8ef3-66014116f297
author: gitmichiko
ms.author: michikos
manager: dongill
ms.date: 03/06/2017
ms.openlocfilehash: 35097cee243239735995a00cec7a6fd3936c62a8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857043"
---
# <a name="whats-new-in-credential-protection"></a>Neues beim Schutz von Anmelde Informationen

## <a name="credential-guard-for-signed-in-user"></a>Credential Guard für angemeldeten Benutzer

Ab Windows 10, Version 1507, Kerberos und NTLM, verwenden Sie virtualisierungsbasierte Sicherheit, um Kerberos-& NTLM-Geheimnisse der Anmelde Sitzung des angemeldeten Benutzers zu schützen. 

Ab Windows 10, Version 1511, verwendet Anmelde Informationen Manager die virtualisierungsbasierte Sicherheit, um gespeicherte Anmelde Informationen des Domänen Anmelde Informations Typs zu schützen. Anmelde Informationen und gespeicherte Domänen Anmelde Informationen werden nicht mithilfe von Remote Desktop an einen Remote Host übermittelt. Credential Guard kann ohne UEFI-Sperre aktiviert werden.

Ab Windows 10, Version 1607, ist der isolierte Benutzermodus in Hyper-V enthalten, sodass er nicht mehr separat für die Credential Guard-Bereitstellung installiert wird.

[Erfahren Sie mehr über Credential Guard](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard).


## <a name="remote-credential-guard-for-signed-in-user"></a>Remote Credential Guard für angemeldeten Benutzer

Ab Windows 10, Version 1607, schützt Remote Credential Guard Anmelde Informationen für angemeldete Benutzer, wenn Remotedesktop, indem die Kerberos-und NTLM-Geheimnisse auf dem Client Gerät geschützt werden. Damit der Remote Host die Netzwerkressourcen als Benutzer bewerten kann, müssen die geheimen Anforderungen vom Client Gerät verwendet werden.

Ab Windows 10, Version 1703, schützt Remote Credential Guard bereitgestellte Benutzer Anmelde Informationen, wenn Sie Remotedesktop verwenden.

[Erfahren Sie mehr über Remote Anmelde Informationen Guard](https://technet.microsoft.com/itpro/windows/keep-secure/remote-credential-guard).

## <a name="domain-protections"></a>Domänen Schutz

Für den Domänen Schutz ist eine Active Directory Domäne erforderlich.

### <a name="domain-joined-device-support-for-authentication-using-public-key"></a>Unterstützung von in die Domäne eingebundenen Geräten für die Authentifizierung mit öffentlichem Schlüssel

Ab Windows 10, Version 1507 und Windows Server 2016, kann das Gerät mithilfe der Kerberos PKINIT-Authentifizierung bei einem Windows Server 2016-Domänen Controller mit dem öffentlichen Schlüssel authentifiziert werden, wenn ein in eine Domäne eingebundenes Gerät seinen gebundenen öffentlichen Schlüssel bei einem Windows Server 2016-Domänen Controller (DC) registrieren kann.

Ab Windows Server 2016 unterstützen KDCs die Authentifizierung mithilfe der Kerberos-Schlüssel Vertrauensstellung.  

[Erfahren Sie mehr über die Unterstützung öffentlicher Schlüssel für in die Domäne eingebundenen Geräten & Kerberos-Schlüssel Vertrauen](https://technet.microsoft.com/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication).

### <a name="pkinit-freshness-extension-support"></a>PKINIT-Aktualität-Erweiterungs Unterstützung

Ab Windows 10, Version 1507 und Windows Server 2016, versuchen die Kerberos-Clients, die PKINIT-Aktualitäts Erweiterung für Anmeldungen mit öffentlichem Schlüssel zu unterstützen. 

Ab Windows Server 2016 können KDCs die Erweiterung PKINIT-Aktualität unterstützen.  Standardmäßig bieten KDCs keine PKINIT-Aktualität-Erweiterung. 

[Weitere Informationen zur Unterstützung von PKINIT-Erweiterungen](https://technet.microsoft.com/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication).

### <a name="rolling-public-key-only-users-ntlm-secrets"></a>Nur die NTLM-Geheimnisse des öffentlichen Schlüssels des öffentlichen Schlüssels

Beginnend mit der Windows Server 2016-Domänen Funktionsebene (DFL) können DCS die NTLM-Geheimnisse eines öffentlichen Schlüssels eines öffentlichen Schlüssels unterstützen. Diese Funktion ist in niedrigeren dfls nicht verfügbar.

> [!WARNING] 
> Wenn Sie einen Domänen Controller zu einer Domäne hinzufügen, bei der parallele NTLM-Geheimnisse aktiviert sind 2016, bevor der DC mit mindestens dem 8 

Konfiguration: für neue Domänen ist dieses Feature standardmäßig aktiviert. Für vorhandene Domänen muss Sie im Active Directory Verwaltungs Center konfiguriert werden: 

1. Klicken Sie im Active Directory Verwaltungs Center im linken Bereich mit der rechten Maustaste auf die Domäne, und wählen Sie **Eigenschaften**aus.

    ![Domänen Eigenschaften](../media/Credentials-Protection-And-Management/domain-properties.png)

2. Aktivieren Sie das **Aktivieren des Rollbacks abgelaufener NTLM-Geheimnisse während der Anmeldung, für Benutzer, die Microsoft Passport oder Smartcard für die interaktive Anmeldung verwenden müssen**.

    ![Autoroll-ablaufende NTLM-Geheimnisse](../media/Credentials-Protection-And-Management/autoroll-ntlm.png)

3. Klicken Sie auf **OK**. 

### <a name="allowing-network-ntlm-when-user-is-restricted-to-specific-domain-joined-devices"></a>Netzwerk-NTLM zulassen, wenn der Benutzer auf bestimmte in die Domäne eingebundenen Geräte beschränkt ist

Beginnend mit der Windows Server 2016-Domänen Funktionsebene (DFL) können DCS das Zulassen von Netzwerk-NTLM unterstützen, wenn ein Benutzer auf bestimmte in die Domäne eingebundenen Geräte beschränkt ist. Diese Funktion ist in niedrigeren dfls nicht verfügbar.

Konfiguration: Klicken Sie in der Authentifizierungs Richtlinie auf **NTLM-Netzwerk Authentifizierung zulassen, wenn der Benutzer auf ausgewählte Geräte beschränkt ist**. 

[Weitere Informationen zu Authentifizierungs Richtlinien](https://technet.microsoft.com/windows-server-docs/security/credentials-protection-and-management/authentication-policies-and-authentication-policy-silos).
