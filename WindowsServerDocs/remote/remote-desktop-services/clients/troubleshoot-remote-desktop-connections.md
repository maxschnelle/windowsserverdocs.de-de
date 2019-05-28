---
title: Problembehandlung bei Remotedesktopverbindungen
description: Problembehandlung bei Prozeduren, die unterteilt nach symptom
ms.custom: na
ms.reviewer: rklemen; josh.bender
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: RobVyK
manager: ''
ms.author: kaushika; rklemen; josh.bender; v-tea
ms.date: 02/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4bbdd17f5e6e2b161e0dda0e172ea862a9107841
ms.sourcegitcommit: 564158d760f902ced7f18e6d63a9daafa2a92bd4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2019
ms.locfileid: "64988335"
---
# <a name="troubleshooting-remote-desktop-connections"></a>Problembehandlung bei Remotedesktopverbindungen
Kurze erläuterungen einiger der am häufigsten auftretenden Probleme mit Remote Desktop Services (RDS), finden Sie unter [häufig gestellte Fragen zu den Remotedesktopclients](https://review.docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-client-faq). Dieser Artikel beschreibt erweiterte Vorgehensweisen zum Beheben von Verbindungsproblemen. Viele der folgenden Verfahren gelten, ob Sie eine einfache Konfiguration, wie ein physischer Computer, die beim Verbinden mit einem anderen physischen Computer oder eine kompliziertere Konfiguration behandeln möchten. Einige Verfahren zur Behebung von Problemen, die nur in komplexeren Szenarien für mehrere Benutzer auftreten. Weitere Informationen über die remote desktop-Komponenten und wie diese zusammenarbeiten, finden Sie unter [Remote Desktop Services-Architektur](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/desktop-hosting-logical-architecture).

> [!NOTE]  
> Viele der Verfahren, die in diesem Artikel beschrieben werden müssen Sie auf mehreren Computern, von denen einige möglicherweise müssen Sie Remotezugriff auf. Weitere Informationen zu den Remoteserver-Verwaltungstools und deren Konfiguration finden Sie unter [Remote Server-Verwaltungstools (RSAT) für Windows-Betriebssysteme](https://support.microsoft.com/en-us/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems).

Identifizieren Sie in der folgenden Liste den Typ des Symptom, auf denen Sie (oder Ihre Benutzer) auftreten.

- [Der Remotedesktop-Client kann keine Verbindung hergestellt, um den Remotedesktop, aber es sind keine bestimmten Symptomen oder Nachrichten (allgemeine Schritte zur Problembehandlung)](#no-specific-symptoms-or-messages-general-troubleshooting-steps)
- [Der Remotedesktop-Client kann keine Verbindung mit Remotedesktop und empfängt eine Nachricht "Klasse nicht registriert"](#client-cannot-connect-class-not-registered)
- [Der Remotedesktop-Client kann keine Verbindung mit Remotedesktop und empfängt eine "keine Lizenzen verfügbar" oder "Sicherheit" Fehlermeldung](#client-cannot-connect-no-licenses-available)
- [Der Benutzer erhält eine Nachricht "Zugriff verweigert" oder Anmeldeinformationen muss zweimal angeben.](#user-cannot-authenticate-or-must-authenticate-twice)
- [Zum Herstellen einer Verbindung, die empfängt eine Nachricht "Remotedesktopdienst ist derzeit ausgelastet."](#on-connecting-user-receives-remote-desktop-service-is-currently-busy-message)
- [Der Remotedesktop-Client getrennt und kann nicht mit der gleichen Sitzung wiederhergestellt](#rd-client-disconnects-and-cannot-reconnect-to-the-same-session)
- [Der Benutzer einen remote-Laptop über ein drahtloses Netzwerk hergestellt, und klicken Sie dann wird der Laptop vom Netzwerk getrennt](#remote-laptop-disconnects-from-wireless-network).
- [Die Benutzeroberflächen, eine schlechte Leistung oder Probleme mit Remoteanwendungen](#user-experiences-poor-performance-or-application-problems)

> [!NOTE]  
> Eine aktuelle Liste der Fehlercodes der RDP-Verbindung trennen, finden Sie unter [ExtendedDisconnectReasonCode Enumeration](https://docs.microsoft.com/en-us/windows/desktop/TermServ/extendeddisconnectreasoncode). 

## <a name="no-specific-symptoms-or-messages-general-troubleshooting-steps"></a>Keine bestimmten Symptomen oder Nachrichten, die (allgemeine Schritte zur Problembehandlung)

Verwenden Sie diese Schritte aus, wenn ein Remotedesktop-Client keine mit einem remote Desktop Verbindung kann bietet jedoch nicht, dass Nachrichten oder andere Symptome, die dabei helfen, würde die Ursache identifizieren. Um viele der häufigsten Ursachen für diese Art von Problem zu beheben, verwenden Sie die folgenden Methoden:

- [Überprüfen Sie den Status des RDP-Protokolls](#check-the-status-of-the-rdp-protocol)
- [Überprüfen Sie den Status der RDP-Dienste](#check-the-status-of-the-rdp-services)
- [Überprüfen Sie, dass die RDP-Listener ausgeführt wird](#check-that-the-rdp-listener-is-functioning)
- [Überprüfen Sie den RDP-Listener-port](#check-the-rdp-listener-port)

### <a name="check-the-status-of-the-rdp-protocol"></a>Überprüfen Sie den Status des RDP-Protokolls

#### <a name="check-the-status-of-the-rdp-protocol-on-a-local-computer"></a>Überprüfen Sie den Status des RDP-Protokolls auf einem lokalen computer

Um zu überprüfen und ändern Sie den Status des RDP-Protokolls auf einem lokalen Computer, finden Sie unter [Gewusst wie: Aktivieren von Remotedesktop](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#how-to-enable-remote-desktop).

> [!NOTE]  
> Wenn der Remotedesktop-Optionen nicht verfügbar sind, finden Sie unter [überprüfen, ob ein Gruppenrichtlinienobjekt RDP blockiert](#check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer).

#### <a name="check-the-status-of-the-rdp-protocol-on-a-remote-computer"></a>Überprüfen Sie den Status des RDP-Protokolls auf einem Remotecomputer

> [!IMPORTANT]  
> Die Schritte in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie Änderungen vornehmen, müssen [sichern Sie die Registrierung für die Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Probleme auftreten.

Um zu überprüfen und ändern Sie den Status des RDP-Protokolls auf einem Remotecomputer befindet, verwenden Sie eine Netzwerkverbindung für die Registrierung:

1. Wählen Sie **starten**Option **ausführen**, und geben Sie dann **regedt32**.
2. Wählen Sie im Registrierungs-Editor **Datei**, und wählen Sie dann **verbinden Netzwerk Registrierung**.
3. In der **Computer auswählen** Dialogfeld ein, geben Sie den Namen des Remotecomputers ein, wählen Sie **Namen überprüfen**, und wählen Sie dann **OK**.
4. Navigieren Sie zu **HKEY\_lokalen\_Computer\\SYSTEM\\CurrentControlSet\\Steuerelement\\Terminalserver**.  
   ![Registrierungs-Editor den Eintrag fDenyTSConnections angezeigt](..\media\troubleshoot-remote-desktop-connections\RegEntry_fDenyTSConnections.png)
   - Wenn der Wert des der **fDenyTSConnections** Schlüssel **0**, und klicken Sie dann die RDP aktiviert ist
   - Wenn der Wert des der **fDenyTSConnections** Schlüssel ist **1**, und klicken Sie dann die RDP deaktiviert ist
5. Zum Aktivieren von RDP ändern Sie den Wert der **fDenyTSConnections** aus **1** zu **0**.

#### <a name="check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer"></a>Überprüfen Sie, ob (Group Policy Object, GPO) RDP auf einem lokalen Computer blockiert wird

Wenn Sie RDP in der Benutzeroberfläche können nicht aktivieren, oder wenn der Wert des **fDenyTSConnections** wiederhergestellt **1** , nachdem Sie sie geändert haben, ein GPO möglicherweise werden überschreiben die Einstellungen auf Computerebene.

Um die Gruppenrichtlinienkonfiguration auf einem lokalen Computer zu überprüfen, öffnen Sie ein Eingabeaufforderungsfenster als Administrator, und geben Sie den folgenden Befehl aus:
```
gpresult /H c:\gpresult.html
```
Öffnen Sie nach Abschluss dieses Befehls gpresult.html. In **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remotedesktopdienste\\Remotedesktop-Sitzungshost\\Verbindungen**, Suchen der **können Benutzer mithilfe von Remote Desktop Services eine Remoteverbindung herstellen** Richtlinie.

- Wenn die Einstellung für diese Richtlinie ist **aktiviert**, Gruppenrichtlinien RDP-Verbindungen nicht blockiert.
- Wenn die Einstellung für diese Richtlinie ist **deaktiviert**, überprüfen Sie **ausschlaggebenden Gruppenrichtlinienobjekts**. Dies ist das Gruppenrichtlinienobjekt, das RDP-Verbindungen blockiert werden.
![Ein Beispiel-Segment der gpresult.html, in dem das GPO der Domänenebene ** Block RDP ** wird RDP deaktivieren.](..\media\troubleshoot-remote-desktop-connections\GPResult_RDSH_Connections_GP.png)
   
  ![Ein Beispiel-Segment der gpresult.html, in dem ** lokalen Gruppe Konfigurationsrichtlinie ** wird RDP deaktivieren.](..\media\troubleshoot-remote-desktop-connections\GPResult_RDSH_Connections_LGP.png)

#### <a name="check-whether-a-gpo-is-blocking-rdp-on-a-remote-computer"></a>Überprüfen Sie, ob ein GPO RDP auf einem Remotecomputer blockiert wird

Um die Konfiguration von Gruppenrichtlinien auf einem Remotecomputer zu überprüfen, lautet der Befehl mit fast genauso wie bei einem lokalen Computer:
```
gpresult /S <computer name> /H c:\gpresult-<computer name>.html
```
Die Datei, die dieser Befehl erzeugt (**Gpresult -\<Computername\>.html**) verwendet das gleiche Informationsformat wie die Version des lokalen Computers (**gpresult.html**) verwendet.

#### <a name="modifying-a-blocking-gpo"></a>Ändern ein Gruppenrichtlinienobjekt blockieren

Sie können diese Einstellungen in der Group Policy-Objekt-Editor (GPE) und Group Policy Management Console (GPM) ändern. Weitere Informationen dazu, wie Sie mithilfe von Gruppenrichtlinien finden Sie unter [Advanced Group Policy Management](https://docs.microsoft.com/en-us/microsoft-desktop-optimization-pack/agpm/).

Verwenden Sie zum Ändern der Richtlinie zum Blockieren von einer der folgenden Methoden aus:

- In GPE, die entsprechenden Ebene des Gruppenrichtlinienobjekts (z. B. ein lokales oder Domänenbenutzerkonto), und navigieren Sie zu **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remote Desktop Services\\ Remotedesktop-Sitzungshost\\Verbindungen**\\**können Benutzer mithilfe von Remote Desktop Services eine Remoteverbindung herstellen**.  
   1. Legen Sie die Richtlinie auf **aktiviert** oder **nicht konfiguriert**.
   2. Klicken Sie auf den betroffenen Computern, öffnen Sie ein Eingabeaufforderungsfenster als Administrator, und führen die **Gpupdate/force** Befehl.
- Navigieren Sie in GPM zu der Organisationseinheit, die in der die Richtlinie zum blockierende der betroffene Computer gilt, und löschen Sie die Richtlinie aus der Organisationseinheit.

### <a name="check-the-status-of-the-rdp-services"></a>Überprüfen Sie den Status der RDP-Dienste

Auf dem Computer lokalen (Client-) und dem Remotecomputer (Zielcomputer)-Computer sollten die folgenden Dienste ausgeführt werden:

- Remotedesktopdienste (TermService)
- Remote Desktop Anschlussumleitung für Terminaldienst-Redirector (UmRdpService)

Sie können das Dienste-MMC-Snap-in verwenden, um die Dienste lokal oder Remote zu verwalten. Sie können auch PowerShell verwenden, lokal oder Remote (wenn der Remotecomputer konfiguriert ist, remote-PowerShell-Befehle akzeptieren).

![Remotedesktopdienste im Dienste-MMC-Snap-in. Ändern Sie die Standardeinstellungen für den Dienst nicht.](..\media\troubleshoot-remote-desktop-connections\RDSServiceStatus.png)

Auf einem der Computer Wenn eine oder beide dieser Dienste nicht ausgeführt werden, starten Sie sie.

> [!NOTE]  
> Wenn Sie die Remote Desktop Services-Dienst starten, klicken Sie auf **Ja** Remote Desktop Services UserMode Port Redirectordienst automatisch neu gestartet.

### <a name="check-that-the-rdp-listener-is-functioning"></a>Überprüfen Sie, dass die RDP-Listener ausgeführt wird

> [!IMPORTANT]  
> Die Schritte in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie Änderungen vornehmen, müssen [sichern Sie die Registrierung für die Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Probleme auftreten.

#### <a name="check-the-status-of-the-rdp-listener"></a>Überprüfen des Status der RDP-listener

Verwenden Sie für dieses Verfahren eine PowerShell-Instanz, die über Administratorberechtigungen verfügt. Für einen lokalen Computer können Sie auch eine Eingabeaufforderung, die über Administratorberechtigungen verfügt. Dieses Verfahren ist jedoch PowerShell verwendet, da die gleichen Befehle sowohl lokal als auch Remote arbeiten.

1. Öffnen Sie ein PowerShell-Fenster. Um eine Verbindung mit einem Remotecomputer herzustellen, geben Sie **Enter-PSSession – ComputerName \<Computername\>** .
2. Geben Sie **Qwinsta**. 
    ![Der Qwinsta Befehl listet die Prozesse, die auf die Anschlüsse des Computers überwachen.](..\media\troubleshoot-remote-desktop-connections\WPS_qwinsta.png)
3. Wenn die Liste enthält **Rdp-TCP-** mit dem Status **Lauschen**, der RDP-Listener arbeitet. Fahren Sie fort mit [überprüfen Sie den RDP-Listener-Port](#check-the-rdp-listener-port). Andernfalls fahren Sie mit Schritt 4.
4. Exportieren Sie die RDP-Listener-Konfiguration auf einem Arbeitscomputer.
    1. Melden Sie sich auf einem Computer, der die gleiche Version des Betriebssystems verfügt wie der betroffenen Computer verfügt, und Zugriff auf Registrierung des Computers (z. B. mithilfe von Registrierungs-Editor).
    2. Navigieren Sie zu den folgenden Registrierungseintrag:  
        **HKEY\_lokalen\_Computer\\SYSTEM\\CurrentControlSet\\Steuerelement\\Terminalserver\\WinStations\\RDP-Tcp**
    3. Exportieren Sie den Eintrag in einer REG-Datei. Zum Beispiel im Registrierungs-Editor mit der rechten Maustaste des Eintrags, wählen Sie **exportieren**, und geben Sie einen Dateinamen für die exportierten Einstellungen.
    4. Kopieren Sie die exportierte REG-Datei, auf dem betroffenen Computer.
5. Um die RDP-Listener-Konfiguration importieren möchten, öffnen Sie ein PowerShell-Fenster, das über Administratorberechtigungen verfügt, auf dem betroffenen Computer (oder öffnen Sie das PowerShell-Fenster, und Herstellen einer Remoteverbindung mit dem betroffenen Computer).
   1. Um den vorhandenen Registrierungseintrag sichern, geben Sie den folgenden Befehl aus:  
   
      ```powershell  
      cmd /c 'reg export "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp" C:\Rdp-tcp-backup.reg'   
      ```  
   

   2. Um den vorhandenen Registrierungseintrag zu entfernen, geben Sie die folgenden Befehle aus:  
   
      ```powershell  
      Remove-Item -path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp' -Recurse -Force  
      ```
   
   3. Zum Importieren des neuen Registrierungseintrags, und klicken Sie dann den Dienst neu starten, geben Sie die folgenden Befehle aus:  
   
      ```powershell  
      cmd /c 'regedit /s c:\<filename>.reg'  
      Restart-Service TermService -Force  
      ```   
      wo \<Filename\> ist der Name der exportierte REG-Datei.
6. Testen Sie die Konfiguration, indem Sie die Remotedesktopverbindung erneut versuchen. Wenn Sie noch keine Verbindung herstellen können, starten Sie den betroffenen Computer neu.
7. Wenn Sie noch keine Verbindung herstellen können, [Überprüfen des Status des selbstsignierten Zertifikats für RDP](#check-the-status-of-the-rdp-self-signed-certificate).

#### <a name="check-the-status-of-the-rdp-self-signed-certificate"></a>Überprüfen des Status des selbstsignierten Zertifikats für RDP

1. Wenn Sie noch keine Verbindung herstellen können, öffnen Sie das Zertifikate-MMC-Snap-in. Wenn Sie aufgefordert werden, wählen Sie den Zertifikatspeicher, wählen Sie zum Verwalten von **Computerkonto**, und wählen Sie dann auf den betroffenen Computer.
2. In der **Zertifikate** Unterordner **Remotedesktop**, des selbstsignierten Zertifikats für RDP zu löschen. 
    ![Remote Desktop Zertifikate im MMC-Zertifikat-Snap-in.](..\media\troubleshoot-remote-desktop-connections\MMCCert_Delete.png)
3. Starten Sie auf dem betroffenen Computer den Remote Desktop Services-Dienst neu.
4. Aktualisieren Sie das Zertifikate-Snap-in.
5. Wenn das selbstsignierte Zertifikat für RDP nicht neu erstellt wurde [überprüfen Sie die Berechtigungen des Ordners "MachineKeys"](#check-the-permissions-of-the-machinekeys-folder).

#### <a name="check-the-permissions-of-the-machinekeys-folder"></a>Überprüfen Sie die Berechtigungen des Ordners "MachineKeys"

1. Auf dem betroffenen Computer, öffnen Sie Explorer, und navigieren Sie zum **C:\\ProgramData\\Microsoft\\Crypto\\RSA\\** .
2. Mit der rechten Maustaste **"MachineKeys"** Option **Eigenschaften**Option **Sicherheit**, und wählen Sie dann **erweitert**.
3. Stellen Sie sicher, dass die folgenden Berechtigungen konfiguriert sind:
      - "Vordefiniert"\\Administratoren: Vollzugriff
      - Alle Benutzer: Lesen, schreiben

### <a name="check-the-rdp-listener-port"></a>Überprüfen Sie den RDP-Listener-port

Auf dem Computer lokalen (Client-) und dem Remotecomputer (Zielcomputer)-Computer sollte die RDP-Listener an Port 3389 überwacht werden. Keine anderen Anwendungen sollten diesen Port verwenden.

> [!IMPORTANT]  
> Die Schritte in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie Änderungen vornehmen, müssen [sichern Sie die Registrierung für die Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Probleme auftreten.

Verwenden Sie zum Überprüfen, oder ändern den RDP-Port, Registrierungs-Editor ein:

1. Wählen Sie auf Start, wählen Sie **ausführen**, und geben Sie dann **regedt32**.
      - Wählen Sie zum Verbinden mit einem Remotecomputer **Datei**, und wählen Sie dann **Netzwerk-Connect-Registrierung**.
      - In der **Computer auswählen** Dialogfeld ein, geben Sie den Namen des Remotecomputers ein, wählen Sie **Namen überprüfen**, und wählen Sie dann **OK**.
2. Öffnen Sie die Registrierung, und navigieren Sie zu **HKEY\_lokalen\_Computer\\SYSTEM\\CurrentControlSet\\Steuerelement\\Terminal Server\\WinStations\\ \<Listener\>** . 
    ![Die PortNumber-Unterschlüssel für das RDP-Protokoll.](..\media\troubleshoot-remote-desktop-connections\RegEntry_PortNumber.png)
3. Wenn **PortNumber** verfügt über einen Wert als **3389**, ändern Sie ihn in **3389**. 
   > [!IMPORTANT]  
    > Sie können Remote Desktop Services über einen anderen Port betreiben. Allerdings empfohlen nicht, dass Sie so vorgehen. Problembehandlung für eine solche Konfiguration ist über den Rahmen dieses Artikels hinaus.
4. Nachdem Sie die Portnummer ändern, starten Sie die Remote Desktop Services-Dienst neu.

#### <a name="check-that-another-application-is-not-trying-to-use-the-same-port"></a>Überprüfen Sie, dass eine andere Anwendung versucht, auf den gleichen Port verwenden

Verwenden Sie für dieses Verfahren eine PowerShell-Instanz, die über Administratorberechtigungen verfügt. Für einen lokalen Computer können Sie auch eine Eingabeaufforderung, die über Administratorberechtigungen verfügt. Dieses Verfahren ist jedoch PowerShell verwendet, da dieselben Befehle lokal und Remote arbeiten.

1. Öffnen Sie ein PowerShell-Fenster. Um eine Verbindung mit einem Remotecomputer herzustellen, geben Sie **Enter-PSSession – ComputerName \<Computername\>** .
2. Geben Sie den folgenden Befehl aus:  
   
     ```powershell  
    cmd /c 'netstat -ano | find "3389"'  
    ```
  
    ![Der Netstat-Befehl erzeugt eine Liste der Ports und die Dienste überwacht.](..\media\troubleshoot-remote-desktop-connections\WPS_netstat.png)
1. Suchen Sie nach einem Eintrag für den TCP-Port 3389 (oder dem zugewiesenen RDP-Port) mit dem Status **Empfangsbereit**. 
    > [!NOTE]  
   > In der Spalte PID wird die PID (Prozess-ID) des Prozesses oder Diensts angezeigt, der diesen Port verwendet.
1. Um zu bestimmen, welche Anwendung Port 3389 (oder den zugewiesene RDP-Port) verwendet wird, geben Sie den folgenden Befehl aus:  
   
     ```powershell  
    cmd /c 'tasklist /svc | find "<pid listening on 3389>"'  
    ```  
  
    ![Die Tasklist-Befehl Gibt Details zu einem bestimmten Prozess.](..\media\troubleshoot-remote-desktop-connections\WPS_tasklist.png)
1. Suchen Sie nach einem Eintrag für die PID-Nummer, die dem Port zugeordnet ist (aus der **Netstat** Ausgabe). Werden Sie auf der rechten Seite angezeigt, die Dienste oder Prozesse, die dieser PID zugeordnet sind.
1. Wenn eine Anwendung oder ein Dienst als Remote Desktop Services (TermServ.exe) auf den Port verwendet wird, können Sie den Konflikt auflösen, indem Sie eine der folgenden Methoden:
      - Konfigurieren Sie die andere Anwendung oder Dienst um einen anderen Port (empfohlen) verwenden.
      - Deinstallieren Sie andere Anwendungen oder Dienste.
      - Konfigurieren von RDP, um einen anderen Port verwenden, und starten Sie den Remote Desktop Services-Dienst (nicht empfohlen).

#### <a name="check-whether-a-firewall-is-blocking-the-rdp-port"></a>Überprüfen Sie, ob eine Firewall den RDP-Port blockiert wird

Verwenden der **Psping** Tool zum Testen, ob Sie über Port 3389 ist den betroffenen Computer erreichen können.

1. Auf einem Computer, die sich von dem betroffenen Computer herunterladen **Psping** aus <https://live.sysinternals.com/psping.exe>.
2. Öffnen Sie ein Eingabeaufforderungsfenster als Administrator, wechseln Sie zu dem Verzeichnis, in dem Sie installiert **Psping**, und geben Sie dann den folgenden Befehl aus:  
   
   ```  
   psping -accepteula <computer IP>:3389  
   ```
   
3. Überprüfen Sie die Ausgabe von der **Psping** für Ergebnisse wie den folgenden Befehl:  
      - **Herstellen einer Verbindung mit \<Computer IP-Adresse\>** : Der Remotecomputer ist erreichbar.
      - **(0 % Loss)** : Alle Versuche, die Verbindung war erfolgreich.
      - **Der Remotecomputer verweigert die Netzwerkverbindung**: Der Remotecomputer ist nicht erreichbar.
      - **(100 %-Verlust)** : Fehler bei der alle Versuche, eine Verbindung herstellen.
1. Führen Sie **Psping** auf mehreren Computern So testen Sie ihre Fähigkeit zum Verbinden mit dem betroffenen Computer.
1. Beachten Sie, ob es sich bei der betroffene Computer Verbindungen von allen anderen Computern, einige andere Computer oder nur einen anderen Computer blockiert.
1. Empfohlene nächste Schritte:
      - Tauschen Sie sich Ihren Netzwerkadministratoren, um sicherzustellen, dass das Netzwerk auf dem betroffenen Computer RDP-Datenverkehr zulässt.
      - Untersuchen Sie die Konfigurationen der alle Firewalls zwischen dem Quellcomputer und dem betroffenen Computer (einschließlich Windows-Firewall auf dem betroffenen Computer), um festzustellen, ob eine Firewall den RDP-Port blockiert wird.

## <a name="client-cannot-connect-class-not-registered"></a>Client keine Verbindung herstellen, "Der Klasse nicht registriert."

Wenn Sie versuchen, eine Verbindung mit einem Remotecomputer mithilfe eines Clients, auf denen Windows 10, Version 1709 ausgeführt wird oder höher, der Client nicht verbunden kann, während der Remote Desktop Session Host-Server eine Meldung, die den Fehlercode "Nicht registriert (0 x 80040154) Class" enthält.

Dieses Problem tritt auf, wenn der Benutzer, die eine Verbindung herzustellen versucht ein verbindliches Benutzerprofil hat. Um dieses Problem zu beheben, installieren die [24. Juli 2018 – KB4338817 (OS Build 16299.579)](https://support.microsoft.com/en-us/help/4338817/windows-10-update-kb4338817) Windows 10-Update.

## <a name="client-cannot-connect-no-licenses-available"></a>Client keine Verbindung herstellen, keine Lizenzen verfügbar

Dies gilt für Bereitstellungen mit einem RDSH-Server und einem Server Remote Desktop Licensing.

Ermitteln Sie, welche Art von Verhalten, die Benutzern angezeigt werden:

- Die Sitzung wurde getrennt, da keine Lizenzen verfügbar sind oder kein License-Server verfügbar ist
- Der Zugriff wurde aufgrund eines Sicherheitsfehlers verweigert.

Melden Sie sich bei dem Remotedesktop-Sitzungshost als Domänenadministrator an, und öffnen Sie die Diagnose der RD-Lizenz. Suchen Sie nach Meldungen wie die folgende:

  - Die Kulanzfrist für die Remote desktop Session Host-Server ist abgelaufen, aber die Remotedesktop-Sitzungshostserver wurde nicht mit Lizenzservern konfiguriert. Verbindungen mit dem Remotedesktop-Sitzungshost-Server werden verweigert werden, es sei denn, ein Lizenzserver für Remotedesktop-Sitzungshostserver konfiguriert ist.
  - Lizenzserver \<Computername\> ist nicht verfügbar. Dies könnte darauf zurückzuführen, dass Probleme mit der Netzwerkverbindung, der Remote Desktop Licensing-Dienst wurde beendet, auf dem Lizenzserver oder RD-Lizenzierung wird nicht mehr auf dem Computer installiert.

Diese Probleme sind tendenziell die folgenden Benutzernachrichten zugeordnet werden:

  - Die Remotesitzung wurde abgebrochen, da keine Remote Desktop-Clientzugriffslizenzen für diesen Computer verfügbar sind.
  - Die Remotesitzung wurde abgebrochen, da keine Remote Desktop License Server eine Lizenz verfügbar sind.

In diesem Fall [konfigurieren Sie den Dienst RD-Lizenzierung](#configure-the-rd-licensing-service).

Wenn die Diagnose der RD-Lizenz anderer Probleme angezeigt werden, wie z. B. "die Komponente X.224 der RDP-Protokoll hat einen Fehler im Protokollablauf erkannt und der Client wurde getrennt," möglicherweise ein Problem darstellen, die die Lizenzzertifikate betroffen sind. Solche Probleme tendenziell benutzermeldungen, wie z. B. die folgenden zugeordnet werden:

Der Client konnte aufgrund eines Sicherheitsfehlers nicht mit dem Terminalserver verbunden werden. Stellen Sie sicher, dass Sie mit dem Netzwerk angemeldet sind, versuchen Sie es erneut eine Verbindung mit dem Server.

In diesem Fall [Registrierungsschlüssel für die Aktualisierung der X509 Zertifikate](#refresh-the-x509-certificate-registry-keys).

### <a name="configure-the-rd-licensing-service"></a>Konfigurieren Sie den Dienst RD-Lizenzierung

Das folgende Verfahren verwendet Server-Manager, um die konfigurationsänderungen vorzunehmen. Weitere Informationen zum Konfigurieren und Server-Manager verwenden, finden Sie unter [Server-Manager](https://docs.microsoft.com/en-us/windows-server/administration/server-manager/server-manager).

1. Öffnen Sie Server-Manager, und navigieren Sie zum **Remote Desktop Services**.
2. Auf **Bereitstellungsübersicht**Option **Aufgaben**, und wählen Sie dann **Bereitstellungseigenschaften bearbeiten**.
3. Wählen Sie **RD-Lizenzierung**, und wählen Sie dann den entsprechenden Lizenzierungsmodus für die Bereitstellung ( **"pro Gerät"** oder **pro Benutzer**).
4. Geben Sie den vollqualifizierten Domänennamen (FQDN) des Servers RD-Lizenz, und wählen Sie dann **hinzufügen**.
5. Wenn Sie mehr als eine Remotedesktop-Lizenzserver verfügen, wiederholen Sie Schritt 4 für jeden Server. 
    ![RD-Lizenz Serverkonfigurationsoptionen im Server-Manager.](..\media\troubleshoot-remote-desktop-connections\RDLicensing_Configure.png)

### <a name="refresh-the-x509-certificate-registry-keys"></a>Registrierungsschlüssel für die Aktualisierung der X509 Zertifikate

> [!IMPORTANT]  
> Die Schritte in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie Änderungen vornehmen, müssen [sichern Sie die Registrierung für die Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Probleme auftreten.

Um dieses Problem zu beheben, sichern, und klicken Sie dann Registrierungsschlüssel für das Entfernen der X509 Zertifikate, neu starten, den Computer, und reaktivieren Sie den Remotedesktop-Lizenzserver. Führen Sie dazu folgende Schritte durch.

> [!NOTE]  
> Führen Sie das folgende Verfahren auf jedem der RDSH-Server.

1. Öffnen Sie die Registrierungs-Editor, und navigieren Sie zu **HKEY\_lokalen\_Computer\\SYSTEM\\CurrentControlSet\\Steuerelement\\Terminal Server\\RCM**.
2. Wählen Sie im Menü Registrierung **Registrierungsdatei exportieren**.
3. Typ **exportierte Zertifikat** in die **Dateiname** Feld, und wählen Sie dann **speichern**.
4. Mit der rechten Maustaste jeweils die folgenden Werte, die Option **löschen**, und wählen Sie dann **Ja** um den Löschvorgang zu überprüfen:  
      - **Certificate**
      - **X509 Certificate**
      - **X509 Certificate ID**
      - **X509 Certificate2**
5. Beenden Sie Registrierungs-Editor zu und Neustarten Sie des RDSH-Servers.

## <a name="user-cannot-authenticate-or-must-authenticate-twice"></a>Benutzer nicht authentifizieren kann, oder muss zweimal authentifizieren

Es gibt mehrere Probleme, die Probleme verursachen können, die Benutzerauthentifizierung zu betreffen. In diesem Abschnitt werden die folgenden Fälle:

  - [Ein Benutzer mit der Meldung "restricted Anmeldetyp" keinen Zugriff](#access-denied-restricted-type-of-logon)
  - [Benutzer oder Anwendungen Zugriff mit Ereignis 16965 verweigert wird, "verfügt über ein Remoteaufruf an der SAM-Datenbank verweigert wurde"](#access-denied-a-remote-call-to-the-sam-database-has-been-denied)
  - [Ein Benutzer kann nicht mit einer Smartcard anmelden](#a-user-cannot-sign-in-by-using-a-smart-card)
  - [Wenn der Remotecomputer gesperrt ist, muss ein Benutzer ein Kennwort zweimal eingeben](#if-the-remote-pc-is-locked-a-user-needs-to-enter-a-password-twice)
  - [Ein Benutzer nicht anmelden und "Authentifizierungsfehler" und "CredSSP Verschlüsselung Oracle-Remediation" Nachrichten empfängt](#user-cannot-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages)
  - [Nach dem Aktualisieren von Clientcomputern einige Benutzer müssen sich zweimal anmelden](#after-you-update-client-computers-some-users-need-to-sign-in-twice).
  - [Benutzer in einer Bereitstellung von Zugriff, die RemoteGuard mit mehreren Remotedesktop-Verbindungsbroker verwendet](#users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers)

### <a name="access-denied-restricted-type-of-logon"></a>Der Zugriff verweigert, eingeschränkten Typ der Anmeldung

In diesem Fall wird ein Windows 10-Benutzer, die versuchen, auf Windows 10 oder Windows Server 2016-Computer eine Verbindung mit der folgenden Meldung Zugriff:

> Remotedesktopverbindung:  
> Der Systemadministrator hat den Typ der Anmeldung eingeschränkt (Netzwerk oder einen interaktiven), die Sie verwenden können. Hilfe zu erhalten wenden Sie sich an Ihren Systemadministrator oder den technischen Support.

Dieses Problem tritt auf, wenn es sich bei (Network Level Authentication, NLA) ist für die RDP-Verbindungen erforderlich, und der Benutzer ist nicht Mitglied der **Remote Desktop Users** Gruppe. Er kann auch auftreten, wenn die **Remote Desktop Users** Gruppe nicht zugewiesen wurde die **Zugriff auf diesen Computer vom Netzwerk** verfügen.

Um dieses Problem zu beheben, führen Sie einen der folgenden Schritte aus:

  - [Ändern der Gruppenmitgliedschaft des Benutzers oder Zuweisen von Benutzerrechten](#modify-the-users-group-membership-or-user-rights-assignment).
  - Deaktivieren Sie NLA (nicht empfohlen).
  - Verwenden Sie remote desktop-Clients als Windows 10. Windows 7-Clients müssen sich beispielsweise nicht auf dieses Problem aus.

#### <a name="modify-the-users-group-membership-or-user-rights-assignment"></a>Ändern der Gruppenmitgliedschaft des Benutzers oder Zuweisen von Benutzerrechten

Wenn dieses Problem einen einzelnen Benutzer betrifft, ist die einfachste Lösung für dieses Problem beim Hinzufügen des Benutzers, der **Remote Desktop Users** Gruppe.

Wenn der Benutzer bereits Mitglied dieser Gruppe zugeordnet ist (oder mehrere Mitglieder auf das gleiche Problem haben), überprüfen Sie die Konfiguration der Benutzerrechte auf dem Remotecomputer Windows 10 oder Windows Server 2016.

1. Group Policy Object Editor (GPE) zu öffnen, und Verbinden mit der lokalen Richtlinie des Remotecomputers.
2. Navigieren Sie zu **Computerkonfiguration\\Windows-Einstellungen\\Sicherheitseinstellungen\\lokale Richtlinien\\Zuweisen von Benutzerrechten**, mit der rechten Maustaste **den Zugriff auf diese Computer vom Netzwerk**, und wählen Sie dann **Eigenschaften**.
3. Überprüfen Sie die Liste von Benutzern und Gruppen für **Remote Desktop Users** (oder eine übergeordnete Gruppe).
4. Die Liste nicht enthalten **Remote Desktop Users** (oder eine übergeordnete Gruppe, z. B. **jeder**) müssen Sie ihn zur Liste hinzufügen (Wenn Sie mehr als ein oder zwei Computern in Ihrer Bereitstellung verfügen, verwenden Sie ein Gruppenrichtlinienobjekt) .  
    Z. B. die Standardmitgliedschaft für **Zugriff auf diesen Computer vom Netzwerk** enthält **jeder**. Wenn die Bereitstellung ein Gruppenrichtlinienobjekts verwendet, um entfernen **jeder**, müssen Sie möglicherweise den Zugriff wiederherzustellen, durch das Gruppenrichtlinienobjekt hinzufügen aktualisieren **Remote Desktop Users**.

### <a name="access-denied-a-remote-call-to-the-sam-database-has-been-denied"></a>Der Zugriff verweigert, ein Remoteaufruf an der SAM-Datenbank wurde verweigert

Dieses Verhalten ist wahrscheinlich auftreten, wenn Benutzer versuchen, eine Verbindung herstellen, mithilfe einer benutzerdefinierten Verbindungs-app und Ihren Domänencontrollern WindowsServer 2016 oder höher ausgeführt werden. Insbesondere werden Anwendungen, die die Benutzerprofilinformationen in Active Directory zugreifen. der Zugriff verweigert.

Dieses Verhalten ist das Ergebnis einer Änderung in Windows. In Windows Server 2012 R2 und früheren Versionen, wenn ein Benutzer meldet sich an eine remote desktop, Kontakte für Remote Connection Manager (RCM) den Domänencontroller (DC), um die Konfigurationen abzufragen, die sich per Remotedesktop für das Benutzerobjekt im Active Directory-Domäne spezifisch sind Domain Services (AD DS). Diese Informationen werden auf der Registerkarte Remote Desktop Services-Profil eines Benutzers von Objekteigenschaften in den Active Directory-Benutzer und Computer MMC-Snap-in angezeigt.

Ab Windows Server 2016, Abfragen RCM nicht mehr die Benutzer-Objekte in AD DS. Wenn Sie benötigen die RCM zu AD DS abgefragt werden, da Sie die Remote Desktop Services-Attribute verwenden, müssen Sie das vorherige Verhalten von RCM manuell aktivieren.

> [!IMPORTANT]  
> Die Schritte in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie Änderungen vornehmen, müssen [sichern Sie die Registrierung für die Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Probleme auftreten.

Um das auf einem Remotedesktop-Sitzungshostserver RCM-Legacyverhalten zu aktivieren, konfigurieren Sie die folgenden Registrierungseinträge, und wiederholen Sie den **Remote Desktop Services** Dienst:  
  - **HKEY\_lokalen\_Computer\\SOFTWARE\\Richtlinien\\Microsoft\\Windows NT\\Terminaldienste**
  - **HKEY\_lokalen\_Computer\\SYSTEM\\CurrentControlSet\\Steuerelement\\Terminal Server\\WinStations\\\<Winstation-Name\>\\**  
      - Name: **fQueryUserConfigFromDC**
      - Typ: **Reg\_DWORD**
      - Wert: **1** (dezimal)

Um das auf einem anderen als einen Remotedesktop-Sitzungshostserver RCM-Legacyverhalten zu aktivieren, konfigurieren Sie diese Registrierungseinträge und die folgenden zusätzlichen Registrierungseintrag (und klicken Sie dann starten Sie den Dienst neu):
  - **HKEY\_lokalen\_Computer\\SYSTEM\\CurrentControlSet\\Steuerelement\\Terminalserver**

Weitere Informationen zu diesem Verhalten finden Sie unter KB 3200967 [Änderungen auf Remote-Verbindungs-Manager in Windows Server](https://support.microsoft.com/en-us/help/3200967/changes-to-remote-connection-manager-in-windows-server).

### <a name="a-user-cannot-sign-in-by-using-a-smart-card"></a>Ein Benutzer kann nicht mit einer Smartcard anmelden

In diesem Artikel werden drei häufige Situationen, in denen ein Benutzer mit einem Remotedesktop anmelden kann nicht mit einer Smartcard:  
  - [Der Benutzer kann nicht an eine Filiale melden Sie sich, die einen schreibgeschützten Domänencontroller (RODC) verwendet.](#cannot-sign-in-with-a-smart-card-in-a-branch-office-with-a-rodc)
  - [Der Benutzer kann nicht auf einem Windows Server 2008 SP2-Computer anmelden, der vor kurzem aktualisiert wurde](#cannot-sign-in-with-a-smart-card-to-a-windows-server-2008-sp2-computer)
  - [Der Benutzer kann nicht in einem Windows-Computer, der vor kurzem aktualisiert wurde angemeldet bleiben, und der Remote Desktop Services-Dienst wird nicht mehr reagiert (hängt)](#cannot-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs)

#### <a name="cannot-sign-in-with-a-smart-card-in-a-branch-office-with-a-rodc"></a>Die Anmeldung mit einer Smartcard, die in einer Zweigstelle mit einem RODC kann nicht ausgeführt werden.

Dieses Problem tritt in Bereitstellungen mit einem RDSH-Server an einem Branch-Standort, der einen RODC verwendet. Die RDSH-Servers wird in der Stammdomäne gehostet. Benutzer in der Zweigniederlassung zu einer untergeordneten Domäne gehören, und Verwenden von Smartcards für die Authentifizierung. Der RODC Benutzerkennwörter Cache konfiguriert ist (der RODC gehört zu den **zulässige RODC-Kennwortreplikationsgruppe**). Wenn Benutzer versuchen, die Sitzungen auf dem RDSH-Server anmelden, erhalten sie Nachrichten wie z. B. "der versuchte Anmeldung ist ungültig. Dies liegt entweder an einen ungültigen Benutzernamen oder die Authentifizierung-Informationen. "

Dies ist ein bekanntes Problem in der Möglichkeit, die den Stamm DC und der RODC-Verschlüsselung der Anmeldeinformationen des Benutzers verwalten. Der Stamm-DC verwendet einen Verschlüsselungsschlüssel, um die Anmeldeinformationen verschlüsselt, und der RODC bietet einen Entschlüsselungsschlüssel an dem Client. Allerdings werden die beiden Schlüssel stimmen nicht überein.

Um dieses Problem zu umgehen, erwägen Sie die DC-Topologie, entweder durch das Zwischenspeichern von Kennwörtern auf dem RODC deaktivieren oder durch Bereitstellung von einem beschreibbaren Domänencontroller in der Zweigniederlassung. Eine alternative Methode ist zum Verschieben des RDSH-Servers auf die gleiche untergeordnete Domäne als der Benutzer. Eine weitere Möglichkeit ist, dass Benutzer ohne Smartcards anmelden können. Jede dieser Lösungen erfordern gefährdungen Leistung oder Sicherheit.

#### <a name="cannot-sign-in-with-a-smart-card-to-a-windows-server-2008-sp2-computer"></a>Die Anmeldung mit einer Smartcard auf einem Windows Server 2008 SP2-Computer kann nicht ausgeführt werden.

Dieses Problem tritt auf, wenn der Benutzer auf einem Windows Server 2008 SP2-Computer anmelden, die mit KB4093227 aktualisiert wurde (2018.4B). Wenn Benutzer versuchen, sich mit einer Smartcard anmelden, wird der Zugriff mit Meldungen wie "keine gültige Zertifikate gefunden. verweigert Überprüfen Sie, ob die Karte richtig eingelegt und passt." Zur gleichen Zeit zeichnet die Windows Server-Computer-Ereignis der Anwendung "Fehler beim Abrufen von eines digitalen Zertifikats aus der eingeführten Smartcard. Ungültige Signatur."

Um dieses Problem zu beheben, aktualisieren Sie die Windows Server-Computer, mit die 2018.06 B vorveröffentlichten KB 4093227, [Beschreibung des Sicherheitsupdates für die Ablehnung Windows Remote Desktop Protocol (RDP) in Windows Server 2008-Service-Sicherheitslücke: 10. April 2018](https://support.microsoft.com/en-us/help/4093227/security-update-for-vulnerabilities-in-windows-server-2008).

#### <a name="cannot-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs"></a>Kann nicht angemeldet ist, sich mit einer Smartcard und Remotedesktopdienste Dienstfehlern bleiben

Dieses Problem tritt auf, wenn der Benutzer auf einem Windows oder Windows Server-Computer anmelden, die mit KB 4056446 aktualisiert wurde. Zunächst der Benutzer möglicherweise auf das System mit einer Smartcard anmelden können, aber dann empfängt eine "RGEBNISSE\_E\_keine\_SERVICE" Fehlermeldung angezeigt. Möglicherweise ist der Remotecomputer reagiert.

Um dieses Problem zu umgehen, starten Sie den Remotecomputer neu.

Um dieses Problem zu beheben, aktualisieren Sie den Remotecomputer mit den entsprechenden Fix:

  - Windows Server 2008 SP2: KB 4090928, [Windows Speicherverluste Handles im Prozess lsm.exe und möglicherweise smartcardanwendungen angezeigt "RGEBNISSE\_E\_keine\_SERVICE" Fehler](https://support.microsoft.com/en-us/help/4090928/scard-e-no-service-errors-when-windows-leaks-handles-in-the-lsm-exe)
  - Windows Server 2012 R2: KB 4103724, [17 Mai 2018 – KB4103724 (Vorschau des monatlichen Rollups)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724)
  - Windows Server 2016 und Windows 10 Version 1607: KB 4103720, [17 Mai 2018 – KB4103720 (Betriebssystembuild 14393.2273)](https://support.microsoft.com/en-us/help/4103720/windows-10-update-kb4103720)

### <a name="if-the-remote-pc-is-locked-a-user-needs-to-enter-a-password-twice"></a>Wenn der Remotecomputer gesperrt ist, muss ein Benutzer ein Kennwort zweimal eingeben

Dieses Problem kann auftreten, wenn ein Benutzer versucht, einen Remotedesktop herstellen, für die Windows 10, Version 1709 in einer Bereitstellung ausgeführt wird, in der RDP-Verbindungen keine Authentifizierung auf Netzwerkebene benötigen. Unter diesen Bedingungen, wenn der Remotedesktop gesperrt wurde, muss der Benutzer seine Anmeldeinformationen eingeben, zweimal, wenn eine Verbindung herstellen.

Um dieses Problem zu beheben, aktualisieren Sie den Computer mit Windows 10 Version 1709 mit KB-4343893 [30. August 2018 – KB4343893 (OS Build 16299.637)](https://support.microsoft.com/en-us/help/4343893/windows-10-update-kb4343893).

### <a name="user-cannot-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages"></a>Benutzer nicht anmelden und "Authentifizierungsfehler" und "CredSSP Verschlüsselung Oracle-Remediation" Nachrichten empfängt

Wenn Benutzer versuchen, melden Sie sich mit einer beliebigen Version von Windows aus Windows Vista SP2 und höher oder Windows Server 2008 SP2 und höheren Versionen, Zugriff verweigert sie, und Empfangen von Nachrichten, wie z. B. die folgenden:

  - Ein Authentifizierungsfehler aufgetreten. Die angeforderte Funktion wird nicht unterstützt.
  - Dies konnte aufgrund von CredSSP Verschlüsselung Oracle Wiederherstellung sein.

"CredSSP Verschlüsselung Oracle-Remediation" bezieht sich auf einen Satz von Sicherheitsupdates, die im März, April und Mai 2018 veröffentlicht wurde. CredSSP ist Authentifizierungsanbieter, der authentifizierungsanforderungen für andere Anwendungen verarbeitet werden. Der 13. März 2018, "3 b" "und" nachfolgenden Updates behandelt ein Exploit, in dem ein Angreifer die Anmeldeinformationen des Benutzers zum Ausführen von Code auf dem Zielsystem relay konnte.

Die erste Updates zusätzliche Unterstützung für ein neues Gruppenrichtlinienobjekt, **Verschlüsselung Oracle Wiederherstellung**, die folgenden möglichen Einstellungen aufweist:

  - **Anfällige**. Clientanwendungen, die CredSSP verwenden, auch möglich, nicht sicheren Versionen, aber dieses Verhalten macht das remote-Desktops für Angriffe. Dienste, die CredSSP verwenden akzeptieren von Clients, die nicht aktualisiert wurden.
  - **Verringert**. Clientanwendungen, die CredSSP verwenden, kein ausweichen auf unsichere Versionen, aber die Dienste, die CredSSP verwenden akzeptieren von Clients, die nicht aktualisiert wurden.
  - **Force aktualisiert Clients**. Clientanwendungen, die CredSSP verwenden, kein ausweichen auf unsichere Versionen, und Dienste, die CredSSP verwenden nicht gepatchten Clients akzeptiert. 
    Hinweis: Diese Einstellung sollte nicht bereitgestellt werden, bis alle remote-Hosts die neueste Version zu unterstützen.

Die Standardeinstellungen geändert, das 8. Mai 2018 Update **Verschlüsselung Oracle Wiederherstellung** aus **gefährdet** zu **entschärft**. Mit dieser Änderung vorgenommen wurde können nicht remote desktop-Clients, die die Updates auf Server zugreifen, die haben sie keine (oder Server, die nicht neu gestartet wurden, aktualisiert). Weitere Informationen zu den Auswirkungen der Updates und die Arten der Kommunikation, die sie blockieren, finden Sie unter KB 4093492, [CredSSP-updates für CVE-2018-0886](https://support.microsoft.com/en-us/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018).

Um dieses Problem zu beheben, stellen Sie sicher, dass alle Systeme vollständig aktualisiert und neu gestartet werden. Eine vollständige Liste der Updates und Weitere Informationen zu den Sicherheitsrisiken, finden Sie unter [CVE-2018-0886 | CredSSP Remote Remotecodeausführung zu erzeugen](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2018-0886).

Um dieses Problem umgehen, bis die Updates abgeschlossen sind, überprüfen Sie KB 4093492 zulässigen Typen von Verbindungen. Wenn es keine alternativen möglichen gibt sollten Sie eine der folgenden Methoden:

  - Legen Sie für den betroffenen Clientcomputern, die **Verschlüsselung Oracle Wiederherstellung** Richtlinie zurück zum **gefährdet**.
  - Ändern Sie die folgenden Richtlinien in der **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remote Desktop Services\\Remote Desktop Session Host\\ Sicherheit** Ordner "Group Policy":  
      - **Verwenden einer bestimmten Sicherheitsstufe für Remoteverbindungen (RDP) erfordern**: Legen Sie auf **aktiviert** , und wählen Sie **RDP**.
      - **Benutzerauthentifizierung mit Authentifizierung auf Netzwerkebene für Remoteverbindungen erfordern**: Legen Sie auf **deaktiviert**.
      > [!IMPORTANT]  
      > Diese Änderungen reduzieren die Sicherheit Ihrer Bereitstellung. Sie sollte nur temporär ist, wenn Sie überhaupt verwendet werden.

Weitere Informationen zum Arbeiten mit der Gruppenrichtlinie finden Sie unter [Ändern eines blockierenden Gruppenrichtlinienobjekts](#modifying-a-blocking-gpo).

### <a name="after-you-update-client-computers-some-users-need-to-sign-in-twice"></a>Nach der Aktualisierung-Clientcomputern müssen einige Benutzer sich zweimal anmelden

Benutzer auf eine Windows 7 oder Windows 10 Version 1709 Anmeldung, um eine Remotedesktopsitzung und sofort einen zweiten Bildschirm Anmeldung angezeigt. Dieses Problem tritt auf, wenn die Clientcomputer die folgenden Updates erhalten haben:

  - Windows 7: KB 4103718, [8. Mai 2018 – KB4103718 (monatliche Rollup)](https://support.microsoft.com/en-us/help/4103718/windows-7-update-kb4103718)
  - Windows 10 1709: KB 4103727, [8. Mai 2018 – KB4103727 (Betriebssystembuild 16299.431)](https://support.microsoft.com/en-us/help/4103727/windows-10-update-kb4103727)

Um dieses Problem zu beheben, stellen Sie sicher, dass der Computer, auf denen die Benutzer (sowie RDSH oder RDVI Server) herstellen möchten, bis Juni 2018 vollständig aktualisiert werden. Dies umfasst die folgenden Updates:

  - Windows Server 2016: KB 4284880, [12. Juni 2018 – KB4284880 (Betriebssystembuild 14393.2312)](https://support.microsoft.com/en-us/help/4284880/windows-10-update-kb4284880)
  - Windows Server 2012 R2: KB 4284815, [12. Juni 2018 – KB4284815 (monatliche Rollup)](https://support.microsoft.com/en-us/help/4284815/windows-81-update-kb4284815)
  - Windows Server 2012: KB 4284855, [12. Juni 2018 – KB4284855 (monatliche Rollup)](https://support.microsoft.com/en-us/help/4284855/windows-server-2012-update-kb4284855)
  - Windows Server 2008 R2: KB 4284826, [12. Juni 2018 – KB4284826 (monatliche Rollup)](https://support.microsoft.com/en-us/help/4284826/windows-7-update-kb4284826)
  - Windows Server 2008 SP2: KB4056564, [Beschreibung des Sicherheitsupdates für die CredSSP Remotecodeausführung zu erzeugen in Windows Server 2008 und Windows Embedded POSReady 2009, Windows Embedded Standard 2009: 13. März 2018](https://support.microsoft.com/en-us/help/4056564/security-update-for-vulnerabilities-in-windows-server-2008)

### <a name="users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers"></a>Benutzer in einer Bereitstellung von Zugriff, die Remote Credential Guard mit mehreren Remotedesktop-Verbindungsbroker verwendet

Dieses Problem tritt in Hochverfügbarkeits-Bereitstellungen mit zwei oder mehr Remotedesktop-Verbindungsbroker, wenn Windows Defender Remote Credential Guard verwendet wird. Benutzer können keine Remotedesktops anmelden.

Dieses Problem tritt auf, weil Remote Credential Guard mithilfe von Kerberos für die Authentifizierung und NTLM beschränkt. Allerdings kann nicht in einer Konfiguration mit hoher Verfügbarkeit mit Lastenausgleich, der Remotedesktop-Verbindungsbroker-Kerberos-Vorgänge unterstützt.

Wenn Sie eine Konfiguration mit hoher Verfügbarkeit mit Remotedesktop-Verbindungsbroker mit Lastenausgleich verwenden möchten, können Sie dieses Problem umgehen, indem Sie Remote Credential Guard deaktivieren. Weitere Informationen zum Verwalten von Windows Defender Remote Credential Guard finden Sie unter [Schützen von Remotedesktop-Anmeldeinformationen mit Remote Credential Guard in Windows Defender](https://docs.microsoft.com/en-us/windows/security/identity-protection/remote-credential-guard#enable-windows-defender-remote-credential-guard).

## <a name="on-connecting-user-receives-remote-desktop-service-is-currently-busy-message"></a>Zum Herstellen einer Verbindung erhält der Benutzer die Meldung "Remotedesktopdienst ist derzeit ausgelastet"

Um eine entsprechende Antwort an die dieses Problem zu ermitteln, verwenden Sie die folgenden Schritte aus:

1. Ist der Remote Desktop Services-Dienst reagiert nicht mehr (z. B. die Remotedesktop-Client "auf der Willkommensseite nicht mehr reagiert." angezeigt).  
      - Wenn der Dienst reagiert, finden Sie unter [RDSH-Servers Arbeitsspeicherproblems](#rdsh-server-memory-issue).
      - Wenn der Client angezeigt wird, normalerweise mit dem Dienst interagieren, weiterhin mit dem nächsten Schritt.
2. Wenn ein oder mehrere Benutzer ihre Remotedesktopsitzungen trennen, können Benutzer erneut eine Verbindung herstellen?  
   - Wenn der Dienst weiterhin Verbindungen unabhängig davon, wie viele Benutzer ihre Sitzungen trennen, finden Sie unter [RD-Listener Problem](#rd-listener-issue).
   - Wenn der Dienst akzeptiert beginnt über Verbindungen erneut nach einer Anzahl der Benutzer ihre Sitzungen, getrennt [überprüfen Sie die Richtlinie für die Verbindung](#check-the-connection-limit-policy).

### <a name="rdsh-server-memory-issue"></a>Speicherproblem für RDSH-server

Ein Arbeitsspeicherverlust wurde auf einigen Servern Windows Server 2012 R2 RDSH gefunden. Beginnen im Laufe der Zeit diese Server sowohl für Remotedesktopverbindungen als auch für Anmeldungen mit Meldungen wie die folgende lokale Konsole verweigern:

> Die Aufgabe, die Sie tun möchten kann nicht abgeschlossen werden, da Remotedesktop-Dienst aktuell ausgelastet ist. Versuchen Sie es in wenigen Minuten. Andere Benutzer sollten immer noch angemeldet sein.

Remote desktop-Clients, die versuchen, auch eine Verbindung nicht mehr reagiert.

Um dieses Problem zu umgehen, starten Sie die RDSH-Server neu.

Dieses Problem zu beheben, weisen Sie die KB-4093114 [10. April 2018 – KB4093114 (monatlichen Rollups)] (file:///C:\\Benutzer\\V-Jesits\\AppData\\lokale\\Microsoft\\Windows\\INetCache\\Content.Outlook\\FUB8OO45\\% für April 2010 % 202018 – KB4093114 %20\(monatliche % 20Rollup\)), auf die RDSH-Server.

### <a name="rd-listener-issue"></a>Remotedesktop-Listener-Problem

Für einige RDSH-Server, die direkt von Windows Server 2008 R2 auf Windows Server 2012 R2 aktualisiert wurden oder Windows Server 2016 wurde ein Problem festgestellt. Bei einem Remotedesktop-Client mit der RDSH-Servers verbunden ist, erstellt die RDSH-Servers ein Remotedesktop-Listeners für die benutzersitzung. Die betroffenen Servern behalten die Anzahl der von die RD-Listener, die steigt, wenn Benutzer eine Verbindung herstellen, aber nicht verringern.

Um dieses Problem zu umgehen, können Sie die folgenden Methoden:

  - Neustarten des RDSH-Servers zum Zurücksetzen des Zählers, der Remotedesktop-Listener
  - Ändern Sie die Grenze Verbindungsrichtlinie auf einen sehr hohen Wert festlegen. Weitere Informationen zum Verwalten der Richtlinie für die Verbindung zu erhalten, finden Sie unter [überprüfen Sie die Richtlinie für die Verbindung](#check-the-connection-limit-policy).

Um dieses Problem zu beheben, müssen wenden Sie die folgenden Updates auf die RDSH-Server an:

  - Windows Server 2012 R2: KB 4343891, [30. August 2018 – KB4343891 (Vorschau des monatlichen Rollups)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)
  - Windows Server 2016: KB 4343884, [30. August 2018 – KB4343884 (Betriebssystembuild 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)

### <a name="check-the-connection-limit-policy"></a>Überprüfen Sie die Richtlinie für Verbindung

Sie können den Grenzwert für die Anzahl der gleichzeitigen Remotedesktopverbindungen Ebene der einzelnen Computer oder durch konfigurieren ein Gruppenrichtlinienobjekt (GPO) festlegen. Standardmäßig ist der Grenzwert nicht festgelegt.

Überprüfen Sie die aktuellen Einstellungen und Gruppenrichtlinienobjekte für die RDSH-Servers zu identifizieren, öffnen Sie ein Eingabeaufforderungsfenster als Administrator, und geben den folgenden Befehl:
  
```
gpresult /H c:\gpresult.html
```
   
Nachdem dieser Befehl abgeschlossen ist, öffnen gpresult.html, und in **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remote Desktop Services\\Remote Desktop Session Host \\Verbindungen**, finden Sie die **Anzahl der Verbindungen einschränken** Richtlinie.

  - Wenn die Einstellung für diese Richtlinie ist **deaktiviert**, und klicken Sie dann die RDP-Verbindungen von der Gruppenrichtlinie nicht eingeschränkt wird.
  - Wenn die Einstellung für diese Richtlinie ist **aktiviert**, überprüfen Sie anschließend **ausschlaggebenden Gruppenrichtlinienobjekts**. Wenn Sie entfernen oder ändern Sie das Verbindungslimit festlegen möchten, bearbeiten Sie dieses Gruppenrichtlinienobjekt.

Um die Änderung der Richtlinie zu erzwingen, öffnen Sie ein Eingabeaufforderungsfenster auf dem betroffenen Computer, und geben Sie den folgenden Befehl aus:
  
```
gpupdate /force
```
  
## <a name="rd-client-disconnects-and-cannot-reconnect-to-the-same-session"></a>Remotedesktop-Client trennt die Verbindung nicht hergestellt werden und mit der gleichen Sitzung

Nach dem Remotedesktop-Client die Verbindung mit dem Remotedesktop verliert, kann nicht der Client sofort erneut eine Verbindung herzustellen. Der Benutzer erhält Fehlermeldungen wie z. B. Folgendes an:

  - Der Client konnte aufgrund eines Sicherheitsfehlers nicht mit dem Terminalserver verbunden werden. Stellen Sie sicher, dass Sie mit dem Netzwerk angemeldet sind, versuchen Sie es erneut eine Verbindung mit dem Server.
  - Remotedesktop nicht verbunden. Der Client konnte aufgrund eines Sicherheitsfehlers nicht mit dem Remotecomputer verbunden. Stellen Sie sicher, dass Sie am Netzwerk angemeldet sind, und wiederholen Sie dann erneut eine Verbindung herzustellen.

Mit dem zu einem späteren Zeitpunkt sich per Remotedesktop die Remotedesktop-Client verbindet. Allerdings anstelle den Client mit der ursprünglichen Sitzung verbinden, die RDSH-Servers vom Client eine Verbindung zu einer neuen Sitzung. Überprüfen die RDSH-Servers zeigt an, die der ursprünglichen Sitzung getrennt nicht eingeben, aber stattdessen bleibt aktiv.

Um dieses Problem zu umgehen, können Sie die **Keep-alive-Verbindungsintervall konfigurieren** Richtlinie in die **Computerkonfiguration\\Administrative Vorlagen\\fürWindows-Komponenten\\ Remote Desktop Services\\Remote Desktop Session Host\\Verbindungen** Ordner "Group Policy". Wenn Sie diese Richtlinie aktivieren, müssen Sie ein Keep-alive-Intervall eingeben. Das Keep-alive-Intervall bestimmt, wie oft in Minuten an, der Server den Sitzungszustand überprüft.

Dieses Problem kann durch die Fehlkonfiguration von Einstellungen für die Authentifizierung und die Konfiguration verursacht werden. Sie können diese Einstellungen auf Serverebene oder mithilfe von Gruppenrichtlinienobjekten konfigurieren. Die gruppenrichtlinieneinstellungen finden Sie in der **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remote Desktop Services\\Remote Desktop Session Host\\ Sicherheit** Ordner "Group Policy".

1. Öffnen Sie auf dem RD-Sitzungshostserver die Konfiguration des Remotedesktop-Sitzungshosts.
2. Klicken Sie unter **Verbindungen**mit der rechten Maustaste auf den Namen der Verbindung, und klicken Sie dann auf **Eigenschaften**.
3. In der **Eigenschaften** im Dialogfeld für die Verbindung, auf die **allgemeine** Registerkarte **Sicherheit** layer, wählen Sie eine Methode.
4. In **Verschlüsselungsstufe**, klicken Sie auf der Ebene, die Sie möchten. Sie können auswählen, **mit niedriger**, **kompatibel mit dem Client**, **hohe**, oder **FIPS-kompatible**.

> [!NOTE]  
>  - Bei der Kommunikation zwischen Clients und RD-Sitzungshostserver die höchste Ebene der Verschlüsselung benötigen, verwenden Sie die FIPS-konforme Verschlüsselung.
>  - Verschlüsselungsstufeneinstellungen, die Sie in der Gruppenrichtlinie konfigurieren, überschreiben die Konfiguration, die Sie über das Remote Desktop Services-Konfigurationstool festlegen. Auch wenn Sie aktivieren die [Systemkryptografie: FIPS-konformen Algorithmus für Verschlüsselung, hashing und Signatur verwenden](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc780081\(v=ws.10\)) Richtlinie, um diese Einstellung überschreibt die **Verschlüsselungsstufe der Clientverbindung festlegen** Richtlinie. Die Kryptografie-Systemrichtlinie befindet sich in der **Computerkonfiguration\\Windows-Einstellungen\\Sicherheitseinstellungen\\lokale Richtlinien\\Sicherheitsoptionen** Ordner.
>  - Wenn Sie die Verschlüsselungsstufe ändern, wird die neue Verschlüsselungsstufe wirksam, sobald sich ein Benutzer das nächste Mal anmeldet. Wenn Sie mehrere Verschlüsselungsstufen auf einem Server benötigen, installieren Sie mehrere Netzwerkadapter, und konfigurieren Sie jeden Adapter getrennt.
>  - Um dieses Zertifikat verfügt über einen entsprechenden privaten Schlüssel in Remote Desktop Services-Konfiguration zu überprüfen, Maustaste die Verbindung für die Sie das Zertifikat anzuzeigen, aktivieren möchten **allgemeine**Option **bearbeiten**, wählen Sie das Zertifikat, das Sie anzeigen möchten, und wählen Sie dann **Zertifikat anzeigen**. Am unteren Rand der **allgemeine** Registerkarte, die Anweisung "Sie verfügen über einen privaten Schlüssel, die dieses Zertifikat entspricht" sollte angezeigt werden. Sie können diese Informationen auch mithilfe der Zertifikat-Snap-in anzeigen.
>  - FIPS-konforme Verschlüsselung (die **Systemkryptografie: FIPS-konformen Algorithmus für Verschlüsselung, hashing und Signatur** Richtlinie oder die **FIPS-kompatible** in Remote Desktop-Serverkonfiguration festlegen) verschlüsselt und entschlüsselt Daten, die vom Client gesendet werden, auf dem Server und aus der Server an den Client mit den Federal Information Processing Standard (FIPS) 140-1-Verschlüsselungsalgorithmen, verwendet kryptografische Module von Microsoft. Weitere Informationen finden Sie unter [FIPS 140-Überprüfung](https://docs.microsoft.com/en-us/windows/security/threat-protection/fips-140-validation).
>  - Die **hohe** Einstellung verschlüsselt die Daten, die vom Client an den Server und vom Server an den Client mithilfe von 128-Bit-Verschlüsselung gesendet.
>  - Die **Clientstandard** Einstellung verschlüsselt Datenübertragungen zwischen dem Client und dem Server unter der maximalen Verschlüsselungsstärke, die vom Client unterstützt werden.
>  - Die **niedrig** Einstellung verschlüsselt die Daten, die vom Client an den Server mit 56-Bit-Verschlüsselung gesendet.

## <a name="remote-laptop-disconnects-from-wireless-network"></a>Remote-Laptop trennt drahtloses Netzwerk

Dieses Problem kann auftreten, wenn einem Remotedesktopclient auf einem Laptop eine Verbindung herstellt, über ein Drahtlosnetzwerk 802.1 X. Gelegentlich, wird der Laptop dem drahtlosen Netzwerk trennt, und nicht automatisch neu.

Dies ist ein bekanntes Problem, das tritt auf, wenn für die drahtlose Netzwerkverbindung netzwerkauthentifizierungseinstellung **Benutzerauthentifizierung**.

Um dieses Problem zu umgehen, legen Sie netzwerkauthentifizierungseinstellung auf **Benutzer- oder Computerauthentifizierung** oder **Computerauthentifizierung**.

 > [!NOTE]  
> Um die Netzwerkeinstellungen für die Authentifizierung auf einem einzelnen Computer zu ändern, müssen Sie die Netzwerk- und Freigabecenter-Systemsteuerung verwenden, um eine neue drahtlose Verbindung mit den neuen Einstellungen zu erstellen.

Eine vollständige Beschreibung der Vorgehensweise: Konfigurieren von Einstellungen für drahtlose Netzwerke mithilfe der Gruppenrichtlinienobjekte finden Sie unter [Konfigurieren von Drahtlosnetzwerkrichtlinien (IEEE 802.11) Policies](https://docs.microsoft.com/en-us/windows-server/networking/core-network-guide/cncg/wireless/e-wireless-access-deployment#bkmk_policies).

## <a name="user-experiences-poor-performance-or-application-problems"></a>Benutzeroberflächen, eine schlechte Leistung oder Anwendungsproblemen

In diesem Abschnitt werden einige allgemeine Probleme, die Benutzer auftreten können, wenn sie die Remotedesktop-Funktionen verwenden:

  - [Benutzer, die für neue virtuelle Maschinen Microsoft Azure nicht ununterbrochen verbunden Probleme](#intermittent-problems-with-new-microsoft-azure-virtual-machines).
  - [Benutzer, die Verbindung mit Windows 10 Version 1709-Remotedesktops möglicherweise Probleme bei der Wiedergabe von video](#video-playback-issues-on-windows-10-version-1709).
  - [Benutzer mit nur-Lese Benutzerprofile, die mit Windows 10-remote-Desktops verbinden können ihre Desktops nicht freigeben.](#desktop-sharing-issues-on-windows-10)
  - [Herstellen einer Verbindung mit Windows 10-Remotedesktops mit Clients, die unter älteren Versionen von Windows 10 ausgeführt werden. Benutzer kommen zu Leistungsproblemen, wenn NLA-Feature deaktiviert ist](#performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled)
  - [Wenn Benutzer mehrere Anwendungen in Remotedesktopsitzungen führen und trennen und häufig wiederherstellen, können sie einen schwarzen Bildschirm beim Wiederherstellen der Verbindung auftreten.](#black-screen-issue)

### <a name="intermittent-problems-with-new-microsoft-azure-virtual-machines"></a>Wiederholt auftretende Probleme mit der neuen Microsoft Azure-Computern

Dieses Problem wirkt sich auf virtuellen Computern, die vor kurzem bereitgestellt wurden. Nachdem der Benutzer eine Verbindung mit dem virtuellen Computer herstellt, die Remotedesktopsitzung kann nicht geladen werden alle die Einstellungen des Benutzers korrekt.

Um dieses Problem zu umgehen, trennen Sie die virtuelle Maschine mindestens 20 Minuten warten Sie und dann erneut eine Verbindung her.

Um dieses Problem zu beheben, müssen wenden Sie die folgenden Updates auf dem virtuellen Computer nach Bedarf an:

  - Windows 10 und WindowsServer 2016: KB 4343884, [30. August 2018 – KB4343884 (Betriebssystembuild 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)
  - Windows Server 2012 R2: KB 4343891, [30. August 2018 – KB4343891 (Vorschau des monatlichen Rollups)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)

### <a name="video-playback-issues-on-windows-10-version-1709"></a>Videowiedergabe-Problemen unter Windows 10 Version 1709

Dieses Problem tritt auf, wenn der Benutzer eine Verbindung mit Remotecomputern herstellen, auf denen Windows 10, Version 1709 ausgeführt werden. Wenn diese Benutzer Videowiedergabe mit der VMR9 (Video das Kombinieren von Renderer 9)-Codec, der Spieler zeigt nur ein schwarzes Fenster.

Dies ist ein bekanntes Problem in Windows 10, Version 1709. Das Problem tritt nicht unter Windows 10 Version 1703.

### <a name="desktop-sharing-issues-on-windows-10"></a>Freigeben von Problemen auf Windows 10 Desktop

Dieses Problem tritt auf, wenn der Benutzer eine nur-Lese Benutzerprofil (sowie den zugehörigen Registrierungsstruktur), z. B. in einem Szenario mit Kiosk verfügt. Wenn diese Benutzer mit einem Remotecomputer herstellt, auf denen Windows 10, Version 1803, ausgeführt wird, können nicht sie ihren Desktop freigeben.

Um dieses Problem beheben, wenden Sie das Windows 10-Update 4340917, [24. Juli 2018 – KB4340917 (OS Build 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917).

### <a name="performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled"></a>Leistungsprobleme beim Kombinieren von Versionen von Windows 10, wenn der NLA-Feature deaktiviert ist

Dieses Problem tritt auf, wenn NLA-Feature ist deaktiviert, und Remotedesktop-Client-Computer, auf denen Windows 10 verbinden, Remotedesktops, die unterschiedliche Versionen von Windows 10 ausführen. Benutzer von remote desktop-Clients auf Computern mit Windows 10, Version 1709 oder früheren Versionen kommen zu Leistungsproblemen, beim Verbinden mit remote-Desktops, auf denen Windows 10, Version 1803 oder eine höhere Version ausgeführt.

Dies tritt auf, da bei der Authentifizierung auf Netzwerkebene deaktiviert ist, die älteren Client-Computer ein langsameres Protokoll beim Verbinden mit Windows 10, Version 1803 oder höher verwendet.

Dieses Problem zu beheben, weisen Sie die KB-4340917 [24. Juli 2018 – KB4340917 (OS Build 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917).

### <a name="black-screen-issue"></a>Schwarzer Bildschirm angezeigt

Dieses Problem tritt in Windows 8.0, Windows 8.1, Windows 10 RTM und Windows Server 2012 R2. Ein Benutzer mehrere Anwendungen auf einem remote Desktop startet, dann aus der Sitzung wird getrennt. In regelmäßigen Abständen, verbindet sich der Benutzer die Remotedesktopverbindung mit den Anwendungen interagieren, und trennen Sie dann erneut. An einem bestimmten Punkt, wenn der Benutzer die Verbindung wiederherstellt, zeigt die Remotedesktopsitzung nur einen schwarzen Bildschirm. Der Benutzer muss über die Remotedesktopsitzung aus dem Remotecomputer-Konsole (oder die RDSH-Server-Verwaltungskonsole) enden. Diese Aktion beendet die Anwendungen.

Um dieses Problem zu beheben, müssen wenden Sie die folgenden Updates nach Bedarf an:

  - Windows 8 und WindowsServer 2012: KB4103719, [17 Mai 2018 – KB4103719 (Vorschau des monatlichen Rollups)](https://support.microsoft.com/en-us/help/4103719/windows-server-2012-update-kb4103719)
  - Windows 8.1 und Windows Server 2012 R2: KB4103724, [17 Mai 2018 – KB4103724 (Vorschau des monatlichen Rollups)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724) und KB 4284863, [am 21. Juni 2018 – KB4284863 (Vorschau des monatlichen Rollups)](https://support.microsoft.com/en-us/help/4284863/windows-81-update-kb4284863)
  - Windows 10: Behoben in KB4284860, [12. Juni 2018 – KB4284860 (Betriebssystembuild 10240.17889)](https://support.microsoft.com/en-us/help/4284860/windows-10-update-kb4284860)
