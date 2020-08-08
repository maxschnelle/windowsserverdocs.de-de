---
title: Schutz und Verwaltung von Anmeldeinformationen
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: e457229c-0126-40fe-948c-101c943e1b57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 3dc1d0ae3658e4379d3a358211471ac7f675651c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948703"
---
# <a name="credentials-protection-and-management"></a>Schutz und Verwaltung von Anmeldeinformationen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema für IT-Experten werden die in Windows Server 2012 R2 eingeführten Features und Methoden sowie die Windows 8.1 für den Schutz von Anmelde Informationen und die Domänen Authentifizierung erläutert, um den Diebstahl von Anmelde Informationen zu verringern.

## <a name="BKMK_CredentialsProtectionManagement"></a>
### <a name="restricted-admin-mode-for-remote-desktop-connection"></a>Eingeschränkter Administratormodus für die Remotedesktopverbindung
Der eingeschränkte Administratormodus stellt eine Methode zum interaktiven Protokollieren auf einem Remotehostserver dar, bei dem Ihre Anmeldeinformationen nicht an den Server übermittelt werden. Dadurch wird verhindert, dass Ihre Anmeldeinformationen beim anfänglichen Verbindungsprozess abgefangen werden, wenn der Server gefährdet ist.

Durch die Verwendung dieses Modus mit Administratoranmeldeinformationen versucht der Remotedesktopclient, sich interaktiv auf einem Host anzumelden, der diesen Modus ebenfalls unterstützt, ohne Anmeldeinformationen zu senden. Die Verbindung wird erfolgreich hergestellt, wenn der Host bestätigt hat, dass das Benutzerkonto, das die Verbindung herstellt, über Administratorrechte verfügt und den eingeschränkten Administratormodus unterstützt. Andernfalls schlägt der Verbindungsversuch fehl. Beim eingeschränkten Administratormodus werden Anmeldeinformationen nie als Nur-Text oder in einer anderen wiederverwendbaren Form an Remotecomputer gesendet.

### <a name="lsa-protection"></a>LSA-Schutz
Mithilfe der lokalen Sicherheitsautorität (Local Security Authority, LSA), die sich im LSASS-Prozess (Local Security Authority Security Service, Sicherheitsdienst für die lokale Sicherheitsautorität) befindet, werden Benutzer für die lokale Anmeldung und Remoteanmeldung überprüft und lokale Sicherheitsrichtlinien erzwungen. Das Betriebssystem Windows 8.1 bietet zusätzlichen Schutz für die LSA, um die Code Injektion durch nicht geschützte Prozesse zu verhindern. Dies sorgt für eine erhöhte Sicherheit in Bezug auf Anmeldeinformationen, die von der lokalen Sicherheitsautorität gespeichert und verwaltet werden. Diese geschützte Prozess Einstellung für LSA kann in Windows 8.1 konfiguriert werden, ist in Windows RT 8,1 jedoch standardmäßig aktiviert und kann nicht geändert werden.

Weitere Informationen zum Konfigurieren des LSA-Schutzes finden Sie unter [Configuring Additional LSA Protection](configuring-additional-lsa-protection.md).

### <a name="protected-users-security-group"></a>Sicherheitsgruppe "Geschützte Benutzer"
Diese neue globale Gruppe der Domäne löst neuen, nicht konfigurierbaren Schutz auf Geräten und Host Computern aus, auf denen Windows Server 2012 R2 und Windows 8.1 ausgeführt wird. Die Gruppe "geschützte Benutzer" ermöglicht zusätzlichen Schutz für Domänen Controller und Domänen in Windows Server 2012 R2-Domänen. Dadurch werden die Anmeldeinformationstypen erheblich verringert, die verfügbar sind, wenn Benutzer über einen nicht gefährdeten Computer auf Computern im Netzwerk angemeldet sind.

Mitglieder der Gruppe "Geschützte Benutzer" werden mithilfe der folgenden Authentifizierungsmethoden weiter eingeschränkt:

-   Ein Mitglied der Gruppe "Geschützte Benutzer" kann sich nur über das Kerberos-Protokoll anmelden. Das Konto kann nicht mithilfe von NTLM, Digestauthentifizierung oder CredSSP authentifiziert werden. Auf einem Gerät, auf dem Windows 8.1 ausgeführt wird, werden Kenn Wörter nicht zwischengespeichert, sodass das Gerät, das einen dieser SSPs (Security Support Providers) verwendet, nicht bei einer Domäne authentifiziert werden kann, wenn das Konto Mitglied der Gruppe der geschützten Benutzer ist.

-   Das Kerberos-Protokoll verwendet die schwächeren Verschlüsselungstypen DES oder RC4 nicht im Vorauthentifizierungsprozess. Daher muss die Domäne so konfiguriert werden, dass mindestens die Verschlüsselungssammlung AES unterstützt wird.

-   Das Konto des Benutzers kann nicht mit eingeschränkter oder nicht eingeschränkter Kerberos-Delegierung delegiert werden. Das bedeutet, dass frühere Verbindungen mit anderen Systemen fehlschlagen, wenn der Benutzer Mitglied der Gruppe "Geschützte Benutzer" ist.

-   Die Standardeinstellung für die Lebensdauer von Kerberos-TGTs (Ticket Granting Tickets) von vier Stunden kann mit Authentifizierungsrichtlinien und -silos konfiguriert werden, auf die über das Active Directory-Verwaltungscenter zugegriffen werden kann. Das heißt, dass sich der Benutzer nach Ablauf von vier Stunden erneut authentifizieren muss.

> [!WARNING]
> Konten für Dienste und Computer sollten nicht Mitglieder der Benutzergruppe "Geschützte Benutzer" sein. Diese Gruppe bietet keinen lokalen Schutz, da das Kennwort oder Zertifikat immer auf dem Host verfügbar ist. Die Authentifizierung schlägt mit dem Fehler "der Benutzername oder das Kennwort ist falsch" für jeden Dienst oder Computer fehl, der der Gruppe "geschützte Benutzer" hinzugefügt wird.

Weitere Informationen zu dieser Gruppe finden Sie unter [Sicherheitsgruppe "Geschützte Benutzer"](protected-users-security-group.md).

### <a name="authentication-policy-and-authentication-policy-silos"></a>Authentifizierungsrichtlinie und Authentifizierungsrichtliniensilos
Gesamtstruktur basierte Active Directory Richtlinien werden eingeführt und können auf Konten in einer Domäne mit einer Windows Server 2012 R2-Domänen Funktionsebene angewendet werden. Mit diesen Authentifizierungsrichtlinien kann gesteuert werden, welche Hosts ein Benutzer zum Anmelden verwenden kann. Sie werden in Verbindung mit der Sicherheitsgruppe „Geschützte Benutzer“ verwendet, und Administratoren können auf die Konten Zugriffssteuerungsbedingungen zur Authentifizierung anwenden. Diese Authentifizierungsrichtlinien isolieren zugehörige Konten, um den Gültigkeitsbereich eines Netzwerks zu beschränken.

Mit der neuen Active Directory Objektklasse "Authentifizierungs Richtlinie" können Sie die Authentifizierungs Konfiguration auf Konto Klassen in Domänen mit einer Windows Server 2012 R2-Domänen Funktionsebene anwenden. Authentifizierungsrichtlinien werden während des Austauschs des Authentifizierungsdiensts (Authentication Service, AS) und des Ticket-Granting Service (TGS) des Kerberos-Protokolls erzwungen. Es existieren die folgenden Active Directory-Kontoklassen:

-   Benutzer

-   Computer

-   Verwaltetes Dienstkonto

-   Gruppenverwaltetes Dienstkonto

Weitere Informationen finden Sie unter [Authentifizierungsrichtlinien und Authentifizierungsrichtliniensilos](authentication-policies-and-authentication-policy-silos.md).

Weitere Informationen zum Konfigurieren geschützter Konten finden Sie unter [Konfigurieren geschützter Konten](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/how-to-configure-protected-accounts).

## <a name="additional-references"></a>Weitere Verweise
Weitere Informationen zu LSA und LSASS finden Sie unter [Technische Übersicht über die Windows-Anmeldung und -Authentifizierung](https://technet.microsoft.com/library/dn169029(v=ws.10).aspx).



