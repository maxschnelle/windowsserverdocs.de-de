---
title: Der Benutzer kann sich nicht authentifizieren oder muss sich zweimal authentifizieren
description: Beheben eines Problems, bei dem sich der Benutzer beim Starten einer Remotedesktopverbindung nicht authentifizieren kann oder sich zweimal authentifizieren muss.
audience: itpro
ms.custom: na
ms.reviewer: rklemen
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: kaushika-msft
manager: ''
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 85e332f5f66b59676ddd3b5383b1e5844c2b4c83
ms.sourcegitcommit: f6503e503d8f08ba8000db9c5eda890551d4db37
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/26/2019
ms.locfileid: "68529920"
---
# <a name="user-cant-authenticate-or-must-authenticate-twice"></a>Der Benutzer kann sich nicht authentifizieren oder muss sich zweimal authentifizieren

In diesem Artikel werden Probleme behandelt, die sich auf die Benutzerauthentifizierung auswirken können.

## <a name="access-denied-restricted-type-of-logon"></a>Zugriff verweigert, eingeschränkter Anmeldungstyp

In diesem Fall wird einem Windows 10-Benutzer, der versucht, eine Verbindung mit Windows 10- oder Windows Server 2016-Computern herzustellen, der Zugriff mit der folgenden Meldung verweigert:

> Remotedesktopverbindung:  
> Der Systemadministrator hat den zulässigen Anmeldetyp (Netzwerk oder interaktiv) eingeschränkt. Bitten Sie Ihren Systemadministrator oder den technischen Support um Hilfe.

Dieses Problem tritt auf, wenn für RDP-Verbindungen Authentifizierung auf Netzwerkebene (Network Level Authentication, NLA) vorgeschrieben ist und der Benutzer kein Mitglied der Gruppe **Remotedesktopbenutzer** ist. Es kann ebenfalls auftreten, wenn die Gruppe **Remotedesktopbenutzer** nicht dem Benutzerrecht **Auf diesen Computer vom Netzwerk aus zugreifen** zugewiesen wurde.

Um dieses Problem zu beheben, ergreifen Sie eine der folgenden Maßnahmen:

  - [Ändern der Gruppenmitgliedschaft oder der Zuweisung von Benutzerrechten für den Benutzer](#modify-the-users-group-membership-or-user-rights-assignment).
  - Deaktivieren von NLA (nicht empfohlen).
  - Verwenden anderer Remotedesktopclients als Windows 10. Beispielsweise tritt dieses Problem mit Windows 7-Clients nicht auf.

### <a name="modify-the-users-group-membership-or-user-rights-assignment"></a>Ändern der Gruppenmitgliedschaft oder der Zuweisung von Benutzerrechten für den Benutzer

Wenn dieses Problem einen einzelnen Benutzer betrifft, besteht die geradlinigste Lösung dieses Problems darin, ihn der Gruppe **Remotedesktopbenutzer** zuzuweisen.

Wenn der Benutzer bereits ein Mitglied dieser Gruppe ist (oder wenn mehrere Gruppenmitglieder das gleiche Problem haben), überprüfen Sie die Konfiguration der Benutzerrechte auf dem Windows 10- oder Windows Server 2016-Remotecomputer.

1. Öffnen Sie den Gruppenrichtlinienobjekt-Editor (GPE), und stellen Sie eine Verbindung mit der lokalen Richtlinie des Remotecomputers her.
2. Navigieren Sie zu **Computerkonfiguration\\Windows-Einstellungen\\Sicherheitseinstellungen\\Lokale Richtlinien\\Zuweisen von Benutzerrechten**, klicken Sie mit der rechten Maustaste auf **Auf diesen Computer vom Netzwerk aus zugreifen**, und wählen Sie dann **Eigenschaften** aus.
3. Überprüfen Sie die Liste der Benutzer und Gruppen für **Remotedesktopbenutzer** (oder eine übergeordnete Gruppe).
4. Wenn die Liste **Remotedesktopbenutzer** oder eine übergeordnete Gruppe wie **Jeder** nicht enthält, müssen Sie sie der Liste hinzufügen. Wenn Ihre Bereitstellung mehr als einen Computer enthält, verwenden Sie ein Gruppenrichtlinienobjekt.  
    Beispielsweise schließt die Standardmitgliedschaft für **Auf diesen Computer vom Netzwerk aus zugreifen** **Jeder** ein. Wenn Ihre Bereitstellung ein Gruppenrichtlinienobjekt verwendet, um **Jeder** zu entfernen, müssen Sie möglicherweise den Zugriff wiederherstellen, indem Sie das Gruppenrichtlinienobjekt so aktualisieren, dass **Remotedesktopbenutzer** hinzugefügt werden.

## <a name="access-denied-a-remote-call-to-the-sam-database-has-been-denied"></a>Zugriff verweigert, ein Remoteaufruf der SAM-Datenbank wurde abgelehnt

Dieses Verhalten tritt mit hoher Wahrscheinlichkeit auf, wenn auf Ihren Domänencontrollern Windows Server 2016 oder höher ausgeführt wird und Benutzer versuchen, mithilfe einer benutzerdefinierten Verbindungs-App eine Verbindung herzustellen. Insbesondere wird Anwendungen, die versuchen, auf Profilinformationen von Benutzern in Active Directory zuzugreifen, der Zugriff verweigert.

Dieses Verhalten ist das Ergebnis einer Änderung an Windows. Wenn sich ein Benutzer unter Windows Server 2012 R2 und früheren Versionen bei einem Remotedesktop anmeldet, wendet sich der Remoteverbindungs-Manager (RCM) an den Domänencontroller (DC), um die Konfigurationen abzufragen, die für Remotedesktop für das Benutzerobjekt in Active Directory Domain Services (AD DS) spezifisch sind. Diese Informationen werden auf der Registerkarte „Remotedesktopdienste“ der Eigenschaften eines Benutzerobjekts im MMC-Snap-In Active Directory-Benutzer und -Computer angezeigt.

Ab Windows Server 2016 fragt RCM die Benutzerobjekte in AD DS nicht mehr ab. Wenn Sie die Abfrage von AD DS durch den RCM benötigen, weil Sie die Remotedesktopdienste-Attribute verwenden, müssen Sie die Abfrage manuell aktivieren.

> [!IMPORTANT]  
> Folgen Sie den Schritten in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie sie ändern, [sichern Sie die Registrierung zwecks Wiederherstellung](https://support.microsoft.com/help/322756) für den Fall, dass Probleme auftreten.

Um das RCM-Legacyverhalten auf einem RD-Sitzungshostserver zu aktivieren, konfigurieren Sie die folgenden Registrierungseinträge, und starten Sie dann den **Remotedesktopdienste**-Dienst erneut:  
  - **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Policies\\Microsoft\\Windows NT\\Terminal Services**
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<Winstation-Name\>\\**  
      - Name: **fQueryUserConfigFromDC**
      - Typ: **Reg\_DWORD**
      - Wert: **1** (Dezimal)

Um das RCM-Legacyverhalten auf einem anderen Server als einem RD-Sitzungshostserver zu aktivieren, konfigurieren Sie diese Registrierungseinträge und den folgenden zusätzlichen Registrierungseintrag (und starten Sie den Dienst dann neu):
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server**

Weitere Informationen zu diesem Verhalten finden Sie unter KB 3200967 [Änderungen am Remote-Verbindungs-Manager in Windows Server](https://support.microsoft.com/help/3200967/changes-to-remote-connection-manager-in-windows-server).

## <a name="user-cant-sign-in-using-a-smart-card"></a>Der Benutzer kann sich nicht mit einer Smartcard anmelden

In diesem Abschnitt werden drei häufige Szenarien behandelt, in denen sich ein Benutzer nicht mit einer Smartcard bei einem Remotedesktop anmelden kann.

### <a name="cant-sign-in-with-a-smart-card-in-a-branch-office-with-a-read-only-domain-controller-rodc"></a>Die Anmeldung mit einer Smartcard bei einer Filiale mit einem schreibgeschützten Domänencontroller (RODC) ist nicht möglich

Dieses Problem tritt in Bereitstellungen auf, die einen RDSH-Server an einem Filialstandort beinhalten, der einen RODC verwendet. Der RDSH-Server ist in der Stammdomäne gehostet. Die Benutzer am Filialstandort gehören zu einer Unterdomäne und verwenden Smartcards zur Authentifizierung. Der RODC ist für das Cachen von Benutzerkennwörtern konfiguriert (der RODC gehört zur **Zulässige RODC-Kennwortreplikationsgruppe**). Wenn Benutzer versuchen, sich bei Sitzungen auf dem RDSH-Server anzumelden, erhalten sie Meldungen wie „Der Anmeldeversuch ist ungültig. Dies liegt entweder an einem ungültigen Benutzernamen oder an ungültigen Authentifizierungsinformationen“.

Dieses Problem wird durch das Verfahren verursacht, mit dem der Stamm-DC und der RODC die Verschlüsselung der Benutzeranmeldeinformationen verwalten. Der Stamm-DC verwendet einen Verschlüsselungsschlüssel zum Verschlüsseln der Anmeldeinformationen, und der RODC übergibt den Entschlüsselungsschlüssel an den Client. Wenn ein Benutzer den Fehler „ungültig“ erhält, stimmen die beiden Schlüssel nicht überein.

Dieses Problem können Sie mit einer der folgenden Methoden umgehen:

- Ändern Sie die DC-Topologie, indem Sie die Kennwortzwischenspeicherung auf dem RODC deaktivieren oder einen beschreibbaren Domänencontroller am Filialstandort bereitstellen.
- Verschieben Sie den RDSH-Server in die gleiche untergeordnete Domäne wie die Benutzer.
- Erlauben Sie Benutzern die Anmeldung ohne Smartcards.

Beachten Sie, dass alle diese Lösungen Kompromisse bei der Leistung oder der Sicherheitsstufe verlangen.

### <a name="user-cant-sign-in-to-a-windows-server-2008-sp2-computer-using-a-smart-card"></a>Der Benutzer kann sich bei einem Windows Server 2008 SP2-Computer nicht mit einer Smartcard anmelden

Dieses Problem tritt auf, wenn Benutzer sich bei einem Windows Server 2008 SP2-Computer anmelden, auf dem ein Update mit KB4093227 (2018.4B) ausgeführt wurde. Wenn Benutzer versuchen, sich mithilfe einer Smartcard anzumelden, wird ihnen der Zugriff mit Meldungen wie „Es wurden keine gültigen Zertifikate gefunden. Überprüfen Sie, ob die Karte ordnungsgemäß eingesteckt wurde und formschlüssig passt“ verweigert. Zugleich zeichnet der Windows Server-Computer das Anwendungsereignis „Fehler beim Abrufen eines digitalen Zertifikats von der eingelegten Smartcard. Ungültige Signatur“ auf.

Um dieses Problem zu beheben, aktualisieren Sie den Windows Server-Computer mit der Neuveröffentlichung 2018.06 B von KB 4093227, [Beschreibung des Sicherheitsupdates für das Denial-of-Service-Sicherheitsrisiko beim Windows-Remotedesktopprotokoll (RDP) in Windows Server 2008: 10. April 2018](https://support.microsoft.com/help/4093227/security-update-for-vulnerabilities-in-windows-server-2008)

### <a name="cant-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs"></a>Der Benutzer kann nicht mit einer Smartcard angemeldet bleiben, und der Remotedesktopdienst reagiert nicht

Dieses Problem tritt auf, wenn sich Benutzer bei einem Windows- oder Windows Server-Computer anmelden, für den ein Update mithilfe von KB 4056446 ausgeführt wurde. Der Benutzer ist möglicherweise zunächst in der Lage, sich mithilfe einer Smartcard beim System anzumelden, aber anschließend erhält er eine Fehlermeldung „SCARD\_E\_NO\_SERVICE“. Der Remotecomputer hört möglicherweise auf, zu reagieren.

Um dieses Problem zu umgehen, führen Sie einen Neustart des Remotecomputers durch.

Um dieses Problem zu beheben, aktualisieren Sie den Remotecomputer mit dem passenden Fix:

  - Windows Server 2008 SP2: KB 4090928, [Windows leaks handles in the lsm.exe process and smart card applications may display "SCARD\_E\_NO\_SERVICE" errors](https://support.microsoft.com/help/4090928/scard-e-no-service-errors-when-windows-leaks-handles-in-the-lsm-exe) (Windows verliert Handles im lsm.exe-Prozess, und für Smartcardanwendungen werden möglicherweise SCARD_E_NO_SERVICE-Fehler angezeigt)
  - Windows Server 2012 R2: KB 4103724, [17. Mai 2018 – KB4103724 (Vorschau der monatlichen Zusammenfassung)](https://support.microsoft.com/help/4103724/windows-81-update-kb4103724)
  - Windows Server 2016 und Windows 10, Version 1607: KB 4103720, [17. Mai 2018 – KB4103720 (Betriebssystembuild 14393.2273)](https://support.microsoft.com/help/4103720/windows-10-update-kb4103720)

## <a name="if-the-remote-pc-is-locked-the-user-needs-to-enter-a-password-twice"></a>Wenn der Remotecomputer gesperrt ist, muss der Benutzer das Kennwort zweimal eingeben

Dieses Problem kann auftreten, wenn ein Benutzer versucht, eine Verbindung mit einem Remotedesktop herzustellen, auf dem Windows 10, Version 1709, in einer Bereitstellung ausgeführt wird, in der für RDP-Verbindungen keine Authentifizierung auf Netzwerkebene vorgeschrieben ist. Wenn unter diesen Umständen der Remotedesktop gesperrt wird, muss der Benutzer seine Anmeldeinformationen beim Herstellen der Verbindung zweimal eingeben.

Um dieses Problem zu beheben, führen Sie ein Update des Computers mit Windows 10, Version 1709, mit KB 4343893, [30. August 30, 2018 – KB4343893 (Betriebssystembuild 16299.637)](https://support.microsoft.com/help/4343893/windows-10-update-kb4343893) aus.

## <a name="user-cant-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages"></a>Der Benutzer kann sich nicht anmelden und erhält die Meldungen „Authentifizierungsfehler“ und „CredSSP encryption oracle remediation“ (CredSSP-Verschlüsselung – Oracle-Wartung)

Wenn Benutzer versuchen, sich mit einer beliebigen Version von Windows ab Windows Vista SP2 und höher oder Windows Server 2008 SP2 und höher anzumelden, wird ihnen der Zugriff verweigert, und es werden Meldungen wie die folgenden angezeigt:

```
An authentication error has occurred. The function requested is not supported.
...
This could be due to CredSSP encryption oracle remediation
...
```

„CredSSP-Verschlüsselung – Oracle-Wartung“ bezieht sich auf einen Satz Sicherheitsupdates, die im März, April und Mai 2018 veröffentlicht wurden. CredSSP ist ein Authentifizierungsanbieter, der Authentifizierungsanforderungen für andere Anwendungen verarbeitet. Das Update „3B“ vom 13. März 2018 und nachfolgende Updates befassten sich mit einem Exploit, der es einem Angreifer ermöglichte, Benutzeranmeldeinformationen weiterzuleiten, um Code auf dem Zielsystem auszuführen.

Mit den anfänglichen Updates wurde Unterstützung für das neue Gruppenrichtlinienobjekt Encryption Oracle-Abwehr eingeführt, das die folgenden möglichen Einstellungen aufweist:

  - Vulnerable (Anfällig): Clientanwendungen, die CredSSP verwenden, können ein Fallback auf unsichere Versionen ausführen, jedoch werden die Remotedesktops durch dieses Verhalten möglichen Angriffen ausgesetzt. Dienste, die CredSSP verwenden, akzeptieren Clients, die nicht aktualisiert wurden.
  - Mitigated (Entschärft): Clientanwendungen, die CredSSP verwenden, können kein Fallback auf unsichere Versionen vornehmen, aber Dienste, die CredSSP verwenden, akzeptieren Clients, für die kein Update ausgeführt wurde.
  - Force Updated Clients (Aktualisierte Clients erzwingen): Clientanwendungen, die CredSSP verwenden, können kein Fallback auf unsichere Versionen vornehmen, und Dienste, die CredSSP verwenden, akzeptieren keine ungepatchten Clients. 
    > [!NOTE]
    > Diese Einstellung sollte erst bereitgestellt werden, wenn alle Remotehosts die neueste Version unterstützen.

Mit dem Update vom 8. Mai 2018 wurde die Standardeinstellung der Encryption Oracle-Abwehr von „Vulnerable“ (Anfällig) in „Mitigated“ (Entschärft) geändert. Dank dieser Änderung können Remotedesktopclients, die die Updates enthalten, keine Verbindungen mit Servern herstellen, die nicht über sie verfügen (oder mit aktualisierten Servern, die nicht neu gestartet wurden). Weitere Informationen zu CredSSP-Updates finden Sie unter [KB 4093492](https://support.microsoft.com/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018).

Um dieses Problem zu beheben, aktualisieren Sie alle Systeme, und starten Sie sie neu. Eine vollständige Liste der Updates und weitere Informationen zu Sicherheitsrisiken finden Sie unter [CVE-2018-0886 | CredSSP Remote Code Execution Vulnerability](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2018-0886) (CVE-2018-0886 | CredSSP – Sicherheitsrisiko bei der Remotecodeausführung).

Um dieses Problem bis zum Abschluss der Updates zu umgehen, lesen Sie KB 4093492 wegen Informationen zu den zulässigen Verbindungstypen. Wenn sich keine realisierbaren Alternativen finden, können Sie eins der folgenden Verfahren in Erwägung ziehen:

- Legen Sie für die betroffenen Clientcomputer die Richtlinie „Encryption Oracle-Abwehr“ wieder auf **Vulnerable** (Anfällig) fest.
- Ändern Sie die folgenden Richtlinien im Gruppenrichtlinienordner **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remotedesktopdienste\\Remotedesktop-Sitzungshost\\Sicherheit**:  
  - **Verwendung einer bestimmten Sicherheitsstufe für Remoteverbindungen (RDP) ist erforderlich**: auf **Aktiviert** festlegen und **RDP** auswählen.
  - **Benutzerauthentifizierung mit Authentifizierung auf Netzwerkebene für Remoteverbindungen ist erforderlich**: auf **Deaktiviert** festlegen.
    > [!IMPORTANT]  
    > Durch Ändern dieser Gruppenrichtlinien verringert sich die Sicherheit der Bereitstellung. Es wird empfohlen, sie nur vorübergehend zu verwenden, wenn überhaupt.

Weitere Informationen zum Arbeiten mit Gruppenrichtlinien finden Sie unter [Ändern ein blockierenden Gruppenrichtlinienobjekts](rdp-error-general-troubleshooting.md#modifying-a-blocking-gpo).

## <a name="after-you-update-client-computers-some-users-need-to-sign-in-twice"></a>Nach einem Update von Clientcomputern müssen sich manche Benutzer zweimal anmelden

Wenn sich Benutzer mit einem Computer mit Windows 7 oder Windows 10, Version 1709, bei Remotedesktop anmelden, wird sofort eine zweite Anmeldeaufforderung angezeigt. Dieses Problem tritt auf, wenn der Clientcomputer über die folgenden Updates verfügt:

  - Windows 7: KB 4103718, [8. Mai 2018 – KB4103718 (monatliches Rollup)](https://support.microsoft.com/help/4103718/windows-7-update-kb4103718)
  - Windows 10 1709: KB 4103727, [8. Mai 2018 – KB4103727 (Betriebssystembuild 16299.431)](https://support.microsoft.com/help/4103727/windows-10-update-kb4103727)

Um dieses Problem zu beheben, stellen Sie sicher, dass die Computer, mit denen Benutzer Verbindungen herstellen wollen (ebenso wie RDSH- oder RDVI-Server), alle Updates bis Juni 2018 erhalten haben. Dies schließt die folgenden Updates ein:

  - Windows Server 2016: KB 4284880, [12. Juni 2018 – KB4284880 (Betriebssystembuild 14393.2312)](https://support.microsoft.com/help/4284880/windows-10-update-kb4284880)
  - Windows Server 2012 R2: KB 4284815, [12. Juni 2018 – KB4284815 (monatliches Rollup)](https://support.microsoft.com/help/4284815/windows-81-update-kb4284815)
  - Windows Server 2012: KB 4284855, [12. Juni 2018 – KB4284855 (monatliches Rollup)](https://support.microsoft.com/help/4284855/windows-server-2012-update-kb4284855)
  - Windows Server 2008 R2: KB 4284826, [12. Juni 2018 – KB4284826 (monatliches Rollup)](https://support.microsoft.com/help/4284826/windows-7-update-kb4284826)
  - Windows Server 2008 SP2: KB4056564, [Beschreibung des Sicherheitsupdates für die CredSSP-Remotecodeausführung in Windows Server 2008, und Windows Embedded POSReady 2009 und Windows Embedded Standard 2009: 13. März 2018](https://support.microsoft.com/help/4056564/security-update-for-vulnerabilities-in-windows-server-2008)

## <a name="users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers"></a>Benutzern wird der Zugriff auf eine Bereitstellung verweigert, die Remote Credential Guard mit mehreren RD-Verbindungsbrokern verwendet

Dieses Problem tritt in Hochverfügbarkeits-Bereitstellungen mit zwei oder mehr Remotedesktop-Verbindungsbrokern auf, wenn Windows Defender Remote Credential Guard verwendet wird. Benutzer können sich nicht an Remotedesktops anmelden.

Dieses Problem tritt auf, weil Remote Credential Guard Kerberos für die Authentifizierung verwendet und NTLM einschränkt. Allerdings können die RD-Verbindungsbroker in einer Hochverfügbarkeitskonfiguration mit Lastenausgleich keine Kerberos-Vorgänge unterstützen.

Wenn Sie eine Hochverfügbarkeitskonfiguration mit RD-Verbindungsbrokern mit Lastenausgleich verwenden müssen, können Sie dieses Problem umgehen, indem Sie Remote Credential Guard deaktivieren. Weitere Informationen über das Verwalten von Windows Defender Remote Credential Guard finden Sie unter [Schützen von Remote Desktop-Anmeldeinformationen mit Windows Defender Remote Credential Guard](https://docs.microsoft.com/windows/security/identity-protection/remote-credential-guard#enable-windows-defender-remote-credential-guard).
