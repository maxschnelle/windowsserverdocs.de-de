---
title: Winlogon-Anmeldung nach einem automatischen Neustart
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: na
ms.suite: na
ms.technology: security-auditing
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15cddcfa-8a8e-45e4-bb76-b8e1a14ceac0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 172eb34fbfdb8a91adf55e35f888e90f5688d0e7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849241"
---
# <a name="winlogon-automatic-restart-sign-on-arso"></a>Winlogon-Anmeldung nach einem automatischen Neustart

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

**Autor**: Justin Turner, Senior Support Escalation Engineer für die Windows-Gruppe  
  
> [!NOTE]  
> Dieser Inhalt wurde von einem Mitarbeiter des Microsoft-Kundendiensts geschrieben und richtet sich an erfahrene Administratoren und Systemarchitekten, die einen tieferen technischen Einblick in die Funktionen und Lösungen von Windows Server 2012 R2 suchen, als Ihnen die Themen im TechNet bieten können. Allerdings wurde er nicht mit der gleichen linguistischen Sorgfalt überprüft wie für die Artikel des TechNet üblich, so dass die Sprache gelegentlich holprig klingen mag.  
  
## <a name="overview"></a>Übersicht  
Windows 8 wurde die Sperre Bildschirm apps eingeführt.  Hierbei handelt es sich um die Anwendungen, die Benachrichtigungen angezeigt, während die Sitzung des Benutzers gesperrt ist und ausgeführt (Kalender, Termine, e-Mail- und Nachrichten.).  Geräte, die aufgrund der Windows Update-Vorgang neu gestartet werden nicht mehr diese Benachrichtigungen bei gesperrtem Bildschirm nach dem Neustart angezeigt.  Einige Benutzer, die diese Sperre Bildschirm-Anwendungen abhängig ist.  
  
## <a name="whats-changed"></a>Änderungen  
Wenn ein Benutzer auf einem Windows 8.1-Gerät anmeldet, speichert der LSA die Anmeldeinformationen des Benutzers im verschlüsselten Speicher zugegriffen werden kann nur von lsass.exe. Wenn Windows Update einen automatischen Neustart ohne Benutzeranwesenheit initiiert wird, werden diese Anmeldeinformationen verwendet werden, so konfigurieren Sie die automatische Anmeldung für den Benutzer. Windows Update als System mit TCB-Berechtigung wird der RPC-Aufruf zu diesem Zweck initiiert.  
  
Beim Neustart wird der Benutzer automatisch über den Mechanismus für die automatische Anmeldung angemeldet sein, und klicken Sie dann darüber gesperrt, um die Sitzung des Benutzers zu schützen. Das Sperren wird über Windows-Anmeldung initiiert werden, während die Verwaltung von Anmeldeinformationen von LSA durchgeführt wird.  Anmeldung automatisch an, und Sperren den Benutzer in der Konsole werden Anwendungen Sperren des Benutzers neu gestartet wurde und verfügbar.  
  
> [!NOTE]  
> Nach dem ein Windows-Update Neustarts verursachte und die letzte interaktive Benutzer automatisch angemeldet wird die Sitzung gesperrt können also auf des Benutzers sperren Bildschirm apps ausführen.  
  
![Screenshot: Sperrbildschirm](../media/winlogon-automatic-restart-sign-on-arso/GTR_ADDS_LockScreenApp.gif)  
  
![Screenshot mit die Sperre Bildschirm apps](../media/winlogon-automatic-restart-sign-on-arso/GTR_ADDS_LockScreen.gif)  
  
**Kurze Übersicht**  
  
-   Windows Update-Neustart erforderlich ist  
  
-   Ist der Computer neu starten (*keine apps ausgeführt, die Daten verlieren würden*)?  
  
    -   Neustart für Sie  
  
    -   Melden Sie sich wieder  
  
    -   Lock-Computer  
  
-   Von der Gruppenrichtlinie aktiviert oder deaktiviert  
  
    -   In Server-SKUs standardmäßig deaktiviert.  
  
-   Weshalb?  
  
    -   Einige Updates abschließen nicht, bis der Benutzer wieder anmeldet.  
  
    -   Bessere Benutzererlebnis: keine Updates für den Abschluss der Installation von 15 Minuten warten, bis  
  
-   Wie? AutoLogon  
  
    -   Speichert das Kennwort, verwendet diese Anmeldeinformationen, um die Anmeldung  
  
    -   speichert Anmeldeinformationen als LSA-Schlüssel in ausgelagerter Speicher  
  
    -   Kann nur aktiviert werden, wenn BitLocker aktiviert ist  
  
## <a name="group-policy-sign-in-last-interactive-user-automatically-after-a-system-initiated-restart"></a>Gruppenrichtlinie: Anmeldung letzten interaktiven Benutzer automatisch nach einem vom System initiierte Neustart  
In Windows 8.1 / Windows Server 2012 R2, die automatische Anmeldung des Benutzers Bildschirm sperren nach ein Neustart des Windows Update ist wurde für Server-SKUs aktivieren und Deaktivieren der für Client-SKUs.  
  
**Richtlinienspeicherort:** Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Option der Windows-Anmeldung  
  
**Richtlinienname:** Anmeldung letzten interaktiven Benutzer automatisch nach einem vom System initiierte Neustart  
  
**Unterstützt auf:** Mindestens WindowsServer 2012 R2, Windows 8.1 oder Windows RT 8.1  
  
**Beschreibung/Hilfe:**  
  
Diese Einstellung steuert, ob ein Gerät automatisch die letzte interaktive Benutzer anmelden wird nach dem Neustart des Systems durch Windows Update-Richtlinie.  
  
Wenn Sie aktivieren oder diese richtlinieneinstellung nicht konfigurieren, speichert das Gerät sicher die Anmeldeinformationen des Benutzers (einschließlich Benutzername, Domäne und das verschlüsselte Kennwort) um die automatische Anmeldung zu konfigurieren, nach dem Neustart eines Windows-Updates. Nach dem Neustart des Windows Update der Benutzer automatisch angemeldet wird, und alle Sperren Bildschirm-Apps, die für diesen Benutzer konfiguriert wird automatisch die Sitzung gesperrt.  
  
Wenn Sie diese richtlinieneinstellung deaktivieren, speichert das Gerät keine Anmeldeinformationen für die automatische Anmeldung des Benutzers, nach dem Neustart eines Windows-Updates. Der Benutzer sperren Bildschirm apps werden nicht neu gestartet, nach dem Neustart des Systems.  
  
**Registrierungs-Editor**  
  
|Wertname|Typ|Daten|  
|-------|----|----|  
|DisableAutomaticRestartSignOn|DWORD|0<br /><br />**Beispiel:**<br /><br />0 (aktiviert)<br /><br />1 (deaktiviert)|  
  
**Registrierungspfad der Richtlinie:** HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System  
  
**Typ:** DWORD  
  
**Registrierungsname:** DisableAutomaticRestartSignOn  
  
Wert: 0 oder 1  
  
0 = aktiviert  
  
1 = deaktiviert  
  
![Screenshot mit Einstellung für die Richtlinie steuert die Benutzeroberfläche, in dem Sie angeben können, ob ein Gerät automatisch die letzte interaktive Benutzer anmelden wird nach dem Neustart des Systems durch Windows Update](../media/winlogon-automatic-restart-sign-on-arso/GTR_ADDS_SignInPolicy.gif)  
  
## <a name="troubleshooting"></a>Problembehandlung  
Bei der Windows-Anmeldung automatisch gesperrt wird, werden im Ereignisprotokoll Windows-Anmeldung WinLogons-Status-Ablaufverfolgung gespeichert.  
  
Der Status eines Versuchs der automatische Konfiguration wird protokolliert.  
  
-   Bei Erfolg  
  
    -   Zeichnet sie als solche  
  
-   Wenn es sich um ein Fehler ist:  
  
    -   zeichnet, was der Fehler aufgetreten  
  
-   Wenn sich BitLockers-Zustand ändert:  
  
    -   das Entfernen der Anmeldeinformationen werden protokolliert  
  
        -   Diese werden in der LSA-Betriebsprotokoll gespeichert werden.  
  
### <a name="reasons-why-autologon-might-fail"></a>Gründe, warum die automatische Anmeldung fehlschlägt  
Es gibt mehrere Fälle, in denen eine automatische Anmeldung der Benutzer nicht erreicht werden.  In diesem Abschnitt soll die bekannten Szenarien zu erfassen, in denen dies auftreten kann.  
  
### <a name="user-must-change-password-at-next-login"></a>Benutzer muss Kennwort bei der nächsten Anmeldung ändern.  
Anmeldung des Benutzers kann einen blockierten Zustand eingeben, wenn eine kennwortänderung bei der nächsten Anmeldung erforderlich ist.  Dies kann vor dem Neustart in den meisten Fällen erkannt, aber nicht alle sein (beispielsweise bei Ablauf des Kennworts erreicht werden kann. zwischen dem Schließen und die nächste Anmeldung.  
  
### <a name="user-account-disabled"></a>Benutzerkonto wurde deaktiviert.  
Auch wenn deaktiviert, kann eine vorhandene benutzersitzung verwaltet werden.  Neustart für ein Konto, das deaktiviert ist kann lokal in den meisten Fällen im voraus, dass je nach Gp erkannt werden, die möglicherweise nicht für Domänenkonten (eine Domäne zwischengespeichert Anmeldung funktionieren, auch wenn das Konto auf dem Domänencontroller deaktiviert ist).  
  
### <a name="logon-hours-and-parental-controls"></a>Anmeldezeiten und Jugendschutz  
Die Anmeldezeiten und Jugendschutz können verhindern, dass eine neue benutzersitzung erstellt wird.  Wenn ein Neustart während dieses Zeitfensters ausgeführt wurden, würde der Benutzer nicht zugelassen anmelden.  Es gibt zusätzliche Richtlinie, die Sperre oder Abmelden als Compliance Aktion bewirkt, dass ein.  Dies kann für viele untergeordnete Fälle, in dem Konto Sperrung zwischen konzentrieren und Reaktivierung auftreten können, problematisch sein, insbesondere, wenn das Wartungsfenster häufig während dieser Zeit ist.  
  
## <a name="additional-resources"></a>Zusätzliche Ressourcen  
**Tabelle SEQ Tabelle \\ \* Arabisch 3: Nach einem-Glossar**  
  
|Begriff|Definition|  
|----|-------|  
|Automatische Anmeldung|Automatische Anmeldung ist ein Feature, das in Windows für mehrere Versionen vorhanden war.  Es ist eine dokumentierte Funktion von Windows, die auch Tools wie z. B. die automatische Anmeldung für Windows-v3.01  *[http:/technet.microsoft.com/sysinternals/bb963905.aspx](https://technet.microsoft.com/sysinternals/bb963905.aspx)*<br /><br />Sie können einen einzelnen Benutzer des Geräts und der automatisch ohne Eingabe von Anmeldeinformationen anmelden. Die Anmeldeinformationen sind konfiguriert und in der Registrierung als verschlüsselte LSA-Schlüssel gespeichert.|  
  

