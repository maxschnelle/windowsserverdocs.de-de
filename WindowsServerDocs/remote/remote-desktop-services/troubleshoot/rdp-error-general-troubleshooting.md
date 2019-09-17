---
title: Allgemeine Problembehandlung bei Remotedesktopverbindungen
description: Beheben des Fehlers „Klasse nicht registriert“ bei der Remotedesktopverbindung.
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
ms.openlocfilehash: 39b11dac044c38f1ae80d4401fbb66af0317ab56
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70870705"
---
# <a name="general-remote-desktop-connection-troubleshooting"></a>Allgemeine Problembehandlung bei Remotedesktopverbindungen

Führen Sie diese Schritte aus, wenn ein Remotedesktopclient keine Verbindung mit einem Remotedesktop herstellen kann, es aber keine Meldungen oder sonstigen Symptome gibt, die zum Bestimmen der Ursache hilfreich wären.

## <a name="check-the-status-of-the-rdp-protocol"></a>Überprüfen des Status des RDP-Protokolls

### <a name="check-the-status-of-the-rdp-protocol-on-a-local-computer"></a>Überprüfen des Status des RDP-Protokolls auf einem lokalen Computer

Informationen zum Überprüfen und Ändern des Status des RDP-Protokolls auf einem lokalen Computer finden Sie unter [So aktivieren Sie Remotedesktop](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#how-to-enable-remote-desktop).

> [!NOTE]  
> Wenn die Remotedesktopoptionen nicht verfügbar sind, lesen Sie [Überprüfen, ob ein Gruppenrichtlinienobjekt RDP blockiert](#check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer).

### <a name="check-the-status-of-the-rdp-protocol-on-a-remote-computer"></a>Überprüfen des Status des RDP-Protokolls auf einem Remotecomputer

> [!IMPORTANT]  
> Befolgen Sie die Anweisungen in diesem Abschnitt sorgfältig. Es können schwerwiegende Probleme auftreten, wenn fehlerhafte Änderungen an der Registrierung vorgenommen werden. Bevor Sie die Registrierung ändern, müssen Sie die [Registrierung sichern](https://support.microsoft.com/help/322756), damit Sie sie bei einem Fehler wiederherstellen können.

Um den Status des RDP-Protokolls auf einem Remotecomputer zu überprüfen und zu ändern, verwenden Sie eine Netzwerkverbindung mit der Registrierung:

1. Wählen Sie im **Startmenü** die Option **Ausführen** aus. Geben Sie im angezeigten Textfeld den Befehl **regedt32** ein.
2. Wählen Sie im Registrierungs-Editor **Datei** und dann **Netzwerkregistrierung verbinden** aus.
3. Geben Sie im Dialogfeld **Computer auswählen** den Namen des Remotecomputers ein, wählen Sie **Namen überprüfen** und dann **OK** aus.
4. Navigieren Sie zu **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server**.  
   ![Registrierungs-Editor mit Darstellung des Eintrags „fDenyTSConnections“](../media/troubleshoot-remote-desktop-connections/RegEntry_fDenyTSConnections.png)
   - Wenn der Schlüssel **fDenyTSConnections** den Wert **0** hat, ist RDP aktiviert.
   - Wenn der Schlüssel **fDenyTSConnections** den Wert **1**, ist RDP deaktiviert.
5. Um RDP zu aktivieren, ändern Sie den Wert von **fDenyTSConnections** von **1** in **0**.

### <a name="check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer"></a>Überprüfen, ob ein Gruppenrichtlinienobjekt RDP auf einem lokalen Computer blockiert

Wenn Sie RDP nicht über die Benutzeroberfläche aktivieren können oder der Wert von **fDenyTSConnections** wieder auf **1** zurückgesetzt wird, nachdem Sie ihn geändert haben, setzt möglicherweise ein GPO die Einstellungen auf Computerebene außer Kraft.

Um die Gruppenrichtlinienkonfiguration auf einem lokalen Computer zu überprüfen, öffnen Sie ein Eingabeaufforderungsfenster als Administrator, und geben Sie den folgenden Befehl ein:

```cmd
gpresult /H c:\gpresult.html
```

Öffnen Sie nach dem Abschluss dieses Befehls „gpresult.html“. Suchen Sie in **Computerkonfiguration\\Administrative Vorlagen\\Windows-Komponenten\\Remotedesktopdienste\\Remotedesktop-Sitzungshost\\Verbindungen** die Richtlinie **Remoteverbindungen für Benutzer mithilfe der Remotedesktopdienste zulassen**.

- Wenn die Einstellung für diese Richtlinie **Aktiviert** ist, werden RDP-Verbindungen nicht durch eine Gruppenrichtlinie blockiert.
- Wenn die Einstellung für diese Richtlinie **Deaktiviert** ist, überprüfen Sie **Ausschlaggebendes Gruppenrichtlinienobjekt**. Das ist das Gruppenrichtlinienobjekt, das RDP-Verbindungen blockiert.
  ![Ein Beispielsegment von „gpresult.html“, in dem das GPO **Block RDP** RDP deaktiviert.](../media/troubleshoot-remote-desktop-connections/GPResult_RDSH_Connections_GP.png)
   
  ![Ein Beispielsegment von „gpresult.html“, in dem **Lokale Gruppenrichtlinie** RDP deaktiviert.](../media/troubleshoot-remote-desktop-connections/GPResult_RDSH_Connections_LGP.png)

### <a name="check-whether-a-gpo-is-blocking-rdp-on-a-remote-computer"></a>Überprüfen, ob ein GPO RDP auf einem Remotecomputer blockiert

Der Befehl zum Überprüfen der Konfiguration von Gruppenrichtlinien auf einem Remotecomputer lautet fast genauso wie für einen lokalen Computer:

```cmd
gpresult /S <computer name> /H c:\gpresult-<computer name>.html
```

Die Datei, die durch diesen Befehl erzeugt wird (**gpresult-\<computername\>.html**) verwendet das gleiche Informationsformat wie in der Version für lokale Computer (**gpresult.html**).

### <a name="modifying-a-blocking-gpo"></a>Ändern ein blockierenden Gruppenrichtlinienobjekts

Sie können diese Einstellungen im Gruppenrichtlinienobjekt-Editor (GPE) und der Gruppenrichtlinien-Verwaltungskonsole (GPM) ändern. Weitere Informationen zum Verwenden der Gruppenrichtlinie finden Sie unter [Advanced Group Policy Management](https://docs.microsoft.com/microsoft-desktop-optimization-pack/agpm/) (Erweiterte Gruppenrichtlinienverwaltung).

Verwenden Sie eins der folgenden Verfahren, um die blockierende Richtlinie zu ändern:

- Greifen Sie im GPE auf die passende GPO-Ebene (wie etwa lokal oder Domäne) zu, und navigieren Sie zu **Computerkonfiguration** > **Administrative Vorlagen** > **Windows-Komponenten** > **Remotedesktopdienste** > **Remotedesktop-Sitzungshost** > **Verbindungen** > **Remoteverbindungen für Benutzer mithilfe der Remotedesktopdienste zulassen**.  
   1. Legen Sie die Richtlinie auf **Aktiviert** oder **Nicht konfiguriert** fest.
   2. Öffnen Sie auf den betroffenen Computern ein Eingabeaufforderungsfenster als Administrator, und führen Sie den Befehl **gpupdate /force** aus.
- Navigieren Sie in GPM zu der Organisationseinheit, in der die blockierende Richtlinie auf die betroffenen Computer angewendet wird, und löschen Sie die Richtlinie aus der Organisationseinheit.

## <a name="check-the-status-of-the-rdp-services"></a>Überprüfen des Status der RDP-Dienste

Auf dem lokalen Computer (Client) und dem Remotecomputer (Zielcomputer) sollten die folgenden Dienste ausgeführt werden:

- Remotedesktopdienste (TermService)
- Portumleitung für Remotedesktopdienste im Benutzermodus (UmRdpService)

Sie können das Dienste-MMC-Snap-In verwenden, um die Dienste lokal oder remote zu verwalten. Sie können darüber hinaus PowerShell lokal oder remote zum Verwalten der Dienste verwenden (wenn der Remotecomputer für das Annehmen von Remote-PowerShell-Cmdlets konfiguriert ist).

![Remotedesktopdienste im Dienste-MMC-Snap-In. Ändern Sie die Standardeinstellungen für den Dienst nicht.](../media/troubleshoot-remote-desktop-connections/RDSServiceStatus.png)

Wenn einer der Dienste (oder beide) auf einem von beiden Computern nicht ausgeführt wird, starten Sie ihn.

> [!NOTE]  
> Wenn Sie den Remotedesktopdienst starten, klicken Sie auf **Ja**, um den Portumleitungsdienst für Remotedesktopdienste im Benutzermodus automatisch neu zu starten.

## <a name="check-that-the-rdp-listener-is-functioning"></a>Überprüfen der Funktion des RDP-Listeners

> [!IMPORTANT]  
> Befolgen Sie die Anweisungen in diesem Abschnitt sorgfältig. Es können schwerwiegende Probleme auftreten, wenn fehlerhafte Änderungen an der Registrierung vorgenommen werden. Bevor Sie die Registrierung ändern, müssen Sie die [Registrierung sichern](https://support.microsoft.com/help/322756), damit Sie sie bei einem Fehler wiederherstellen können.

### <a name="check-the-status-of-the-rdp-listener"></a>Überprüfen des Status des RDP-Listeners

Verwenden Sie für dieses Verfahren eine PowerShell-Instanz, die über Administratorberechtigungen verfügt. Für einen lokalen Computer können Sie auch eine Eingabeaufforderung mit Administratorberechtigungen verwenden. In diesem Verfahren verwenden wir jedoch PowerShell, da die gleichen Cmdlets sowohl lokal als auch remote funktionieren.

1. Führen Sie das folgende Cmdlet aus, um eine Verbindung mit einem Remotecomputer herzustellen:

   ```powershell
   Enter-PSSession -ComputerName <computer name>
   ```

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
   1. Geben Sie das folgende Cmdlet ein, um den vorhandenen Registrierungseintrag zu sichern:  
   
      ```powershell  
      cmd /c 'reg export "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp" C:\Rdp-tcp-backup.reg'   
      ```  
   

   2. Geben Sie das folgende Cmdlet ein, um den vorhandenen Registrierungseintrag zu entfernen:  
   
      ```powershell  
      Remove-Item -path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp' -Recurse -Force  
      ```
   
   3. Um den neuen Registrierungseintrag zu importieren und den Dienst anschließend neu zu starten, geben Sie die folgenden Cmdlets ein:  
   
      ```powershell  
      cmd /c 'regedit /s c:\<filename>.reg'  
      Restart-Service TermService -Force  
      ```
      
      Ersetzen Sie \<filename\> durch den Namen der exportierten REG-Datei.

6. Testen Sie die Konfiguration, indem Sie erneut versuchen, die Remotedesktopverbindung herzustellen. Wenn Sie trotzdem keine Verbindung herstellen können, führen Sie einen Neustart des betroffenen Computers durch.
7. Wenn Sie noch immer keine Verbindung herstellen können, [überprüfen Sie den Status des selbstsignierten RDP-Zertifikats](#check-the-status-of-the-rdp-self-signed-certificate).

### <a name="check-the-status-of-the-rdp-self-signed-certificate"></a>Überprüfen des Status des selbstsignierten RDP-Zertifikats

1. Wenn Sie immer noch keine Verbindung herstellen können, öffnen Sie das MMC-Zertifikate-Snap-In. Wenn Sie aufgefordert werden, den zu verwaltenden Zertifikatspeicher auszuwählen, wählen Sie **Computerkonto** und dann den betroffenen Computer aus.
2. Löschen Sie im Ordner **Certificates** unter **Remote Desktop** das selbstsignierte RDP-Zertifikat. 
    ![Remotedesktopzertifikate im MMC-Zertifikate-Snap-In.](../media/troubleshoot-remote-desktop-connections/MMCCert_Delete.png)
3. Starten Sie auf dem betroffenen Computer die Remotedesktopdienste erneut.
4. Aktualisieren Sie das Zertifikate-Snap-In.
5. Wenn das selbstsignierte RDP-Zertifikat nicht erneut erstellt wurde, [überprüfen Sie die Berechtigungen des MachineKeys-Ordners](#check-the-permissions-of-the-machinekeys-folder).

### <a name="check-the-permissions-of-the-machinekeys-folder"></a>Überprüfen der Berechtigungen des MachineKeys-Ordners

1. Öffnen Sie auf dem betroffenen Computer den Explorer, und navigieren Sie dann zu **C:\\Programme\\Microsoft\\Crypto\\RSA\\** .
2. Klicken Sie mit der rechen Maustaste auf **MachineKeys**, wählen Sie **Eigenschaften**, dann **Sicherheit** und schließlich **Erweitert** aus.
3. Vergewissern Sie sich, dass die folgenden Berechtigungen konfiguriert sind:
      - Vordefiniert\\Administratoren: Vollzugriff
      - Jeder: Lesen, Schreiben

## <a name="check-the-rdp-listener-port"></a>Überprüfen des RDP-Listener-Ports

Auf dem lokalen Computer (Client) und dem Remotecomputer (Zielcomputer) sollte der RDP-Listener an Port 3389 lauschen. Keine anderen Anwendungen sollten diesen Port verwenden.

> [!IMPORTANT]  
> Befolgen Sie die Anweisungen in diesem Abschnitt sorgfältig. Es können schwerwiegende Probleme auftreten, wenn fehlerhafte Änderungen an der Registrierung vorgenommen werden. Bevor Sie die Registrierung ändern, müssen Sie die [Registrierung sichern](https://support.microsoft.com/help/322756), damit Sie sie bei einem Fehler wiederherstellen können.

Um den RDP-Port zu überprüfen oder zu ändern, verwenden Sie den Registrierungs-Editor:

1. Wählen Sie im Startmenü die Option **Ausführen**, und geben Sie im angezeigten Textfeld **regedt32** ein.
      - Um eine Verbindung mit einem Remotecomputer herzustellen, wählen Sie **Datei** und dann **Mit Netzwerkregistrierung verbinden** aus.
      - Geben Sie im Dialogfeld **Computer auswählen** den Namen des Remotecomputers ein, wählen Sie **Namen überprüfen** und dann **OK** aus.
2. Öffnen Sie die Registrierung, und navigieren Sie zu **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<listener\>** . 
    ![Der PortNumber-Unterschlüssel für das RDP-Protokoll.](../media/troubleshoot-remote-desktop-connections/RegEntry_PortNumber.png)
3. Wenn **PortNumber** einen anderen Wert als **3389** aufweist, ändern Sie ihn in **3389**. 
   > [!IMPORTANT]  
    > Sie können die Remotedesktopdienste über einen anderen Port betreiben. Dies wird jedoch nicht empfohlen. In diesem Artikel wird die Behebung von Problemen mit dieser Art von Konfiguration nicht behandelt.
4. Führen Sie nach dem Ändern der Portnummer einen Neustart des Remotedesktopdiensts durch.

### <a name="check-that-another-application-isnt-trying-to-use-the-same-port"></a>Überprüfen, ob eine andere Anwendung den gleichen Port zu verwenden versucht

Verwenden Sie für dieses Verfahren eine PowerShell-Instanz, die über Administratorberechtigungen verfügt. Für einen lokalen Computer können Sie auch eine Eingabeaufforderung mit Administratorberechtigungen verwenden. In diesem Verfahren verwenden wir jedoch PowerShell, da die gleichen Cmdlets lokal und remote funktionieren.

1. Öffnen Sie ein PowerShell-Fenster. Um eine Verbindung mit einem Remotecomputer herzustellen, geben Sie **Enter-PSSession -ComputerName \<Computername\>** ein.
2. Geben Sie den folgenden Befehl aus:  
   
     ```powershell  
    cmd /c 'netstat -ano | find "3389"'  
    ```
  
    ![Der Netstat-Befehl erzeugt eine Liste der Ports und der Dienste, die an ihnen lauschen.](../media/troubleshoot-remote-desktop-connections/WPS_netstat.png)
3. Suchen Sie nach einem Eintrag für den TCP-Port 3389 (oder dem zugewiesenen RDP-Port) mit dem Status **Empfangsbereit**. 
    > [!NOTE]  
   > In der Spalte PID wird die Prozess-ID (PID) des Prozesses oder Diensts angezeigt, der diesen Port verwendet.
4. Um zu bestimmen, welche Anwendung Port 3389 (oder den zugewiesenen RDP-Port) verwendet, geben Sie den folgenden Befehl ein:  
   
     ```powershell  
    cmd /c 'tasklist /svc | find "<pid listening on 3389>"'  
    ```  
  
    ![Der Aufgabenlistenbefehl meldet Details zu einem bestimmten Prozess.](../media/troubleshoot-remote-desktop-connections/WPS_tasklist.png)
5. Suchen Sie nach einem Eintrag für die PID-Nummer, die dem Port zugeordnet ist (gemäß der **netstat**-Ausgabe). Die Dienste oder Prozesse, die der betreffenden PID zugeordnet sind, werden in der rechten Spalte angezeigt.
6. Wenn eine andere Anwendung oder ein anderer Dienst als Remotedesktopdienste (TermServ.exe) den Port verwendet, können Sie den Konflikt mit einem der folgenden Verfahren beheben:
      - Konfigurieren der anderen Anwendung oder des anderen Diensts für die Verwendung eines anderen Ports (empfohlen).
      - Deinstallieren der anderen Anwendung oder des anderen Diensts.
      - Konfigurieren von RDP für die Verwendung eines anderen Ports, gefolgt von einem Neustart der Remotedesktopdienste (nicht empfohlen).

### <a name="check-whether-a-firewall-is-blocking-the-rdp-port"></a>Überprüfen, ob der RDP-Port durch eine Firewall blockiert wird

Verwenden Sie das **psping**-Tool, um zu testen, ob Sie den betroffenen Computer über Port 3389 erreichen können.

1. Wechseln Sie zu einem anderen Computer, der nicht betroffen ist, und laden Sie **psping** von <https://live.sysinternals.com/psping.exe> herunter.
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
