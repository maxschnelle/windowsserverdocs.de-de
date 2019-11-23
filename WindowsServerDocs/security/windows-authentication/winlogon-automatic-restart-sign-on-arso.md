---
title: Winlogon-Anmeldung nach einem automatischen Neustart
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: f085cf78a01148f97a450577131213ce977a432a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402331"
---
# <a name="winlogon-automatic-restart-sign-on-arso"></a>Winlogon-Anmeldung nach einem automatischen Neustart

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

**Autor**: Justin Turner, Senior Support Eskalations Techniker mit der Windows-Gruppe  
  
> [!NOTE]  
> Dieser Inhalt wurde von einem Mitarbeiter des Microsoft-Kundendiensts geschrieben und richtet sich an erfahrene Administratoren und Systemarchitekten, die einen tieferen technischen Einblick in die Funktionen und Lösungen von Windows Server 2012 R2 suchen, als Ihnen die Themen im TechNet bieten können. Allerdings wurde er nicht mit der gleichen linguistischen Sorgfalt überprüft wie für die Artikel des TechNet üblich, so dass die Sprache gelegentlich holprig klingen mag.  
  
## <a name="overview"></a>Übersicht  
Windows 8 hat Sperrbildschirm-apps eingeführt.  Dies sind die Anwendungen, die Benachrichtigungen ausführen und anzeigen, während die Sitzung des Benutzers gesperrt ist (Kalendertermine, e-Mail und Nachrichten usw.).  Geräte, die aufgrund des Windows Update Prozesses neu gestartet werden, können diese Sperrbildschirm Benachrichtigungen beim Neustart nicht anzeigen.  Einige Benutzer sind von diesen Sperrbildschirm Anwendungen abhängig.  
  
## <a name="whats-changed"></a>Änderungen  
Wenn ein Benutzer sich auf einem Windows 8.1 Gerät anmeldet, speichert LSA die Anmelde Informationen des Benutzers in verschlüsseltem Speicher, auf den nur von "Lsass. exe" zugegriffen werden kann. Wenn Windows Update einen automatischen Neustart ohne Benutzer Präsenz initiiert, werden diese Anmelde Informationen verwendet, um die Authentifizierung für den Benutzer zu konfigurieren. Windows Update, das als System mit TCB-Berechtigung ausgeführt wird, wird der RPC-Aufruf zu diesem Zweck initiiert.  
  
Beim Neustart wird der Benutzer automatisch über den automatischen Authentifizierungsmechanismus angemeldet und anschließend zum Schutz der Benutzersitzung gesperrt. Die Sperrung wird über Winlogon initiiert, während die Verwaltung der Anmelde Informationen von LSA erfolgt.  Wenn Sie den Benutzer in der Konsole automatisch anmelden und sperren, werden die Anwendungen für den Sperrbildschirm des Benutzers neu gestartet und sind verfügbar.  
  
> [!NOTE]  
> Nach einem Windows Update induzierten Neustart wird der letzte interaktive Benutzer automatisch angemeldet, und die Sitzung ist gesperrt, sodass die APP für den Sperrbildschirm des Benutzers ausgeführt werden kann.  
  
![Screenshot mit dem Sperrbildschirm](../media/winlogon-automatic-restart-sign-on-arso/GTR_ADDS_LockScreenApp.gif)  
  
![Screenshot mit den Apps für den Sperrbildschirm](../media/winlogon-automatic-restart-sign-on-arso/GTR_ADDS_LockScreen.gif)  
  
**Kurze Übersicht**  
  
-   Windows Update Neustart erforderlich  
  
-   Kann der Computer neu gestartet werden (es werden*keine apps ausgeführt, die Daten verlieren*)?  
  
    -   Neu starten  
  
    -   Wieder anmelden  
  
    -   Computer sperren  
  
-   Aktiviert oder deaktiviert von Gruppenrichtlinie  
  
    -   In Server-SKUs standardmäßig deaktiviert  
  
-   Weshalb?  
  
    -   Einige Updates können erst abgeschlossen werden, wenn sich der Benutzer wieder anmeldet.  
  
    -   Bessere Benutzer Leistung: Sie müssen nicht 15 Minuten warten, bis die Installation von Updates abgeschlossen ist.  
  
-   Dass? AutoLogon  
  
    -   speichert das Kennwort, verwendet diese Anmelde Informationen für die Anmeldung.  
  
    -   speichert Anmelde Informationen als LSA-Geheimnis im Auslagerungsseiten.  
  
    -   Kann nur aktiviert werden, wenn BitLocker aktiviert ist.  
  
## <a name="group-policy-sign-in-last-interactive-user-automatically-after-a-system-initiated-restart"></a>Gruppenrichtlinie: Letzter interaktiver Benutzer automatisch nach einem vom System initiierten Neustart  
In Windows 8.1/Windows Server 2012 R2 ist die automatische Anmeldung des Benutzers für den Sperrbildschirm nach einem Windows Update Neustart für Server-SKUs vorgesehen und für Client-SKUs zu entscheiden.  
  
**Richtlinien Speicherort:** Computer Konfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Windows-Anmelde Option  
  
**Richtlinien Name:** Letzter interaktiver Benutzer automatisch nach einem vom System initiierten Neustart  
  
**Unterstützt für:** Mindestens Windows Server 2012 R2, Windows 8.1 oder Windows RT 8,1  
  
**Beschreibung/Hilfe:**  
  
Mit dieser Richtlinien Einstellung wird gesteuert, ob ein Gerät den letzten interaktiven Benutzer automatisch anmeldet, nachdem Windows Update das System neu gestartet hat.  
  
Wenn Sie diese Richtlinien Einstellung aktivieren oder nicht konfigurieren, speichert das Gerät die Anmelde Informationen des Benutzers (einschließlich Benutzername, Domäne und verschlüsseltes Kennwort), um die automatische Anmeldung nach einem Windows Update Neustart zu konfigurieren. Nach dem Neustart des Windows Update wird der Benutzer automatisch angemeldet, und die Sitzung wird automatisch mit allen für diesen Benutzer konfigurierten Sperrbildschirm-apps gesperrt.  
  
Wenn Sie diese Richtlinien Einstellung deaktivieren, speichert das Gerät die Anmelde Informationen des Benutzers für die automatische Anmeldung nach einem Windows Update Neustart nicht. Die apps für den Sperrbildschirm des Benutzers werden nach dem Neustart des Systems nicht neu gestartet.  
  
**Registrierungs-Editor**  
  
|Wertname|Typ|Daten|  
|-------|----|----|  
|Disableautomatikrestartsignon|DWORD|0<br /><br />**Beispiel:**<br /><br />0 (aktiviert)<br /><br />1 (deaktiviert)|  
  
**Registrierungs Speicherort der Richtlinie:** Hklm\software\microsoft\windows\currentversion\policies\system  
  
**Typ:** DWORD  
  
**Registrierungs Name:** Disableautomatikrestartsignon  
  
Wert: 0 oder 1  
  
0 = aktiviert  
  
1 = deaktiviert  
  
![Screenshot der Richtlinien Einstellung steuert die Benutzeroberfläche, mit der Sie angeben können, ob ein Gerät automatisch den letzten interaktiven Benutzer anmeldet, nachdem Windows Update das System neu gestartet hat.](../media/winlogon-automatic-restart-sign-on-arso/GTR_ADDS_SignInPolicy.gif)  
  
## <a name="troubleshooting"></a>Problembehandlung  
Wenn Winlogon automatisch gesperrt wird, wird die Zustands Ablauf Verfolgung von Winlogon im Ereignisprotokoll Winlogon gespeichert.  
  
Der Status eines automatischen Konfigurations Versuchs wird protokolliert.  
  
-   Wenn erfolgreich  
  
    -   zeichnet ihn als solche auf  
  
-   Wenn ein Fehler auftritt:  
  
    -   zeichnet den Fehler auf  
  
-   Wenn sich der Status von BitLocker ändert:  
  
    -   das Entfernen von Anmelde Informationen wird protokolliert.  
  
        -   Diese werden im LSA-Betriebsprotokoll gespeichert.  
  
### <a name="reasons-why-autologon-might-fail"></a>Gründe für Fehler bei automatische Anmeldung  
Es gibt mehrere Fälle, in denen der automatische Anmelde Name eines Benutzers nicht erreicht werden kann.  In diesem Abschnitt werden die bekannten Szenarien erfasst, in denen dies vorkommen kann.  
  
### <a name="user-must-change-password-at-next-login"></a>Benutzer muss das Kennwort bei der nächsten Anmeldung ändern  
Die Benutzeranmeldung kann einen blockierten Zustand eingeben, wenn eine Kenn Wort Änderung bei der nächsten Anmeldung erforderlich ist.  Dies kann vor dem Neustart in den meisten Fällen erkannt werden, aber nicht alle (z. b. kann das Kenn Wort Ablauf zwischen dem Herunterfahren und der nächsten Anmeldung erreicht werden.  
  
### <a name="user-account-disabled"></a>Benutzerkonto deaktiviert  
Eine vorhandene Benutzersitzung kann auch dann beibehalten werden, wenn Sie deaktiviert ist.  Der Neustart für ein deaktiviertes Konto kann in den meisten Fällen lokal erkannt werden, abhängig von der Verwendung von Domänen Konten, die nicht für Domänen Konten gelten (einige Domänen zwischengespeicherte Anmelde Szenarios funktionieren auch dann, wenn das Konto auf dem DC deaktiviert ist).  
  
### <a name="logon-hours-and-parental-controls"></a>Anmeldezeiten und Eltern Kontrollen  
Die Anmeldezeiten und die Steuerelement-Steuerelemente können verhindern, dass eine neue Benutzersitzung erstellt wird.  Wenn während dieses Fensters ein Neustart stattfindet, ist der Benutzer nicht berechtigt, sich anzumelden.  Es gibt zusätzliche Richtlinien, die eine Sperr-oder Abmelde Aktion als Konformitäts Aktion verursachen.  Dies könnte für viele untergeordnete Fälle problematisch sein, bei denen eine Kontosperrung zwischen der Zeit des Abrufs und der Reaktivierung auftreten kann, insbesondere, wenn das Wartungsfenster in der Regel während dieser Zeit liegt.  
  
## <a name="additional-resources"></a>Weitere Ressourcen  
**Tabelle \\\* Arabisch 3: ARSO Glossar**  
  
|Begriff|Definition|  
|----|-------|  
|Automatische Anmeldung|Autologon ist ein Feature, das in Windows für mehrere Versionen vorhanden ist.  Dabei handelt es sich um ein dokumentiertes Feature von Windows, das auch Tools wie Autologon für Windows v 3.01  *[http:/technet. Microsoft. com/Sysinternals/bb963905. aspx](https://technet.microsoft.com/sysinternals/bb963905.aspx) enthält.*<br /><br />Dadurch kann sich ein einzelner Benutzer des Geräts automatisch anmelden, ohne Anmelde Informationen einzugeben. Die Anmelde Informationen werden konfiguriert und als verschlüsselter LSA-Schlüssel in der Registrierung gespeichert.|  
  

