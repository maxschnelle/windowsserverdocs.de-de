---
title: "Sicherheitsgruppe \"geschützte Benutzer\""
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="protected-users-security-group"></a>Sicherheitsgruppe "geschützte Benutzer"

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema für IT-Experten beschreibt die Active Directory-Sicherheitsgruppe geschützte Benutzer und erläutert, wie es funktioniert. Diese Gruppe existiert seit Windows Server2012 R2-Domänencontrollern.

## <a name="BKMK_ProtectedUsers"></a>(Übersicht)

Diese Sicherheitsgruppe dient als Teil einer Strategie zum Verwalten der Offenlegung von Anmeldeinformationen innerhalb des Unternehmens. Mitglieder dieser Gruppe gilt automatisch nicht konfigurierbarer Schutz für ihre Konten. Mitgliedschaft in der Gruppe der geschützten Benutzer ist restriktive und proaktive Sicherheit standardmäßig vorgesehen. Die einzige Methode so ändern Sie diese Schutzmaßnahmen für ein Konto ist das Konto aus der Sicherheitsgruppe zu entfernen.

> [!WARNING]
> Konten für Dienste und Computer sollten nie Mitglied der Gruppe der geschützten Benutzer sein. Diese Gruppe würde schützt unvollständig trotzdem, da das Kennwort oder Zertifikat immer auf dem Host verfügbar ist. Authentifizierung schlägt fehl mit Fehler \"the Benutzernamen oder Kennwort ist Incorrect\" für alle Dienste oder Computer, die Gruppe der geschützten Benutzer hinzugefügt wird.

Diese domänenbezogene globale Gruppe löst nicht konfigurierbaren Schutz auf Geräten und Hostcomputern, die unter Windows Server2012 R2 und Windows8.1 oder höher für Benutzer in Domänen mit einem primären Domänencontroller unter Windows Server2012 R2. Dies reduziert erheblich die Standard-Speicherbedarf von Anmeldeinformationen, wenn Benutzer von Computern mit diese Schutzmaßnahmen anmelden.

Weitere Informationen finden Sie unter [wie der geschützten Benutzer funktioniert Gruppe](#BKMK_HowItWorks) in diesem Thema.



## <a name="BKMK_Requirements"></a>Geschützte Benutzer Gruppe Anforderungen
Anforderungen zum Gerät Schutzmaßnahmen für Mitglieder der Gruppe der geschützten Benutzer bereitstellt umfassen Folgendes:

- Die globale Sicherheitsgruppe der geschützten Benutzer wird auf alle Domänencontroller in der Kontodomäne repliziert.

- Windows8.1 und Windows Server2012 R2 unterstützt standardmäßig hinzugefügt. [Microsoft Security Advisory 2871997](https://technet.microsoft.com/library/security/2871997) unterstützt Windows7, Windows Server2008 R2 und Windows Server2012.

Anforderungen für die Domain Controller Schutz für Mitglieder der Gruppe der geschützten Benutzer sind:

- Benutzer müssen in Domänen befinden, die Windows Server2012 R2 oder höher Funktionsebene der Domäne sind.

### <a name="adding-protected-user-global-security-group-to-down-level-domains"></a>Hinzufügen von geschützten Benutzer globale Sicherheitsgruppe Domänen

Domänencontroller, auf denen ein Betriebssystem vor Windows Server2012 R2 können das Hinzufügen von Mitgliedern der neuen Sicherheitsgruppe der geschützten Benutzer unterstützen. Dadurch können die Benutzer profitieren Sie von Gerät Schutzmaßnahmen vor der Aktualisierung der Domäne. 

> [!Note]
> Der Domänencontroller werden keine Domäne Schutzmaßnahmen unterstützen. 

"Geschützte Benutzer" kann erstellt werden, indem Sie [übertragen die Emulatorrolle primärer Domänencontroller (PDC)](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx) auf einen Domänencontroller, der Windows Server2012 R2 ausgeführt wird. Nachdem das Gruppenobjekt auf andere Domänencontroller repliziert wurde, kann der PDC-Emulatorrolle auf einem Domänencontroller gehostet werden, die eine frühere Version von Windows Server ausgeführt wird.

### <a name="BKMK_ADgroup"></a>Eigenschaften von geschützten AD-Gruppe

Die folgende Tabelle gibt die Eigenschaften der Gruppe der geschützten Benutzer.

|Attribut|Wert|
|-------|-----|
|Bekannte SID/RID|S-1-5-21 -<domain>-525|
|Typ|Globale Domäne|
|Standardcontainer|CN = Users, DC =<domain>, DC =|
|Standardmitglieder|Keine|
|Standardmitglied von|Keine|
|Geschützt durch ADMINSDHOLDER?|Nein|
|Speichern, um aus Standardcontainer zu verschieben?|Ja|
|Speichern, um die Verwaltung dieser Gruppe zu Nicht-Dienstadministratoren delegieren?|Nein|
|Standardbenutzerrechte|Keine Standardbenutzerrechte|

## <a name="BKMK_HowItWorks"></a>Funktionsweise der Gruppe "geschützte Benutzer"
In diesem Abschnittwird erläutert, wie die Gruppe geschützte Benutzer beim funktioniert:

-   In einem Windows-Gerät angemeldet

-   Domäne des Benutzerkontos ist in einer Windows Server2012 R2 oder höher Domänenfunktionsebene

### <a name="device-protections-for-signed-in-protected-users"></a>Gerät Schutzmaßnahmen für geschützte Benutzer angemeldet
Wenn der Benutzer Mitglied der Gruppe der geschützten Benutzer ist, werden die folgenden Schutzmaßnahmen angewendet:

-   Anmeldeinformationen (CredSSP)-Delegierung wird nicht Cache, die Nur-Text-Anmeldeinformationen des Benutzers ist es auch bei der **zulassen der Delegierung von Standardanmeldeinformationen** Einstellung der Gruppenrichtlinie aktiviert ist.

-   Ab Windows8.1 und Windows Server2012 R2, wird Windows Digest nicht Nur-Text-Anmeldeinformationen des Benutzers im cache auch wenn Windows Digest aktiviert ist.

> [!Note]
> Nach der Installation von [Microsoft Security Advisory 2871997](https://technet.microsoft.com/library/security/2871997) Windows Digest wird zum Zwischenspeichern von Anmeldeinformationen fortgesetzt, bis der Registrierungsschlüssel konfiguriert ist. Weitere Informationen finden Sie unter [Microsoft-Sicherheitsempfehlung: Update zur Verbesserung der Schutz und Verwaltung von Anmeldeinformationen: 13.Mai 2014](https://support.microsoft.com/en-us/help/2871997/microsoft-security-advisory-update-to-improve-credentials-protection-a) Anweisungen.

-   NTLM wird nicht zwischengespeichert werden Nur-Text-Anmeldeinformationen des Benutzers oder der unidirektionalen NT-Funktion (NTOWF).

-   Kerberos wird nicht mehr des- oder RC4-Schlüssel erstellt. Außerdem wird es nicht im cache Nur-Text-Anmeldeinformationen oder langfristigen Schlüssel des Benutzers nach der anfängliche TGT erworben wurde.

-   Zwischengespeicherte Überprüfung wird beim Anmelden nicht erstellt oder entsperren, sodass Offline-Anmeldung nicht mehr unterstützt wird.

Nachdem das Benutzerkonto zur Gruppe geschützte Benutzer hinzugefügt wurde, beginnt Schutz, wenn der Benutzer auf das Gerät anmeldet.

### <a name="domain-controller-protections-for-protected-users"></a>Domain Controller Schutzmaßnahmen für geschützte Benutzer
Konten, die Mitglieder der Gruppe der geschützten Benutzer sind, die in einem Windows Server2012 R2-Domäne authentifiziert werden konnte nicht:

-   Authentifizieren Sie mit NTLM-Authentifizierung.

-   Verwenden von des- oder RC4-Verschlüsselungstypen in Kerberos-Vorauthentifizierung.

-   Mit uneingeschränkter oder eingeschränkter Delegierung delegiert werden.

-   Erneuern der Kerberos-TGTs außerhalb der ursprünglichen Lebensdauer von vier Stunden.

Nicht konfigurierbare Einstellungen zum Ablauf von TGTs werden für jedes Konto in der Gruppe der geschützten Benutzer eingerichtet. Normalerweise legt der Domänencontroller, der TGTs-Lebensdauer und -Erneuerung, basierend auf den Domänenrichtlinien **Max. Gültigkeitsdauer des Benutzertickets** und **Max. Zeitraum, in dem ein Benutzerticket**. Für die Gruppe der geschützten Benutzer ist 600Minuten für diese Domänenrichtlinien festgelegt.

Weitere Informationen finden Sie unter [How to Configure Protected Accounts](how-to-configure-protected-accounts.md).

## <a name="troubleshooting"></a>Problembehandlung
Zwei operationalen administrationsprotokollen stehen für die Behandlung von Ereignissen, die im Zusammenhang mit geschützten Benutzern zur Verfügung. Diese neuen Protokolle befinden sich in der Ereignisanzeige und sind standardmäßig deaktiviert und befinden sich unter **Anwendungs- und dienstprotokolle\microsoft\windows\microsoft\authentifizierung**.

|Ereignis-ID und Protokoll|Beschreibung|
|----------|--------|
|104<br /><br />**ProtectedUser-Client**|Grund: Das Sicherheitspaket auf dem Client enthält keine Anmeldeinformationen.<br /><br />Der Fehler wird im Clientcomputer protokolliert, wenn das Konto Mitglied der Sicherheitsgruppe der geschützten Benutzer ist. Dieses Ereignis zeigt an, dass das Sicherheitspaket die Anmeldeinformationen nicht zwischenspeichert, die erforderlich sind, um mit dem Server zu authentifizieren.<br /><br />Zeigt den Paketnamen, Benutzernamen, Domänennamen und Servernamen.|
|304<br /><br />**ProtectedUser-Client**|Grund: Das Sicherheitspaket speichert nicht die geschützte Anmeldeinformationen des Benutzers.<br /><br />Ein Ereignis wird protokolliert, auf dem Client, um anzugeben, dass das Sicherheitspaket die Anmeldeinformationen des Benutzers anmelden nicht zwischenspeichert. Es wird erwartet, dass Digest (WDigest), Delegierung der Standardanmeldeinformationen (CredSSP) und NTLM keine Anmeldeinformationen für geschützte Benutzer haben. Anwendungen können weiterhin erfolgreich nach Anmeldeinformationen Fragen.<br /><br />Zeigt den Paketnamen, Benutzernamen und Domänennamen.|
|100<br /><br />**ProtectedUserFailures-DomainController**|Grund: Ein NTLM-Anmeldefehler ereignet sich für ein Konto, das in der Sicherheitsgruppe der geschützten Benutzer ist.<br /><br />Ein Fehler wird protokolliert, auf dem Domänencontroller, um anzugeben, dass die NTLM-Authentifizierung ist fehlgeschlagen, da das Konto Mitglied der Sicherheitsgruppe der geschützten Benutzer.<br /><br />Zeigt den Kontonamen und den Gerätenamen.|
|104<br /><br />**ProtectedUserFailures-DomainController**|Grund: Des- oder RC4-Verschlüsselungstypen werden für die Kerberos-Authentifizierung verwendet, und eine-Anmeldefehler ereignet sich für einen Benutzer in der Sicherheitsgruppe "geschützte Benutzer".<br /><br />Kerberos-Präauthentifizierung ist fehlgeschlagen, da des- und RC4-Verschlüsselungstypen nicht verwendet werden können, wenn das Konto Mitglied der Sicherheitsgruppe der geschützten Benutzer ist.<br /><br />(AES wird akzeptiert.)|
|303<br /><br />**ProtectedUserSuccesses-DomainController**|Grund: Ein Kerberos-Ticket-granting-Ticket (TGT) wurde erfolgreich für ein Mitglied der Gruppe der geschützten Benutzer ausgegeben.|



## <a name="additional-resources"></a>Zusätzliche Ressourcen

-   [Schutz von Anmeldeinformationen und Verwaltung](credentials-protection-and-management.md)

-   [Authentifizierungsrichtlinien und Authentifizierungsrichtliniensilos](authentication-policies-and-authentication-policy-silos.md)

-   [Konfigurieren geschützter Konten](how-to-configure-protected-accounts.md)


