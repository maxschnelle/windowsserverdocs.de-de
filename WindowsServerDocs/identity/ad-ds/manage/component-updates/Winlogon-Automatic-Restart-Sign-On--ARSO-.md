---
ms.assetid: cb834273-828a-4141-9387-37dd8270e932
title: Automatische Winlogon-Neustart Anmeldung (ARSO)
description: Wie Sie mit dem automatischen Neustart von Windows die Benutzerproduktivität steigern können.
author: iainfoulds
ms.author: daveba
manager: daveba
ms.reviewer: cahick
ms.date: 08/20/2019
ms.topic: article
ms.openlocfilehash: bbeff22ce85e1c108852a0e978ad56b1e70d10c5
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070542"
---
# <a name="winlogon-automatic-restart-sign-on-arso"></a>Automatische Winlogon-Neustart Anmeldung (ARSO)

Während eines Windows Update müssen benutzerspezifische Prozesse ausgeführt werden, damit das Update fertiggestellt wird. Diese Prozesse erfordern, dass der Benutzer bei seinem Gerät angemeldet ist. Bei der ersten Anmeldung nach dem Initiieren eines Updates müssen die Benutzer warten, bis diese benutzerspezifischen Prozesse abgeschlossen sind, bevor Sie mit der Verwendung Ihres Geräts beginnen können.

## <a name="how-does-it-work"></a>Wie funktioniert dies?

Wenn Windows Update einen automatischen Neustart initiiert, extrahiert ARSO die abgeleiteten Anmelde Informationen des aktuell angemeldeten Benutzers, speichert Sie auf dem Datenträger und konfiguriert die automatische Anmeldung für den Benutzer. Windows Update, das als System mit TCB-Berechtigung ausgeführt wird, wird der RPC-Aufruf zu diesem Zweck initiiert.

Nachdem der endgültige Windows Update neu gestartet wurde, wird der Benutzer automatisch über den automatischen Anmelde Mechanismus angemeldet, und die Sitzung des Benutzers wird mit den beibehaltenen Geheimnissen reaktiviert. Außerdem ist das Gerät gesperrt, um die Sitzung des Benutzers zu schützen. Die Sperrung wird über Winlogon initiiert, während die Verwaltung der Anmelde Informationen von der lokalen Sicherheits Autorität (Local Security Authority, LSA) erfolgt. Bei erfolgreicher Konfiguration und Anmeldung von ARSO werden die gespeicherten Anmelde Informationen sofort von der Festplatte gelöscht.

Wenn Sie den Benutzer in der Konsole automatisch anmelden und sperren, können Windows Update die benutzerspezifischen Prozesse durchführen, bevor der Benutzer zum Gerät zurückkehrt. Auf diese Weise kann der Benutzer sofort mit der Verwendung des Geräts beginnen.

ARSO behandelt nicht verwaltete und verwaltete Geräte anders. Bei nicht verwalteten Geräten wird die Geräteverschlüsselung verwendet, ist aber nicht erforderlich, damit der Benutzer ARSO erhält. Für verwaltete Geräte sind TPM 2,0, secureboot und BitLocker für die Konfiguration von ARSO erforderlich. IT-Administratoren können diese Anforderung über Gruppenrichtlinie außer Kraft setzen. ARSO für verwaltete Geräte ist zurzeit nur für Geräte verfügbar, die mit Azure Active Directory verknüpft sind.

| Windows-Update | Herunterfahren-g-t 0 | Vom Benutzer initiierte Neustarts | APIs mit SHUTDOWN_ARSO/EWX_ARSO-Flags |
|--|--|--|--|
| Verwaltete Geräte: Ja<p>Nicht verwaltete Geräte: Ja | Verwaltete Geräte: Ja<p>Nicht verwaltete Geräte: Ja | Verwaltete Geräte-Nein<p>Nicht verwaltete Geräte: Ja | Verwaltete Geräte: Ja<p>Nicht verwaltete Geräte: Ja |

> [!NOTE]
> Nach einem Windows Update induzierten Neustart wird der letzte interaktive Benutzer automatisch angemeldet, und die Sitzung wird gesperrt. Dies bietet die Möglichkeit, dass die Sperrbildschirm-apps eines Benutzers trotz des Windows Update Neustarts weiterhin ausgeführt werden.

![Seite „Einstellungen“](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/gtr-adds-lockscreenapp.png)

## <a name="policy-1"></a>Richtlinien #1

### <a name="sign-in-and-lock-last-interactive-user-automatically-after-a-restart"></a>Nach einem Neustart automatisch anmelden und letzten interaktiven Benutzer sperren

In Windows 10 ist ARSO für Server-SKUs deaktiviert und für Client-SKUs deaktiviert.

**Speicherort der Gruppenrichtlinie:** Computer Konfigurations > administrative Vorlagen > Windows-Komponenten > Windows-Anmelde Optionen

**InTune-Richtlinie:**

- Plattform: Windows 10 und höher
- Profiltyp: administrative Vorlagen
- Pfad: \Windows components\windows Logon Options

**Unterstützt für:** Mindestens Windows 10, Version 1903

**Beschreibung:**

Mit dieser Richtlinien Einstellung wird gesteuert, ob ein Gerät sich automatisch anmeldet und den letzten interaktiven Benutzer sperrt, nachdem das System neu gestartet wurde, oder nach einem Herunterfahren und einem Kaltstart.

Dies geschieht nur, wenn sich der letzte interaktive Benutzer vor dem Neustart oder dem Herunterfahren nicht abgemeldet hat.

Wenn das Gerät mit Active Directory oder Azure Active Directory verknüpft ist, gilt diese Richtlinie nur für Windows Update Neustarts. Andernfalls gilt dies für Windows Update Neustarts und vom Benutzer initiierte Neustarts und Herunterfahren.

Wenn Sie diese Richtlinien Einstellung nicht konfigurieren, ist Sie standardmäßig aktiviert. Wenn die Richtlinie aktiviert ist, wird der Benutzer automatisch angemeldet, und die Sitzung wird automatisch mit allen Sperrbildschirm-apps gesperrt, die für diesen Benutzer konfiguriert sind, nachdem das Gerät gestartet wurde.

Nachdem Sie diese Richtlinie aktiviert haben, können Sie Ihre Einstellungen über die configautomatikrestartsignon-Richtlinie konfigurieren, die den Modus für die automatische Anmeldung und Sperrung des letzten interaktiven Benutzers nach einem Neustart oder Kaltstart konfiguriert.

Wenn Sie diese Richtlinien Einstellung deaktivieren, wird die automatische Anmeldung vom Gerät nicht konfiguriert. Die apps für den Sperrbildschirm des Benutzers werden nach dem Neustart des Systems nicht neu gestartet.

**Registrierungs-Editor:**

| Wertname | Typ | Daten |
| --- | --- | --- |
| Disableautomatikrestartsignon | DWORD | 0 (ARSO aktivieren) |
|   |   | 1 (ARSO deaktivieren) |

**Registrierungs Speicherort der Richtlinie:** Hklm\software\microsoft\windows\currentversion\policies\system

**Typ:** DWORD

![winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/gtr-adds-signinpolicy.png)

## <a name="policy-2"></a>Richtlinien #2

### <a name="configure-the-mode-of-automatically-signing-in-and-locking-last-interactive-user-after-a-restart-or-cold-boot"></a>Konfigurieren des Modus für das automatische anmelden und Sperren des letzten interaktiven Benutzers nach einem Neustart oder einem Kaltstart

**Speicherort der Gruppenrichtlinie:** Computer Konfigurations > administrative Vorlagen > Windows-Komponenten > Windows-Anmelde Optionen

**InTune-Richtlinie:**

- Plattform: Windows 10 und höher
- Profiltyp: administrative Vorlagen
- Pfad: \Windows components\windows Logon Options

**Unterstützt für:** Mindestens Windows 10, Version 1903

**Beschreibung:**

Mit dieser Richtlinien Einstellung wird die Konfiguration gesteuert, unter der nach einem Neustart oder einem Kaltstart ein automatischer Neustart, eine Anmeldung und eine Sperre erfolgt. Wenn Sie in der Richtlinie "der letzte interaktive Benutzer automatisch nach einem Neustart" die Option "deaktiviert" ausgewählt haben, erfolgt keine automatische Anmeldung, und diese Richtlinie muss nicht konfiguriert werden.

Wenn Sie diese Richtlinien Einstellung aktivieren, können Sie eine der folgenden beiden Optionen auswählen:

1. "Aktiviert, wenn BitLocker aktiviert und nicht angehalten wird" gibt an, dass die automatische Anmeldung und Sperre nur dann erfolgt, wenn BitLocker aktiv ist und während des Neustarts oder herunter Fahrens nicht angehalten wird. Auf persönliche Daten kann auf der Festplatte des Geräts zu diesem Zeitpunkt zugegriffen werden, wenn BitLocker während eines Updates nicht eingeschaltet oder angehalten wird. Durch die BitLocker-Unterbrechung wird der Schutz für Systemkomponenten und Daten vorübergehend aufgehoben, kann jedoch unter bestimmten Umständen erforderlich sein, um die Start kritischen Komponenten erfolgreich zu aktualisieren
   - BitLocker wird bei Updates angehalten, wenn Folgendes gilt:
      - Das Gerät verfügt nicht über TPM 2,0 und PCR7, oder
      - Das Gerät verwendet keine nur-TPM-Schutzvorrichtung.
2. "Immer aktiviert" gibt an, dass die automatische Anmeldung auch dann erfolgt, wenn BitLocker während des Neustarts oder herunter Fahrens deaktiviert oder angehalten wird. Wenn BitLocker nicht aktiviert ist, kann auf der Festplatte auf persönliche Daten zugegriffen werden. Der automatische Neustart und die Anmeldung sollten nur unter dieser Bedingung ausgeführt werden, wenn Sie sicher sind, dass sich das konfigurierte Gerät an einem sicheren physischen Speicherort befindet.

Wenn Sie diese Einstellung deaktivieren oder nicht konfigurieren, wird die automatische Anmeldung standardmäßig auf das Verhalten aktiviert, wenn BitLocker aktiviert und nicht angehalten ist.

**Registrierungs-Editor**

| Wertname | Typ | Daten |
| --- | --- | --- |
| Automatikrestartsignonconfig | DWORD | 0 (ARSO aktivieren, falls sicher) |
|   |   | 1 (ARSO immer aktivieren) |

**Registrierungs Speicherort der Richtlinie:** Hklm\software\microsoft\windows\currentversion\policies\system

**Typ:** DWORD

![winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/arso-policy-setting.png)

## <a name="troubleshooting"></a>Problembehandlung

Wenn Winlogon automatisch gesperrt wird, wird die Zustands Ablauf Verfolgung von Winlogon im Ereignisprotokoll Winlogon gespeichert.

Der Status eines automatischen Konfigurations Versuchs wird protokolliert.

- Wenn erfolgreich
   - zeichnet ihn als solche auf
- Wenn ein Fehler auftritt:
   - zeichnet den Fehler auf
- Wenn sich der Status von BitLocker ändert:
   - das Entfernen von Anmelde Informationen wird protokolliert.
   - Diese werden im LSA-Betriebsprotokoll gespeichert.

### <a name="reasons-why-autologon-might-fail"></a>Gründe für Fehler bei automatische Anmeldung

Es gibt mehrere Fälle, in denen der automatische Anmelde Name eines Benutzers nicht erreicht werden kann.  In diesem Abschnitt werden die bekannten Szenarien erfasst, in denen dies vorkommen kann.

### <a name="user-must-change-password-at-next-login"></a>Benutzer muss das Kennwort bei der nächsten Anmeldung ändern

Die Benutzeranmeldung kann einen blockierten Zustand eingeben, wenn eine Kenn Wort Änderung bei der nächsten Anmeldung erforderlich ist.  Dies kann vor dem Neustart in den meisten Fällen erkannt werden, aber nicht alle (z. b. kann das Kenn Wort Ablauf zwischen dem Herunterfahren und der nächsten Anmeldung erreicht werden.

### <a name="user-account-disabled"></a>Benutzerkonto deaktiviert

Eine vorhandene Benutzersitzung kann auch dann beibehalten werden, wenn Sie deaktiviert ist.  Der Neustart für ein deaktiviertes Konto kann in den meisten Fällen lokal erkannt werden, abhängig von der Verwendung von Domänen Konten, die nicht für Domänen Konten gelten (einige Domänen zwischengespeicherte Anmelde Szenarios funktionieren auch dann, wenn das Konto auf dem DC deaktiviert ist).

### <a name="logon-hours-and-parental-controls"></a>Anmeldezeiten und Eltern Kontrollen

Die Anmeldezeiten und die Steuerelement-Steuerelemente können verhindern, dass eine neue Benutzersitzung erstellt wird.  Wenn während dieses Fensters ein Neustart stattfindet, ist der Benutzer nicht berechtigt, sich anzumelden.  Es gibt zusätzliche Richtlinien, die eine Sperr-oder Abmelde Aktion als Konformitäts Aktion verursachen. Der Status eines automatischen Konfigurations Versuchs wird protokolliert.

## <a name="security-details"></a>Sicherheitsdetails

### <a name="credentials-stored"></a>Gespeicherte Anmelde Informationen

| Kenn Wort Hash | Anmelde Informations Schlüssel | Ticket für Ticket Gewährung | Primäres Aktualisierungs Token |
|--|--|--|--|
| Lokales Konto: Ja | Lokales Konto: Ja | Lokales Konto-Nein | Lokales Konto-Nein |
| MSA-Konto: Ja | MSA-Konto: Ja | MSA-Konto-Nein | MSA-Konto-Nein |
| Azure AD beige hörenden Konto: Ja | Azure AD beige hörenden Konto: Ja | Azure AD beige hörenden Konto-ja (bei Hybrid) | Azure AD beige hörenden Konto: Ja |
| Domänen gebundenes Konto: Ja | Domänen gebundenes Konto: Ja | Domänen gebundenes Konto: Ja | In die Domäne eingebundenes Konto-ja (bei Hybrid) |

### <a name="credential-guard-interaction"></a>Credential Guard-Interaktion

Wenn für ein Gerät Credential Guard aktiviert ist, werden die abgeleiteten geheimen Schlüssel eines Benutzers mit einem Schlüssel verschlüsselt, der für die aktuelle Start Sitzung spezifisch ist. Daher wird ARSO derzeit nicht auf Geräten unterstützt, auf denen Credential Guard aktiviert ist.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

Autologon ist ein Feature, das in Windows für mehrere Versionen vorhanden ist. Dabei handelt es sich um ein dokumentiertes Feature von Windows, das auch Tools wie Autologon für Windows [http:/technet. Microsoft. com/Sysinternals/bb963905. aspx](/sysinternals/downloads/autologon)enthält. Dadurch kann sich ein einzelner Benutzer des Geräts automatisch anmelden, ohne Anmelde Informationen einzugeben. Die Anmelde Informationen werden konfiguriert und als verschlüsselter LSA-Schlüssel in der Registrierung gespeichert. Dies könnte für viele untergeordnete Fälle problematisch sein, bei denen eine Kontosperrung zwischen der Zeit des Abrufs und der Reaktivierung auftreten kann, insbesondere, wenn das Wartungsfenster in der Regel während dieser Zeit liegt.
