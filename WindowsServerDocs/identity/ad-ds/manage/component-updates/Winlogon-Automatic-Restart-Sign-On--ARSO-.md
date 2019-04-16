---
ms.assetid: cb834273-828a-4141-9387-37dd8270e932
title: Windows-Anmeldung automatisch Neustart anmelden (nach einem)
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 27d4285d34105908555458a95bd70fc04fd2901a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="winlogon-automatic-restart-sign-on-arso"></a>Windows-Anmeldung automatisch Neustart anmelden (nach einem)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

**"Author"**: Justin Turner, Senior Support Escalation Engineer mit der Windows-Gruppe

> [!NOTE]
> Dieser Inhalt wird von Microsoft Customer Support-Mitarbeiter geschrieben und richtet erfahrene Administratoren und Systemarchitekten, die als Themen auf TechNet finden Sie in der Regel einen tieferen technischen Einblick Funktionen und Lösungen in Windows Server 2012 R2 suchen. Allerdings hat es nicht die gleichen linguistischen damit einige der Sprache möglicherweise weniger glänzend als was in der Regel auf TechNet-Website gefunden wird.

## <a name="overview"></a>(Übersicht)
Sperrbildschirm-apps, Windows 8 eingeführt.  Hierbei handelt es sich um den Programmen, ausführen und Benachrichtigungen anzeigen, während die Sitzung des Benutzers gesperrt ist (Kalender, Termine, e-Mails und Nachrichten.).  Geräte, die aufgrund der Windows Update-Prozesses neu gestartet werden nicht auf diese Benachrichtigungen bei gesperrtem Bildschirm nach dem Neustart angezeigt.  Einige Benutzer hängen diese Anwendungen sperren.

## <a name="whats-changed"></a>Was hat sich geändert?
Wenn ein Benutzer auf einem Windows 8.1-Gerät anmeldet, speichert LSA die Anmeldeinformationen des Benutzers im verschlüsselten Speicher zugegriffen werden nur von lsass.exe. Wenn Windows Update einen automatischen Neustart ohne Benutzeranwesenheit initiiert, werden diese Anmeldeinformationen verwendet werden, so konfigurieren Sie die automatische Anmeldung für den Benutzer. Windows Update mit TCB-Berechtigung als System ausgeführten initiieren den RPC-Aufruf dazu.

Auf einem Neustart wird der Benutzer automatisch über den Mechanismus für die automatische Anmeldung angemeldet und darüber hinaus zum Schutz der Sitzung des Benutzers gesperrt werden. Das Sperren wird über Windows-Anmeldung initiiert werden, während die Verwaltung von Anmeldeinformationen von LSA ausgeführt wird.  Automatisch anmelden, und den Benutzer auf der Konsole Sperren werden die Anwendungen des Benutzers gesperrten Bildschirm Neustart und Verfügbarkeit.

> [!NOTE]
> Nach dem ein Windows-Update Neustart ausgelöst, der letzte interaktive Benutzer automatisch angemeldet, und die Sitzung gesperrt ist, können also des Benutzers Sperrbildschirm-apps ausführen.

![Windows-Anmeldung](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_LockScreenApp.gif)

![Windows-Anmeldung](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_LockScreen.gif)

**Kurzübersicht**

-   Windows Update Neustart erforderlich ist.

-   Computer neu gestartet wird (*keine apps ausgeführt, die Daten verloren gehen würden*)?

    -   Neustart für Sie

    -   Melden Sie sich wieder in

    -   Sperren

-   Durch eine Gruppenrichtlinie aktiviert oder deaktiviert

    -   In Server-SKUs standardmäßig deaktiviert.

-   Warum?

    -   Einige Updates können nicht abgeschlossen werden, bis der Benutzer wieder anmeldet.

    -   Eine bessere benutzererfahrung: müssen nicht warten Sie 15 Minuten für Updates zum Abschließen der Installation

-   Wie? Die automatische Anmeldung

    -   Speichert das Kennwort, verwendet die Anmeldeinformationen zum Anmelden bei

    -   speichert Anmeldeinformationen als LSA-Schlüssel im Auslagerungsspeicher

    -   Kann nur aktiviert werden, wenn BitLocker aktiviert ist

## <a name="group-policy-sign-in-last-interactive-user-automatically-after-a-system-initiated-restart"></a>Gruppenrichtlinie: Anmeldung letzte interaktive Benutzer automatisch nach einem systeminitiierten Neustart
In Windows 8.1 / Windows Server 2012 R2, die automatische Anmeldung des Benutzers Bildschirm sperren nach ein Neustart von Windows Update wird Abonnieren von Server-SKUs und für die Client-SKUs abmelden.

**Richtlinienspeicherort:** Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Windows-Anmeldeoption

**Richtlinienname:** Anmeldung letzte interaktive Benutzer automatisch nach einem systeminitiierten Neustart

**Unterstützt in:** mindestens Windows Server 2012 R2, Windows 8.1 oder Windows RT 8.1

**Beschreibung/Hilfe:**

Mit dieser richtlinieneinstellung wird gesteuert, ob ein Gerät automatisch die letzten interaktiven Anmeldung wird nach dem Neustart des Systems durch Windows Update.

Wenn Sie aktivieren oder diese Einstellung nicht konfigurieren, wird das Gerät sicher die Anmeldeinformationen des Benutzers (einschließlich der Benutzername, Domäne und das verschlüsselte Kennwort) um die automatische Anmeldung konfigurieren, nach dem Neustart von Windows Update gespeichert. Der Benutzer automatisch angemeldet ist, und die Sitzung automatisch mit allen der Sperrbildschirm-apps für diesen Benutzer konfiguriert gesperrt ist, nach dem Neustart von Windows Update.

Wenn Sie diese Einstellung deaktivieren, speichert das Gerät nicht die Anmeldeinformationen des Benutzers für die automatische Anmeldung, nach dem Neustart von Windows Update. Der Benutzer Sperrbildschirm-apps werden nicht neu gestartet, nach dem Neustart des Systems.

**Registrierungs-Editor**

|Wertname|Typ|Daten|
|--------------|--------|--------|
|DisableAutomaticRestartSignOn|DWORD-WERT|0<br /><br />**Beispiel:**<br /><br />0 (aktiviert)<br /><br />1 (deaktiviert)|

**Richtlinie Registrierungsspeicherort:** HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System

**Typ:** DWORD-Wert

**Registrierungsname:** DisableAutomaticRestartSignOn

Wert: 0 oder 1

0 = aktiviert

1 = deaktiviert

![Windows-Anmeldung](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_SignInPolicy.gif)

## <a name="troubleshooting"></a>Problembehandlung
Beim Windows-Anmeldung automatisch sperrt, wird im Ereignisprotokoll Windows-Anmeldung WinLogon Zustand Trace gespeichert werden.

Der Status der automatischen Anmeldung Konfiguration versucht wird protokolliert.

-   Ist dies erfolgreich

    -   Daher werden

-   Wenn ein Fehler ist:

    -   Zeichnet des Fehlers

-   Wenn die BitLocker Status ändert:

    -   das Entfernen der Anmeldeinformationen werden protokolliert

        -   Diese werden in der LSA-Betriebsprotokoll gespeichert werden.

### <a name="reasons-why-autologon-might-fail"></a>Gründe, warum die automatische Anmeldung möglicherweise nicht
Es gibt mehrere Fälle, in denen eine automatische Anmeldung des Benutzers nicht erreicht werden.  In diesem Abschnitt sollen die bekannten Szenarien erfassen, in denen dies auftreten kann.

### <a name="user-must-change-password-at-next-login"></a>Benutzer muss Kennwort bei der nächsten Anmeldung ändern.
Anmeldung des Benutzers kann einen blockierten Zustand übergeht, wenn eine Änderung des Kennworts bei der nächsten Anmeldung erforderlich ist.  Dies kann vor dem Neustart in den meisten Fällen erkannt, aber nicht alle sein (z. B. Kennwortablauf erreicht werden kann zwischen Herunterfahren und der nächsten Anmeldung.

### <a name="user-account-disabled"></a>Benutzerkonto wurde deaktiviert.
Eine vorhandene Sitzung des Benutzers kann verwaltet werden, auch wenn deaktiviert.  Neustart für ein Konto, das deaktiviert ist kann lokal in den meisten Fällen im Voraus je nach Gp erkannt werden, die möglicherweise nicht für Domänenkonten (einige Domäne zwischengespeichert Anmeldung Szenarien Arbeit, auch wenn das Konto Domänencontroller deaktiviert ist).

### <a name="logon-hours-and-parental-controls"></a>Anmeldezeiten und Jugendschutz
Die Anmeldezeiten und Jugendschutz können verhindern, dass eine neue Sitzung des Benutzers erstellt wird.  Wenn ein Neustart während dieses Fenster auftreten würden, würde der Benutzer nicht zulässig, anmelden.  Zusätzliche Richtlinie, bei dem Sperren oder Abmelden als Aktion Kompatibilität, ist vorhanden.  Dies kann für viele untergeordnete Fälle, in dem Konto Sperrmodus zwischen Bett und Reaktivierung auftreten kann, problematisch sein, insbesondere dann, wenn das Wartungsfenster häufig während dieser Zeit ist.

## <a name="additional-resources"></a>Zusätzliche Ressourcen
**Tabelle SEQ Tabelle \\\ * Arabisch 3: nach einem Glossar**

|Begriff|Definition|
|--------|--------------|
|Die automatische Anmeldung|Die automatische Anmeldung ist ein Feature, das in Windows für mehrere Versionen vorhanden war.  Es ist ein dokumentierten Feature von Windows, die Tools, z. B. die automatische Anmeldung für Windows-v3.01 ist * [http:/technet.microsoft.com/sysinternals/bb963905.aspx](https://technet.microsoft.com/sysinternals/bb963905.aspx)*<br /><br />Sie können einen einzelnen Benutzer des Geräts automatisch anmelden, ohne Anmeldeinformationen eingeben zu müssen. Die Anmeldeinformationen sind konfiguriert und in der Registrierung als verschlüsselte LSA-Schlüssel gespeichert.|


