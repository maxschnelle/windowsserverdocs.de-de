---
title: Windows Admin Center allgemeine Schritte zur Problembehandlung
description: Windows Admin Center allgemeine Problembehandlungsschritte (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 06/07/2019
ms.openlocfilehash: 5df216d8c7b829a6c60db4e5d771824a7bacdb47
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322882"
---
# <a name="troubleshooting-windows-admin-center"></a>Problembehandlung für Windows Admin Center

> Gilt für: Windows Admin Center, Windows Admin Center Preview

> [!Important]
> Dieses Handbuch hilft Ihnen beim Diagnostizieren und Beheben von Problemen, die mit Windows Admin Center auftreten. Wenn Sie ein Problem mit einem bestimmten Tool haben, überprüfen Sie, ob Sie ein [bekanntes Problems haben.](https://aka.ms/wacknownissues)

## <a name="installer-fails-with-message-_the-module-microsoftpowershelllocalaccounts-could-not-be-loaded_"></a>Der Installer schlägt mit der folgenden Meldung fehl:  **_das Modul "Microsoft. PowerShell. LocalAccounts" konnte nicht geladen werden._**

Dies kann vorkommen, wenn Ihr PowerShell-Standard Modulpfad geändert oder entfernt wurde. Stellen Sie sicher, dass ```%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules``` das **erste** Element in der psmodulepath-Umgebungsvariablen ist, um das Problem zu beheben. Dies können Sie mit der folgenden PowerShell-Zeile erreichen:

```powershell
[Environment]::SetEnvironmentVariable("PSModulePath","%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules;" + ([Environment]::GetEnvironmentVariable("PSModulePath","User")),"User")
```

## <a name="i-get-a-this-sitepage-cant-be-reached-error-in-my-web-browser"></a>Ich erhalte einen Fehler **diese Websiteseite kann nicht erreicht werden** im Webbrowser

### <a name="if-youve-installed-windows-admin-center-as-an-app-on-windows-10"></a>Wenn Sie Windows Admin Center als eine **App für Windows 10** installiert haben

* Überprüfen Sie, dass Windows Admin Center ausgeführt wird. Suchen Sie im Task-Manager nach dem Windows Admin Center-Symbol ![](../media/trayIcon.PNG) in der Task Leiste oder im **Windows Admin Center Desktop/smedesktop. exe** . Wenn dies nicht der Fall ist, starten Sie **Windows Admin Center** im Startmenü.

> [!NOTE] 
> Nach dem Neustart müssen Sie Windows Admin Center im Startmenü starten.  

* [Überprüfen der Windows-Version](#check-the-windows-version)

* Stellen Sie sicher, dass Sie Microsoft Edge oder Google Chrome als Webbrowser verwenden.

* Haben Sie [beim Startvorgang](../use/get-started.md#selecting-a-client-certificate) das richtige Zertifikat ausgewählt?

  * Versuchen Sie Ihren Browser in einer privaten Sitzung zu öffnen - Wenn das funktioniert, müssen Sie Ihren Cache leeren.

* Haben Sie kürzlich ein Upgrade von Windows 10 auf einen neuen Build oder eine neue Version durchgeführt?

  * Dadurch haben Sie möglicherweise die Einstellungen für vertrauenswürdige Hosts gelöscht. [Befolgen Sie diese Anweisungen, um die Einstellungen für vertrauenswürdige Hosts zu aktualisieren.](#configure-trustedhosts)

### <a name="if-youve-installed-windows-admin-center-as-a-gateway-on-windows-server"></a>Wenn Sie Windows Admin Center als **Gateway unter Windows Server** installiert haben

* [Überprüfen Sie die Windows-Version](#check-the-windows-version) auf dem Client und Server.

* Stellen Sie sicher, dass Sie Microsoft Edge oder Google Chrome als Webbrowser verwenden.

* Öffnen Sie auf dem-Server den Task-Manager >-Dienste, und stellen Sie sicher, dass **servermanagementgateway/Windows Admin Center** ausgeführt wird.
![](../media/Service-TaskMan.PNG)

* Testen Sie die Netzwerkverbindung mit dem Gateway (ersetzen Sie \<Werte > durch die Informationen aus der Bereitstellung).

    ```powershell
    Test-NetConnection -Port <port> -ComputerName <gateway> -InformationLevel Detailed
    ```

### <a name="if-you-have-installed-windows-admin-center-in-an-azure-windows-server-vm"></a>Wenn Sie Windows Admin Center auf einer Azure Windows Server-VM installiert haben

* [Überprüfen der Windows-Version](#check-the-windows-version)
* Haben Sie eine eingehende Portregel für HTTPS hinzugefügt? 
* [Weitere Informationen zum Installieren des Windows Admin Centers auf einer Azure-VM](https://docs.microsoft.com/windows-server/manage/windows-admin-center/configure/azure-integration#use-a-windows-admin-center-gateway-deployed-in-azure)

### <a name="check-the-windows-version"></a>Überprüfen Sie die Windows-Version

* Öffnen Sie das Dialogfeld "Ausführen" (Windows-Taste + R) und starten Sie ```winver```.

* Bei Verwendung der Windows 10 Version 1703 oder niedriger wird Windows Admin Center von Ihrer Version von Microsoft Edge nicht unterstützt. Aktualisieren Sie auf eine neuere Version von Windows 10 oder verwenden Sie Chrome.

* Wenn Sie eine Insider-Vorschauversion von Windows 10 oder Server mit einer Buildversion zwischen 17134 und 17637 verwenden, hatte Windows einen Fehler, der dazu geführt hat, dass Windows Admin Center fehlgeschlagen ist. Verwenden Sie eine aktuelle unterstützte Version von Windows.

### <a name="make-sure-the-windows-remote-management-winrm-service-is-running-on-both-the-gateway-machine-and-managed-node"></a>Stellen Sie sicher, dass der Windows-Remoteverwaltung (WinRM)-Dienst auf dem Gatewaycomputer und dem verwalteten Knoten ausgeführt wird.

* Öffnen Sie das Dialogfeld "ausführen" mit WindowsKey + R.
* Geben Sie ```services.msc``` ein, und drücken Sie
* Suchen Sie im geöffneten Fenster nach Windows-Remoteverwaltung (WinRM), stellen Sie sicher, dass es ausgeführt wird und auf automatisch starten festgelegt ist.

### <a name="did-you-upgrade-your-server-from-2016-to-2019"></a>Haben Sie Ihren Server von 2016 auf 2019 aktualisiert?

* Dadurch haben Sie möglicherweise die Einstellungen für vertrauenswürdige Hosts gelöscht. [Befolgen Sie diese Anweisungen, um die Einstellungen für vertrauenswürdige Hosts zu aktualisieren.](#configure-trustedhosts) 

## <a name="i-get-the-message-cant-connect-securely-to-this-page-this-might-be-because-the-site-uses-outdated-or-unsafe-tls-security-settings"></a>Ich erhalte die folgende Meldung: "eine sichere Verbindung mit dieser Seite wird hergestellt. Dies kann daran liegen, dass für die Website veraltete oder unsichere TLS-Sicherheitseinstellungen verwendet werden.

Ihr Computer ist auf http/2-Verbindungen beschränkt. Windows Admin Center verwendet die integrierte Windows-Authentifizierung, die in http/2 nicht unterstützt wird. Fügen Sie die folgenden beiden Registrierungs Werte unter dem ```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Http\Parameters``` Schlüssel auf dem Computer hinzu, auf dem **der Browser ausgeführt** wird, um die http/2-Einschränkung zu entfernen:

```
EnableHttp2Cleartext=dword:00000000
EnableHttp2Tls=dword:00000000
```

## <a name="im-having-trouble-with-the-remote-desktop-events-and-powershell-tools"></a>Ich habe Probleme mit dem Remotedesktop, den Ereignissen und den PowerShell-Tools.

Diese drei Tools erfordern das WebSocket-Protokoll, das häufig von Proxy Servern und Firewalls blockiert wird. Wenn Sie Google Chrome verwenden, gibt es ein [bekanntes Problem](known-issues.md#google-chrome) bei websockets und NTLM-Authentifizierung.

## <a name="i-can-connect-to-some-servers-but-not-others"></a>Ich kann eine Verbindung zu einigen Servern, jedoch nicht zu anderen herstellen.

* Melden Sie sich lokal am Gatewaycomputer an, und versuchen Sie, ```Enter-PSSession <machine name>``` in PowerShell auszuführen. ersetzen Sie dabei \<Computernamen > durch den Namen des Computers, den Sie im Windows Admin Center verwalten möchten. 

* Wenn Ihre Umgebung eine Arbeitsgruppe anstatt eine Domäne verwendet, lesen Sie [Windows Admin Center in einer Arbeitsgruppe verwenden](#using-windows-admin-center-in-a-workgroup).

* **Mit lokalen Administratorkonten:** Wenn Sie ein lokales Benutzerkonto verwenden, das nicht das integrierte Administratorkonto ist, müssen Sie die Richtlinie auf dem Zielcomputer mithilfe des folgenden Befehls in PowerShell oder an einer Eingabeaufforderung als Administrator auf dem Zielcomputer aktivieren:

    ```
    REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1
    ```

## <a name="using-windows-admin-center-in-a-workgroup"></a>Verwenden von Windows Admin Center in einer Arbeitsgruppe

### <a name="what-account-are-you-using"></a>Welches Konto verwenden Sie?
Stellen Sie sicher, dass die Anmeldeinformationen, die Sie verwenden, Mitglied der lokalen Administratorgruppe des Zielservers sind. In einigen Fällen erfordert WinRM auch die Mitgliedschaft in der Gruppe Remoteverwaltungsbenutzer. Wenn Sie ein lokales Benutzerkonto verwenden, das **nicht das integrierte Administratorkonto** ist, müssen Sie die Richtlinie auf dem Zielcomputer mithilfe des folgenden Befehls in PowerShell oder an einer Eingabeaufforderung als Administrator auf dem Zielcomputer aktivieren:

```cmd
REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1
```
### <a name="are-you-connecting-to-a-workgroup-machine-on-a-different-subnet"></a>Verbinden Sie einen Arbeitsgruppencomputer in einem anderen Subnetz?

Um zu einem Arbeitsgruppencomputer eine Verbindung zu erstellen, die nicht im selben Subnetz wie das Gateway ist, stellen Sie sicher, dass die der Firewall-Port (TCP 5985) WinRM den eingehenden Datenverkehr auf dem Zielcomputer ermöglicht. Sie können den folgenden Befehl in PowerShell oder an einer Eingabeaufforderung als Administrator auf dem Zielcomputer zum Erstellen dieser Firewallregel ausführen:

- **Windows Server**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any
    ```

- **Windows 10**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any
    ```

### <a name="configure-trustedhosts"></a>Konfigurieren von TrustedHosts

Beim Installieren von Windows Admin Center können Sie Windows Admin Center optional die Gateway TrustedHosts-Einstellung verwalten lassen. Dies ist in einer Arbeitsgruppe erforderlich oder wenn Sie Anmeldeinformationen für lokale Administratoren in einer Domäne verwenden. Wenn Sie auf diese Einstellung verzichten, müssen Sie TrustedHosts manuell konfigurieren.

**So ändern Sie "Treuhänder Hosts" mithilfe von PowerShell-Befehlen:**

1. Öffnen Sie eine Administrator PowerShell-Sitzung.
2. Zeigen Sie die aktuelle Einstellung von TrustedHosts an:

    ```powershell
    Get-Item WSMan:\localhost\Client\TrustedHosts
    ```

   > [!WARNING]
   > Wenn die aktuelle Einstellung von TrustedHosts nicht leer ist, werden die folgenden Befehle die Einstellung überschreiben. Es wird empfohlen, dass Sie die aktuelle Einstellung in eine Textdatei mit dem folgenden Befehl speichern, damit Sie diese wiederherstellen können, falls erforderlich:
   > 
   > `Get-Item WSMan:localhost\Client\TrustedHosts | Out-File C:\OldTrustedHosts.txt`

3. Legen Sie TrustedHosts auf NetBIOS-IP oder FQDN der Computer fest, den Sie verwalten möchten:

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '192.168.1.1,server01.contoso.com,server02'
    ```

   > [!TIP]
   > Eine einfache Möglichkeit, alle TrustedHosts gleichzeitig festlegen zu können, ist das Verwenden von Platzhaltern.
   >
   > ```powershell
   > Set-Item WSMan:\localhost\Client\TrustedHosts -Value '*'
   > ```

4. Wenn Sie fertig mit dem Testen sind, können Sie den folgenden Befehl aus einer PowerShell-Sitzung mit erhöhten Rechten zum Deaktivieren der TrustedHosts-Einstellung ausgeben:

    ```powershell
    Clear-Item WSMan:localhost\Client\TrustedHosts
    ```

5. Wenn Sie Ihre Einstellungen zuvor exportiert haben, öffnen Sie die Datei, kopieren Sie die Werte, und verwenden Sie diesen Befehl:

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '<paste values from text file>'
    ```

## <a name="i-previously-had-windows-admin-center-installed-and-now-nothing-else-can-use-the-same-tcpip-port"></a>Ich hatte zuvor das Windows Admin Center installiert, und jetzt kann nichts mehr denselben TCP/IP-Port verwenden.

Führen Sie diese beiden Befehle manuell an einer Eingabeaufforderung mit erhöhten Rechten aus:

```cmd
netsh http delete sslcert ipport=0.0.0.0:443
netsh http delete urlacl url=https://+:443/
```

## <a name="azure-features-dont-work-properly-in-edge"></a>Azure-Features funktionieren in Edge nicht ordnungsgemäß

Edge hat [bekannte Probleme](https://github.com/AzureAD/azure-activedirectory-library-for-js/wiki/Known-issues-on-Edge) im Zusammenhang mit Sicherheitszonen, die sich auf die Azure-Anmeldung im Windows Admin Center auswirken. Wenn Sie Probleme bei der Verwendung von Azure-Features bei der Verwendung von Edge haben, versuchen Sie, https://login.microsoftonline.com, https://login.live.com und die URL Ihres Gateways als vertrauenswürdige Sites und zulässige Sites für die Einstellungen für den Popup Blocker im Client seitigen Browser hinzuzufügen. 

Dazu gehen Sie folgendermaßen vor:
1. **Internet Optionen** im Windows-Startmenü suchen
2. Zur Registerkarte " **Sicherheit** " wechseln
3. Klicken Sie unter der Option **Vertrauenswürdige Sites** auf die Schaltfläche **Sites** , und fügen Sie die URLs in dem daraufhin geöffneten Dialogfeld hinzu. Sie müssen ihre Gateway-URL sowie https://login.microsoftonline.com und https://login.live.comhinzufügen.
4. Zur Registerkarte " **Datenschutz** " wechseln
5. Klicken Sie im Abschnitt **Popup Blocker** auf die Schaltfläche **Einstellungen** , und fügen Sie die URLs in dem daraufhin geöffneten Dialogfeld hinzu. Sie müssen ihre Gateway-URL sowie https://login.microsoftonline.com und https://login.live.comhinzufügen.

## <a name="having-an-issue-with-an-azure-related-feature"></a>Haben Sie ein Problem mit einer Azure-bezogenen Funktion?

Senden Sie uns eine e-Mail unter wacFeedbackAzure@microsoft.com mit den folgenden Informationen:
* Allgemeine Problem Informationen aus den [unten aufgeführten Fragen](#providing-feedback-on-issues).
* Beschreiben Sie Ihr Problem und die Schritte, die Sie ausgeführt haben, um das Problem zu reproduzieren. 
* Haben Sie zuvor Ihr Gateway mithilfe des herunterladbaren Skripts New-AadApp. ps1 bei Azure registriert und dann auf Version 1807 aktualisiert? Oder haben Sie Ihr Gateway in Azure über die Benutzeroberfläche über die Gatewayeinstellungen > Azure registriert?
* Ist Ihr Azure-Konto mehreren Verzeichnissen/Mandanten zugeordnet?
    * Wenn ja: bei der Registrierung der Azure AD Anwendung bei Windows Admin Center war das Verzeichnis, in dem Sie Ihr Standardverzeichnis in Azure verwendet haben? 
* Hat ihr Azure-Konto Zugriff auf mehrere Abonnements?
* Ist für das Abonnement, das Sie verwenden, eine Abrechnung angefügt?
* Haben Sie bei Auftreten des Problems bei mehreren Azure-Konten angemeldet?
* Erfordert Ihr Azure-Konto Multi-Factor Authentication?
* Möchten Sie einen virtuellen Azure-Computer verwalten?
* Ist Windows Admin Center auf einer Azure-VM installiert?

## <a name="providing-feedback-on-issues"></a>Bereitstellen von Feedback zu Problemen

Navigieren Sie zur Ereignisanzeige > Anwendung und Dienste > Microsoft ServerManagementExperience und suchen Sie nach Fehlern oder Warnungen.

Melden Sie den Fehler und eine Beschreibung auf unserer [UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5BBug%5D).

Geben Sie dabei auch alle Fehler oder Warnungen an, die Sie im Ereignisprotokoll gefunden haben sowie die folgenden Informationen: 

* Die Plattform, auf der Windows Admin Center (Windows 10 oder Windows Server) **installiert** ist:
    * Wenn auf dem Server installiert ist, wie lautet die Windows- [Version](#check-the-windows-version) des Computers, auf **dem der Browser ausgeführt** wird, um auf Windows Admin Center zuzugreifen: 
    * Verwenden Sie das selbst signierte Zertifikat, das vom Installationsprogramm erstellt wurde?
    * Wenn Sie Ihr eigenes Zertifikat verwenden, stimmt der Antragstellername des Computers überein?
    * Wenn Sie Ihr eigenes Zertifikat verwenden, gibt es einen alternativen Antragstellernamen an?
* Haben Sie den Standard-Port installiert?
    * Falls dies nicht der Fall ist, welchen Port haben Sie angegeben?
* Ist der Computer, auf dem Windows Admin Center **installiert** ist, Mitglied einer Domäne?
* Die -[Version](#check-the-windows-version), auf der Windows Admin Center **installiert** ist:
* Ist der Computer, den Sie **verwalten möchten**, Mitglied einer Domäne?
* Die Windows-[Version](#check-the-windows-version) des Computers, den Sie **versuchen zu verwalten**:
* Welche Browser verwenden Sie?
    * Wenn Sie Google Chrome verwenden, was ist die Version? (Hilfe > Info zu Google Chrome)

