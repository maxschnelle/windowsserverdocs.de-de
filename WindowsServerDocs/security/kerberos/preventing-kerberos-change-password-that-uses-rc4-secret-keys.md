---
title: Verhindern eines Kerberos-Änderungs Kennworts, das RC4-Geheimnis Schlüssel verwendet
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: de207d55-aa3d-4c16-bd3b-496db43663a4
manager: alanth
author: justinha
ms.technology: security-crdential-protection-and-management
ms.date: 11/09/2016
ms.openlocfilehash: 21c2d3d79653bd02fea9d2ac0d09bd18690a388f
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949748"
---
# <a name="preventing-kerberos-change-password-that-uses-rc4-secret-keys"></a>Verhindern, dass ein Kennwort, das geheime RC4-Schlüssel verwendet, von Kerberos geändert wird

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2008 R2 und Windows Server 2008

In diesem Thema für IT-Experten werden einige Einschränkungen im Kerberos-Protokoll erläutert, die dazu führen können, dass böswillige Benutzer die Kontrolle über das Konto eines Benutzers nehmen. Der Kerberos-Netzwerk Authentifizierungsdienst (V5) (RFC 4120), der in der Branche gut bekannt ist, gibt eine Einschränkung, bei der sich ein Angreifer als Benutzer authentifizieren oder das Kennwort des Benutzers ändern kann, wenn der Angreifer den geheimen Schlüssel des Benutzers kennt.

Der Besitz der von Kenn Wörtern abgeleiteten Kerberos-Schlüssel eines Benutzers (RC4 und Advanced Encryption Standard [AES] wird standardmäßig bei der Kerberos-Kenn Wort Änderungs Änderung pro RFC 4757 überprüft. Das nur-Text-Kennwort des Benutzers wird niemals für den Schlüsselverteilungscenter (KDC) bereitgestellt, und Active Directory Domänen Controller besitzen standardmäßig keine Kopie von nur-Text-Kenn Wörtern für Konten. Wenn der Domänen Controller keinen Kerberos-Verschlüsselungstyp unterstützt, kann der geheime Schlüssel nicht zum Ändern des Kennworts verwendet werden. 

In den Windows-Betriebssystemen, die in der Liste gilt für am Anfang dieses Themas angegeben sind, gibt es drei Möglichkeiten, um die Möglichkeit zum Ändern von Kenn Wörtern mithilfe von Kerberos mit RC4-geheimen Schlüsseln zu blockieren:

- Konfigurieren Sie das Benutzerkonto für die Konto Option Smartcard ist für die interaktive Anmeldung erforderlich. Dadurch wird der Benutzer darauf beschränkt, sich nur mit einer gültigen Smartcard anzumelden, damit RC4-Authentifizierungsdienst Anforderungen (as-reqs) abgelehnt werden. Klicken Sie mit der rechten Maustaste auf das Konto, klicken Sie auf Eigenschaften, und klicken Sie auf die Registerkarte Konto, um die Konto Optionen für ein Konto festzulegen. 

- Deaktivieren Sie die RC4-Unterstützung für Kerberos auf allen Domänen Controllern. Dies erfordert mindestens eine Windows Server 2008-Domänen Funktionsebene und eine Umgebung, in der alle Kerberos-Clients, Anwendungsserver und Vertrauens Stellungen von und von der Domäne AES unterstützen müssen. Die Unterstützung für AES wurde in Windows Server 2008 und Windows Vista eingeführt.

    [!NOTE]
    Es gibt ein bekanntes Problem beim Deaktivieren von RC4, das dazu führen kann, dass das System neu gestartet wird. Weitere Informationen finden Sie in den folgenden Hotfixes:
    - [Windows Server 2012 R2](https://support.microsoft.com/kb/3038261)
    - [Windows Server 2012](https://support.microsoft.com/kb/3086213)
    - Für frühere Versionen von Windows Server ist kein Hotfix verfügbar.

- Stellen Sie Domänen auf Windows Server 2012 R2-Domänen Funktionsebene oder höher bereit, und konfigurieren Sie die Benutzer als Mitglieder der Sicherheitsgruppe "geschützte Benutzer". Da dieses Feature mehr als nur die RC4-Verwendung im Kerberos-Protokoll unterbricht, finden Sie weitere Informationen unter Ressourcen [im folgenden Abschnitt](#see-also) .

## <a name="see-also"></a>Siehe auch

- Informationen dazu, wie Sie die Verwendung des RC4-Verschlüsselungs Typs in Windows Server 2012 R2-Domänen verhindern, finden Sie unter [Sicherheitsgruppe "geschützte Benutzer](/../credentials-protection-and-management/protected-users-security-group.md)" und [Konfigurieren geschützter Konten](/../credentials-protection-and-management/how-to-configure-protected-accounts.md).

- Erläuterungen zu RFC 4120 und RFC 4757 finden Sie unter [IETF Documents (IETF-Dokumente](http://tools.ietf.org/html/)).
