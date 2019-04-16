---
title: "Verhindern, dass Kerberos ändern, Kennwort, das geheime RC4-Schlüssel verwenden."
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: de207d55-aa3d-4c16-bd3b-496db43663a4
manager: alanth
author: justinha
ms.technology: security-crdential-protection-and-management
ms.date: 11/09/2016
ms.openlocfilehash: 3cfa4ae2442f0cd1e3e4110a355da675fa2d61db
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="preventing-kerberos-change-password-that-uses-rc4-secret-keys"></a>Verhindern, dass Kerberos-Kennwort ändern, das geheime RC4-Schlüssel verwendet.

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016, Windows Server2008 R2 und Windows Server 2008

In diesem Thema für IT-Experten erläutert einige Einschränkungen in das Kerberos-Protokoll, das ein böswilliger Benutzer, die Kontrolle des Kontos eines Benutzers zur Folge haben könnte. Es ist eine Einschränkung im Netzwerk Kerberos-Authentifizierungsdienst (V5)-Standard (RFC 4120), die bekannten innerhalb der Branche, bei dem ein Angreifer kann authentifizieren sich als Benutzer oder Kennwort des Benutzers zu ändern, wenn der Angreifer geheime Schlüssel des Benutzers bekannt ist.

Der Besitz des Benutzers Kennwort abgeleiteten geheime Kerberos-Schlüssel (RC4 und Advanced Encryption Standard [AES] in der Standardeinstellung) ist während der Kerberos-Kennwort ändern Exchange pro RFC 4757 überprüft. Nur-Text-Kennwort des Benutzers wird nie auf das Schlüsselverteilungscenter (KDC) bereitgestellt, und in der Standardeinstellung werden Active Directory-Domänencontroller eine Kopie des Nur-Text-Kennwörter für Konten nicht besitzen. Wenn der Domänencontroller einen Kerberos-Verschlüsselungstyp nicht unterstützt, kann diese geheimen Schlüssel verwendet werden, das Kennwort ändern. 

In den Windows-Betriebssystemen in der Liste "betrifft" am Anfang dieses Themas benannt gibt es drei Möglichkeiten, die Möglichkeit, Kennwörter zu ändern, indem Sie mithilfe von Kerberos mit geheime RC4-Schlüssel zu sperren:

- Konfigurieren den Benutzer die Option für das Konto Smartcard einbezogen werden sollen für die interaktive Anmeldung erforderlich ist. Dadurch wird den Benutzer nur mit einer gültigen Smartcard Protokollierung, sodass RC4-Dienst Authentifizierungsanforderungen (AS-REQs) abgelehnt werden. Klicken Sie zum Festlegen der Optionen für die Computerkonten für ein Konto mit der rechten Maustaste auf das Konto, klicken Sie dann auf Eigenschaften, und klicken Sie auf der Registerkarte "Konto". 

- Die RC4-Unterstützung für Kerberos auf allen Domänencontrollern deaktiviert. Dies erfordert mindestens eine Domänenfunktionsebene von Windows Server2008 und in einer Umgebung, in dem alle Kerberos-Clients, Anwendungsserver und Vertrauensstellungen in und aus der Domäne AES unterstützen muss. Unterstützung für AES wurde in Windows Server2008 und Windows Vista eingeführt.

    [!NOTE]
    Es ist ein bekanntes Problem mit der Deaktivierung von RC4, wodurch das System neu starten können. Finden Sie die folgenden Hotfixes:
    - [Windows Server2012 R2](https://support.microsoft.com/en-us/kb/3038261)
    - [Windows Server 2012](https://support.microsoft.com/en-us/kb/3086213)
    - Kein Hotfix steht für frühere Versionen von Windows Server

- Domänen Satz bereitstellen, auf die Domänenfunktionsebene Windows Server2012 R2 oder höher, und Konfigurieren von Benutzern als Mitglieder der Sicherheitsgruppe "geschützte Benutzer". Da dieses Feature nicht nur RC4 Verwendung der Kerberos-Protokolls unterbrochen wird, finden Sie in den folgenden Ressourcen [Siehe auch](#see-also) Abschnitt.

## <a name="see-also"></a>Siehe auch

- Informationen dazu, wie Sie verhindern, dass die Verwendung des Typs RC4-Verschlüsselung in Windows Server2012 R2-Domänen finden Sie unter [Protected Users Security Group](/../credentials-protection-and-management/protected-users-security-group.md), und [How to Configure Protected Accounts](/../credentials-protection-and-management/how-to-configure-protected-accounts.md).

- Erläuterungen zu RFC 4120 und RFC 4757, finden Sie unter [IETF-Dokumenten](http://tools.ietf.org/html/).
