---
title: Problembehandlung bei Remotedesktopverbindungen
description: Nach Symptom angeordnete Verfahren zur Problembehandlung
ms.custom: na
ms.reviewer: rklemen;josh.bender
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: jobende
manager: ''
ms.author: v-tea;kaushika;rklemen;josh.bender
ms.date: 02/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8965df09fd57decf7f4a1b6b89861e5a67034a0a
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297399"
---
# Problembehandlung bei Remotedesktopverbindungen
Kurz einige der am häufigsten auftretenden Probleme Remote Desktop Services (RDS) finden Sie unter [häufig gestellte Fragen zu den Remotedesktop-Clients](https://review.docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-client-faq). Dieser Artikel beschreibt verschiedene erweiterte Ansätze für die Behandlung von Verbindungsproblemen. Viele dieser Prozeduren gilt, ob Sie eine einfache Konfiguration, z. B. einem physischen Computer Herstellen einer Verbindung mit einem anderen physischen Computer oder eine komplexere Konfiguration beheben. Einige Verfahren zur Behebung von Problemen, die nur in komplexen Mehrbenutzer-Szenarien auftreten. Weitere Informationen zu den remote Desktopkomponenten und wie sie zusammenarbeiten finden Sie unter [Remote Desktop Services-Architektur](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/desktop-hosting-logical-architecture).

> [!NOTE]  
> Viele der in diesem Artikel beschriebenen Verfahren benötigen Sie auf mehreren Computern zugreifen, von denen einige Sie möglicherweise für den Remotezugriff auf. Weitere Informationen zu Remoteserver-Verwaltungstools und so konfigurieren Sie diese finden Sie unter [Remote Server Administration Tools (RSAT) für Windows-Betriebssystemen](https://support.microsoft.com/en-us/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems).

Identifizieren Sie in der folgenden Liste den Typ der Symptom, das Sie (bzw. Ihre Benutzer) aufgetreten ist.

- [Remotedesktopclient keine Verbindung mehr mit dem remote Desktop, aber es gibt keine bestimmte Symptome oder Nachrichten (allgemeine Schritte zur Problembehandlung)](#no-specific-symptoms-or-messages-general-troubleshooting-steps)
- [Im Remotedesktop-Client kann keine Verbindung mit dem remote Desktop und erhält eine Nachricht "Klasse nicht registriert"](#client-cannot-connect-class-not-registered)
- [Im Remotedesktop-Client kann keine Verbindung mit dem remote Desktop und erhält einen "keine Lizenzen verfügbar" oder "Sicherheit" Fehlermeldung](#client-cannot-connect-no-licenses-available)
- [Der Benutzer erhält eine "Zugriff verweigert" angezeigt oder Anmeldeinformationen muss zweimal bereitstellen.](#user-cannot-authenticate-or-must-authenticate-twice)
- [Zum Herstellen einer Verbindung, die erhält eine Nachricht "Remote Desktop Service ist derzeit ausgelastet"](#on-connecting-user-receives-remote-desktop-service-is-currently-busy-message)
- [Remotedesktopclient trennt und kann nicht in der gleichen Sitzung wiederherstellen](#rd-client-disconnects-and-cannot-reconnect-to-the-same-session)
- [Der Benutzer stellt eine Verbindung mit einem remote Laptop über ein drahtloses Netzwerk, und klicken Sie dann den Laptop trennt über das Netzwerk](#remote-laptop-disconnects-from-wireless-network).
- [Das Benutzererlebnis eine schlechte Leistung oder Probleme mit dem remote-Anwendungen](#user-experiences-poor-performance-or-application-problems)

> [!NOTE]  
> Eine aktuelle Liste der RDP zum Trennen-Codes finden Sie unter [ExtendedDisconnectReasonCode-Enumeration](https://docs.microsoft.com/en-us/windows/desktop/TermServ/extendeddisconnectreasoncode). 

## Keine spezifischen Symptome oder Nachrichten (allgemeine Schritte zur Problembehandlung)

Verwenden Sie diese Schritte aus, wenn ein Remotedesktop-Client keine mit einem Remotedesktop Verbindung kann jedoch keine Nachrichten oder andere Symptome, die dabei helfen bietet, würde die Ursache. Um viele der Hauptursachen für diese Art von Problem zu beheben, verwenden Sie die folgenden Methoden:

- [Überprüfen Sie den Status des RDP-Protokolls](#check-the-status-of-the-rdp-protocol)
- [Überprüfen Sie den Status der RDP-Dienste](#check-the-status-of-the-rdp-services)
- [Überprüfen der Funktionsweise des RDP-Listeners](#check-that-the-rdp-listener-is-functioning)
- [Überprüfen Sie die RDP-Listener-port](#check-the-rdp-listener-port)

### Überprüfen Sie den Status des RDP-Protokolls

#### Überprüfen Sie den Status des RDP-Protokolls auf einem lokalen computer

Um zu überprüfen, und ändern Sie den Status des RDP-Protokolls auf einem lokalen Computer, finden Sie unter [den Remotedesktop aktivieren](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#how-to-enable-remote-desktop).

> [!NOTE]  
> Wenn die remote desktop Optionen nicht verfügbar sind, finden Sie unter [überprüfen, ob ein Gruppenrichtlinienobjekt RDP blockiert](#check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer).

#### Überprüfen Sie den Status des RDP-Protokolls auf einem Remotecomputer

> [!IMPORTANT]  
> Die Schritte in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Vor dem Ändern Sie es, [Sichern Sie die Registrierung für die Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Sie Probleme auftreten.

Verwenden Sie zum Suchen, und ändern Sie den Status des RDP-Protokolls auf einem Remotecomputer, eine Netzwerkverbindung für die Registrierung:

1. Wählen Sie **Starten**, wählen Sie **Ausführen**, und geben Sie **regedt32**.
2. Wählen Sie im Registrierungs-Editor die **Datei**, und wählen Sie dann die **Netzwerk-Registrierung verbinden**.
3. Klicken Sie in das Dialogfeld **Computer auswählen** Geben Sie den Namen des Remotecomputers, wählen Sie **Namen überprüfen**, und wählen Sie dann auf **OK**.
4. Navigieren Sie zum **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server**.  
   ![Registrierungs-Editor mit der fDenyTSConnections-Eintrag](..\media\troubleshoot-remote-desktop-connections\RegEntry_fDenyTSConnections.png)
   - Wenn der Wert des Schlüssels **fDenyTSConnections** **0**ist, ist RDP aktiviert.
   - Wenn der Wert des Schlüssels **fDenyTSConnections** **1**ist, ist RDP deaktiviert.
5. Um RDP zu aktivieren, ändern Sie den Wert der **fDenyTSConnections** von **1** auf **0 fest**.

#### Überprüfen Sie, ob ein Gruppenrichtlinienobjekt (GPO) auf einem lokalen Computer RDP blockiert

Wenn Sie nicht in der Benutzeroberfläche RDP aktivieren oder der Wert des **fDenyTSConnections** auf **1** wird zurückgesetzt, nachdem Sie es nicht geändert haben, kann ein Gruppenrichtlinienobjekt die Computerebene Einstellungen überschreiben.

Um die Gruppenrichtlinienkonfiguration auf einem lokalen Computer zu überprüfen, öffnen Sie ein Eingabeaufforderungsfenster als Administrator, und geben Sie den folgenden Befehl aus:
```
gpresult /H c:\gpresult.html
```
Öffnen Sie nach Abschluss dieses Befehls gpresult.html. Finden Sie im **Computer computerkonfiguration\\administrative vorlagen\\windows Components\\Remote Desktop Services\\Remote Desktop Sitzung Host\\Connections**die Richtlinie **Benutzern erlauben, Remote mithilfe der Remotedesktopdienste herzustellen** .

- Wenn die Einstellung für diese Richtlinie **aktiviert**ist, wird der Gruppenrichtlinie RDP-Verbindungen nicht blockiert.
- Wenn die Einstellung für diese Richtlinie **deaktiviert**ist, überprüfen Sie **Ausschlaggebende Gruppenrichtlinienobjekt**. Dies ist das Gruppenrichtlinienobjekt, das RDP-Verbindungen blockiert.
![Eine Beispiel-Segment der gpresult.html, in denen das Gruppenrichtlinienobjekt auf Domänenebene ** Block RDP ** ist RDP deaktivieren.](..\media\troubleshoot-remote-desktop-connections\GPResult_RDSH_Connections_GP.png)
   
  ![Eine Beispiel-Segment der gpresult.html, in denen ** lokale Gruppe Richtlinie ** ist RDP deaktivieren.](..\media\troubleshoot-remote-desktop-connections\GPResult_RDSH_Connections_LGP.png)

#### Überprüfen Sie, ob ein Gruppenrichtlinienobjekt RDP auf einem Remotecomputer blockiert

Um die Gruppenrichtlinien-Konfiguration auf einem Remotecomputer zu überprüfen, ist der Befehl fast genauso wie bei einem lokalen Computer:
```
gpresult /S <computer name> /H c:\gpresult-<computer name>.html
```
Die Datei, die diesen Befehl erzeugt (**Gpresult-\<computer name\>.html**) verwendet das gleiche Informationsformat, wie die lokalen Computer-Version (**gpresult.html**) verwendet.

#### Eine blockierende GPO ändern

Sie können diese Einstellungen in der Gruppe Richtlinie Objekt-Editor (GPE) und Group Policy Management Console (GPM) ändern. Weitere Informationen zum Verwenden von Gruppenrichtlinien finden Sie unter [Advanced Group Policy Management](https://docs.microsoft.com/en-us/microsoft-desktop-optimization-pack/agpm/).

Um die blockierende Richtlinie zu ändern, verwenden Sie eine der folgenden Methoden:

- In GPE, die geeignete Sicherheitsstufe des Gruppenrichtlinienobjekts (z. B. lokal oder Domäne), und navigieren Sie zu **Computer computerkonfiguration\\administrative vorlagen\\windows Components\\Remote Desktop Services\\Remote Desktop Sitzung Host\\Connections**\\**Zulassen Benutzern die Remoteverbindung mit Remote Desktop Services**.  
   1. Legen Sie die Richtlinie **aktiviert** oder **Nicht konfiguriert**.
   2. Klicken Sie auf den betroffenen Computern öffnen Sie ein Eingabeaufforderungsfenster als Administrator, und führen Sie den Befehl **Gpupdate/force** .
- Navigieren Sie in GPM zu der Organisationseinheit, in denen die blockierende Richtlinie auf die betroffenen Computer angewendet wird, und löschen Sie die Richtlinie aus der Organisationseinheit.

### Überprüfen Sie den Status der RDP-Dienste

Auf dem Computer lokal (Client) und dem Computer Remotecomputer (Ziel) sollten die folgenden Dienste ausgeführt werden:

- Remotedesktopdienste (TermService)
- Remote Desktop Services Benutzermodus-Port-Redirector (UmRdpService)

Sie können das Dienste-MMC-Snap-in verwenden, Sie um die Dienste lokal oder Remote zu verwalten. Sie können PowerShell auch verwenden, lokal oder Remote (wenn der Remotecomputer konfiguriert ist, um remote PowerShell-Befehle zu akzeptieren).

![Remotedesktopdienste in der Dienste-MMC-Snap-in. Ändern Sie die Standardeinstellungen für den Dienst nicht.](..\media\troubleshoot-remote-desktop-connections\RDSServiceStatus.png)

Auf einem der Computer Wenn einer oder beide Dienste nicht ausgeführt werden, starten Sie sie.

> [!NOTE]  
> Wenn Sie den Remotedesktop-Services-Dienst zu starten, klicken Sie auf **Ja,** um den Remote Desktop Services Benutzermodus Port-Redirector-Dienst automatisch neu starten.

### Überprüfen der Funktionsweise des RDP-Listeners

> [!IMPORTANT]  
> Die Schritte in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Vor dem Ändern Sie es, [Sichern Sie die Registrierung für die Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Sie Probleme auftreten.

#### Überprüfen Sie den Status des Listeners RDP

Verwenden Sie bei diesem Verfahren eine PowerShell-Instanz, die über Administratorrechte verfügt. Für einen lokalen Computer können Sie auch eine Befehlszeile verwenden, die über Administratorrechte verfügt. Bei diesem Verfahren verwendet jedoch PowerShell, da die gleichen Befehle sowohl lokal als auch Remote funktionieren.

1. Öffnen Sie ein PowerShell-Fenster. Geben Sie die Verbindung mit einem Remotecomputer **Enter-PSSession-Computername \<computer name\>**.
2. Geben Sie **Qwinsta**. 
    ![Der Qwinsta-Befehl listet die Prozesse, die auf die Anschlüsse des Computers.](..\media\troubleshoot-remote-desktop-connections\WPS_qwinsta.png)
3. Enthält die Liste **Rdp-TCP-** mit dem Status **hören**, wird die RDP-Listener arbeiten. Fahren Sie mit [den RDP-Listener-Port überprüfen](#check-the-rdp-listener-port). Andernfalls fahren Sie unter Schritt 4.
4. Exportieren Sie die RDP-Listener-Konfiguration von einem Arbeitscomputer.
    1. Melden Sie sich bei einem Computer mit der gleichen Version des Betriebssystems wie die betroffene Computer verfügt und Zugriff auf Registrierung des Computers (z. B. mithilfe der Registrierungs-Editor).
    2. Navigieren Sie zu den folgenden Registrierungseintrag:  
        **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\RDP-Tcp**
    3. Exportieren Sie den Eintrag in einer REG-Datei. Z. B. im Registrierungs-Editor mit der rechten Maustaste in des Eintrags **Exportieren**wählen und geben Sie einen Dateinamen für die exportierten Einstellungen.
    4. Kopieren Sie die exportierte REG-Datei auf den betroffenen Computer.
5. Um die RDP-Listener-Konfiguration importieren möchten, öffnen Sie ein PowerShell-Fenster, das über Administratorrechte auf dem betreffenden Computer verfügt (oder öffnen Sie das PowerShell-Fenster, und eine Remoteverbindung zu dem betreffenden Computer).
   1. Um die vorhandenen Registrierungseintrag sichern, geben Sie den folgenden Befehl ein:  
   
      ```powershell  
      cmd /c 'reg export "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp" C:\Rdp-tcp-backup.reg'   
      ```  
   

   2. Um die vorhandenen Registrierungseintrag zu entfernen, geben Sie die folgenden Befehle ein:  
   
      ```powershell  
      Remove-Item -path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp' -Recurse -Force  
      ```
   
   3. Um den neuen Registrierungseintrag importieren, und starten Sie den Dienst, geben Sie die folgenden Befehle ein:  
   
      ```powershell  
      cmd /c 'regedit /s c:\<filename>.reg'  
      Restart-Service TermService -Force  
      ```   
      wobei \<filename\> der Name der exportierte REG-Datei ist.
6. Testen Sie die Konfiguration, indem Sie die Remotedesktopverbindung erneut versuchen. Wenn Sie noch keine Verbindung herstellen können, starten Sie den betroffenen Computer.
7. Wenn Sie immer noch kann keine Verbindung herstellen, [Überprüfen Sie den Status des RDP selbstsignierten Zertifikats](#check-the-status-of-the-rdp-self-signed-certificate).

#### Überprüfen Sie den Status des RDP selbstsignierten Zertifikats

1. Wenn Sie noch keine Verbindung herstellen können, öffnen Sie das Zertifikat-MMC-Snap-in. Wenn Sie werden aufgefordert, den Zertifikatspeicher verwalten, wählen Sie **Computerkonto**auszuwählen, und wählen Sie dann den betroffenen Computer.
2. Löschen Sie im Ordner " **Zertifikate** " unter **Remotedesktop**das selbstsignierte Zertifikat für RDP. 
    ![Remote Desktop Zertifikate in das MMC-Zertifikate-Snap-in.](..\media\troubleshoot-remote-desktop-connections\MMCCert_Delete.png)
3. Starten Sie auf dem betreffenden Computer der Remote Desktop Services-Dienst neu.
4. Aktualisieren Sie das Zertifikate-Snap-in.
5. Wenn das selbstsignierte Zertifikat für RDP wurde nicht neu erstellt werden, [Überprüfen Sie die Berechtigungen des Ordners MachineKeys](#check-the-permissions-of-the-machinekeys-folder).

#### Überprüfen Sie die Berechtigungen des Ordners MachineKeys

1. Klicken Sie auf dem betreffenden Computer öffnen Sie Explorer, und navigieren Sie zu **C:\\ProgramData\\Microsoft\\Crypto\\RSA\\**.
2. Mit der rechten Maustaste **MachineKeys**, **Eigenschaften**auswählen, wählen Sie **Sicherheit**, und wählen Sie dann **Erweitert**.
3. Stellen Sie sicher, dass die folgenden Berechtigungen konfiguriert werden:
      - Builtin\\Administrators: Vollzugriff
      - Jeder: Lesen, schreiben

### Überprüfen Sie die RDP-Listener-port

Auf dem Computer lokal (Client) und dem Computer Remotecomputer (Ziel) sollte die RDP-Listener Port 3389 überwachen. Keine anderen Anwendungen sollten diesen Port verwenden.

> [!IMPORTANT]  
> Die Schritte in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Vor dem Ändern Sie es, [Sichern Sie die Registrierung für die Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Sie Probleme auftreten.

Verwenden Sie zum Überprüfen oder ändern Sie die RDP-Port, Registrierungs-Editor:

1. Wählen Sie Start, wählen Sie **Ausführen**, und geben Sie **regedt32**.
      - Um eine Verbindung mit einem Remotecomputer herstellen, wählen Sie die **Datei**, und wählen Sie dann die **Netzwerk-Registrierung verbinden**.
      - Klicken Sie in das Dialogfeld **Computer auswählen** Geben Sie den Namen des Remotecomputers, wählen Sie **Namen überprüfen**, und wählen Sie dann auf **OK**.
2. Öffnen Sie die Registrierung, und navigieren Sie zu **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<listener\>**. 
    ![Die Portnummer Unterschlüssel für das RDP-Protokoll.](..\media\troubleshoot-remote-desktop-connections\RegEntry_PortNumber.png)
3. Wenn **PortNumber** einen anderen Wert als **3389**verfügt, ändern Sie es in **3389**. 
   > [!IMPORTANT]  
    > Sie können Remote Desktop Services mit einem anderen Anschluss betreiben. Jedoch empfohlen nicht, dass Sie dies tun. Problembehandlung bei einer solchen Konfiguration ist nicht Gegenstand dieses Artikels.
4. Nachdem Sie die Portnummer ändern, starten Sie den Remotedesktop-Services-Dienst neu.

#### Überprüfen Sie, dass eine andere Anwendung nicht versucht, den gleichen Port verwenden

Verwenden Sie bei diesem Verfahren eine PowerShell-Instanz, die über Administratorrechte verfügt. Für einen lokalen Computer können Sie auch eine Befehlszeile verwenden, die über Administratorrechte verfügt. Bei diesem Verfahren verwendet jedoch PowerShell, da die gleichen Befehle lokal und Remote funktionieren.

1. Öffnen Sie ein PowerShell-Fenster. Geben Sie die Verbindung mit einem Remotecomputer **Enter-PSSession-Computername \<computer name\>**.
2. Geben Sie den folgenden Befehl ein:  
   
     ```powershell  
    cmd /c 'netstat -ano | find "3389"'  
    ```
  
    ![Der Befehl Netstat erzeugt eine Liste von Ports und die Dienste überwacht.](..\media\troubleshoot-remote-desktop-connections\WPS_netstat.png)
1. Suchen Sie nach einem Eintrag für TCP-Port 3389 (oder den zugewiesenen RDP-Port), mit dem Status der **Spracherkennung**. 
    > [!NOTE]  
   > Die PID (Prozess-ID) des Prozesses oder Dienst mit diesem Port wird unter der Spalte "PID" angezeigt.
1. Um zu ermitteln, welche Anwendung Port 3389 (oder den zugewiesenen RDP-Port) verwendet wird, geben Sie den folgenden Befehl ein:  
   
     ```powershell  
    cmd /c 'tasklist /svc | find "<pid listening on 3389>"'  
    ```  
  
    ![Mit dem Befehl Tasklist meldet Details zu einem bestimmten Prozess.](..\media\troubleshoot-remote-desktop-connections\WPS_tasklist.png)
1. Suchen Sie nach einem Eintrag für die Produkt-ID, die den Port (aus der **Netstat** -Ausgabe) zugeordnet ist. Die Dienste oder Prozesse, die diese PID zugeordnet sind werden auf der rechten Seite angezeigt.
1. Wenn eine Anwendung oder einem anderen Dienst als Remote Desktop Services (TermServ.exe) den Port verwendet, können Sie den Konflikt auflösen, indem Sie eine der folgenden Methoden:
      - Konfigurieren Sie die andere Anwendung oder den Dienst um einen anderen Port (empfohlen) verwenden.
      - Deinstallieren Sie die andere Anwendung oder den Dienst.
      - Konfigurieren von RDP, um einen anderen Port verwenden, und starten Sie den Remotedesktop-Services-Dienst (nicht empfohlen).

#### Überprüfen Sie, ob eine Firewall den RDP-Port blockiert

Verwenden Sie das Tool **Psping** , um zu testen, ob Sie die betroffenen Computer mithilfe von Port 3389 erreichen können.

1. Laden Sie auf einem Computer, die von der betroffene Computer unterscheidet, **Psping** von <https://live.sysinternals.com/psping.exe>.
2. Öffnen Sie ein Eingabeaufforderungsfenster als Administrator, ändern Sie in das Verzeichnis, in dem Sie **Psping**installiert haben, und geben Sie den folgenden Befehl aus:  
   
   ```  
   psping -accepteula <computer IP>:3389  
   ```
   
3. Überprüfen Sie die Ausgabe des Befehls **Psping** für Ergebnisse wie folgt:  
      - **Herstellen einer Verbindung mit \<computer IP\>**: der Remotecomputer erreichbar ist.
      - **(0 % Verlust)**: alle Versuche zum Verbinden erfolgreich war.
      - **Der Remotecomputer hat die Netzwerkverbindung abgelehnt**: der Remotecomputer ist nicht erreichbar.
      - **(100 % Verlust)**: alle Versuche zum Verbinden fehlgeschlagen ist.
1. Führen Sie **Psping** auf mehreren Computern, die ihre Fähigkeit zum Herstellen einer des betroffenen Computers zu testen.
1. Beachten Sie, ob der betroffene Computer Verbindungen von allen anderen Computern, einige andere Computer- oder nur einen anderen Computer blockiert.
1. Empfohlene nächste Schritte:
      - Erreichen Sie Ihre Netzwerkadministratoren, um sicherzustellen, dass das Netzwerk RDP-Datenverkehr auf den betroffenen Computer ermöglicht.
      - Untersuchen Sie die Konfigurationen der Firewalls zwischen der Quell- und der betroffene Computer (einschließlich Windows-Firewall auf dem betreffenden Computer), um festzustellen, ob eine Firewall den RDP-Port blockiert.

## Client kann keine Verbindung herstellen, "Klasse nicht registriert"

Beim Herstellen einer mit einem Remotecomputer Verbindung mithilfe von einem Client mit Windows 10, Version 1709 oder höher, der Client möglicherweise nicht verbunden, während der Remotedesktop-Sitzungshost-Server eine Nachricht meldet enthält, die den Fehlercode "Klasse nicht registriert (0 x 80040154)".

Dieses Problem tritt auf, wenn der Benutzer, die eine Verbindung herstellt ein obligatorisches Benutzerprofil hat. Um dieses Problem zu beheben, installieren die [24 Juli 2018 – KB4338817 (OS Build 16299.579)](https://support.microsoft.com/en-us/help/4338817/windows-10-update-kb4338817) Windows 10-Updates.

## Client kann keine Verbindung herstellen, keine Lizenzen, die verfügbar sind

Diese Situation gilt für Bereitstellungen, die eine RDSH-Servers und einem Server Remote Desktop-Lizenzierung enthalten.

Ermitteln Sie, welche Art von Verhalten, die Benutzern angezeigt werden:

- Die Sitzung wurde getrennt, da keine Lizenzen verfügbar sind oder kein Lizenzserver verfügbar ist
- Aufgrund einer Sicherheitsfehler wurde der Zugriff verweigert

Melden Sie sich bei der RD-Sitzungshostserver als Domänenadministrator, und öffnen Sie die Diagnoser RD-Lizenz. Suchen Sie nach Nachrichten wie folgt:

  - Die Frist für die Remote desktop-Sitzungshostserver abgelaufen, aber der Remotedesktop-Sitzungshostserver nicht mit keine Lizenzserver konfiguriert wurde. Verbindungen mit den RD-Sitzungshostserver werden abgelehnt, es sei denn, ein Lizenzserver für den RD-Sitzungshostserver konfiguriert ist.
  - Lizenz Server \<computer name\> ist nicht verfügbar. Dies kann durch Probleme bei der Netzwerkkonnektivität verursacht werden, der Desktop-Lizenzierungsdienst auf dem Lizenzserver beendet wird oder RD-Lizenzierung nicht mehr auf dem Computer installiert ist.

Diese Probleme in der Regel die folgenden Benutzernachrichten zugeordnet werden:

  - Die Remotesitzung wurde getrennt, da keine Remotedesktop-Clientzugriffslizenzen für diesen Computer vorhanden sind.
  - Die Remotesitzung wurde getrennt, da keine Remote Desktop Lizenz Server eine Lizenz verfügbar sind.

In diesem Fall [den RD-Lizenzierung-Dienst zu konfigurieren](#configure-the-rd-licensing-service).

Wenn der Remotedesktop-Lizenz Diagnoser andere Probleme aufgeführt, z. B. "die RDP-Protokoll-Komponente X.224 hat einen Fehler in den Datenstrom Protokoll und den Client getrennt" gibt es möglicherweise ein Problem, das die Lizenzzertifikate betrifft. Solche Probleme neigen dazu, benutzermeldungen, wie die folgende zugeordnet werden:

Der Client konnte aufgrund einer Sicherheitsfehler herzustellen nicht verbunden. Stellen Sie sicher, dass Sie mit dem Netzwerk angemeldet sind, versuchen Sie es erneut an den Server zu verbinden.

In diesem Fall [Registrierungsschlüssel für die Aktualisierung der X509 Zertifikate](#refresh-the-x509-certificate-registry-keys).

### Konfigurieren Sie den Dienst RD-Lizenzierung

Das folgende Verfahren verwendet Server-Manager, um die Konfiguration zu ändern. Informationen zum Konfigurieren und Server-Manager verwenden finden Sie in der [Server-Manager](https://docs.microsoft.com/en-us/windows-server/administration/server-manager/server-manager).

1. Öffnen Sie Server-Manager, und navigieren Sie dann zum **Remote Desktop Services**.
2. **Übersicht über die Bereitstellung**wählen Sie die **Aufgaben**und wählen Sie dann die **Bereitstellungseigenschaften bearbeiten**.
3. Wählen Sie die **RD-Lizenzierung**, und wählen Sie dann den entsprechenden Lizenzierung Modus für die Bereitstellung (**Pro Gerät** oder **Pro Benutzer**).
4. Geben Sie den vollqualifizierten Domänennamen (FQDN) des Servers RD-Lizenz, und wählen Sie dann **Hinzufügen**.
5. Wenn Sie mehr als einen RD-Lizenz-Server verfügen, wiederholen Sie Schritt 4 für jeden Server. 
    ![Remotedesktop-Lizenz Serverkonfigurationsoptionen im Server-Manager.](..\media\troubleshoot-remote-desktop-connections\RDLicensing_Configure.png)

### Aktualisieren der X509 Zertifikat-Registrierungsschlüssel

> [!IMPORTANT]  
> Die Schritte in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Vor dem Ändern Sie es, [Sichern Sie die Registrierung für die Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Sie Probleme auftreten.

Um dieses Problem zu beheben, Sichern und Registrierungsschlüssel für das Entfernen der X509 Zertifikate, starten Sie den Computer, und Reaktivieren der RD-Licensing-Server. Gehen Sie hierzu folgendermaßen vor.

> [!NOTE]  
> Führen Sie die folgenden Schritte auf jedem der RDSH-Server.

1. Öffnen Sie Registrierungs-Editor, und navigieren Sie zu **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\RCM**.
2. Wählen Sie im Menü Registrierung **Registrierungsdatei exportieren**.
3. Geben Sie im **Dateinamen** **Exportiert Zertifikat** , und wählen Sie dann **Speichern**.
4. Mit der rechten Maustaste jedes der folgenden Werte, wählen **Löschen**, und wählen Sie dann **Ja** , den Löschvorgang zu überprüfen:  
      - **Zertifikat**
      - **X509 Zertifikat**
      - **X509 Zertifikat-ID**
      - **X509 Certificate2**
5. Beenden Sie des Registrierungs-Editor, und starten Sie des RDSH-Servers.

## Benutzer können sich nicht authentifizieren oder zweimal authentifizieren muss

Es gibt mehrere Probleme, die Probleme verursachen können, die Benutzerauthentifizierung zu beeinflussen. In diesem Abschnitt behandelt die folgenden Fällen:

  - [Ein Benutzer mit der Meldung "eingeschränkt Anmeldetyp" Zugriff](#access-denied-restricted-type-of-logon)
  - [Ein Benutzer oder eine Anwendung mit Ereignis 16965 Zugriff verweigert wird, wurde "ein Remoteaufruf an die SAM-Datenbank verweigert"](#access-denied-a-remote-call-to-the-sam-database-has-been-denied)
  - [Ein Benutzer kann nicht mit einer Smartcard anmelden](#a-user-cannot-sign-in-by-using-a-smart-card)
  - [Wenn die remote-PC gesperrt ist, benötigt der Benutzer zum Eingeben eines Kennworts zweimal](#if-the-remote-pc-is-locked-a-user-needs-to-enter-a-password-twice)
  - [Benutzer können sich nicht anmelden und empfängt "Authentifizierungsfehler" und "CredSSP Verschlüsselung Oracle Wartung" Nachrichten](#user-cannot-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages)
  - [Nach der Aktualisierung von Clientcomputern, einige Benutzer zweimal anmelden müssen](#after-you-update-client-computers-some-users-need-to-sign-in-twice).
  - [Benutzern werden der Zugriff auf eine Bereitstellung verweigert, die RemoteGuard mit mehreren Remotedesktop-Verbindungsbroker verwendet](#users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers)

### Der Zugriff verweigert, eingeschränkte Art der Anmeldung

In diesem Fall ein Windows 10-Benutzer, der versucht, die Verbindung zu Windows 10 oder Windows Server 2016-Computern mit folgender Meldung Zugriff:

> Remotedesktop-Verbindung:  
> Der Systemadministrator hat den Typ der Anmeldung eingeschränkt (Netzwerk oder interaktiv), die Sie verwenden können. Wenden Sie um Unterstützung zu erhalten sich an Ihr Systemadministrator oder den technischen Support.

Dieses Problem tritt auf, wenn die Authentifizierung (Netzwerk Ebene Authentifizierung auf Netzwerkebene) ist erforderlich für RDP-Verbindungen, und der Benutzer ist kein Mitglied der Gruppe **Remotedesktop-Benutzer** . Es kann auch auftreten, wenn die Gruppe **Remotedesktopbenutzer** nicht an den richtigen **auf diesen Computer vom Netzwerk** Benutzer zugewiesen wurde.

Um dieses Problem zu beheben, führen Sie einen der folgenden Schritte aus:

  - [Ändern der Gruppenmitgliedschaft des Benutzers oder Zuweisen von Benutzerrechten](#modify-the-users-group-membership-or-user-rights-assignment).
  - Deaktivieren Sie den Authentifizierung auf Netzwerkebene (nicht empfohlen).
  - Verwenden Sie Remotedesktopclients als Windows 10. Windows 7-Clients müssen beispielsweise nicht dieses Problem.

#### Ändern der Gruppenmitgliedschaft des Benutzers oder Zuweisen von Benutzerrechten

Wenn dieses Problem wirkt sich auf einen einzelnen Benutzer, ist die einfachste Lösung für dieses Problem, den Benutzer zur Gruppe **Remotedesktop-Benutzer** hinzuzufügen.

Wenn der Benutzer bereits ein Mitglied dieser Gruppe zugeordnet ist (oder mehrere Mitglieder der Gruppe das gleiche Problem haben), überprüfen Sie die Konfiguration der Benutzerrechte auf dem Remotecomputer Windows 10 oder Windows Server 2016.

1. Öffnen Sie Group Policy Object Editor (GPE), und die lokale Richtlinie dem Remotecomputer herstellen.
2. Navigieren Sie zu **Configuration\\Windows Settings\\Security Einstellungen\\Lokale Policies\\User Benutzerrechten**, mit der rechten Maustaste **auf diesen Computer vom Netzwerk**, und wählen Sie dann **Eigenschaften**.
3. Überprüfen Sie die Liste der Benutzer und Gruppen für **Remotedesktop-Benutzer** (oder eine übergeordnete Gruppe).
4. Wenn in der Liste nicht **Remotedesktop-Benutzer** (oder eine übergeordnete Gruppe, z. B. **"Jeder"**) enthalten müssen Sie sie zur Liste hinzufügen (Wenn Sie mehr als eine oder zwei Computern in Ihrer Bereitstellung haben, verwenden Sie ein Gruppenrichtlinienobjekt).  
    So enthält z. B. die Standardmitgliedschaft für **auf diesen Computer vom Netzwerk** **jeder**. Wenn Ihre Bereitstellung Group Policy Object verwendet, um **alle Benutzer**zu entfernen, müssen Sie den Zugriff wiederherzustellen, indem Sie das Gruppenrichtlinienobjekt, das zum Hinzufügen von **Remotedesktop-Benutzer**aktualisieren.

### Der Zugriff verweigert, ein Remoteaufruf an die SAM-Datenbank wurde verweigert

Dieses Verhalten ist am wahrscheinlichsten auftreten, wenn Ihre Domänencontroller WindowsServer 2016 oder höher ausgeführt werden, und Benutzer versuchen, eine Verbindung mit einer angepassten Verbindungs-app. Insbesondere werden Anwendungen, die Zugriff des Benutzers Profilinformationen in Active Directory der Zugriff verweigert.

Dieses Verhalten ist das Ergebnis einer Änderung in Windows. In Windows Server 2012 R2 und früheren Versionen, wenn ein Benutzer anmeldet auf einem remote desktop, Remote Verbindungs-Manager (RCM)-Kontakte den Domänencontroller (DC), um die Konfigurationen abzufragen, die speziell für Remotedesktop für das Benutzerobjekt in Active Directory-Domäne sind Services (AD DS). Diese Informationen werden in der Registerkarte "Remote Desktop Services-Profil" der Eigenschaften eines Benutzers Objekt in der Active Directory-Benutzer und-Computer MMC-Snap-in angezeigt.

Ab Windows Server 2016, fragt RCM nicht mehr die Benutzer-Objekts in AD DS ab. Wenn Sie RCM benötigen von AD DS Abfragen, da Sie die Remote Desktop Services-Attribute verwenden, müssen Sie das vorherige Verhalten RCM manuell aktivieren.

> [!IMPORTANT]  
> Die Schritte in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Vor dem Ändern Sie es, [Sichern Sie die Registrierung für die Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Sie Probleme auftreten.

Um das legacy RCM Verhalten auf einem Remotedesktop-Sitzungshostserver zu aktivieren, konfigurieren Sie die folgenden Registrierungseinträge, und starten Sie den Dienst **Remote Desktop Services** :  
  - **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Policies\\Microsoft\\Windows NT\\Terminal Dienste**
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<Winstation name\>\\**  
      - Name: **fQueryUserConfigFromDC**
      - Typ: **Reg\_DWORD**
      - Wert: **1** (dezimal)

Um das legacy RCM Verhalten auf einem anderen Server als einen RD-Sitzungshostserver zu aktivieren, konfigurieren Sie diese Registrierungseinträge und den folgenden zusätzlichen Registrierungseintrag (und starten Sie den Dienst):
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server**

Weitere Informationen zu diesem Verhalten finden Sie unter KB 3200967 [Änderungen auf Remote-Verbindungs-Manager in Windows Server](https://support.microsoft.com/en-us/help/3200967/changes-to-remote-connection-manager-in-windows-server).

### Ein Benutzer kann nicht mit einer Smartcard anmelden

In diesem Artikel werden drei allgemeine Situationen, in denen ein Benutzer mit einem Remotedesktop anmelden kann nicht mithilfe einer Smartcards:  
  - [Der Benutzer kann nicht auf einer Zweigstelle anmelden, die eine schreibgeschützte Domänencontroller (RODC) verwendet](#cannot-sign-in-with-a-smart-card-in-a-branch-office-with-a-rodc)
  - [Der Benutzer kann nicht auf einen Windows Server 2008 SP2-Computer anzumelden, die kürzlich aktualisiert wurde](#cannot-sign-in-with-a-smart-card-to-a-windows-server-2008-sp2-computer)
  - [Der Benutzer kann nicht auf einem Windows-Computer, der kürzlich aktualisiert wurde angemeldet bleiben, und der Remotedesktop-Services-Dienst wird nicht mehr reagiert (hängt)](#cannot-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs)

#### Können sich eine Smartcard in einer Zweigstelle mit einem RODC nicht anmelden

Dieses Problem tritt bei der Bereitstellung, die eine RDSH-Servers an einem Standort Branch enthalten, die eine RODC verwendet. Des RDSH-Servers wird in der Stammdomäne gehostet. Benutzer auf der Website Branch zu einer untergeordneten Domäne angehören und Smartcards für die Authentifizierung verwenden. RODC ist für von Benutzerkennwörtern Cache konfiguriert (RODC gehört **Zulässig Gruppe RODC**). Wenn Benutzer versuchen, sich Sitzungen mit RDSH-Servers anmelden, erhalten sie Nachrichten z. B. "der Anmeldeversuch ist ungültig. Dies ist entweder aufgrund einer fehlerhaften Benutzernamen oder Authentifizierung Informationen."

Dies ist ein bekanntes Problem in die Möglichkeit, die den Stamm DC und dem RODC Verschlüsselung von Anmeldeinformationen des Benutzers zu verwalten. Der Stamm DC verwendet einen Schlüssel, um die Anmeldeinformationen verschlüsselt und der RODC bietet einen Entschlüsselungsschlüssel an dem Client. Allerdings wird die zwei Schlüssel stimmen nicht überein.

Um dieses Problem zu umgehen, überlegen Sie, ob die Topologie DC, entweder durch das Zwischenspeichern von Kennwörtern auf dem RODC deaktivieren oder durch die Bereitstellung von einem beschreibbaren Domänencontroller das Branch-Website. Eine alternative Methode ist des RDSH-Servers auf die gleiche untergeordnete Domäne wie die Benutzer wechseln. Eine weitere Alternative ist, dass Benutzer ohne Smartcards anmelden können. Für diese Lösungen möglicherweise Kompromisse in Leistung oder Sicherheitsebene eine erforderlich ist.

#### Die Anmeldung mit einer Smartcard mit einem Windows Server 2008 SP2-Computer kann nicht ausgeführt werden.

Dieses Problem tritt auf, wenn Benutzer auf einen Windows Server 2008 SP2-Computer anmelden, die mit KB4093227 aktualisiert wurde (2018.4B). Wenn Benutzer versuchen, melden Sie sich mit einer Smartcard, wird der Zugriff von Nachrichten, z. B. "keine gültige Zertifikate gefunden. verweigert Überprüfen, ob die Karte richtig eingelegt und eng." Gleichzeitig zeichnet die Windows Server-Computer-Ereignis der Anwendung "beim Abrufen eines digitalen Zertifikats von der eingefügte Smartcard ist ein Fehler aufgetreten. Ungültige Signatur."

Um dieses Problem zu beheben, aktualisieren Sie die Windows Server-Computer mit der 2018.06Bre-Version von KB-4093227 [Beschreibung des Sicherheitsupdates für die Windows (Remotedesktopprotokoll) Denial-of-Service-Risiko in Windows Server 2008: 10 April 2018](https://support.microsoft.com/en-us/help/4093227/security-update-for-vulnerabilities-in-windows-server-2008).

#### Kann nicht mit einer Smartcard und Remotedesktopdienste-Dienst Blockaden angemeldet bleiben

Dieses Problem tritt auf, wenn Benutzer auf einen Windows oder Windows Server-Computer anmelden, die mit KB 4056446 aktualisiert wurde. Am Anfang der Benutzer möglicherweise in der Lage, mit dem System melden Sie sich mit einer Smartcard, aber dann empfängt eine Fehlermeldung "SCARD\_E\_NO\_SERVICE". Der Remotecomputer möglicherweise nicht mehr reagiert.

Um dieses Problem zu umgehen, starten Sie die remote Computer neu.

Um dieses Problem zu beheben, aktualisieren Sie den Remotecomputer mit den entsprechenden beheben:

  - Windows Server 2008 SP2: KB 4090928, [Windows Speicherverlusten Handles im Prozess lsm.exe und Smartcard-Anwendungen möglicherweise Fehler "SCARD\_E\_NO\_SERVICE" angezeigt](https://support.microsoft.com/en-us/help/4090928/scard-e-no-service-errors-when-windows-leaks-handles-in-the-lsm-exe)
  - Windows Server 2012 R2: KB 4103724, [17. Mai 2018 – KB4103724 (Vorschau monatlichen Rollups)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724)
  - Windows Server 2016 und Windows 10, Version 1607: KB-4103720 [17. Mai 2018 – KB4103720 (OS Build 14393.2273)](https://support.microsoft.com/en-us/help/4103720/windows-10-update-kb4103720)

### Wenn die remote-PC gesperrt ist, benötigt der Benutzer zum Eingeben eines Kennworts zweimal

Dieses Problem kann auftreten, wenn ein Benutzer versucht, für die Verbindung mit einem Remotedesktop, die Windows 10, Version 1709 in einer Bereitstellung ausgeführt wird, in denen RDP-Verbindungen keine Authentifizierung auf Netzwerkebene erforderlich ist. Unter diesen Umständen, wenn der Remotedesktop gesperrt wurde, muss der Benutzer ihre Anmeldeinformationen eingeben zweimal beim Herstellen einer Verbindung.

Um dieses Problem zu beheben, aktualisieren Sie die Windows 10 Version 1709-Computer mit KB-4343893 [30. August 2018 – KB4343893 (OS Build 16299.637)](https://support.microsoft.com/en-us/help/4343893/windows-10-update-kb4343893).

### Benutzer können sich nicht anmelden und erhält die "Authentifizierungsfehler" und "CredSSP Verschlüsselung Oracle Wartung" Nachrichten

Wenn Benutzer versuchen, melden Sie sich mit allen Versionen von Windows aus Windows Vista SP2 und höher oder Windows Server 2008 SP2 und späteren Versionen, sie werden der Zugriff verweigert und Empfangen von Nachrichten wie folgt:

  - Authentifizierung Fehler. Die angeforderte Funktion wird nicht unterstützt.
  - Dies kann aufgrund von CredSSP Verschlüsselung Oracle Wartung sein.

"CredSSP Verschlüsselung Oracle Wartung" bezieht sich auf eine Reihe von Sicherheitsupdates, die im März und April Mai von 2018 veröffentlicht. CredSSP ist eine Authentifizierungsanbieter, der authentifizierungsanforderungen für andere Anwendungen verarbeitet. Die März 13 2018 "3 b" und nachfolgende Updates behandelt ein Exploit, in denen Angreifer Benutzeranmeldeinformationen zum Ausführen von Code auf dem Zielsystem weiterleiten konnte.

Die anfänglichen Updates zusätzliche Unterstützung für ein neues Gruppenrichtlinienobjekt, **Verschlüsselung Oracle Wartung**, die die folgenden möglichen Einstellungen hat:

  - **Anfällig**. Clientanwendungen, die CredSSP verwenden, können ein Fallback auf unsicheren Versionen dieses Verhalten, offenbart aber den Remotedesktops für Angriffe. Dienste, die CredSSP verwenden akzeptieren von Clients, die nicht aktualisiert wurden.
  - **Verringert**. Clientanwendungen, die CredSSP verwenden, können nicht ein Fallback auf unsicheren Versionen, aber Dienste, die CredSSP verwenden akzeptieren Clients, die nicht aktualisiert wurden.
  - **Force Clients aktualisiert**. Clientanwendungen, die CredSSP verwenden, können nicht ein Fallback auf unsicheren Versionen und Dienste, die CredSSP verwenden akzeptiert keine nicht gepatchte Clients. 
    Hinweis: Diese Einstellung sollte nicht bereitgestellt werden, bis alle Remotehosts die neueste Version unterstützen.

Das 8 Mai 2018-Update, die die Standardeinstellung für die **Verschlüsselung Oracle Wartung** von **gefährdet** in **gemindert**geändert wird. Aufgrund dieser Änderung Designfeatures können nicht Remotedesktopclients, die die Updates auf Server zugreifen, die keinen diese (oder aktualisiert Servern, die nicht neu gestartet wurde). Weitere Informationen über die Auswirkungen der Updates und die Arten von Kommunikation, die sie blockieren finden Sie in KB 4093492, [CredSSP Updates für CVE-2018-0886](https://support.microsoft.com/en-us/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018).

Um dieses Problem zu beheben, stellen Sie sicher, dass alle Systeme vollständig aktualisiert und neu gestartet werden. Eine vollständige Liste der Updates und Weitere Informationen zu den Sicherheitslücken, finden Sie unter [CVE-2018-0886 | Schwachstelle CredSSP Remote Code-Ausführung](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2018-0886).

Um dieses Problem umgehen, bis die Updates abgeschlossen sind, überprüfen Sie KB 4093492 für zulässige Verbindungstypen. Wenn es keine realisierbar alternativen gibt könnten Sie eine der folgenden Methoden:

  - Legen Sie für die betroffenen Clientcomputer die **Verschlüsselung Oracle Wartung** Richtlinie zurück auf **gefährdet**.
  - Ändern Sie die folgenden Richtlinien im Ordner " **Computer computerkonfiguration\\administrative vorlagen\\windows Components\\Remote Desktop Services\\Remote Desktop Sitzung Host\\Security** Group Policy":  
      - **Verwendung einer bestimmten Sicherheitsstufe für Remoteverbindungen (RDP) erforderlich**: Legen Sie auf **aktiviert** , und wählen Sie die **RDP**.
      - **Benutzerauthentifizierung für Remoteverbindungen mithilfe der Netzwerkebene Authentifizierung erfordern**: auf **Disabled**festgelegt.
      > [!IMPORTANT]  
      > Diese Änderungen werden die Sicherheit Ihrer Bereitstellung verringert. Sie sollten nur werden temporäre, wenn Sie überhaupt verwendet werden.

Weitere Informationen zum Arbeiten mit "Gruppenrichtlinie" finden Sie [eine blockierende GPO ändern](#modifying-a-blocking-gpo).

### Nachdem Sie Client-Computer aktualisieren, müssen einige Benutzer zweimal anmelden

Benutzer auf einigen Windows 7 oder Windows 10, Version 1709 melden Sie sich für eine Remotedesktopsitzung und sofort eine zweite-Anmeldebildschirm angezeigt. Dieses Problem tritt auf, wenn die Client-Computer die folgenden Updates erhalten haben:

  - Windows 7: KB 4103718, [8 Mai 2018 – KB4103718 (monatliche Updaterollup)](https://support.microsoft.com/en-us/help/4103718/windows-7-update-kb4103718)
  - Windows 10 1709: KB 4103727, [8 Mai 2018 – KB4103727 (BS-Build 16299.431)](https://support.microsoft.com/en-us/help/4103727/windows-10-update-kb4103727)

Um dieses Problem zu beheben, stellen Sie sicher, dass die Computer, denen die Benutzer (sowie RDSH oder RDVI Server) Herstellen einer Verbindung möchten über Juni 2018 vollständig aktualisiert werden. Dazu zählen die folgenden Updates:

  - WindowsServer 2016: KB 4284880, [12. Juni 2018 – KB4284880 (BS-Build 14393.2312)](https://support.microsoft.com/en-us/help/4284880/windows-10-update-kb4284880)
  - Windows Server 2012 R2: KB 4284815, [12. Juni 2018 – KB4284815 (monatliche Updaterollup)](https://support.microsoft.com/en-us/help/4284815/windows-81-update-kb4284815)
  - WindowsServer 2012: KB 4284855, [12. Juni 2018 – KB4284855 (monatliche Updaterollup)](https://support.microsoft.com/en-us/help/4284855/windows-server-2012-update-kb4284855)
  - Windows Server 2008 R2: KB 4284826, [12. Juni 2018 – KB4284826 (monatliche Updaterollup)](https://support.microsoft.com/en-us/help/4284826/windows-7-update-kb4284826)
  - WindowsServer 2008 SP2: KB4056564, [Beschreibung des Sicherheitsupdates für die CredSSP remote Code-Ausführung Sicherheitslücke in Windows Server 2008, Windows Embedded POSReady 2009 und Windows Embedded Standard 2009: 13. März 2018](https://support.microsoft.com/en-us/help/4056564/security-update-for-vulnerabilities-in-windows-server-2008)

### Benutzern werden der Zugriff auf eine Bereitstellung verweigert, die mit mehreren Remotedesktop-Verbindungsbroker Remote Credential Guard verwendet

Dieses Problem tritt bei der Bereitstellung von hoher Verfügbarkeit, mit denen zwei oder mehr Remote Desktop Connection Broker, wenn Windows Defender Remote Credential Guard verwendet wird. Benutzer können sich Remotedesktops anmelden.

Dieses Problem tritt auf, da Remote Credential Guard NTLM schränkt und Kerberos für die Authentifizierung verwendet. Allerdings kann nicht in einer Konfiguration mit hoher Verfügbarkeit mit Lastenausgleich, der Remotedesktop-Verbindungsbroker Kerberos-Vorgänge unterstützen.

Wenn Sie eine Konfiguration mit hoher Verfügbarkeit mit Lastenausgleich Remotedesktop-Verbindungsbroker verwenden müssen, können Sie dieses Problem umgehen, indem Sie Remote Credential Guard zu deaktivieren. Weitere Informationen zum Verwalten von Windows Defender Remote Credential Guard finden Sie unter [Schützen von Remotedesktop-Anmeldeinformationen mit Windows Defender Remote Credential Guard](https://docs.microsoft.com/en-us/windows/security/identity-protection/remote-credential-guard#enable-windows-defender-remote-credential-guard).

## Zum Herstellen einer Verbindung erhält der Benutzer "Remote Desktop Service ist derzeit ausgelastet" Nachricht

Um als Antwort auf dieses Problem zu ermitteln, gehen Sie folgendermaßen vor:

1. Ist der Remote Desktop Services-Dienst reagiert (z. B. Remotedesktopclient erscheint "auf der Willkommensseite nicht mehr reagiert").  
      - Wenn der Dienst nicht mehr reagiert, finden Sie unter [RDSH Server Arbeitsspeicher Problem](#rdsh-server-memory-issue).
      - Wird der Client als normalerweise mit dem Dienst interagieren, weiterhin mit dem nächsten Schritt fort.
2. Wenn ein oder mehrere Benutzer ihre Remotedesktopsitzungen trennen, können Benutzer erneut eine Verbindung herstellen?  
   - Wenn der Dienst verweigern Verbindungen weiterhin, unabhängig davon, wie viele Benutzer ihre Sitzungen trennen, finden Sie unter [RD-Listener Problem](#rd-listener-issue).
   - Wenn der Dienst akzeptieren beginnt haben Verbindungen wieder nach einer Anzahl von Benutzern ihre Sitzungen, [Überprüfen Sie die Verbindung Limit Richtlinie](#check-the-connection-limit-policy)getrennt.

### RDSH Server Arbeitsspeicher Problem

Auf einigen Windows Server 2012 R2 RDSH-Servern verfügt über ein Arbeitsspeicherverlust gefunden wurden. Beginnen im Laufe der Zeit diese Server verweigern, Remotedesktopverbindungen und lokale Konsole Anmeldungen von Nachrichten wie folgt:

> Die Aufgabe, die Sie tun möchten kann nicht abgeschlossen werden, da Remotedesktopdienst beschäftigt ist. Versuchen Sie erneut in wenigen Minuten. Andere Benutzer sollte weiterhin anmelden können.

Remotedesktopclients Verbindungsversuch auch nicht mehr reagiert.

Um dieses Problem zu umgehen, starten Sie den RDSH-Server.

Um dieses Problem zu beheben, anzuwenden KB-4093114 [10 April 2018 – KB4093114 (monatliche Updaterollup)] (file:///C:\\Users\\v-jesits\\AppData\\Local\\Microsoft\\Windows\\INetCache\\Content.Outlook\\FUB8OO45\\April%2010,%202018—KB4093114%20\(Monthly% 20Rollup\)), auf die RDSH-Server.

### Remotedesktop-Listener Problem

Auf einigen RDSH-Servern, die direkt von Windows Server 2008 R2, Windows Server 2012 R2 aktualisiert wurden oder Windows Server 2016 wurde ein Problem festgestellt. Wenn eine Remotedesktopclient mit RDSH-Servers verbunden ist, erstellt des RDSH-Servers einen RD-Listener für die Sitzung des Benutzers. Die betroffenen Server halten Anzahl von Remotedesktop-Listener, die zunimmt, wenn der Benutzer eine Verbindung herstellen, jedoch nie abnimmt.

Um dieses Problem zu umgehen, können Sie die folgenden Methoden:

  - Starten des RDSH-Servers, um die Anzahl der Remotedesktop-Listener zurückzusetzen.
  - Ändern Sie die Verbindung Limit Richtlinie, die sie auf einen sehr großen Wert festlegen. Weitere Informationen zum Verwalten der Richtlinie für das Verbindung finden Sie unter [Überprüfen Sie die Verbindung Limit-Richtlinie](#check-the-connection-limit-policy).

Um dieses Problem zu beheben, wenden Sie die folgenden Updates für die RDSH-Server:

  - Windows Server 2012 R2: KB 4343891, [30. August 2018 – KB4343891 (Vorschau monatlichen Rollups)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)
  - WindowsServer 2016: KB 4343884, [30. August 2018 – KB4343884 (BS-Build 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)

### Überprüfen Sie die Verbindung Limit-Richtlinie

Sie können den Grenzwert für die Anzahl der gleichzeitigen Remotedesktopverbindungen auf der Ebene der einzelnen Computer oder durch das Konfigurieren ein Gruppenrichtlinienobjekt (GPO) festlegen. Standardmäßig ist der Grenzwert nicht festgelegt.

Überprüfen Sie die aktuellen Einstellungen und alle vorhandenen Gruppenrichtlinienobjekten auf des RDSH-Servers zu identifizieren, öffnen Sie ein Eingabeaufforderungsfenster als Administrator, und geben Sie den folgenden Befehl aus:
  
```
gpresult /H c:\gpresult.html
```
   
Nachdem dieser Befehl abgeschlossen ist, öffnen Sie gpresult.html und in **Computer computerkonfiguration\\administrative vorlagen\\windows Components\\Remote Desktop Services\\Remote Desktop Sitzung Host\\Connections**, suchen Sie die **Anzahl der Verbindungen einschränken** Richtlinie.

  - Wenn die Einstellung für diese Richtlinie **deaktiviert**ist, wird dann Gruppenrichtlinien nicht RDP-Verbindungen zu begrenzen.
  - Wenn die Einstellung für diese Richtlinie **aktiviert**ist, überprüfen Sie **Ausschlaggebende Gruppenrichtlinienobjekt**. Wenn Sie entfernen oder Verbindung Grenzwert ändern müssen, bearbeiten Sie dieses Gruppenrichtlinienobjekt.

Um die Änderungen an zu erzwingen, öffnen Sie ein Eingabeaufforderungsfenster auf dem betreffenden Computer, und geben Sie den folgenden Befehl aus:
  
```
gpupdate /force
```
  
## Remotedesktopclient trennt und kann nicht in der gleichen Sitzung wiederherstellen

Nach der Remotedesktop-Client die Verbindung mit dem remote Desktop verliert, wird der Client kann nicht sofort Verbindung wiederherstellen. Der Benutzer erhält eine Fehlermeldung wie folgt:

  - Der Client konnte aufgrund einer Sicherheitsfehler herzustellen nicht verbunden. Stellen Sie sicher, dass Sie mit dem Netzwerk angemeldet sind, versuchen Sie es erneut an den Server zu verbinden.
  - Remotedesktop getrennt. Der Client konnte aufgrund eines Sicherheitsfehlers nicht mit dem Remotecomputer verbunden. Stellen Sie sicher, dass Sie das Netzwerk angemeldet sind, und versuchen Sie es dann erneut.

Zu einem späteren Zeitpunkt sollte der Remotedesktop-Client den Remotedesktop wird. Anstelle einer Verbindung des Clients mit der ursprünglichen Sitzung, verbindet des RDSH-Servers den Client auf eine neue Sitzung. Des RDSH-Servers nachsehen, die der ursprünglichen Sitzung getrennt haben keinen eingegeben, stattdessen bleibt jedoch aktiv.

Um dieses Problem zu umgehen, können Sie die Richtlinie **Konfigurieren Keep-alive-Verbindungsintervall** in die **Computer computerkonfiguration\\administrative vorlagen\\windows Components\\Remote Desktop Services\\Remote Desktop-Sitzung Host\\Connections aktivieren. **Richtlinie-Ordner. Wenn Sie diese Richtlinie aktivieren, müssen Sie ein Keep-alive-Intervall angeben. Der Keep-alive-Intervall bestimmt, wie oft in Minuten an, der Server die Sitzungszustand überprüft.

Dieses Problem kann durch Fehlkonfiguration der Einstellungen für die Authentifizierung und Konfiguration verursacht werden. Sie können diese Einstellungen auf der Serverebene oder mithilfe von Gruppenrichtlinienobjekten konfigurieren. Die gruppenrichtlinieneinstellungen sind im Ordner " **Computer computerkonfiguration\\administrative vorlagen\\windows Components\\Remote Desktop Services\\Remote Desktop Sitzung Host\\Security** Group Policy" verfügbar.

1. Öffnen Sie auf den RD-Sitzungshostserver Konfiguration des Remotedesktop-Sitzung.
2. Unter **Verbindungen**mit der rechten Maustaste in des Namens der Verbindung, und klicken Sie dann auf **Eigenschaften**.
3. Wählen Sie im Dialogfeld " **Eigenschaften** " für die Verbindung auf der Registerkarte " **Allgemein** " in **der Sicherheitsstufe** eine Methode ein.
4. **Verschlüsselungsstufe**klicken Sie auf die gewünschte Ebene. Sie können **mit geringer**, **Client-kompatibel**, **Hoch**oder **FIPS-kompatibel**auswählen.

> [!NOTE]  
>  - Bei der Kommunikation zwischen Clients und RD-Sitzungshostserver die höchste Ebene der Verschlüsselung erforderlich ist, verwenden Sie die FIPS-konformen Verschlüsselung.
>  - Alle Einstellungen auf Verschlüsselung, die Sie in der Gruppenrichtlinie konfigurieren überschreiben die Konfiguration, die Sie festlegen, mit dem Tool für die Konfiguration des Remotedesktop-Dienste. Auch wenn Sie aktivieren die [Systemkryptografie: FIPS-konformen Algorithmus für Verschlüsselung, hashing und Signatur](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc780081\(v=ws.10\)) Richtlinie, diese Einstellung überschreibt die Richtlinie **Client Verschlüsselungsstufe festlegen** . Die System-Kryptografie-Richtlinie ist im Ordner " **Computer Configuration\\Windows Settings\\Security Einstellungen\\Lokale Policies\\Security Optionen** ".
>  - Wenn Sie die Verschlüsselungsstufe ändern, wirkt sich die neue Verschlüsselungsstufe das nächste Mal, wenn, das ein Benutzer anmeldet. Wenn Sie mehrere Ebenen der Verschlüsselung auf einem Server benötigen, installieren Sie mehrere Netzwerkadapter und konfigurieren Sie jeden Adapter getrennt.
>  - Um sicherzustellen, dass das Zertifikat einen entsprechenden privaten Schlüssel in Remote Desktop Services-Konfiguration verfügt, Maustaste die Verbindung für die Anzeigen des Zertifikats **Allgemeine**, wählen Sie **Bearbeiten**, wählen das Zertifikat, dem Sie möchten werden soll Zeigen Sie an, und wählen Sie dann **Zertifikat anzeigen**. Am unteren Rand der Registerkarte " **Allgemein** " die Anweisung "einen privaten Schlüssel, die für dieses Zertifikat stehen Ihnen" sollte angezeigt werden. Sie können diese Informationen auch anzeigen, indem Sie mithilfe der Zertifikate-Snap-Ins.
>  - FIPS-konformen Verschlüsselung (die **Systemkryptografie: FIPS-konformen Algorithmus für Verschlüsselung, hashing und Signatur** Richtlinie oder die **FIPS-kompatible** Einstellung in der Konfiguration des Remotedesktop-Server) von gesendeten Daten verschlüsselt und entschlüsselt die Client an den Server und vom Server an den Client mit den FIPS Federal Information Processing Standard ()-140-1-Verschlüsselungsalgorithmen kryptografischen Module von Microsoft verwenden. Weitere Informationen finden Sie unter [FIPS 140-Überprüfung](https://docs.microsoft.com/en-us/windows/security/threat-protection/fips-140-validation).
>  - Die **hohe** Einstellung verschlüsselt Daten mithilfe von 128-Bit-Verschlüsselung vom Client an den Server und vom Server an den Client gesendet.
>  - Die **Client-kompatible** Einstellung verschlüsselt Daten zwischen dem Client und einem Server mit der maximalen Schlüssellänge vom Client gesendet.
>  - Die Einstellung **Niedrig** verschlüsselt Daten, die vom Client mit 56-Bit-Verschlüsselung an den Server gesendet.

## Remote Laptop trennt Drahtlosnetzwerk

Dieses Problem kann auftreten, wenn Remotedesktopclients auf einen Laptopcomputer eine Verbindung herstellt, mit einem 802. 1 X-Netzwerk. Aufgelisteter, der Laptop aus dem drahtlosen Netzwerk trennt und nicht automatisch wieder.

Dies ist ein bekanntes Problem, das tritt auf, wenn die Einstellung der Netzwerk-Authentifizierung für die drahtlose Verbindung **Benutzerauthentifizierung**.

Um dieses Problem zu umgehen, legen Sie die Einstellung der Netzwerk-Authentifizierung auf **Benutzer oder Computer** oder **Computer-Authentifizierung**.

 > [!NOTE]  
> Um den Netzwerkeinstellungen für die Authentifizierung auf einem einzelnen Computer zu ändern, müssen Sie möglicherweise die Systemsteuerung Netzwerk- und Freigabecenter verwenden, um eine neue drahtlose Verbindung mit den neuen Einstellungen zu erstellen.

Eine vollständige Beschreibung der Drahtlosnetzwerk-Einstellungen, die mithilfe von Gruppenrichtlinienobjekten konfigurieren finden Sie unter [konfigurieren (IEEE 802.11) Drahtlosnetzwerkrichtlinien](https://docs.microsoft.com/en-us/windows-server/networking/core-network-guide/cncg/wireless/e-wireless-access-deployment#bkmk_policies).

## Benutzererfahrungen eine schlechte Leistung oder Anwendungsprobleme

In diesem Abschnitt behandelt mehrere allgemeine Probleme, die Benutzer bei Verwendung von Remotedesktop-Funktionen auftreten:

  - [Remotebenutzer neuer virtueller Maschinen Microsoft Azure aufgelisteter Probleme auftreten](#intermittent-problems-with-new-microsoft-azure-virtual-machines).
  - [Remotebenutzer Windows 10 Version 1709 Remotedesktops Videowiedergabe Probleme haben](#video-playback-issues-on-windows-10-version-1709).
  - [Benutzer mit schreibgeschützt Benutzerprofile, die auf Windows 10-Remotedesktops zugreifen können nicht ihren Desktops gemeinsam nutzen.](#desktop-sharing-issues-on-windows-10)
  - [Herstellen einer Verbindung mit Windows 10-Remotedesktops mithilfe von Clients, die für ältere Versionen von Windows 10 ausgeführt bemerkbar eine schlechte Leistung bei der Authentifizierung auf Netzwerkebene deaktiviert ist](#performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled)
  - [Wenn Benutzer mehrere Anwendungen in Remotedesktopsitzungen ausführen und trennen und häufig herzustellen, können sie einen schwarzen Bildschirm auf Wiederherstellen der Verbindung auftreten.](#black-screen-issue)

### Wiederholt auftretende Probleme mit neuen Microsoft Azure-VMs

Dieses Problem betrifft die virtuellen Computer, die kürzlich bereitgestellt wurden. Nachdem der Benutzer mit dem virtuellen Computer verbunden ist, kann die Remotedesktopsitzung nicht alle die Einstellungen des Benutzers laden ordnungsgemäß.

Um dieses Problem zu umgehen, trennen Sie den virtuellen Computer mindestens 20 Minuten warten Sie und dann erneut eine Verbindung herzustellen.

Um dieses Problem zu beheben, wenden Sie die folgenden Updates auf den virtuellen Computer, je nach Bedarf:

  - Windows 10 und WindowsServer 2016: KB 4343884, [30. August 2018 – KB4343884 (BS-Build 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)
  - Windows Server 2012 R2: KB 4343891, [30. August 2018 – KB4343891 (Vorschau monatlichen Rollups)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)

### Die Videowiedergabe Probleme auf Windows 10, Version 1709

Dieses Problem tritt auf, wenn Benutzer mit einem Remotecomputer herstellen, Windows 10, Version 1709 ausgeführt wird. Wenn diese Benutzer Wiedergeben von Videos mithilfe der VMR9 (Video MixingRenderer9) Codec, der Spieler zeigt nur ein schwarzes Fenster.

Dies ist ein bekanntes Problem im Windows 10, Version 1709. Das Problem tritt nicht in Windows 10 Version 1703.

### Freigeben von Problemen bei Windows 10 Desktop

Dieses Problem tritt auf, wenn der Benutzer eine schreibgeschützte Benutzerprofil (und zugehörigen Registrierungsstruktur), z. B. in ein kioskszenario verfügt. Wenn ein Benutzer mit einem Remotecomputer stellt eine Verbindung her, auf denen Windows 10, Version 1803, ausgeführt wird, können nicht sie ihren Desktop freigeben.

Um dieses Problem zu beheben, wenden Sie das Windows 10-Update 4340917, [24 Juli 2018 – KB4340917 (OS Build 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917).

### Leistungsprobleme beim Kombinieren von Versionen von Windows 10, wenn die Authentifizierung auf Netzwerkebene deaktiviert ist

Dieses Problem tritt auf, wenn die Authentifizierung auf Netzwerkebene ist deaktiviert, und remote desktop Clientcomputer unter Windows 10 herstellen Remotedesktops, die unterschiedliche Versionen von Windows 10 ausführen. Benutzer von remote desktop-Clients auf Computern mit Windows 10, Version 1709 oder früheren Versionen auftreten eine schlechte Leistung beim Verbinden mit Remotedesktops, auf denen Windows 10, Version 1803 oder höher ausgeführt.

Dies tritt auf, da bei der Authentifizierung auf Netzwerkebene deaktiviert ist, die ältere Clientcomputer ein langsameres Protokoll beim Verbinden mit Windows 10, Version 1803 oder höher verwenden.

Um dieses Problem zu beheben, anzuwenden KB-4340917 [24 Juli 2018 – KB4340917 (OS Build 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917).

### Schwarzen Bildschirm Problem

Dieses Problem tritt in Windows 8.0, Windows 8.1, Windows 10 RTM und Windows Server 2012 R2. Ein Benutzer startet mehrere Anwendungen in einem Remotedesktop und dann die Sitzung trennt. In regelmäßigen Abständen, stellt der Benutzer mit der Remotedesktop zur Interaktion mit der Anwendung, und trennen Sie dann erneut wieder her. Irgendwann Wenn der Benutzer erneut eine Verbindung herstellt, zeigt die Remotedesktopsitzung nur einen schwarzen Bildschirm. Der Benutzer muss die Remotedesktopsitzung aus dem Remotecomputer-Konsole (oder die RDSH-Server-Konsole) enden. Dieser Vorgang verhindert, dass die Anwendungen.

Um dieses Problem zu beheben, wenden Sie die folgenden Updates nach Bedarf:

  - Windows 8 und WindowsServer 2012: KB4103719, [17. Mai 2018 – KB4103719 (Vorschau monatlichen Rollups)](https://support.microsoft.com/en-us/help/4103719/windows-server-2012-update-kb4103719)
  - Windows 8.1 und Windows Server 2012 R2: KB4103724, [17. Mai 2018 – KB4103724 (Vorschau monatlichen Rollups)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724) und KB 4284863, [21. Juni 2018 – KB4284863 (Vorschau monatlichen Rollups)](https://support.microsoft.com/en-us/help/4284863/windows-81-update-kb4284863)
  - Windows 10: In KB4284860, behoben [12. Juni 2018 – KB4284860 (BS-Build 10240.17889)](https://support.microsoft.com/en-us/help/4284860/windows-10-update-kb4284860)
