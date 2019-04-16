---
title: Schutz von Anmeldeinformationen und Verwaltung
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e457229c-0126-40fe-948c-101c943e1b57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 16cc1f2260bf0552da6902dc3e97de65d29c7931
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="credentials-protection-and-management"></a>Schutz von Anmeldeinformationen und Verwaltung

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema für IT-Experten beschreibt die Funktionen und Methoden, die in Windows Server2012 R2 und Windows8.1 für den Schutz von Anmeldeinformationen und authentifizierungssteuerelemente für Domänen, um den Diebstahl von Anmeldeinformationen zu verringern, eingeführt.

## <a name="BKMK_CredentialsProtectionManagement"></a>
### <a name="restricted-admin-mode-for-remote-desktop-connection"></a>Eingeschränkter Administratormodus für Remote Desktop Connection
Eingeschränkte Administratormodus stellt eine Methode zum interaktiven protokollieren auf einem Remote-Hostserver ohne Ihre Anmeldeinformationen an den Server übertragen. Dadurch wird verhindert, dass Ihre Anmeldeinformationen beim anfänglichen Verbindungsprozess abgefangen werden, wenn der Server gefährdet ist.

Verwenden diesen Modus mit Administratoranmeldeinformationen, versucht der Remotedesktopclient, sich interaktiv auf einem Host anzumelden, die diesen Modus ebenfalls unterstützt, ohne Anmeldeinformationen zu senden. Wenn der Host bestätigt, dass das Benutzerkonto, das Herstellen einer Verbindung über Administratorrechte verfügt und eingeschränkten Administratormodus unterstützt, sollte eine Verbindung hergestellt. Andernfalls schlägt der Verbindungsversuch fehl. Eingeschränkten Administratormodus werden nicht auf den Punkt senden Nur-Text oder anderen wiederverwendbaren Form von Anmeldeinformationen auf Remotecomputern.

### <a name="lsa-protection"></a>LSA-Schutz
Die Local Security Authority (LSA), die sich innerhalb des Prozesses Local Security Authority Security Service (LSASS) befindet, Benutzer für die lokale und remote Anmeldung und Remoteanmeldung überprüft und lokale Sicherheitsrichtlinien. Das Betriebssystem Windows8.1 bietet zusätzlichen Schutz für das Injizieren von Code durch ungeschützte Prozesse zu verhindern. Dies bietet zusätzliche Sicherheit für die Anmeldeinformationen, die der lokalen Sicherheitsautorität gespeichert und verwaltet. Diese geschützte prozesseinstellung für LSA kann in Windows8.1 konfiguriert werden, jedoch ist standardmäßig unter Windows RT 8.1 und kann nicht geändert werden.

Informationen zum Konfigurieren des LSA-Schutzes finden Sie unter [Configuring Additional LSA Protection](configuring-additional-lsa-protection.md).

### <a name="protected-users-security-group"></a>Sicherheitsgruppe "geschützte Benutzer"
Diese neue globale Gruppe der Domäne löst neue nicht konfigurierbaren Schutz auf Geräten und Hostcomputern, die unter Windows Server2012 R2 und Windows8.1. Gruppe der geschützten Benutzer kann zusätzliche Schutzmaßnahmen für Domänencontroller und Domänen in Windows Server2012 R2-Domänen. Dies reduziert erheblich die Typen von Anmeldeinformationen verfügbar, wenn Benutzer auf Computern im Netzwerk von einem nicht gefährdeten Computer angemeldet sind.

Mitglieder der Gruppe der geschützten Benutzer sind beschränkt indem Sie die folgenden Authentifizierungsmethoden:

-   Ein Mitglied der Gruppe der geschützten Benutzer kann nur mit dem Kerberos-Protokoll anmelden. Das Konto kann nicht mithilfe von NTLM, Digestauthentifizierung oder CredSSP authentifizieren. Auf einem Gerät unter Windows8.1 werden Kennwörter nicht zwischengespeichert, sodass das Gerät, das keines dieser Security Support Provider (SSP) verwendet, nicht ausgeführt werden, zu einer Domäne zu authentifizieren, wenn das Konto Mitglied der Gruppe der geschützten Benutzer ist.

-   Das Kerberos-Protokoll wird nicht die schwächeren des- oder RC4-Verschlüsselungstypen bei der Vorauthentifizierung verwendet. Dies bedeutet, dass die Domäne so konfiguriert werden muss, um mindestens die Verschlüsselungssammlung AES unterstützt.

-   Das Konto des Benutzers kann nicht delegiert werden, mit der eingeschränkten und uneingeschränkten Kerberos Delegierung. Dies bedeutet, dass frühere Verbindungen mit anderen Systemen fehlschlagen, wenn der Benutzer Mitglied der Gruppe der geschützten Benutzer ist.

-   Die Standardeinstellung für die Lebensdauer von Kerberos-Ticket Granting Tickets (TGTs) von vier Stunden kann mit Authentifizierungsrichtlinien und Silos zugegriffen über die Active Directory Administrative Center (ADAC) konfiguriert werden. Dies bedeutet, dass bei der vier Stunden vergangen ist, die der Benutzer erneut authentifizieren muss.

> [!WARNING]
> Konten für Dienste und Computer sollten nicht Mitglieder der Gruppe der geschützten Benutzer sein. Diese Gruppe bietet keinen lokalen Schutz, da das Kennwort oder Zertifikat immer auf dem Host verfügbar ist. Authentifizierung schlägt fehl mit Fehler "der Benutzername oder Kennwort ist ungültig" für alle Dienste oder Computer, die Gruppe der geschützten Benutzer hinzugefügt wird.

Weitere Informationen zu dieser Gruppe finden Sie unter [Protected Users Security Group](protected-users-security-group.md).

### <a name="authentication-policy-and-authentication-policy-silos"></a>Authentifizierungsrichtlinie und Authentifizierungsrichtliniensilos
Gesamtstruktur-Active Directory-Richtlinien eingeführt werden, und Konten in einer Domäne mit einer Domänenfunktionsebene von Windows Server2012 R2 angewendet werden können. Diese Authentifizierungsrichtlinien können steuern, welche Hosts ein Benutzer zum Anmelden verwenden kann. Bei der Arbeit in Verbindung mit der Sicherheitsgruppe der Benutzer zu schützen, und Administratoren können auf die Konten zugriffssteuerungsbedingungen zur Authentifizierung anwenden. Diese Authentifizierungsrichtlinien isolieren zugehörige Konten, um den Bereich eines Netzwerks zu beschränken.

Die neue Active Directory-Objektklasse Authentifizierungsrichtlinie, können Sie die Authentifizierungskonfiguration auf Kontoklassen in Domänen mit einer Domänenfunktionsebene von Windows Server2012 R2 gelten. Authentifizierungsrichtlinien werden während der Kerberos AS oder der TGS erzwungen Exchange. Active Directory-Konto-Klassen sind:

-   Benutzer

-   Computer

-   Verwaltetes Dienstkonto

-   Gruppenverwaltetes Dienstkonto

Weitere Informationen finden Sie unter [Authentifizierungsrichtlinien und Authentifizierungsrichtliniensilos](authentication-policies-and-authentication-policy-silos.md).

Weitere Informationen zum Konfigurieren geschützter Konten finden Sie unter [How to Configure Protected Accounts](how-to-configure-protected-accounts.md).

## <a name="see-also"></a>Siehe auch
Weitere Informationen zu LSA und LSASS finden Sie unter der [Windows-Anmeldung und Authentifizierung: technische Übersicht](https://technet.microsoft.com/library/dn169029(v=ws.10).aspx).



