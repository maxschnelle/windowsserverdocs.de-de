---
title: Problembehandlung bei Remotedesktopverbindungen
description: Vorgehensweisen zur Problembehandlung, nach Symptom geordnet
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
ms.openlocfilehash: c6ce719ffa24cfc6704348c17548fe5cf33d9271
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284145"
---
# <a name="troubleshooting-remote-desktop-connections"></a>Problembehandlung bei Remotedesktopverbindungen
Kurze Erläuterungen einiger der häufigsten Probleme mit Remotedesktopdiensten (RDS) finden Sie unter [Häufig gestellte Fragen zu den Remotedesktopclients](https://review.docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-client-faq). Dieser Artikel beschreibt eine Reihe höher entwickelter Vorgehensweisen zum Beheben von Verbindungsproblemen. Viele dieser Verfahren gelten für Probleme in einfachen Konfigurationen, wie etwa Verbindungen zwischen zwei physischen Computern, ebenso wie für komplexere Konfigurationen. Einige Vorgehensweisen befassen sich mit Problemen, die nur in komplexeren Szenarien mit mehreren Benutzern auftreten. Weitere Informationen über die Remotedesktopkomponenten und die Weise ihrer Interaktion finden Sie unter [Architektur der Remotedesktopdienste](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/desktop-hosting-logical-architecture).

> [!NOTE]  
> Viele der in diesem Artikel beschriebenen Prozeduren erfordern von Ihnen den Zugriff auf mehrere Computer, von denen Sie auf einige remote zugreifen müssen. Weitere Informationen über Tools zur Remoteverwaltung und ihre Konfiguration finden Sie unter [Remoteserver-Verwaltungstools (RSAT) für Windows-Betriebssysteme](https://support.microsoft.com/en-us/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems).

Identifizieren Sie in der folgenden Liste die Art des Symptoms, das bei Ihnen (oder Ihren Benutzern) auftritt.

- [Der Remotedesktopclient kann keine Verbindung mit dem Remotedesktop herstellen, es gibt aber keine spezifischen Symptome oder Nachrichten (allgemeine Schritte zur Problembehandlung)](#no-specific-symptoms-or-messages-general-troubleshooting-steps)
- [Der Remotedesktopclient kann keine Verbindung mit dem Remotedesktop herstellen und empfängt eine Nachricht „Klasse nicht registriert“](#client-cannot-connect-class-not-registered)
- [Der Remotedesktopclient kann keine Verbindung mit dem Remotedesktop herstellen und empfängt eine Nachricht „Keine Lizenzen verfügbar“ oder „Sicherheitsfehler“](#client-cannot-connect-no-licenses-available)
- [Der Benutzer empfängt eine Nachricht „Zugriff verweigert“ oder muss die Anmeldeinformationen zweimal eingeben](#user-cannot-authenticate-or-must-authenticate-twice)
- [Beim Herstellen der Verbindung wird eine Nachricht „Der Remotedesktopdienst ist aktuell ausgelastet“ empfangen](#on-connecting-user-receives-remote-desktop-service-is-currently-busy-message)
- [Der Remotedesktopclient wird getrennt und kann die Verbindung zur gleichen Sitzung nicht wiederherstellen](#rd-client-disconnects-and-cannot-reconnect-to-the-same-session)
- [Der Benutzer stellt über ein drahtloses Netzwerk eine Verbindung mit einem Remotelaptop her, anschließend trennt der Laptop die Netzwerkverbindung](#remote-laptop-disconnects-from-wireless-network).
- [Beim Benutzer treten schlechte Leistung von oder Probleme mit Remoteanwendungen auf](#user-experiences-poor-performance-or-application-problems)

> [!NOTE]  
> Eine aktuelle Liste der RDP-Trennungscodes finden Sie unter [ExtendedDisconnectReasonCode enumeration](https://docs.microsoft.com/windows/desktop/TermServ/extendeddisconnectreasoncode) (Erweiterte DisconnectReasonCode-Enumeration). 

## <a name="no-specific-symptoms-or-messages-general-troubleshooting-steps"></a>Keine spezifischen Symptome oder Nachrichten (allgemeine Schritte zur Problembehandlung)

Führen Sie diese Schritte aus, wenn ein Remotedesktopclient keine Verbindung mit einem Remotedesktop herstellen kann, aber keine Nachrichten oder sonstigen Symptome zur Verfügung stellt, die beim Bestimmen der Ursache nützlich wären. Verwenden Sie die folgenden Methoden, um viele der häufigsten Ursachen dieser Art von Problem zu beheben:

- [Überprüfen des Status des RDP-Protokolls](#check-the-status-of-the-rdp-protocol)
- [Überprüfen des Status der RDP-Dienste](#check-the-status-of-the-rdp-services)
- [Überprüfen der Funktion des RDP-Listeners](#check-that-the-rdp-listener-is-functioning)
- [Überprüfen des RDP-Listener-Ports](#check-the-rdp-listener-port)

### <a name="check-the-status-of-the-rdp-protocol"></a>Überprüfen des Status des RDP-Protokolls

#### <a name="check-the-status-of-the-rdp-protocol-on-a-local-computer"></a>Überprüfen des Status des RDP-Protokolls auf einem lokalen Computer

Informationen zum Überprüfen und Ändern des Status des RDP-Protokolls auf einem lokalen Computer finden Sie unter [So aktivieren Sie Remotedesktop](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#how-to-enable-remote-desktop).

> [!NOTE]  
> Wenn die Remotedesktopoptionen nicht verfügbar sind, lesen Sie [Überprüfen, ob ein Gruppenrichtlinienobjekt RDP blockiert](#check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer).

#### <a name="check-the-status-of-the-rdp-protocol-on-a-remote-computer"></a>Überprüfen des Status des RDP-Protokolls auf einem Remotecomputer

> [!IMPORTANT]  
> Folgen Sie den Schritten in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie sie ändern, [sichern Sie die Registrierung zwecks Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Probleme auftreten.

Um den Status des RDP-Protokolls auf einem Remotecomputer zu überprüfen und zu ändern, verwenden Sie eine Netzwerkverbindung mit der Registrierung:

1. Wählen Sie **Start** und dann **Ausführen** aus, und geben Sie dann **regedt32** ein.
2. Wählen Sie im Registrierungs-Editor **Datei** und dann **Netzwerkregistrierung verbinden** aus.
3. Geben Sie im Dialogfeld **Computer auswählen** den Namen des Remotecomputers ein, wählen Sie **Namen überprüfen** und dann **OK** aus.
4. Navigieren Sie zu **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server**.  
   ![Registrierungs-Editor mit Darstellung des Eintrags „fDenyTSConnections“](../media/troubleshoot-remote-desktop-connections/RegEntry_fDenyTSConnections.png)
   - Wenn der Wert des **fDenyTSConnections**-Schlüssels **0** ist, ist RDP aktiviert
   - Wenn der Wert des **fDenyTSConnections**-Schlüssels **1** ist, ist RDP deaktiviert
5. Um RDP zu aktivieren, ändern Sie den Wert von **fDenyTSConnections** von **1** in **0**.

#### <a name="check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer"></a>Überprüfen, ob ein Gruppenrichtlinienobjekt RDP auf einem lokalen Computer blockiert

Wenn Sie RDP nicht auf der Benutzeroberfläche aktivieren können oder der Wert von **fDenyTSConnections** wieder auf **1** zurückgesetzt wird, nachdem Sie ihn geändert haben, setzt möglicherweise ein GPO die Einstellungen auf Computerebene außer Kraft.

Um die Gruppenrichtlinienkonfiguration auf einem lokalen Computer zu überprüfen, öffnen Sie ein Eingabeaufforderungsfenster als Administrator, und geben Sie den folgenden Befehl ein:
```
gpresult /H c:\gpresult.html
```
Öffnen Sie nach dem Abschluss dieses Befehls „gpresult.html“. Suchen Sie in **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remotedesktopdienste\\Remotedesktop-Sitzungshost\\Verbindungen** die Richtlinie **Remoteverbindungen für Benutzer mithilfe der Remotedesktopdienste zulassen**.

- Wenn die Einstellung für diese Richtlinie **Aktiviert** ist, werden RDP-Verbindungen nicht durch eine Gruppenrichtlinie blockiert.
- Wenn die Einstellung für diese Richtlinie **Deaktiviert** ist, überprüfen Sie **Ausschlaggebendes Gruppenrichtlinienobjekt**. Das ist das Gruppenrichtlinienobjekt, das RDP-Verbindungen blockiert.
  ![Ein Beispielsegment von „gpresult.html“, in dem das GPO **Block RDP** RDP deaktiviert.](../media/troubleshoot-remote-desktop-connections/GPResult_RDSH_Connections_GP.png)
   
  ![Ein Beispielsegment von „gpresult.html“, in dem **Lokale Gruppenrichtlinie** RDP deaktiviert.](../media/troubleshoot-remote-desktop-connections/GPResult_RDSH_Connections_LGP.png)

#### <a name="check-whether-a-gpo-is-blocking-rdp-on-a-remote-computer"></a>Überprüfen, ob ein GPO RDP auf einem Remotecomputer blockiert

Der Befehl zum Überprüfen der Konfiguration von Gruppenrichtlinien auf einem Remotecomputer lautet fast genauso wie für einen lokalen Computer:
```
gpresult /S <computer name> /H c:\gpresult-<computer name>.html
```
Die Datei, die durch diesen Befehl erzeugt wird (**gpresult-\<computername\>.html**) verwendet das gleiche Informationsformat wie in der Version für lokale Computer (**gpresult.html**).

#### <a name="modifying-a-blocking-gpo"></a>Ändern ein blockierenden Gruppenrichtlinienobjekts

Sie können diese Einstellungen im Gruppenrichtlinienobjekt-Editor (GPE) und der Gruppenrichtlinien-Verwaltungskonsole (GPM) ändern. Weitere Informationen zum Verwenden der Gruppenrichtlinie finden Sie unter [Advanced Group Policy Management](https://docs.microsoft.com/microsoft-desktop-optimization-pack/agpm/) (Erweiterte Gruppenrichtlinienverwaltung).

Verwenden Sie eins der folgenden Verfahren, um die blockierende Richtlinie zu ändern:

- Greifen Sie im GPE auf die passende GPO-Ebene (wie etwa lokal oder Domäne) zu, und navigieren Sie zu **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remotedesktopdienste\\Remotedesktop-Sitzungshost\\Verbindungen**\\**Remoteverbindungen für Benutzer mithilfe der Remotedesktopdienste zulassen**.  
   1. Legen Sie die Richtlinie auf **Aktiviert** oder **Nicht konfiguriert** fest.
   2. Öffnen Sie auf den betroffenen Computern ein Eingabeaufforderungsfenster als Administrator, und führen Sie den Befehl **gpupdate /force** aus.
- Navigieren Sie in GPM zu der Organisationseinheit, in der die blockierende Richtlinie auf die betroffenen Computer angewendet wird, und löschen Sie die Richtlinie aus der Organisationseinheit.

### <a name="check-the-status-of-the-rdp-services"></a>Überprüfen des Status der RDP-Dienste

Auf dem lokalen Computer (Client) und dem Remotecomputer (Zielcomputer) sollten die folgenden Dienste ausgeführt werden:

- Remotedesktopdienste (TermService)
- Portumleitung für Remotedesktopdienste im Benutzermodus (UmRdpService)

Sie können das Dienste-MMC-Snap-In verwenden, um die Dienste lokal oder remote zu verwalten. Sie können darüber hinaus PowerShell lokal oder remote verwenden (wenn der Remotecomputer für das Annehmen von PowerShell-Remotebefehlen konfiguriert ist).

![Remotedesktopdienste im Dienste-MMC-Snap-In. Ändern Sie die Standardeinstellungen für den Dienst nicht.](../media/troubleshoot-remote-desktop-connections/RDSServiceStatus.png)

Wenn einer der Dienste (oder beide) auf einem von beiden Computern nicht ausgeführt wird, starten Sie ihn.

> [!NOTE]  
> Wenn Sie den Remotedesktopdienst starten, klicken Sie auf **Ja**, um den Portumleitungsdienst für Remotedesktopdienste im Benutzermodus automatisch neu zu starten.

### <a name="check-that-the-rdp-listener-is-functioning"></a>Überprüfen der Funktion des RDP-Listeners

> [!IMPORTANT]  
> Folgen Sie den Schritten in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie sie ändern, [sichern Sie die Registrierung zwecks Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Probleme auftreten.

#### <a name="check-the-status-of-the-rdp-listener"></a>Überprüfen des Status des RDP-Listeners

Verwenden Sie für dieses Verfahren eine PowerShell-Instanz, die über Administratorberechtigungen verfügt. Für einen lokalen Computer können Sie auch eine Eingabeaufforderung mit Administratorberechtigungen verwenden. In diesem Verfahren verwenden wir aber PowerShell, da die gleichen Befehle sowohl lokal als auch remote funktionieren.

1. Öffnen Sie ein PowerShell-Fenster. Um eine Verbindung mit einem Remotecomputer herzustellen, geben Sie **Enter-PSSession -ComputerName \<Computername\>** ein.
2. Geben Sie **qwinsta** ein. 
    ![Der Befehl „qwinsta“ listet die Prozesse auf, die an den Ports des Computers lauschen.](../media/troubleshoot-remote-desktop-connections/WPS_qwinsta.png)
3. Wenn die Liste **rdp-tcp** mit dem Status **Listen** (Lauschen) enthält, funktioniert der RDP-Listener. Fahren Sie mit [Überprüfen des RDP-Listener-Ports](#check-the-rdp-listener-port) fort. Fahren Sie andernfalls mit Schritt 4 fort.
4. Exportieren der RDP-Listener-Konfiguration von einem funktionierenden Computer.
    1. Melden Sie sich bei einem Computer an, der die gleiche Betriebssystemversion wie der betroffene Computer aufweist, und greifen Sie auf die Registrierung dieses Computers zu (beispielsweise mithilfe des Registrierungs-Editors).
    2. Navigieren Sie zu folgendem Registrierungseintrag:  
        **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\RDP-Tcp**
    3. Exportieren Sie den Eintrag in eine REG-Datei. Klicken Sie beispielsweise im Registrierungs-Editor mit der rechten Maustaste auf den Eintrag, wählen Sie **Exportieren** aus, und geben Sie dann einen Dateinamen für die exportierten Einstellungen ein.
    4. Kopieren Sie die exportierte REG-Datei auf den betroffenen Computer.
5. Um die Konfiguration des RDP-Listeners zu importieren, öffnen Sie ein PowerShell-Fenster, das über Administratorberechtigungen auf dem betroffenen Computer verfügt (oder öffnen Sie das PowerShell-Fenster, und stellen Sie eine Remoteverbindung mit dem betroffenen Computer her).
   1. Geben Sie den folgenden Befehl ein, um den vorhandenen Registrierungseintrag zu sichern:  
   
      ```powershell  
      cmd /c 'reg export "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp" C:\Rdp-tcp-backup.reg'   
      ```  
   

   2. Geben Sie den folgenden Befehl ein, um den vorhandenen Registrierungseintrag zu entfernen:  
   
      ```powershell  
      Remove-Item -path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp' -Recurse -Force  
      ```
   
   3. Um den neuen Registrierungseintrag zu importieren und den Dienst anschließend neu zu starten, geben Sie die folgenden Befehle ein:  
   
      ```powershell  
      cmd /c 'regedit /s c:\<filename>.reg'  
      Restart-Service TermService -Force  
      ```   
      dabei steht \<Dateiname\> für den Namen der exportierten REG-Datei.
6. Testen Sie die Konfiguration, indem Sie erneut versuchen, die Remotedesktopverbindung herzustellen. Wenn Sie trotzdem keine Verbindung herstellen können, führen Sie einen Neustart des betroffenen Computers durch.
7. Wenn Sie noch immer keine Verbindung herstellen können, [überprüfen Sie den Status des selbstsignierten RDP-Zertifikats](#check-the-status-of-the-rdp-self-signed-certificate).

#### <a name="check-the-status-of-the-rdp-self-signed-certificate"></a>Überprüfen des Status des selbstsignierten RDP-Zertifikats

1. Wenn Sie immer noch keine Verbindung herstellen können, öffnen Sie das MMC-Zertifikate-Snap-In. Wenn Sie aufgefordert werden, den zu verwaltenden Zertifikatspeicher auszuwählen, wählen Sie **Computerkonto** und dann den betroffenen Computer aus.
2. Löschen Sie im Ordner **Certificates** unter **Remote Desktop** das selbstsignierte RDP-Zertifikat. 
    ![Remotedesktopzertifikate im MMC-Zertifikate-Snap-In.](../media/troubleshoot-remote-desktop-connections/MMCCert_Delete.png)
3. Starten Sie auf dem betroffenen Computer die Remotedesktopdienste erneut.
4. Aktualisieren Sie das Zertifikate-Snap-In.
5. Wenn das selbstsignierte RDP-Zertifikat nicht erneut erstellt wurde, [überprüfen Sie die Berechtigungen des MachineKeys-Ordners](#check-the-permissions-of-the-machinekeys-folder).

#### <a name="check-the-permissions-of-the-machinekeys-folder"></a>Überprüfen der Berechtigungen des MachineKeys-Ordners

1. Öffnen Sie auf dem betroffenen Computer den Explorer, und navigieren Sie dann zu **C:\\Programme\\Microsoft\\Crypto\\RSA\\** .
2. Klicken Sie mit der rechen Maustaste auf **MachineKeys**, wählen Sie **Eigenschaften**, dann **Sicherheit** und schließlich **Erweitert** aus.
3. Vergewissern Sie sich, dass die folgenden Berechtigungen konfiguriert sind:
      - Vordefiniert\\Administratoren: Vollzugriff
      - Jeder: Lesen, Schreiben

### <a name="check-the-rdp-listener-port"></a>Überprüfen des RDP-Listener-Ports

Auf dem lokalen Computer (Client) und dem Remotecomputer (Zielcomputer) sollte der RDP-Listener an Port 3389 lauschen. Keine anderen Anwendungen sollten diesen Port verwenden.

> [!IMPORTANT]  
> Folgen Sie den Schritten in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie sie ändern, [sichern Sie die Registrierung zwecks Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Probleme auftreten.

Um den RDP-Port zu überprüfen oder zu ändern, verwenden Sie den Registrierungs-Editor:

1. Wählen Sie „Start“, dann **Ausführen** aus, und geben Sie dann **regedt32** ein.
      - Um eine Verbindung mit einem Remotecomputer herzustellen, wählen Sie **Datei** und dann **Mit Netzwerkregistrierung verbinden** aus.
      - Geben Sie im Dialogfeld **Computer auswählen** den Namen des Remotecomputers ein, wählen Sie **Namen überprüfen** und dann **OK** aus.
2. Öffnen Sie die Registrierung, und navigieren Sie zu **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<listener\>** . 
    ![Der PortNumber-Unterschlüssel für das RDP-Protokoll.](../media/troubleshoot-remote-desktop-connections/RegEntry_PortNumber.png)
3. Wenn **PortNumber** einen anderen Wert als **3389** aufweist, ändern Sie ihn in **3389**. 
   > [!IMPORTANT]  
    > Sie können die Remotedesktopdienste über einen anderen Port betreiben. Allerdings raten wir davon ab. Die Problembehandlung für eine derartige Konfiguration liegt außerhalb des Bereichs dieses Artikels.
4. Führen Sie nach dem Ändern der Portnummer einen Neustart des Remotedesktopdiensts durch.

#### <a name="check-that-another-application-is-not-trying-to-use-the-same-port"></a>Überprüfen, ob eine andere Anwendung den gleichen Port zu verwenden versucht

Verwenden Sie für dieses Verfahren eine PowerShell-Instanz, die über Administratorberechtigungen verfügt. Für einen lokalen Computer können Sie auch eine Eingabeaufforderung mit Administratorberechtigungen verwenden. In diesem Verfahren verwenden wir aber PowerShell, da die gleichen Befehle lokal wie auch remote funktionieren.

1. Öffnen Sie ein PowerShell-Fenster. Um eine Verbindung mit einem Remotecomputer herzustellen, geben Sie **Enter-PSSession -ComputerName \<Computername\>** ein.
2. Geben Sie den folgenden Befehl aus:  
   
     ```powershell  
    cmd /c 'netstat -ano | find "3389"'  
    ```
  
    ![Der Netstat-Befehl erzeugt eine Liste der Ports und der Dienste, die an ihnen lauschen.](../media/troubleshoot-remote-desktop-connections/WPS_netstat.png)
3. Suchen Sie nach einem Eintrag für den TCP-Port 3389 (oder dem zugewiesenen RDP-Port) mit dem Status **Empfangsbereit**. 
    > [!NOTE]  
   > In der Spalte PID wird die PID (Prozess-ID) des Prozesses oder Diensts angezeigt, der diesen Port verwendet.
4. Um zu bestimmen, welche Anwendung Port 3389 (oder den zugewiesenen RDP-Port) verwendet, geben Sie den folgenden Befehl ein:  
   
     ```powershell  
    cmd /c 'tasklist /svc | find "<pid listening on 3389>"'  
    ```  
  
    ![Der Aufgabenlistenbefehl meldet Details zu einem bestimmten Prozess.](../media/troubleshoot-remote-desktop-connections/WPS_tasklist.png)
5. Suchen Sie nach einem Eintrag für die PID-Nummer, die dem Port zugeordnet ist (gemäß der **netstat**-Ausgabe). Die Dienste oder Prozesse, die der betreffenden PID zugeordnet sind, werden rechts angezeigt.
6. Wenn eine andere Anwendung oder ein anderer Dienst als Remotedesktopdienste (TermServ.exe) den Port verwendet, können Sie den Konflikt mit einem der folgenden Verfahren beheben:
      - Konfigurieren der anderen Anwendung oder des anderen Diensts für die Verwendung eines anderen Ports (empfohlen).
      - Deinstallieren der anderen Anwendung oder des anderen Diensts.
      - Konfigurieren von RDP für die Verwendung eines anderen Ports, gefolgt von einem Neustart der Remotedesktopdienste (nicht empfohlen).

#### <a name="check-whether-a-firewall-is-blocking-the-rdp-port"></a>Überprüfen, ob der RDP-Port durch eine Firewall blockiert wird

Verwenden Sie das **psping**-Tool, um zu testen, ob Sie den betroffenen Computer über Port 3389 erreichen können.

1. Laden Sie auf einem anderen als dem betroffenen Computer **psping** von <https://live.sysinternals.com/psping.exe> herunter.
2. Öffnen Sie ein Eingabeaufforderungsfenster als Administrator, wechseln Sie in das Verzeichnis, in dem Sie **psping** installiert haben, und geben Sie dann den folgenden Befehl ein:  
   
   ```  
   psping -accepteula <computer IP>:3389  
   ```
   
3. Überprüfen Sie die Ausgabe des **psping**-Befehls auf Ergebnisse wie das folgende:  
      - **Herstellen einer Verbindung mit \<Computer-IP-Adresse\>** : Der Remotecomputer ist erreichbar.
      - **(0 % Verlust)** : Alle Verbindungsversuche waren erfolgreich.
      - **Der Remotecomputer hat die Netzwerkverbindung abgelehnt**: Der Remotecomputer ist nicht erreichbar.
      - **(100 % Verlust)** : Bei allen Verbindungsversuchen ist ein Fehler aufgetreten.
1. Führen Sie **psping** auf mehreren Computern aus, um ihre Fähigkeit zu überprüfen, eine Verbindung mit dem betroffenen Computer herzustellen.
1. Achten Sie darauf, ob der betroffene Computer Verbindungen von allen anderen Computern, von einigen anderen Computern oder nur von einem anderen Computer blockiert.
1. Empfohlene nächste Schritte:
      - Tauschen Sie sich mit Ihren Netzwerkadministratoren aus, um sicherzustellen, dass das Netzwerk RDP-Datenverkehr zum betroffenen Computer zulässt.
      - Untersuchen Sie die Konfigurationen aller Firewalls zwischen den Quellcomputern und dem betroffenen Computer (einschließlich der Windows Firewall auf dem betroffenen Computer), um zu bestimmen, ob eine Firewall den RDP-Port blockiert.

## <a name="client-cannot-connect-class-not-registered"></a>Der Client kann keine Verbindung herstellen, „Klasse nicht registriert“

Wenn Sie versuchen, eine Verbindung mit einem Remotecomputer mithilfe eines Clients herzustellen, der Windows 10, Version 1709 oder höher, ausführt, stellt der Client möglicherweise keine Verbindung her, während der Remotedesktop-Sitzungshostserver eine Nachricht meldet, die den Fehlercode „Klasse nicht registriert (0x80040154)“ enthält.

Dieses Problem tritt auf, wenn der Benutzer, der die Verbindung herzustellen versucht, über ein obligatorisches Benutzerprofil verfügt. Um dieses Problem zu beheben, installieren Sie das Windows 10-Update vom [24. Juli 2018—KB4338817 (Betriebssystembuild 16299.579)](https://support.microsoft.com/en-us/help/4338817/windows-10-update-kb4338817).

## <a name="client-cannot-connect-no-licenses-available"></a>Der Client kann keine Verbindung herstellen, keine Lizenzen verfügbar

Diese Situation betrifft alle Bereitstellungen, die einen RDSH-Server und einen Remotedesktop-Lizenzierungsserver beinhalten.

Bestimmen Sie die Art von Verhalten, die Benutzer erleben:

- Die Sitzung wurde getrennt, weil keine Lizenzen verfügbar sind oder kein Lizenzserver verfügbar ist
- Der Zugriff wurde aufgrund eines Sicherheitsfehlers verweigert

Melden Sie sich beim RD-Sitzungshost als Domänenadministrator an, und öffnen Sie die RD-Lizenzdiagnose. Suchen Sie nach Nachrichten wie der folgenden:

  - Die Kulanzfrist für den Remotedesktop-Sitzungshostserver ist abgelaufen, der RD-Sitzungshostserver wurde jedoch noch nicht mit Lizenzservern konfiguriert. Verbindungen mit dem RD-Sitzungshostserver werden abgelehnt, bis ein Lizenzserver für den RD-Sitzungshostserver konfiguriert wurde.
  - Der Lizenzserver \<Computername\> ist nicht verfügbar. Dies könnte durch Probleme mit der Netzwerkverbindung verursacht sein oder darauf beruhen, dass der Remotedesktop-Lizenzierungsdienst auf dem Lizenzserver beendet wurde oder die RD-Lizenzierung nicht mehr auf dem Computer installiert ist.

Diese Probleme gehen häufig mit den folgenden Benutzermeldungen einher:

  - Die Remotesitzung wurde getrennt, da für diesen Computer keine Remotedesktop-Clientzugriffslizenzen verfügbar sind.
  - Die Remotesitzung wurde getrennt, da keine Remotedesktop-Lizenzserver verfügbar sind, um eine Lizenz bereitzustellen.

In diesem Fall können Sie [den RD-Lizenzierungsdienst konfigurieren](#configure-the-rd-licensing-service).

Wenn die RD-Lizenzdiagnose andere Probleme auflistet, wie etwa „Die RDP-Protokollkomponente X.224 hat einen Fehler im Protokolldatenstrom erkannt und den Client getrennt“, liegt möglicherweise ein Problem vor, das die Lizenzzertifikate betrifft. Solche Probleme gehen häufig mit Benutzermeldungen einher, wie etwa der folgenden:

Aufgrund eines Sicherheitsfehlers konnte der Client keine Verbindung mit dem Terminalserver herstellen. Nachdem Sie sichergestellt haben, dass Sie beim Netzwerk angemeldet sind, versuchen Sie noch einmal, eine Verbindung mit dem Server herzustellen.

In diesem Fall können Sie [die Registrierungsschlüssel des X509-Zertifikats aktualisieren](#refresh-the-x509-certificate-registry-keys).

### <a name="configure-the-rd-licensing-service"></a>Konfigurieren des RD-Lizenzierungsdiensts

Im folgenden Verfahren wird der Server-Manager für die Konfigurationsänderungen verwendet. Weitere Informationen zum Konfigurieren und Verwenden des Server-Managers finden Sie unter [Server-Manager](https://docs.microsoft.com/windows-server/administration/server-manager/server-manager).

1. Öffnen Sie Server-Manager, und navigieren Sie dann zu **Remotedesktopdienste**.
2. Wählen Sie unter **Bereitstellungsübersicht** zuerst **Aufgaben** und anschließend **Bereitstellungseigenschaften bearbeiten** aus.
3. Wählen Sie **RD-Lizenzierung** und dann den passenden Lizenzierungsmodus für Ihre Bereitstellung aus (**Pro Gerät** oder **Pro Benutzer**).
4. Geben Sie den vollqualifizierten Domänennamen (FQDN) Ihres RD-Lizenzservers ein, und wählen Sie dann **Hinzufügen** aus.
5. Wenn Sie über mehrere RD-Lizenzserver verfügen, wiederholen Sie Schritt 4 für jeden Server. 
    ![Konfigurationsoptionen für den RD-Lizenzserver in Server-Manager.](../media/troubleshoot-remote-desktop-connections/RDLicensing_Configure.png)

### <a name="refresh-the-x509-certificate-registry-keys"></a>Aktualisieren der Registrierungsschlüssel des X509-Zertifikats

> [!IMPORTANT]  
> Folgen Sie den Schritten in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie sie ändern, [sichern Sie die Registrierung zwecks Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Probleme auftreten.

Um dieses Problem zu beheben, sichern Sie die Registrierungsschlüssel des X509-Zertifikats, entfernen Sie sie anschließend, starten Sie den Computer neu, und aktivieren Sie den RD-Lizenzierungsserver erneut. Führen Sie dazu folgende Schritte durch.

> [!NOTE]  
> Führen Sie den folgenden Vorgang auf jedem der RDSH-Server durch.

1. Öffnen Sie den Registrierungs-Editor, und navigieren Sie zu **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\RCM**.
2. Wählen Sie im Menü „Registrierung“ **Registrierungsdatei exportieren** aus.
3. Geben Sie **exportiertes Zertifikat** im Feld **Dateiname** ein, und wählen Sie dann **Speichern** aus.
4. Klicken Sie mit der rechten Maustaste auf jeden der folgenden Werte, wählen Sie **Löschen** und anschließend **Ja** aus, um die Löschung zu bestätigen:  
      - **Certificate**
      - **X509 Certificate**
      - **X509 Certificate ID**
      - **X509-Zertifikat2**
5. Schließen Sie den Registrierungs-Editor, und starten Sie den RDSH-Server anschließend neu.

## <a name="user-cannot-authenticate-or-must-authenticate-twice"></a>Der Benutzer kann sich nicht authentifizieren oder muss sich zweimal authentifizieren

Probleme, die sich auf die Benutzerauthentifizierung auswirken, können in verschiedenen Bereichen auftreten. In diesem Abschnitt werden die folgenden Fälle behandelt:

  - [Einem Benutzer wird der Zugriff verweigert und eine Meldung „eingeschränkter Anmeldetyp“ zurückgegeben](#access-denied-restricted-type-of-logon)
  - [Einem Benutzer oder einer Anwendung wird der Zugriff mit Ereignis 16965 verweigert, „Ein Remoteaufruf der SAM-Datenbank wurde verweigert“](#access-denied-a-remote-call-to-the-sam-database-has-been-denied)
  - [Ein Benutzer kann sich nicht mithilfe einer Smartcard anmelden](#a-user-cannot-sign-in-by-using-a-smart-card)
  - [Wenn der Remotecomputer gesperrt ist, muss ein Benutzer das Kennwort zweimal eingeben](#if-the-remote-pc-is-locked-a-user-needs-to-enter-a-password-twice)
  - [Ein Benutzer kann sich nicht anmelden und erhält die Meldungen „Authentifizierungsfehler“ und „CredSSP encryption oracle remediation“ (CredSSP-Verschlüsselung – Oracle-Wartung)](#user-cannot-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages)
  - [Nach einem Update von Clientcomputern müssen sich manche Benutzer zweimal anmelden](#after-you-update-client-computers-some-users-need-to-sign-in-twice).
  - [Benutzern wird der Zugriff auf eine Bereitstellung verweigert, die RemoteGuard mit mehreren RD-Verbindungsbrokern verwendet](#users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers)

### <a name="access-denied-restricted-type-of-logon"></a>Zugriff verweigert, eingeschränkter Anmeldungstyp

In diesem Fall wird einem Windows 10-Benutzer, der versucht, eine Verbindung mit Windows 10- oder Windows Server 2016-Computern herzustellen, der Zugriff mit der folgenden Meldung verweigert:

> Remotedesktopverbindung:  
> Der Systemadministrator hat den zulässigen Anmeldetyp (Netzwerk oder interaktiv) eingeschränkt. Bitten Sie Ihren Systemadministrator oder den technischen Support um Hilfe.

Dieses Problem tritt auf, wenn für RDP-Verbindungen Authentifizierung auf Netzwerkebene (Network Level Authentication, NLA) vorgeschrieben ist und der Benutzer kein Mitglied der Gruppe **Remotedesktopbenutzer** ist. Es kann ebenfalls auftreten, wenn die Gruppe **Remotedesktopbenutzer** nicht dem Benutzerrecht **Auf diesen Computer vom Netzwerk aus zugreifen** zugewiesen wurde.

Um dieses Problem zu beheben, führen Sie einen der folgenden Schritte aus:

  - [Ändern der Gruppenmitgliedschaft oder der Zuweisung von Benutzerrechten für den Benutzer](#modify-the-users-group-membership-or-user-rights-assignment).
  - Deaktivieren von NLA (nicht empfohlen).
  - Verwenden anderer Remotedesktopclients als Windows 10. Beispielsweise tritt dieses Problem mit Windows 7-Clients nicht auf.

#### <a name="modify-the-users-group-membership-or-user-rights-assignment"></a>Ändern der Gruppenmitgliedschaft oder der Zuweisung von Benutzerrechten für den Benutzer

Wenn dieses Problem einen einzelnen Benutzer betrifft, besteht die geradlinigste Lösung dieses Problems darin, ihn der Gruppe **Remotedesktopbenutzer** zuzuweisen.

Wenn der Benutzer bereits ein Mitglied dieser Gruppe ist (oder wenn mehrere Gruppenmitglieder das gleiche Problem haben), überprüfen Sie die Konfiguration der Benutzerrechte auf dem Windows 10- oder Windows Server 2016-Remotecomputer.

1. Öffnen Sie den Gruppenrichtlinienobjekt-Editor (GPE), und stellen Sie eine Verbindung mit der lokalen Richtlinie des Remotecomputers her.
2. Navigieren Sie zu **Computerkonfiguration\\Windows-Einstellungen\\Sicherheitseinstellungen\\Lokale Richtlinien\\Zuweisen von Benutzerrechten**, klicken Sie mit der rechten Maustaste auf **Auf diesen Computer vom Netzwerk aus zugreifen**, und wählen Sie dann **Eigenschaften** aus.
3. Überprüfen Sie die Liste der Benutzer und Gruppen für **Remotedesktopbenutzer** (oder eine übergeordnete Gruppe).
4. Wenn die Liste keine **Remotedesktopbenutzer** (oder eine übergeordnete Gruppe, wie etwa **Jeder**) enthält, müssen Sie sie der Liste hinzufügen (wenn Ihre Bereitstellung mehr als ein oder zwei Computer umfasst, verwenden Sie ein Gruppenrichtlinienobjekt).  
    Beispielsweise schließt die Standardmitgliedschaft für **Auf diesen Computer vom Netzwerk aus zugreifen** **Jeder** ein. Wenn Ihre Bereitstellung ein Gruppenrichtlinienobjekt verwendet, um **Jeder** zu entfernen, müssen Sie möglicherweise den Zugriff wiederherstellen, indem Sie das Gruppenrichtlinienobjekt so aktualisieren, dass **Remotedesktopbenutzer** hinzugefügt werden.

### <a name="access-denied-a-remote-call-to-the-sam-database-has-been-denied"></a>Zugriff verweigert, ein Remoteaufruf der SAM-Datenbank wurde abgelehnt

Dieses Verhalten tritt mit hoher Wahrscheinlichkeit auf, wenn auf Ihren Domänencontrollern Windows Server 2016 oder höher ausgeführt wird und Benutzer versuchen, mithilfe einer benutzerdefinierten Verbindungs-App eine Verbindung herzustellen. Insbesondere wird Anwendungen, die versuchen, auf Profilinformationen von Benutzern in Active Directory zuzugreifen, der Zugriff verweigert.

Dieses Verhalten ist das Ergebnis einer Änderung an Windows. Wenn sich ein Benutzer in Windows Server 2012 R2 und früheren Versionen bei einem Remotedesktop anmeldet, wendet sich der Remoteverbindungs-Manager (RCM) an den Domänencontroller (DC), um die Konfigurationen abzufragen, die für Remote Desktop für das Benutzerobjekt in Active Directory Domain Services (AD DS) spezifisch sind. Diese Informationen werden auf der Registerkarte „Remotedesktopdienste“ der Eigenschaften eines Benutzerobjekts im MMC-Snap-In Active Directory-Benutzer und -Computer angezeigt.

Seit Windows Server 2016 fragt RCM die Benutzerobjekte in AD DS nicht mehr ab. Wenn Sie die Abfrage von AD DS durch den RCM benötigen, weil Sie die Remotedesktopdienste-Attribute verwenden, müssen Sie das frühere RCM-Verhalten manuell aktivieren.

> [!IMPORTANT]  
> Folgen Sie den Schritten in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie sie ändern, [sichern Sie die Registrierung zwecks Wiederherstellung](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) für den Fall, dass Probleme auftreten.

Um das RCM-Legacyverhalten auf einem RD-Sitzungshostserver zu aktivieren, konfigurieren Sie die folgenden Registrierungseinträge, und starten Sie dann den **Remotedesktopdienste**-Dienst erneut:  
  - **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Policies\\Microsoft\\Windows NT\\Terminal Services**
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<Winstation-Name\>\\**  
      - Name: **fQueryUserConfigFromDC**
      - Typ: **Reg\_DWORD**
      - Wert: **1** (Dezimal)

Um das RCM-Legacyverhalten auf einem anderen Server als einem RD-Sitzungshostserver zu aktivieren, konfigurieren Sie diese Registrierungseinträge und den folgenden zusätzlichen Registrierungseintrag (und starten Sie den Dienst dann neu):
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server**

Weitere Informationen zu diesem Verhalten finden Sie unter KB 3200967 [Änderungen am Remote-Verbindungs-Manager in Windows Server](https://support.microsoft.com/en-us/help/3200967/changes-to-remote-connection-manager-in-windows-server).

### <a name="a-user-cannot-sign-in-by-using-a-smart-card"></a>Ein Benutzer kann sich nicht mithilfe einer Smartcard anmelden

Dieser Artikel behandelt drei häufige Umstände, unter denen ein Benutzer sich nicht mithilfe einer Smartcard an einem Remotedesktop anmelden kann:  
  - [Der Benutzer kann sich nicht bei einer Filiale anmelden, die einen schreibgeschützten Domänencontroller (RODC) verwendet](#cannot-sign-in-with-a-smart-card-in-a-branch-office-with-a-rodc)
  - [Der Benutzer kann sich nicht bei einem Windows Server 2008 SP2-Computer anmelden, der vor Kurzem aktualisiert wurde](#cannot-sign-in-with-a-smart-card-to-a-windows-server-2008-sp2-computer)
  - [Der Benutzer kann nicht bei einem Windows-Computer angemeldet bleiben, der vor Kurzem aktualisiert wurde, und der Remotedesktopdienst reagiert nicht mehr (hängt)](#cannot-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs)

#### <a name="cannot-sign-in-with-a-smart-card-in-a-branch-office-with-a-rodc"></a>Die Anmeldung mit einer Smartcard bei einer Filiale mit einem RODC ist nicht möglich

Dieses Problem tritt in Bereitstellungen auf, die einen RDSH-Server an einem Filialstandort beinhalten, der einen RODC verwendet. Der RDSH-Server ist in der Stammdomäne gehostet. Die Benutzer am Filialstandort gehören zu einer Unterdomäne und verwenden Smartcards zur Authentifizierung. Der RODC ist für das Cachen von Benutzerkennwörtern konfiguriert (der RODC gehört zur **Zulässige RODC-Kennwortreplikationsgruppe**). Wenn Benutzer versuchen, sich bei Sitzungen auf dem RDSH-Server anzumelden, erhalten sie Meldungen wie „Der Anmeldeversuch ist ungültig. Dies liegt entweder an einem ungültigen Benutzernamen oder an ungültigen Authentifizierungsinformationen“.

Dies ist ein bekanntes Problem bei dem Verfahren, mit dem der Stamm-DC und der RODC die Verschlüsselung der Benutzeranmeldeinformationen handhaben. Der Stamm-DC verwendet einen Verschlüsselungsschlüssel zum Verschlüsseln der Anmeldeinformationen, und der RODC stellt dem Client einen Entschlüsselungsschlüssel bereit. Allerdings stimmen die beiden Schlüssel nicht überein.

Um dieses Problem zu umgehen, erwägen Sie eine Änderung Ihrer DC-Topologie, entweder indem Sie das Cachen von Kennwörtern auf dem RODC deaktivieren oder einen DC mit Schreibberechtigung am Filialstandort bereitstellen. Eine alternative Methode besteht darin, den RDSH-Server in die gleiche untergeordnete Domäne wie die Benutzer zu verschieben. Eine weitere Alternative ist es, Benutzern die Anmeldung ohne Smartcards zu erlauben. Jede dieser Lösungen bringt möglicherweise Kompromisse beim Leistungs- oder Sicherheitsniveau mit sich.

#### <a name="cannot-sign-in-with-a-smart-card-to-a-windows-server-2008-sp2-computer"></a>Die Anmeldung mit einer Smartcard bei einem Windows Server 2008 SP2-Computer ist nicht möglich

Dieses Problem tritt auf, wenn Benutzer sich bei einem Windows Server 2008 SP2-Computer anmelden, auf dem ein Update mit KB4093227 (2018.4B) ausgeführt wurde. Wenn Benutzer versuchen, sich mithilfe einer Smartcard anzumelden, wird ihnen der Zugriff mit Meldungen wie „Es wurden keine gültigen Zertifikate gefunden. Überprüfen Sie, ob die Karte ordnungsgemäß eingesteckt wurde und formschlüssig passt“ verweigert. Zugleich zeichnet der Windows Server-Computer das Anwendungsereignis „Fehler beim Abrufen eines digitalen Zertifikats von der eingelegten Smartcard. Ungültige Signatur“ auf.

Um dieses Problem zu beheben, aktualisieren Sie den Windows Server-Computer mit der Wiederveröffentlichung 2018.06 B von KB 4093227, [Beschreibung des Sicherheitsupdates für das Denial-of-Service-Sicherheitsrisiko beim Windows-Remotedesktopprotokoll (RDP) in Windows Server 2008: 10. April 2018](https://support.microsoft.com/en-us/help/4093227/security-update-for-vulnerabilities-in-windows-server-2008)

#### <a name="cannot-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs"></a>Der Benutzer kann nicht mit einer Smartcard angemeldet bleiben, und der Remotedesktopdienst reagiert nicht

Dieses Problem tritt auf, wenn sich Benutzer bei einem Windows- oder Windows Server-Computer anmelden, für den ein Update mithilfe von KB 4056446 ausgeführt wurde. Der Benutzer ist möglicherweise zunächst in der Lage, sich mithilfe einer Smartcard beim System anzumelden, aber anschließend erhält er eine Fehlermeldung „SCARD\_E\_NO\_SERVICE“. Der Remotecomputer hört möglicherweise auf, zu reagieren.

Um dieses Problem zu umgehen, führen Sie einen Neustart des Remotecomputers durch.

Um dieses Problem zu beheben, aktualisieren Sie den Remotecomputer mit dem passenden Fix:

  - Windows Server 2008 SP2: KB 4090928, [Windows leaks handles in the lsm.exe process and smart card applications may display "SCARD\_E\_NO\_SERVICE" errors](https://support.microsoft.com/en-us/help/4090928/scard-e-no-service-errors-when-windows-leaks-handles-in-the-lsm-exe) (Windows verliert Handles im lsm.exe-Prozess, und für Smartcardanwendungen werden möglicherweise SCARD_E_NO_SERVICE-Fehler angezeigt)
  - Windows Server 2012 R2: KB 4103724, [17. Mai 2018 – KB4103724 (Vorschau der monatlichen Zusammenfassung)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724)
  - Windows Server 2016 und Windows 10, Version 1607: KB 4103720, [17. Mai 2018 – KB4103720 (Betriebssystembuild 14393.2273)](https://support.microsoft.com/en-us/help/4103720/windows-10-update-kb4103720)

### <a name="if-the-remote-pc-is-locked-a-user-needs-to-enter-a-password-twice"></a>Wenn der Remotecomputer gesperrt ist, muss ein Benutzer das Kennwort zweimal eingeben

Dieses Problem kann auftreten, wenn ein Benutzer versucht, eine Verbindung mit einem Remotedesktop herzustellen, auf dem Windows 10, Version 1709, in einer Bereitstellung ausgeführt wird, in der für RDP-Verbindungen keine Authentifizierung auf Netzwerkebene vorgeschrieben ist. Wenn unter diesen Umständen der Remotedesktop gesperrt wird, muss der Benutzer seine Anmeldeinformationen beim Herstellen der Verbindung zweimal eingeben.

Um dieses Problem zu beheben, führen Sie ein Update des Computers mit Windows 10, Version 1709, mit KB 4343893, [30. August 30, 2018 – KB4343893 (Betriebssystembuild 16299.637)](https://support.microsoft.com/en-us/help/4343893/windows-10-update-kb4343893) aus.

### <a name="user-cannot-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages"></a>Der Benutzer kann sich nicht anmelden und erhält die Meldungen „Authentifizierungsfehler“ und „CredSSP encryption oracle remediation“ (CredSSP-Verschlüsselung – Oracle-Wartung)

Wenn Benutzer versuchen, sich mit einer beliebigen Version von Windows ab Windows Vista SP2 und höher oder Windows Server 2008 SP2 und höher anzumelden, wird ihnen der Zugriff verweigert, und es werden Meldungen wie die folgende angezeigt:

  - Authentifizierungsfehler. Die angeforderte Funktion wird nicht unterstützt.
  - Dies könnte seine Ursache in der Oracle-Wartung der CredSSP-Verschlüsselung haben

„CredSSP-Verschlüsselung – Oracle-Wartung“ bezieht sich auf einen Satz Sicherheitsupdates, die im März, April und Mai 2018 veröffentlicht wurden. CredSSP ist ein Authentifizierungsanbieter, der Authentifizierungsanforderungen für andere Anwendungen verarbeitet. Das Update „3B“ vom 13. März 2018 und nachfolgende Updates befassten sich mit einem Exploit, der es einem Angreifer ermöglichte, Benutzeranmeldeinformationen weiterzuleiten, um Code auf dem Zielsystem auszuführen.

Mit den anfänglichen Updates wurde Unterstützung für ein neues Gruppenrichtlinienobjekt, **Encryption Oracle-Abwehr**, eingeführt, das die folgenden möglichen Einstellungen aufweist:

  - **Vulnerable** (Anfällig). Clientanwendungen, die CredSSP verwenden, können ein Fallback auf unsichere Versionen ausführen, jedoch werden die Remotedesktops durch dieses Verhalten möglichen Angriffen ausgesetzt. Dienste, die CredSSP verwenden, akzeptieren Clients, die nicht aktualisiert wurden.
  - **Mitigated** (Entschärft). Clientanwendungen, die CredSSP verwenden, können kein Fallback auf unsichere Versionen vornehmen, aber Dienste, die CredSSP verwenden, akzeptieren Clients, für die kein Update ausgeführt wurde.
  - **Force Updated Clients** (Aktualisierte Clients erzwingen). Clientanwendungen, die CredSSP verwenden, können kein Fallback auf unsichere Versionen vornehmen, und Dienste, die CredSSP verwenden, akzeptieren keine ungepachten Clients. 
    Hinweis: Diese Einstellung sollte erst bereitgestellt werden, wenn alle Remotehosts die neueste Version unterstützen.

Mit dem Update vom 8. Mai 2018 wurde die Standardeinstellung von **Encryption Oracle-Abwehr** von **Vulnerable** (Anfällig) in **Mitigated** (Entschärft) geändert. Dank dieser Änderung können Remotedesktopclients, die die Updates enthalten, keine Verbindungen mit Servern herstellen, die nicht über sie verfügen (oder mit aktualisierten Servern, die nicht neu gestartet wurden). Weitere Informationen über die Wirkungen der Updates und die Kommunikationstypen, die durch sie blockiert werden, finden Sie unter KB 4093492, [CredSSP updates for CVE-2018-0886](https://support.microsoft.com/en-us/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018) (CredSSP-Updates für CVE-2018-0886).

Um dieses Problem zu beheben, stellen Sie sicher, dass alle Systeme vollständig aktualisiert und neu gestartet werden. Eine vollständige Liste der Updates und weitere Informationen zu Sicherheitsrisiken finden Sie unter [CVE-2018-0886 | CredSSP Remote Code Execution Vulnerability](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2018-0886) (CVE-2018-0886 | CredSSP – Sicherheitsrisiko bei der Remotecodeausführung).

Um dieses Problem bis zum Abschluss der Updates zu umgehen, lesen Sie KB 4093492 wegen Informationen zu den zulässigen Verbindungstypen. Wenn sich keine realisierbaren Alternativen finden, können Sie eins der folgenden Verfahren in Erwägung ziehen:

- Legen Sie für die betroffenen Clientcomputer die Richtlinie **Encryption Oracle-Abwehr** wieder auf **Vulnerable** (Anfällig) fest.
- Ändern Sie die folgenden Richtlinien im Gruppenrichtlinienordner **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remotedesktopdienste\\Remotedesktop-Sitzungshost\\Sicherheit**:  
  - **Verwendung einer bestimmten Sicherheitsstufe für Remoteverbindungen (RDP) ist erforderlich**: auf **Aktiviert** festlegen und **RDP** auswählen.
  - **Benutzerauthentifizierung mit Authentifizierung auf Netzwerkebene für Remoteverbindungen ist erforderlich**: auf **Deaktiviert** festlegen.
    > [!IMPORTANT]  
    > Durch diese Änderungen verringert sich die Sicherheit Ihrer Bereitstellung. Sie sollten nur vorübergehend vorgenommen werden, falls überhaupt.

Weitere Informationen zum Arbeiten mit Gruppenrichtlinien finden Sie unter [Ändern ein blockierenden Gruppenrichtlinienobjekts](#modifying-a-blocking-gpo).

### <a name="after-you-update-client-computers-some-users-need-to-sign-in-twice"></a>Nach einem Update von Clientcomputern müssen sich manche Benutzer zweimal anmelden

Benutzer auf manchen Computern mit Windows 7 oder Windows 10, Version 1709, melden sich bei einer Remotedesktopsitzung an und sehen unmittelbar darauf einen zweiten Anmeldebildschirm. Dieses Problem tritt auf, wenn die Clientcomputer die folgenden Updates empfangen haben:

  - Windows 7: KB 4103718, [8. Mai 2018 – KB4103718 (monatliches Rollup)](https://support.microsoft.com/en-us/help/4103718/windows-7-update-kb4103718)
  - Windows 10 1709: KB 4103727, [8. Mai 2018 – KB4103727 (Betriebssystembuild 16299.431)](https://support.microsoft.com/en-us/help/4103727/windows-10-update-kb4103727)

Um dieses Problem zu beheben, stellen Sie sicher, dass die Computer, mit denen Benutzer Verbindungen herstellen wollen (ebenso wie RDSH- oder RDVI-Server), alle Updates bis Juni 2018 erhalten haben. Dies schließt die folgenden Updates ein:

  - Windows Server 2016: KB 4284880, [12. Juni 2018 – KB4284880 (Betriebssystembuild 14393.2312)](https://support.microsoft.com/en-us/help/4284880/windows-10-update-kb4284880)
  - Windows Server 2012 R2: KB 4284815, [12. Juni 2018 – KB4284815 (monatliches Rollup)](https://support.microsoft.com/en-us/help/4284815/windows-81-update-kb4284815)
  - Windows Server 2012: KB 4284855, [12. Juni 2018 – KB4284855 (monatliches Rollup)](https://support.microsoft.com/en-us/help/4284855/windows-server-2012-update-kb4284855)
  - Windows Server 2008 R2: KB 4284826, [12. Juni 2018 – KB4284826 (monatliches Rollup)](https://support.microsoft.com/en-us/help/4284826/windows-7-update-kb4284826)
  - Windows Server 2008 SP2: KB4056564, [Beschreibung des Sicherheitsupdates für die CredSSP-Remotecodeausführung in Windows Server 2008, und Windows Embedded POSReady 2009 und Windows Embedded Standard 2009: 13. März 2018](https://support.microsoft.com/en-us/help/4056564/security-update-for-vulnerabilities-in-windows-server-2008)

### <a name="users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers"></a>Benutzern wird der Zugriff auf eine Bereitstellung verweigert, die Remote Credential Guard mit mehreren RD-Verbindungsbrokern verwendet

Dieses Problem tritt in Hochverfügbarkeits-Bereitstellungen mit zwei oder mehr Remotedesktop-Verbindungsbrokern auf, wenn Windows Defender Remote Credential Guard verwendet wird. Benutzer können sich nicht an den Remotedesktops anmelden.

Dieses Problem tritt auf, weil Remote Credential Guard Kerberos für die Authentifizierung verwendet und NTLM einschränkt. Allerdings können in einer Hochverfügbarkeitskonfiguration mit Lastenausgleich die RD-Verbindungsbroker keine Kerberos-Vorgänge unterstützen.

Wenn Sie eine Hochverfügbarkeitskonfiguration mit RD-Verbindungsbrokern mit Lastenausgleich verwenden müssen, können Sie dieses Problem umgehen, indem Sie Remote Credential Guard deaktivieren. Weitere Informationen über das Verwalten von Windows Defender Remote Credential Guard finden Sie unter [Schützen von Remote Desktop-Anmeldeinformationen mit Windows Defender Remote Credential Guard](https://docs.microsoft.com/windows/security/identity-protection/remote-credential-guard#enable-windows-defender-remote-credential-guard).

## <a name="on-connecting-user-receives-remote-desktop-service-is-currently-busy-message"></a>Beim Herstellen der Verbindung erhält der Benutzer die Meldung „Der Remotedesktopdienst ist aktuell ausgelastet“

Um eine passende Reaktion auf dieses Problem zu ermitteln, verwenden Sie die folgenden Schritte:

1. Hört der Remotedesktopdienst auf, zu reagieren (beispielsweise scheint der Remotedesktopclient beim Begrüßungsbildschirm zu „hängen“)?  
      - Wenn der Dienst nicht mehr reagiert, sehen Sie beim [RDSH-Server-Arbeitsspeicherproblem](#rdsh-server-memory-issue) nach.
      - Wenn der Client normal mit dem Dienst zu interagieren scheint, fahren Sie mit dem nächsten Schritt fort.
2. Wenn mindestens ein Benutzer seine Remotedesktopsitzungen trennt, kann er sie wieder herstellen?  
   - Wenn der Dienst Verbindungen auch weiterhin ablehnt, ganz gleich, wie viele Benutzer ihre Sitzungen trennen, lesen Sie [RD-Listener-Problem](#rd-listener-issue).
   - Wenn der Dienst beginnt, Verbindungen anzunehmen, nachdem eine Reihe von Benutzern ihre Sitzungen getrennt haben, [überprüfen Sie die Richtlinie für den Verbindungsgrenzwert](#check-the-connection-limit-policy).

### <a name="rdsh-server-memory-issue"></a>RDSH-Server-Arbeitsspeicherproblem

Auf einigen Windows Server 2012 R2-RDSH-Servern wurde Arbeitsspeicherverlust festgestellt. Im Lauf der Zeit beginnen diese Server, sowohl Remotedesktopverbindungen als auch lokale Konsolenanmeldungen mit Meldungen wie der folgenden abzulehnen:

> Die Aufgabe, die Sie erledigen möchten, kann nicht ausgeführt werden, da der Remotedesktopdienst zurzeit ausgelastet ist. Wiederholen Sie den Vorgang in einigen Minuten. Andere Benutzer sollten immer noch in der Lage sein, sich anzumelden.

Remotedesktopclients, die versuchen, eine Verbindung herzustellen, hören auf, zu reagieren.

Um dieses Problem zu umgehen, führen Sie einen Neustart des RDSH-Servers durch.

Um dieses Problem zu beheben, wenden Sie KB 4093114, [10. April 2018 – KB4093114 (Monatliches Rollup)](Datei:///C:/Users/v-jesits/AppData/Local/Microsoft/Windows/INetCache/Content.Outlook/FUB8OO45/April%2010,%202018—KB4093114%20(Monthly%20Rollup)) auf die RDSH-Server an.

### <a name="rd-listener-issue"></a>RD-Listener-Problem

Auf einigen RDSH-Servern, für die ein direktes Upgrade von Windows Server 2008 R2 auf Windows Server 2012 R2 oder Windows Server 2016 ausgeführt wurde, wurde ein Problem festgestellt. Wenn ein Remotedesktopclient eine Verbindung mit dem RDSH-Server herstellt, erstellt der RDSH-Server einen RD-Listener für die Benutzersitzung. Die betroffenen Server unterhalten einen Zähler für die RD-Listener, der heraufgesetzt wird, wenn Benutzer Verbindungen herstellen, aber nicht wieder heruntergesetzt.

Um dieses Problem zu umgehen, können Sie die folgenden Methoden verwenden:

  - Führen Sie einen Neustart des RDSH-Servers durch, um den Zähler der RD-Listener zurückzusetzen
  - Ändern Sie den Grenzwert der Verbindungsrichtlinie, und legen Sie sie auf einen sehr hohen Wert fest. Weitere Informationen zum Verwalten der Richtlinie für den Verbindungsgrenzwert finden Sie unter [Überprüfen der Richtlinie für den Verbindungsgrenzwert](#check-the-connection-limit-policy).

Um dieses Problem zu beheben, wenden Sie die folgenden Updates auf die RDSH-Server an:

  - Windows Server 2012 R2: KB 4343891, [30. August 2018 – KB4343891 (Vorschau des monatlichen Rollups)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)
  - Windows Server 2016: KB 4343884, [30. August 2018 – KB4343884 (Betriebssystembuild 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)

### <a name="check-the-connection-limit-policy"></a>Überprüfen der Verbindungsgrenzwert-Richtlinie

Sie können die Anzahl der gleichzeitigen Remotedesktopverbindungen auf der Ebene der einzelnen Computer oder durch Konfiguration eines Gruppenrichtlinienobjekts (GPO) einschränken. Standardmäßig ist der Grenzwert nicht festgelegt.

Um die aktuellen Einstellungen zu überprüfen und die für die RDSH-Server vorhandenen Gruppenrichtlinienobjekte zu bestimmen, öffnen Sie ein Eingabeaufforderungsfenster als Administrator, und geben Sie den folgenden Befehl ein:
  
```
gpresult /H c:\gpresult.html
```
   
Öffnen Sie nach dem Abschluss dieses Befehls „gpresult.html“, und suchen Sie in **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remotedesktopdienste\\Remotedesktop-Sitzungshost\\Verbindungen** die Richtlinie **Anzahl der Verbindungen einschränken**.

  - Wenn die Einstellung für diese Richtlinie **Deaktiviert** ist, wird die Anzahl der RDP-Verbindungen nicht durch eine Gruppenrichtlinie eingeschränkt.
  - Wenn die Einstellung für diese Richtlinie **Aktiviert** ist, überprüfen Sie **Ausschlaggebendes Gruppenrichtlinienobjekt**. Wenn Sie den Grenzwert für Verbindungen entfernen oder ändern müssen, bearbeiten Sie dieses GPO.

Um die Änderung der Richtlinie zu erzwingen, öffnen Sie auf dem betroffenen Computer ein Eingabeaufforderungsfenster, und geben Sie den folgenden Befehl ein:
  
```
gpupdate /force
```
  
## <a name="rd-client-disconnects-and-cannot-reconnect-to-the-same-session"></a>Der Remotedesktopclient wird getrennt und kann die Verbindung zur gleichen Sitzung nicht wiederherstellen

Nachdem der Remotedesktopclient die Verbindung mit dem Remotedesktop verloren hat, kann der Client die Verbindung nicht sofort wiederherstellen. Der Benutzer empfängt Fehlermeldungen wie etwa die folgenden:

  - Aufgrund eines Sicherheitsfehlers konnte der Client keine Verbindung mit dem Terminalserver herstellen. Nachdem Sie sichergestellt haben, dass Sie beim Netzwerk angemeldet sind, versuchen Sie noch einmal, eine Verbindung mit dem Server herzustellen.
  - Remotedesktop getrennt. Aufgrund eines Sicherheitsfehlers konnte der Client keine Verbindung mit dem Remotecomputer herstellen. Stellen Sie sicher, dass Sie am Netzwerk angemeldet sind, und versuchen Sie dann noch einmal, eine Verbindung herzustellen.

Zu einem späteren Zeitpunkt stellt der Remotedesktopclient die Verbindung mit dem Remotedesktop wieder her. Anstatt jedoch den Client mit der ursprünglichen Sitzung zu verbinden, stellt der RDSH-Server eine Verbindung des Clients mit einer neuen Sitzung her. Beim Überprüfen des RDSH-Servers stellt sich heraus, dass die ursprüngliche Sitzung nicht in einen getrennten Zustand versetzt wurde, sondern stattdessen weiterhin aktiv bleibt.

Um dieses Problem zu umgehen, können Sie die Richtlinie **„Keep Alive“-Verbindungsintervall konfigurieren** im Gruppenrichtlinienordner **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remotedesktopdienste\\Remotedesktop-Sitzungshost\\Verbindungen** aktivieren. Wenn Sie diese Richtlinie aktivieren, müssen Sie ein Keep-Alive-Intervall angeben. Das Keep-Alive-Intervall bestimmt, wie oft der Server den Sitzungsstatus überprüft (Angabe in Minuten).

Dieses Problem kann seine Ursache in einer Fehlkonfiguration Ihrer Authentifizierungs- und Konfigurationseinstellungen haben. Sie können diese Einstellungen auf Serverebene oder mithilfe von GPOs konfigurieren. Die Gruppenrichtlinieneinstellungen stehen im Gruppenrichtlinienordner **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remotedesktopdienste\\Remotedesktop-Sitzungshost\\Sicherheit** zur Verfügung.

1. Öffnen Sie auf dem RD-Sitzungshostserver die Konfiguration des Remotedesktop-Sitzungshosts.
2. Klicken Sie unter **Verbindungen** mit der rechten Maustaste auf den Namen der Verbindung, und klicken Sie dann auf **Eigenschaften**.
3. Wählen Sie im Dialogfeld **Eigenschaften** für die Verbindung auf der Registerkarte **Allgemein** in der Schicht **Sicherheit** eine Sicherheitsmethode aus.
4. Klicken Sie in **Verschlüsselungsstufe** auf die gewünschte Stufe. Sie können zwischen **Niedrig**, **Clientkompatibel**, **Hoch** und **FIPS-konform** wählen.

> [!NOTE]  
>  - Wenn für Verbindungen zwischen Clients und RD-Sitzungshostservern die höchste Verschlüsselungsstufe erforderlich ist, verwenden Sie FIPS-konforme Verschlüsselung.
>  - Alle Einstellungen zur Verschlüsselungsstufe, die Sie in Gruppenrichtlinien konfigurieren, setzen die Konfiguration außer Kraft, die Sie mithilfe des Konfigurationstools für Remotedesktopdienste festlegen. Und wenn Sie die Richtlinie [Systemkryptografie: FIPS-konforme Algorithmen für Verschlüsselung, Hashing und Signatur verwenden](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc780081\(v=ws.10\)) aktivieren, setzt diese Einstellung die Richtlinie **Verschlüsselungsstufe der Clientverbindung festlegen** außer Kraft. Die Richtlinie für Systemkryptografie befindet sich im Ordner **Computerkonfiguration\\Windows-Einstellungen\\Sicherheitseinstellungen\\Lokale Richtlinien\\Sicherheitsoptionen**.
>  - Wenn Sie die Verschlüsselungsstufe ändern, wird die neue Verschlüsselungsstufe wirksam, sobald sich ein Benutzer das nächste Mal anmeldet. Wenn Sie mehrere Verschlüsselungsstufen auf einem Server unterstützen müssen, installieren Sie mehrere Netzwerkadapter, und konfigurieren Sie jeden Adapter separat.
>  - Um zu überprüfen, ob ein Zertifikat über einen entsprechenden privaten Schlüssel verfügt, klicken Sie mit der rechten Maustaste in „Remotedesktopdienste-Konfiguration“ mit der rechten Maustaste auf die Verbindung, für die Sie das Zertifikat anzeigen möchten, wählen Sie **Allgemein**, dann **Bearbeiten**, dann das Zertifikat, das Sie anzeigen möchten, und schließlich **Zertifikat anzeigen** aus. Unten auf der Registerkarte **Allgemein** sollte die Aussage „Sie verfügen über einen privaten Schlüssel, der diesem Zertifikat entspricht“ angezeigt werden. Sie können diese Informationen auch mithilfe des Zertifikat-Snap-Ins anzeigen.
>  - FIPS-konforme Verschlüsselung (die Richtlinie **Systemkryptografie: FIPS-konforme Algorithmen für Verschlüsslung, Hashing und Signatur verwenden** oder die Einstellung **FIPS-konform** in der Remotedesktop-Serverkonfiguration) verschlüsselt und entschlüsselt die zwischen Client und Server ausgetauschten Daten mit Verschlüsselungsalgorithmen nach dem FIPS 140-1-Standard (Federal Information Processing Standard ) mithilfe von Microsoft-Kryptografiemodulen. Weitere Informationen finden Sie unter [FIPS 140-Überprüfung](https://docs.microsoft.com/windows/security/threat-protection/fips-140-validation).
>  - Bei der Einstellung **Hoch** werden vom Client an den Server und vom Server an den Client gesendete Daten mithilfe von starker 128-Bit-Verschlüsselung verschlüsselt.
>  - Bei der Einstellung **Clientkompatibel** werden die zwischen dem Client und dem Server ausgetauschten Daten mit der vom Client unterstützten maximalen Schlüsselstärke verschlüsselt.
>  - Die Einstellung **Niedrig** verschlüsselt vom Client an den Server gesendete Daten mit 56-Bit-Verschlüsselung.

## <a name="remote-laptop-disconnects-from-wireless-network"></a>Der Remotelaptop trennt die WLAN-Verbindung

Dieses Problem kann auftreten, wenn ein Remotedesktopclient eine Verbindung mit einem Laptopcomputer mithilfe eines drahtlosen 802.1x-Netzwerks herstellt. Gelegentlich trennt der Laptop die Verbindung im dem Drahtlosnetzwerk und stellt sie nicht automatisch wieder her.

Dies ist ein bekanntes Problem, das auftritt, wenn die Netzwerk-Authentifizierungseinstellung für die drahtlose Netzwerkverbindung **Benutzerauthentifizierung** ist.

Um dieses Problem zu umgehen, legen Sie Netzwerk-Authentifizierungseinstellung auf **Benutzer- oder Computerauthentifizierung** oder auf **Computerauthentifizierung** fest.

 > [!NOTE]  
> Um die Netzwerk-Authentifizierungseinstellungen auf einem einzelnen Computer zu ändern, müssen Sie möglicherweise die Systemsteuerung im Netzwerk- und Freigabecenter verwenden, um eine neue Drahtlosverbindung mit den neuen Einstellungen zu erstellen.

Eine vollständige Beschreibung der Konfiguration von Netzwerkeinstellungen mithilfe von Gruppenrichtlinienobjekten finden Sie unter [Configure Wireless Network (IEEE 802.11) Policies](https://docs.microsoft.com/windows-server/networking/core-network-guide/cncg/wireless/e-wireless-access-deployment#bkmk_policies) (Konfigurieren von Richtlinien für Drahtlosnetzwerke (IEEE 802.11)).

## <a name="user-experiences-poor-performance-or-application-problems"></a>Beim Benutzer treten schlechte Leistung oder Probleme mit Anwendungen auf

Dieser Abschnitt behandelt verschiedene häufige Probleme, die bei Benutzern auftreten können, wenn sie Remotedesktopfunktionen verwenden:

  - [Bei Benutzern, die Verbindungen mit neuen virtuellen Computern auf Microsoft Azure herstellen, treten gelegentlich Probleme auf](#intermittent-problems-with-new-microsoft-azure-virtual-machines).
  - [Bei Benutzern, die Verbindungen mit Remotedesktops herstellen, die Windows 10, Version 1709, ausführen, treten möglicherweise Probleme mit der Videowiedergabe auf](#video-playback-issues-on-windows-10-version-1709).
  - [Benutzer mit schreibgeschützten Benutzerprofilen, die Verbindungen mit Windows 10-Remotedesktops herstellen, können ihren Desktop nicht freigeben.](#desktop-sharing-issues-on-windows-10)
  - [Benutzer, die Verbindungen mit Windows 10-Remotedesktops mithilfe von Clients herstellen, auf denen ältere Versionen von Windows 10 ausgeführt werden, stellen schlechte Leistung fest, wenn NLA deaktiviert ist](#performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled)
  - [Wenn Benutzer mehrere Anwendungen in Remotedesktopsitzungen ausführen und die Verbindung häufig trennen und wiederherstellen, tritt möglicherweise beim Wiederherstellen der Verbindung ein schwarzer Bildschirm auf.](#black-screen-issue)

### <a name="intermittent-problems-with-new-microsoft-azure-virtual-machines"></a>Gelegentlich auftretende Probleme bei virtuellen Microsoft Azure-Computern

Dieses Problem betrifft virtuelle Computer, die vor Kurzem bereitgestellt wurden. Nachdem der Benutzer eine Verbindung mit dem virtuellen Computer hergestellt hat, lädt die Remotedesktopsitzung möglicherweise nicht alle Einstellungen des Benutzers ordnungsgemäß.

Um dieses Problem zu umgehen, trennen Sie die Verbindung mit dem virtuellen Computer, warten Sie mindestens 20 Minuten lang, und stellen Sie dann wieder eine Verbindung her.

Um dieses Problem zu lösen, wenden Sie die folgenden Updates nach Eignung auf die virtuellen Computer an:

  - Windows 10 und Windows Server 2016: KB 4343884, [30. August 2018 – KB4343884 (Betriebssystembuild 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)
  - Windows Server 2012 R2: KB 4343891, [30. August 2018 – KB4343891 (Vorschau des monatlichen Rollups)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)

### <a name="video-playback-issues-on-windows-10-version-1709"></a>Probleme mit der Videowiedergabe unter Windows 10, Version 1709

Dieses Problem tritt auf, wenn Benutzer Verbindungen mit Remotecomputern herstellen, die Windows 10, Version 1709, ausführen. Wenn diese Benutzer Video mithilfe des VMR9-Codecs (Video Mixing Renderer 9) wiedergeben, zeigt der Player nur ein schwarzes Fenster an.

Dies ist ein bekanntes Problem in Windows 10, Version 1709. Das Problem tritt unter Windows 10, Version 1703, nicht auf.

### <a name="desktop-sharing-issues-on-windows-10"></a>Probleme mit der Desktopfreigabe unter Windows 10

Dieses Problem tritt auf, wenn der Benutzer ein schreibgeschütztes Benutzerprofil (und eine zugeordnete Registrierungsstruktur) besitzt, wie etwa in einem Kioskszenario. Wenn ein solcher Benutzer eine Verbindung mit einem Remotecomputer unter Windows 10, Version 1803, herstellt, kann er seinen Desktop nicht freigeben.

Um dieses Problem zu beheben, wenden Sie das Windows 10-Update 4340917, [24. Juli 2018 – KB4340917 (Betriebssystembuild 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917) an.

### <a name="performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled"></a>Leistung bei der gemischten Verwendung von Windows 10-Versionen, wenn NLA deaktiviert ist

Dieses Problem tritt auf, wenn NLA deaktiviert ist und Remotedesktop-Clientcomputer, die Windows 10 ausführen, Verbindungen mit Remotedesktops herstellen, die andere Versionen von Windows 10 ausführen. Benutzer von Remotedesktopclients auf Computern, die Windows 10, Version 1709 oder früher, ausführen, erfahren schlechte Leistung bei Verbindungen mit Remotedesktops, die Windows 10, Version 1803 oder höher, ausführen.

Dies tritt auf, weil bei deaktivierter NLA die älteren Clientcomputer ein langsameres Protokoll für Verbindungen mit Windows 10, Version 1803 oder höher, verwenden.

Um dieses Problem zu beheben, wenden Sie KB 4340917, [24. Juli 2018 — KB4340917 (Betriebssystembuild 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917) an.

### <a name="black-screen-issue"></a>Problem mit schwarzem Bildschirm

Dieses Problem tritt in Windows 8.0, Windows 8.1, Windows 10 RTM und Windows Server 2012 R2 auf. Ein Benutzer startet mehrere Anwendungen auf einem Remotedesktop und trennt anschließend die Verbindung. In regelmäßigen Abständen stellt der Benutzer die Verbindung mit dem Remotedesktop wieder her, um mit den Anwendungen zu interagieren, und trennt die Verbindung dann wieder. An einem bestimmten Punkt zeigt die Remotedesktopsitzung beim Wiederherstellen der Verbindung nur einen schwarzen Bildschirm an. Der Benutzer muss die Remotedesktopsitzung von der Konsole des Remotecomputers aus (oder an der Konsole des RDSH-Servers) beenden. Bei dieser Aktion werden die Anwendungen beendet.

Um dieses Problem zu beheben, wenden Sie die folgenden Updates nach Eignung an:

  - Windows 8 und Windows Server 2012 KB4103719, [17. Mai 2018 – KB4103719 (Vorschau der monatlichen Zusammenfassung)](https://support.microsoft.com/en-us/help/4103719/windows-server-2012-update-kb4103719)
  - Windows 8.1 und Windows Server 2012 R2: KB4103724, [17 Mai 2018 – KB4103724 (Vorschau des monatlichen Rollups)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724) und KB 4284863, [21. Juni 2018 – KB4284863 (Vorschau des monatlichen Rollups)](https://support.microsoft.com/en-us/help/4284863/windows-81-update-kb4284863)
  - Windows 10: Behoben in KB4284860, [12. Juni 2018 – KB4284860 (Betriebssystembuild 10240.17889)](https://support.microsoft.com/en-us/help/4284860/windows-10-update-kb4284860)
