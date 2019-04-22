---
title: Verhindern, dass Kerberos kennwortänderung, die geheime RC4-Schlüssel verwenden.
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: de207d55-aa3d-4c16-bd3b-496db43663a4
manager: alanth
author: justinha
ms.technology: security-crdential-protection-and-management
ms.date: 11/09/2016
ms.openlocfilehash: 3cfa4ae2442f0cd1e3e4110a355da675fa2d61db
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816271"
---
# <a name="preventing-kerberos-change-password-that-uses-rc4-secret-keys"></a>Verhindern, dass ein Kennwort, das geheime RC4-Schlüssel verwendet, von Kerberos geändert wird

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2008 R2 und WindowsServer 2008

In diesem Thema für IT-Experten erläutert einige Einschränkungen in das Kerberos-Protokoll, das für böswillige Benutzer die Steuerung der dem Konto eines Benutzers führen können. Es ist eine Einschränkung in der Kerberos-Authentifizierung-Netzwerkdienst (V5)-Standard (RFC 4120), handelt es sich innerhalb der Branche, bei dem ein Angreifer authentifizieren Sie sich als ein Benutzer oder Kennwort des Benutzers zu ändern, wenn der Angreifer geheimen Schlüssel des Benutzers bekannt ist, kann ein.

Besitz eines Benutzers Kennwort abgeleiteten Kerberos geheime Schlüssel (RC4 und Advanced Encryption Standard [AES] in der Standardeinstellung) wird während des Kerberos-Kennwort ändern Austauschs pro RFC 4757 überprüft. Nur-Text-Kennwort des Benutzers wird nie auf das Schlüsselverteilungscenter (KDC) bereitgestellt und standardmäßig Active Directory-Domänencontroller ist nicht im Besitz einer Kopie des nur-Text-Kennwörter für Konten. Wenn der Domänencontroller ein Kerberos-Verschlüsselung nicht unterstützt, kann nicht, geheime Schlüssel zum Ändern des Kennworts verwendet werden. 

In den Windows-Betriebssystemen in der Liste am Anfang dieses Themas festgelegt gibt es drei Möglichkeiten, um die Möglichkeit, Kennwörter zu ändern, indem Sie mithilfe von Kerberos mit geheimen Schlüsseln RC4 blockieren:

- Konfigurieren des Benutzers ist für die interaktive Anmeldung erforderlich, die Option "Konto" Smartcard einbezogen werden sollen. Dadurch wird den Benutzer nur eine gültige Smartcard anzumelden, sodass RC4-Dienst-authentifizierungsanforderungen (AS-REQs) abgelehnt werden. Um die Optionen für ein Konto für das Konto festzulegen, mit der rechten Maustaste auf das Konto, klicken Sie auf Eigenschaften, und klicken Sie auf der Registerkarte "Konto" aus. 

- Deaktivieren von RC4-Unterstützung für Kerberos auf allen Domänencontrollern. Dies erfordert mindestens eine Domänenfunktionsebene von Windows Server 2008 und einer Umgebung, in denen alle Kerberos-Clients, Anwendungsserver und -Vertrauensstellungen in und aus der Domäne AES unterstützen müssen. Unterstützung für AES wurde in Windows Server 2008 und Windows Vista eingeführt.

    [!NOTE]
    Es gibt ein bekanntes Problem beim Deaktivieren von RC4, wodurch das System neu starten können. Finden Sie die folgenden Hotfixes:
    - [Windows Server 2012 R2](https://support.microsoft.com/en-us/kb/3038261)
    - [Windows Server 2012](https://support.microsoft.com/en-us/kb/3086213)
    - Kein Hotfix ist verfügbar für frühere Versionen von Windows Server

- Bereitstellen Sie Domänen-Gruppe, auf die Domänenfunktionsebene Windows Server 2012 R2 oder höher, und konfigurieren Sie Benutzer als Mitglied der Sicherheitsgruppe der geschützten Benutzer. Da diese Funktion mehr als nur RC4 Nutzung des Kerberos-Protokolls unterbrochen wird, finden Sie Ressourcen in der folgenden [Siehe auch](#see-also) Abschnitt.

## <a name="see-also"></a>Siehe auch

- Informationen dazu, wie Sie die Verwendung der RC4-Verschlüsselungstyp in Windows Server 2012 R2-Domänen zu verhindern, finden Sie unter [Sicherheitsgruppe "geschützte Benutzer"](/../credentials-protection-and-management/protected-users-security-group.md), und [konfigurieren geschützter Konten](/../credentials-protection-and-management/how-to-configure-protected-accounts.md).

- Erläuterungen zu RFC 4120 und RFC 4757, finden Sie unter [IETF-Dokumenten](http://tools.ietf.org/html/).
