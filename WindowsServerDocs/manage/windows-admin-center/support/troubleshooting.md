---
title: Allgemeine Schritte zur Problembehandlung in Windows Admin Center
description: Allgemeine Schritte zur Problembehandlung in Windows Admin Center (Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 06/07/2019
ms.openlocfilehash: 2ddcf101b6eae3be6f48c66de3c400c66ed53f2b
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519649"
---
# <a name="troubleshooting-windows-admin-center"></a>Problembehandlung für Windows Admin Center

> Gilt für: Windows Admin Center, Windows Admin Center (Vorschauversion)

> [!Important]
> Dieses Handbuch hilft Ihnen bei der Diagnose und Behebung von Problemen, die die Verwendung des Windows Admin Centers verhindern. Wenn Sie ein Problem mit einem bestimmten Tool haben, überprüfen Sie, ob ein [bekanntes Problem vorliegt.](https://aka.ms/wacknownissues)

## <a name="installer-fails-with-message-_the-module-microsoftpowershelllocalaccounts-could-not-be-loaded_"></a>Der Installer schlägt mit der folgenden Meldung fehl: ** _das Modul "Microsoft. PowerShell. LocalAccounts" konnte nicht geladen werden._**

Dies kann vorkommen, wenn Ihr PowerShell-Standard Modulpfad geändert oder entfernt wurde. Stellen Sie sicher, dass das ```%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules``` **erste** Element in der psmodulepath-Umgebungsvariablen ist, um das Problem zu beheben. Dies können Sie mit der folgenden PowerShell-Zeile erreichen:

```powershell
[Environment]::SetEnvironmentVariable("PSModulePath","%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules;" + ([Environment]::GetEnvironmentVariable("PSModulePath","User")),"User")
```

## <a name="i-get-a-this-sitepage-cant-be-reached-error-in-my-web-browser"></a>Ich erhalte eine Fehlermeldung für **diese Site/Seite kann in meinem Webbrowser nicht erreicht werden** .

### <a name="if-youve-installed-windows-admin-center-as-an-app-on-windows-10"></a>Wenn Sie Windows Admin Center als **app unter Windows 10** installiert haben

* Stellen Sie sicher, dass das Windows Admin Center ausgeführt wird. Suchen Sie in ![ ](../media/trayIcon.PNG) der Task Leiste oder im **Windows Admin Center-Desktop/SmeDesktop.exe** im Task-Manager nach dem Windows Admin Center-Symbol. Wenn dies nicht der Wert ist, starten Sie **Windows Admin Center** über das Startmenü.

> [!NOTE]
> Nach dem Neustart müssen Sie Windows Admin Center über das Startmenü starten.

* [Überprüfen der Windows-Version](#check-the-windows-version)

* Stellen Sie sicher, dass Sie Microsoft Edge oder Google Chrome als Webbrowser verwenden.

* Haben Sie beim [ersten Start](../use/get-started.md#selecting-a-client-certificate) das richtige Zertifikat ausgewählt?

  * Versuchen Sie, Ihren Browser in einer privaten Sitzung zu öffnen. wenn dies funktioniert, müssen Sie den Cache löschen.

* Haben Sie kürzlich ein Upgrade von Windows 10 auf einen neuen Build oder eine neue Version durchgeführt?

  * Dadurch haben Sie möglicherweise die Einstellungen für vertrauenswürdige Hosts gelöscht. [Befolgen Sie diese Anweisungen, um die Einstellungen für vertrauenswürdige Hosts zu aktualisieren.](#configure-trustedhosts)

### <a name="if-youve-installed-windows-admin-center-as-a-gateway-on-windows-server"></a>Wenn Sie Windows Admin Center als **Gateway unter Windows Server** installiert haben

* [Überprüfen Sie die Windows-Version](#check-the-windows-version) des Clients und des Servers.

* Stellen Sie sicher, dass Sie Microsoft Edge oder Google Chrome als Webbrowser verwenden.

* Öffnen Sie auf dem-Server den Task-Manager >-Dienste, und stellen Sie sicher, dass **servermanagementgateway/Windows Admin Center** ausgeführt wird.

    ![Task-Manager: Registerkarte Dienste](../media/Service-TaskMan.PNG)

* Testen Sie die Netzwerkverbindung mit dem Gateway (ersetzen \<values> Sie durch die Informationen aus der Bereitstellung).

    ```powershell
    Test-NetConnection -Port <port> -ComputerName <gateway> -InformationLevel Detailed
    ```

### <a name="if-you-have-installed-windows-admin-center-in-an-azure-windows-server-vm"></a>Wenn Sie Windows Admin Center auf einer Azure Windows Server-VM installiert haben

* [Überprüfen der Windows-Version](#check-the-windows-version)
* Haben Sie eine Regel für den eingehenden Port für HTTPS hinzugefügt?
* [Weitere Informationen zum Installieren des Windows Admin Centers auf einer Azure-VM](https://docs.microsoft.com/windows-server/manage/windows-admin-center/configure/azure-integration#use-a-windows-admin-center-gateway-deployed-in-azure)

### <a name="check-the-windows-version"></a>Überprüfen der Windows-Version

* Öffnen Sie das Dialogfeld Ausführen (Windows-Taste + R), und starten Sie ```winver``` .

* Wenn Sie Windows 10, Version 1703 oder eine andere Version verwenden, wird Windows Admin Center in Ihrer Microsoft Edge-Version nicht unterstützt. Aktualisieren Sie entweder auf eine aktuelle Version von Windows 10, oder verwenden Sie Chrome.

* Wenn Sie eine Insider-Vorschauversion von Windows 10 oder Server mit einer Buildversion zwischen 17134 und 17637 verwenden, hatte Windows einen Fehler, der dazu geführt hat, dass Windows Admin Center fehlgeschlagen ist. Verwenden Sie eine aktuelle unterstützte Version von Windows.

### <a name="make-sure-the-windows-remote-management-winrm-service-is-running-on-both-the-gateway-machine-and-managed-node"></a>Stellen Sie sicher, dass der Windows-Remoteverwaltung (WinRM)-Dienst auf dem Gatewaycomputer und dem verwalteten Knoten ausgeführt wird.

* Öffnen Sie das Dialogfeld "ausführen" mit WindowsKey + R.
* Eingeben ```services.msc``` und drücken der EINGABETASTE
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

## <a name="i-can-connect-to-some-servers-but-not-others"></a>Ich kann eine Verbindung mit einigen Servern herstellen, aber nicht mit anderen.

* Melden Sie sich lokal am Gatewaycomputer an, und versuchen ```Enter-PSSession <machine name>``` Sie es in PowerShell, indem \<machine name> Sie durch den Namen des Computers ersetzen, den Sie im Windows Admin Center verwalten möchten.

* Wenn in Ihrer Umgebung eine Arbeitsgruppe anstelle einer Domäne verwendet wird, finden Sie weitere Informationen unter [Verwenden des Windows Admin Centers in einer Arbeitsgruppe](#using-windows-admin-center-in-a-workgroup).

* **Verwenden lokaler Administrator Konten:** Wenn Sie ein lokales Benutzerkonto verwenden, das nicht das integrierte Administrator Konto ist, müssen Sie die Richtlinie auf dem Zielcomputer aktivieren, indem Sie den folgenden Befehl in PowerShell oder an einer Eingabeaufforderung als Administrator auf dem Zielcomputer ausführen:

    ```
    REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1
    ```

## <a name="using-windows-admin-center-in-a-workgroup"></a>Verwenden des Windows Admin Centers in einer Arbeitsgruppe

### <a name="what-account-are-you-using"></a>Welches Konto verwenden Sie?
Stellen Sie sicher, dass die Anmelde Informationen, die Sie verwenden, ein Mitglied der lokalen Administratoren Gruppe des Zielservers sind. In einigen Fällen muss WinRM auch Mitglied der Gruppe "Remote Verwaltungs Benutzer" sein. Wenn Sie ein lokales Benutzerkonto verwenden, das **nicht das integrierte Administrator Konto**ist, müssen Sie die Richtlinie auf dem Zielcomputer aktivieren, indem Sie den folgenden Befehl in PowerShell oder an einer Eingabeaufforderung als Administrator auf dem Zielcomputer ausführen:

```cmd
REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1
```
### <a name="are-you-connecting-to-a-workgroup-machine-on-a-different-subnet"></a>Stellen Sie eine Verbindung mit einem Arbeitsgruppencomputer in einem anderen Subnetz her?

Zum Herstellen einer Verbindung mit einem Arbeitsgruppen Computer, der sich nicht im gleichen Subnetz wie das Gateway befindet, stellen Sie sicher, dass der Firewallport für WinRM (TCP 5985) eingehenden Datenverkehr auf dem Zielcomputer zulässt. Sie können den folgenden Befehl in PowerShell oder an einer Eingabeaufforderung als Administrator auf dem Zielcomputer ausführen, um diese Firewallregel zu erstellen:

- **Windows Server**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any
    ```

- **Windows 10**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any
    ```

### <a name="configure-trustedhosts"></a>Konfigurieren von "Treuhänder Hosts"

Bei der Installation von Windows Admin Center haben Sie die Möglichkeit, die Einstellung "Treuhänder" des Gateways durch das Windows Admin Center zu verwalten. Dies ist in einer Arbeitsgruppen Umgebung oder bei Verwendung lokaler Administrator Anmelde Informationen in einer Domäne erforderlich. Wenn Sie diese Einstellung auswählen, müssen Sie "Treuhänder Hosts" manuell konfigurieren.

**So ändern Sie "Treuhänder Hosts" mithilfe von PowerShell-Befehlen:**

1. Öffnen Sie eine PowerShell-Administrator Sitzung.
2. Aktuelle Einstellung für "Treuhänder Hosts" anzeigen:

    ```powershell
    Get-Item WSMan:\localhost\Client\TrustedHosts
    ```

   > [!WARNING]
   > Wenn die aktuelle Einstellung Ihrer Treuhänder Hosts nicht leer ist, überschreiben die folgenden Befehle Ihre Einstellung. Es wird empfohlen, die aktuelle Einstellung mit dem folgenden Befehl in einer Textdatei zu speichern, damit Sie Sie bei Bedarf wiederherstellen können:
   >
   > `Get-Item WSMan:localhost\Client\TrustedHosts | Out-File C:\OldTrustedHosts.txt`

3. Legen Sie "Treuhänder Hosts" auf NetBIOS, IP oder FQDN der Computer fest, die Sie verwalten möchten:

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '192.168.1.1,server01.contoso.com,server02'
    ```

   > [!TIP]
   > Um alle Treuhänder Hosts auf einfache Weise gleichzeitig festzulegen, können Sie einen Platzhalter verwenden.
   >
   > ```powershell
   > Set-Item WSMan:\localhost\Client\TrustedHosts -Value '*'
   > ```

4. Wenn Sie die Tests abgeschlossen haben, können Sie den folgenden Befehl in einer PowerShell-Sitzung mit erhöhten Rechten ausgeben, um die Einstellung für "Treuhänder Hosts" zu löschen:

    ```powershell
    Clear-Item WSMan:localhost\Client\TrustedHosts
    ```

5. Wenn Sie zuvor Ihre Einstellungen exportiert haben, öffnen Sie die Datei, kopieren Sie die Werte, und verwenden Sie den folgenden Befehl:

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

Edge hat [bekannte Probleme](https://github.com/AzureAD/azure-activedirectory-library-for-js/wiki/Known-issues-on-Edge) im Zusammenhang mit Sicherheitszonen, die sich auf die Azure-Anmeldung im Windows Admin Center auswirken. Wenn Sie Probleme bei der Verwendung von Azure-Features bei der Verwendung von Edge haben, versuchen Sie https://login.microsoftonline.com , https://login.live.com die URL des Gateways als vertrauenswürdige Sites und zulässige Sites für die Einstellungen für den Popup Blocker in Ihrem Client seitigen Browser hinzuzufügen.

Gehen Sie dazu folgendermaßen vor:
1. **Internet Optionen** im Windows-Startmenü suchen
2. Zur Registerkarte " **Sicherheit** " wechseln
3. Klicken Sie unter der Option **Vertrauenswürdige Sites** auf die Schaltfläche **Sites**, und fügen Sie im daraufhin geöffneten Dialogfeld die URLs hinzu. Sie müssen ihre Gateway-URL sowie und hinzufügen https://login.microsoftonline.com https://login.live.com .
4. Zur Registerkarte " **Datenschutz** " wechseln
5. Klicken Sie im Abschnitt **Popup Blocker** auf die Schaltfläche **Einstellungen** , und fügen Sie die URLs in dem daraufhin geöffneten Dialogfeld hinzu. Sie müssen ihre Gateway-URL sowie und hinzufügen https://login.microsoftonline.com https://login.live.com .

## <a name="having-an-issue-with-an-azure-related-feature"></a>Haben Sie ein Problem mit einer Azure-bezogenen Funktion?

Senden Sie uns eine e-Mail unter wacFeedbackAzure@microsoft.com mit den folgenden Informationen:
* Allgemeine Problem Informationen aus den [unten aufgeführten Fragen](#providing-feedback-on-issues).
* Beschreiben Sie Ihr Problem und die Schritte, die Sie ausgeführt haben, um das Problem zu reproduzieren.
* Haben Sie zuvor Ihr Gateway mit dem New-AadApp.ps1 herunterladbaren Skript bei Azure registriert und dann auf Version 1807 aktualisiert? Oder haben Sie Ihr Gateway in Azure über die Benutzeroberfläche über die Gatewayeinstellungen > Azure registriert?
* Ist Ihr Azure-Konto mehreren Verzeichnissen/Mandanten zugeordnet?
    * Wenn ja: bei der Registrierung der Azure AD Anwendung bei Windows Admin Center war das Verzeichnis, in dem Sie Ihr Standardverzeichnis in Azure verwendet haben?
* Hat ihr Azure-Konto Zugriff auf mehrere Abonnements?
* Ist für das Abonnement, das Sie verwenden, eine Abrechnung angefügt?
* Haben Sie bei Auftreten des Problems bei mehreren Azure-Konten angemeldet?
* Erfordert Ihr Azure-Konto Multi-Factor Authentication?
* Möchten Sie einen virtuellen Azure-Computer verwalten?
* Ist Windows Admin Center auf einer Azure-VM installiert?

## <a name="providing-feedback-on-issues"></a>Bereitstellen von Feedback zu Problemen

Wechseln Sie zu Ereignisanzeige > Anwendungs-und Dienst > Microsoft-servermanagementexperience, und suchen Sie nach Fehlern oder Warnungen.

Melden Sie einen Fehler auf unserer [UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5BBug%5D) , der Ihr Problem beschreibt.

Fügen Sie alle Fehler oder Warnungen, die Sie im Ereignisprotokoll finden, sowie die folgenden Informationen ein:

* Plattform, auf der Windows Admin Center **installiert** ist (Windows 10 oder Windows Server):
    * Wenn auf dem Server installiert ist, wie lautet die Windows- [Version](#check-the-windows-version) des Computers, auf **dem der Browser ausgeführt** wird, um auf Windows Admin Center zuzugreifen:
    * Verwenden Sie das selbst signierte Zertifikat, das vom Installationsprogramm erstellt wurde?
    * Wenn Sie Ihr eigenes Zertifikat verwenden, entspricht der Antragsteller Name dem Computer?
    * Wenn Sie Ihr eigenes Zertifikat verwenden, wird von ein alternativer Antragsteller Name angegeben?
* Haben Sie mit der Standard Port Einstellung installiert?
    * Wenn dies nicht der Fall ist, welchen Port haben Sie angegeben?
* Ist der Computer, auf dem das Windows Admin Center **installiert** ist, einer Domäne beigetreten?
* Windows- [Version](#check-the-windows-version) , auf der das Windows Admin Center **installiert**ist:
* Wird der Computer, den Sie **Verwalten** möchten, einer Domäne hinzugefügt?
* Windows- [Version](#check-the-windows-version) des Computers, den Sie **verwalten möchten**:
* Welchen Browser verwenden Sie?
    * Was ist die Version, wenn Sie Google Chrome verwenden? (Hilfe > zu Google Chrome)

