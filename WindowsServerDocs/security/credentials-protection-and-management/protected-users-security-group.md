---
title: Sicherheitsgruppe „Geschützte Benutzer“
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b0b5180-f65a-43ac-8ef3-66014116f296
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: bd6b53c0febdfb2d344136097a9654c981405568
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862361"
---
# <a name="protected-users-security-group"></a>Sicherheitsgruppe „Geschützte Benutzer“

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema für IT-Experten beschreibt die Active Directory-Sicherheitsgruppe „Geschützte Benutzer“ und erklärt deren Funktionsweise. Diese Gruppe existiert seit Windows Server 2012 R2-Domänencontroller.

## <a name="BKMK_ProtectedUsers"></a>Übersicht über die

Diese Sicherheitsgruppe dient als Teil einer Strategie für die Offenlegung von Anmeldeinformationen in Ihrem Unternehmen zu verwalten. Für Mitglieder dieser Gruppe gilt automatisch nicht konfigurierbarer Schutz für deren Konten. Eine Mitgliedschaft in der Gruppe der geschützten Benutzer bedeutet standardmäßig eine restriktive und proaktive Sicherheit. Die einzige Methode zum Ändern dieses Schutzes für ein Konto ist die Entfernung dieses Kontos aus der Sicherheitsgruppe.

> [!WARNING]
> Konten für Dienste und Computer sollten nie Mitglied der Gruppe geschützte Benutzer sein. Diese Gruppe würde bietet unvollständigen Schutz dennoch da das Kennwort oder Zertifikat immer auf dem Host verfügbar ist. Authentifizierung schlägt fehl mit Fehler \"der Benutzername oder Kennwort ist falsch\" für alle Dienste oder Computer, die Gruppe der geschützten Benutzer hinzugefügt wird.

Diese domänenbezogene globale Gruppe löst nicht konfigurierbaren Schutz auf Geräten und Hostcomputern, die unter Windows Server 2012 R2 und Windows 8.1 oder höher für Benutzer in Domänen mit einem primären Domänencontroller mit Windows Server 2012 R2. Dies reduziert erheblich die Standard-Speicherbedarf von Anmeldeinformationen, wenn Benutzer mit diesen Schutz bei Computern anmelden.

Weitere Informationen finden Sie unter [wie die Gruppe von der geschützten Benutzer auf funktioniert](#BKMK_HowItWorks) in diesem Thema.



## <a name="BKMK_Requirements"></a>Anforderungen für geschützte Benutzer
Anforderungen für die Geräte-Schutz für Mitglieder der Gruppe der geschützten Benutzer sind:

- Die globale Sicherheitsgruppe der geschützten Benutzer wird zu allen Domänencontrollern in der Kontodomäne repliziert.

- Windows 8.1 und Windows Server 2012 R2 unterstützen standardmäßig hinzugefügt. [Microsoft Security Advisory 2871997](https://technet.microsoft.com/library/security/2871997) fügt Unterstützung für Windows 7, Windows Server 2008 R2 und Windows Server 2012.

Folgende Anforderungen müssen erfüllt sein, damit Mitglieder der Gruppe der geschützten Benutzer Domänencontrollerschutz erhalten:

- Benutzer müssen sich in Domänen befinden, die Windows Server 2012 R2 oder höher Funktionsebene der Domäne sind.

### <a name="adding-protected-user-global-security-group-to-down-level-domains"></a>Hinzufügen von Gruppe der geschützten Benutzer globale Sicherheit auf Elementebene Domänen

Domänencontroller, auf denen ein Betriebssystem vor Windows Server 2012 R2 ausgeführt werden können das Hinzufügen von Mitgliedern, die neue Sicherheitsgruppe der geschützten Benutzer unterstützen. Dies ermöglicht Benutzern das Gerät Schutzmaßnahmen profitieren, bevor die Domäne aktualisiert wird. 

> [!Note]
> Die Domänencontroller werden Domäne Schutzmaßnahmen nicht unterstützt werden. 

Gruppe "geschützte Benutzer" erstellt werden kann, indem [übertragen die Emulatorrolle primärer Domänencontroller (PDC)](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx) zu einem Domänencontroller, die Windows Server 2012 R2 ausgeführt wird. Nachdem das Gruppenobjekt auf andere Domänencontroller repliziert wurde, kann die PDC-Emulatorrolle auf einem Domänencontroller gehostet werden, der unter einer älteren Windows Server-Version läuft.

### <a name="BKMK_ADgroup"></a>Geschützte Benutzer AD-Gruppe-Eigenschaften

Die folgende Tabelle zeigt die Eigenschaften der Gruppe der geschützten Benutzer.

|Attribut|Wert|
|-------|-----|
|Gut bekannte SID/RID|S-1-5-21-<domain>-525|
|Typ|Globale Domäne|
|Standardcontainer|CN=Benutzer, DC=<domain>, DC=|
|Standardmitglieder|Keine|
|Standardmitglied von|Keine|
|Geschützt durch ADMINSDHOLDER?|Nein|
|Speichern, um aus Standardcontainer zu entfernen?|Ja|
|Speichern, um die Verwaltung dieser Gruppe zu Nicht-Dienstadministratoren zu delegieren?|Nein|
|Standardbenutzerrechte|Keine Standardbenutzerrechte.|

## <a name="BKMK_HowItWorks"></a>Funktionsweise der Gruppe "geschützte Benutzer"
In diesem Abschnitt wird erklärt, wie die Gruppe der geschützten Benutzer funktioniert, wenn folgende Voraussetzungen erfüllt sind:

-   Angemeldet von einem Windows-Gerät

-   Domäne des Benutzerkontos wird in einer Windows Server 2012 R2 oder höher Domänenfunktionsebene

### <a name="device-protections-for-signed-in-protected-users"></a>Gerät Schutzmaßnahmen für anmelden geschützte Benutzer
Die folgenden Schutzmaßnahmen werden angewendet, wenn der angemeldete Benutzer Mitglied der Gruppe der geschützten Benutzer ist:

-   Anmeldeinformationen (CredSSP)-Delegierung wird nicht zwischenspeichert, die nur-Text-Anmeldeinformationen des Benutzers, wenn auch die **zulassen der Delegierung von Standardanmeldeinformationen** Einstellung der Gruppenrichtlinie aktiviert ist.

-   Ab Windows 8.1 und Windows Server 2012 R2, speichert Windows Digest nicht nur-Text-Anmeldeinformationen des Benutzers auch, wenn Windows Digest aktiviert ist.

> [!Note]
> Nach der Installation von [Microsoft Security Advisory 2871997](https://technet.microsoft.com/library/security/2871997) Windows Digest wird, Anmeldeinformationen zwischenzuspeichern fortgesetzt, bis die Registrierungsschlüssel konfiguriert ist. Finden Sie unter [Microsoft-Sicherheitsempfehlung: Update zur Verbesserung der Schutz von Anmeldeinformationen und Verwaltung: 13. Mai 2014](https://support.microsoft.com/en-us/help/2871997/microsoft-security-advisory-update-to-improve-credentials-protection-a) Anweisungen.

-   NTLM wird nicht nur-Text-Anmeldeinformationen des Benutzers oder der unidirektionalen NT-Funktion (NTOWF) zwischengespeichert werden.

-   Kerberos wird nicht mehr des- oder RC4-Schlüssel erstellen. Auch ist es nicht zwischengespeichert werden nur-Text-Anmeldeinformationen oder in der langfristigen Schlüssel des Benutzers nach das ersten TGT abgerufen wird.

-   Zwischengespeicherte Überprüfung wird bei der Anmeldung bei nicht erstellt oder zu entsperren, damit offline-Anmeldung nicht mehr unterstützt wird.

Nachdem das Benutzerkonto zur Gruppe geschützte Benutzer hinzugefügt wurde, beginnt Schutz, wenn der Benutzer auf dem Gerät anmeldet.

### <a name="domain-controller-protections-for-protected-users"></a>Domain-Controller-Schutzmaßnahmen für geschützte Benutzer
Konten, die Mitglieder der Gruppe der geschützten Benutzer sind, die in einem Windows Server 2012 R2-Domäne authentifiziert werden kann nicht:

-   Authentifizieren mit NTLM-Authentifizierung.

-   Verwenden von DES- oder RC4-Verschlüsselungstypen in Kerberos-Vorauthentifizierung.

-   Delegierung mit eingeschränkter oder nicht eingeschränkter Delegierung.

-   Erneuern der Kerberos-TGTs außerhalb der ursprünglichen Lebensdauer von vier Stunden.

Nicht konfigurierbare Einstellungen zum Ablauf von TGTs werden für jedes Konto in der Gruppe der geschützten Benutzer eingerichtet. Normalerweise legt der Domänencontroller die Lebensdauer und Erneuerung der TGTs basierend auf den Domänenrichtlinien fest, **Max. Gültigkeitsdauer des Benutzertickets** und **Max. Zeitraum, in dem ein Benutzerticket erneuert werden kann**. Für die Gruppe der geschützten Benutzer ist 600 Minuten für diese Domänenrichtlinien eingestellt.

Weitere Informationen finden Sie unter [Konfigurieren geschützter Konten](how-to-configure-protected-accounts.md).

## <a name="troubleshooting"></a>Problembehandlung
Es gibt zwei betriebliche Administrativprotokolle für die Fehlerbehebung von Ereignissen hinsichtlich geschützter Benutzer. Diese neuen Protokolle befinden sich in der Ereignisanzeige und sind standardmäßig deaktiviert. Sie finden Sie unter **Anwendungs- und Dienstprotokolle\Microsoft\Windows\Microsoft\Authentifizierung**.

|Ereignis-ID und Protokoll|Beschreibung|
|----------|--------|
|104<br /><br />**ProtectedUser-Client**|Grund: Das Sicherheitspaket auf dem Client enthält keine Anmeldeinformationen.<br /><br />Der Fehler wird im Clientcomputer protokolliert, wenn das Konto Mitglied der Sicherheitsgruppe der geschützten Benutzer ist. Das Ereignis zeigt an, dass das Sicherheitspaket die Anmeldeinformationen, die für die Serverauthentifizierung erforderlich sind, nicht zwischenspeichert.<br /><br />Zeigt den Paketnamen, Benutzernamen, Domänennamen und den Servernamen an.|
|304<br /><br />**ProtectedUser-Client**|Grund: Das Sicherheitspaket speichert nicht die Anmeldeinformationen des geschützten Benutzers.<br /><br />Ein Ereignis wird protokolliert, auf dem Client, um anzugeben, dass das Sicherheitspaket die Anmeldeinformationen des Benutzers-Anmeldung nicht zwischenspeichert. Es wird erwartet, dass Digest (WDigest), Delegierung von Anmeldeinformationen (CredSSP) und NTLM keine Anmeldeinformationen für geschützte Benutzer haben können. Anwendungen können weiterhin erfolgreich nach Anmeldeinformationen fragen.<br /><br />Zeigt den Paketnamen, Benutzernamen und Domänennamen an.|
|100<br /><br />**ProtectedUserFailures-DomainController**|Grund: Ein NTLM-Anmeldefehler ereignet sich für ein Konto in der Sicherheitsgruppe der geschützten Benutzer.<br /><br />Im Domänencontroller wird ein Fehler protokolliert, um anzugeben, dass die NTLM-Authentifizierung fehlgeschlagen ist, da das Konto Mitglied der Sicherheitsgruppe der geschützten Benutzer ist.<br /><br />Zeigt den Kontonamen und den Gerätenamen an.|
|104<br /><br />**ProtectedUserFailures-DomainController**|Grund: DES- oder RC4-Verschlüsselungstypen werden für die Kerberos-Authentifizierung verwendet, und ein Anmeldefehler ereignet sich für einen Benutzer in der Sicherheitsgruppe der geschützten Benutzer.<br /><br />Kerberos-Vorauthentifizierung ist fehlgeschlagen, da DES- und RC4-Verschlüsselungstypen nicht verwendet werden können, wenn das Konto Mitglied der Sicherheitsgruppe der geschützten Benutzer ist.<br /><br />(AES wird akzeptiert.)|
|303<br /><br />**ProtectedUserSuccesses-DomainController**|Grund: Ein Kerberos-Ticket-Granting-Ticket (TGT) wurde erfolgreich für ein Mitglied der Gruppe der geschützten Benutzer ausgegeben.|



## <a name="additional-resources"></a>Zusätzliche Ressourcen

-   [Schutz und Verwaltung von Anmeldeinformationen](credentials-protection-and-management.md)

-   [Authentifizierungsrichtlinien und Authentifizierungsrichtliniensilos](authentication-policies-and-authentication-policy-silos.md)

-   [Konfigurieren geschützter Konten](how-to-configure-protected-accounts.md)


