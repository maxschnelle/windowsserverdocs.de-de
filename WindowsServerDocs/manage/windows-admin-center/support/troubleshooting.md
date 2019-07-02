---
title: Windows Admin Center allgemeine Schritte zur Problembehandlung
description: Windows Admin Center allgemeine Problembehandlungsschritte (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 06/07/2019
ms.openlocfilehash: 4d108161dd4f6b57d4a86cbcaa5852aff53f0ac3
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469521"
---
# <a name="troubleshooting-windows-admin-center"></a>Problembehandlung für Windows Admin Center

> Gilt für: Windows Admin Center, Windows Admin Center Preview

> [!Important]
> Dieses Handbuch hilft Ihnen beim Diagnostizieren und Beheben von Problemen, die mit Windows Admin Center auftreten. Wenn Sie ein Problem mit einem bestimmten Tool haben, überprüfen Sie, ob Sie ein [bekanntes Problems haben.](http://aka.ms/wacknownissues)

## <a name="installer-fails-with-message-the-module-microsoftpowershelllocalaccounts-could-not-be-loaded"></a>Installer gibt zurück: **_Das Modul 'Microsoft.PowerShell.LocalAccounts' konnte nicht geladen werden._ **

Dies kann vorkommen, wenn der Standardpfad für PowerShell-Modul geändert oder entfernt wurde. Um das Problem zu beheben, stellen sicher, dass ```%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules``` ist die **erste** Element in der PSModulePath-Umgebungsvariablen. Sie können dies mit der folgenden Zeile von PowerShell erreichen:

```powershell
[Environment]::SetEnvironmentVariable("PSModulePath","%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules;" + ([Environment]::GetEnvironmentVariable("PSModulePath","User")),"User")
```

## <a name="i-get-a-this-sitepage-cant-be-reached-error-in-my-web-browser"></a>Ich erhalte einen Fehler **diese Websiteseite kann nicht erreicht werden** im Webbrowser

### <a name="if-youve-installed-windows-admin-center-as-an-app-on-windows-10"></a>Wenn Sie Windows Admin Center als eine **App für Windows 10** installiert haben

* Überprüfen Sie, dass Windows Admin Center ausgeführt wird. Suchen Sie nach dem Symbol "Windows Admin Center" ![](../media/trayIcon.PNG) in der Taskleiste oder **Windows Admin Center-Desktop / SmeDesktop.exe** im Task-Manager. Wenn dies nicht der Fall ist, starten Sie **Windows Admin Center** im Startmenü.

> [!NOTE] 
> Nach dem Neustart müssen Sie Windows Admin Center im Startmenü starten.  

* [Überprüfen Sie die Windows-version](#check-the-windows-version)

* Stellen Sie sicher, dass Sie Microsoft Edge oder Google Chrome als Webbrowser verwenden.

* Haben Sie [beim Startvorgang](../use/get-started.md#selecting-a-client-certificate) das richtige Zertifikat ausgewählt?

  * Versuchen Sie Ihren Browser in einer privaten Sitzung zu öffnen - Wenn das funktioniert, müssen Sie Ihren Cache leeren.

* Aktualisieren Sie Windows 10 vor kurzem auf einen neuen Build oder die Version?

  * Dies kann die Einstellungen für die vertrauenswürdigen Hosts gelöscht haben. [Um die Einstellungen für die vertrauenswürdigen Hosts aktualisieren, gehen Sie wie folgt vor.](#configure-trustedhosts)

### <a name="if-youve-installed-windows-admin-center-as-a-gateway-on-windows-server"></a>Wenn Sie Windows Admin Center als **Gateway unter Windows Server** installiert haben

* Durchführen Sie ein Upgrade von einer früheren Version von Windows Admin Center? Stellen Sie sicher, dass die Firewall-Regel wurde nicht gelöscht werden, da [dieses bekannte Problem](known-issues.md#upgrade). Verwenden Sie den folgenden PowerShell-Befehl, um zu bestimmen, ob die Regel vorhanden ist. Wenn dies nicht der Fall, führen Sie die [diese Anweisungen](known-issues.md#upgrade) neu erstellt.
    
    ```powershell
    Get-NetFirewallRule -DisplayName "SmeInboundOpenException"
    ```

* [Überprüfen Sie die Windows-Version](#check-the-windows-version) auf dem Client und Server.

* Stellen Sie sicher, dass Sie Microsoft Edge oder Google Chrome als Webbrowser verwenden.

* Öffnen Sie auf dem Server, Task-Manager > Dienste und stellen Sie sicher, dass **ServerManagementGateway / Windows Admin Center** ausgeführt wird.
![](../media/Service-TaskMan.PNG)

* Testen Sie die Netzwerkverbindung mit dem Gateway (ersetzen Sie dies \<Werte > mit den Informationen aus der Bereitstellung)

    ```powershell
    Test-NetConnection -Port <port> -ComputerName <gateway> -InformationLevel Detailed
    ```

### <a name="if-you-have-installed-windows-admin-center-in-an-azure-windows-server-vm"></a>Wenn Sie Windows Admin Center auf einer Azure Windows Server-VM installiert haben

* [Überprüfen Sie die Windows-version](#check-the-windows-version)
* Haben Sie eine eingehende Portregel für HTTPS hinzugefügt? 
* [Weitere Informationen zum Installieren von Windows Admin Center in einer Azure-VM](https://docs.microsoft.com/windows-server/manage/windows-admin-center/configure/azure-integration#use-a-windows-admin-center-gateway-deployed-in-azure)

### <a name="check-the-windows-version"></a>Überprüfen Sie die Windows-Version

* Öffnen Sie das Dialogfeld "Ausführen" (Windows-Taste + R) und starten Sie ```winver```.

* Bei Verwendung der Windows 10 Version 1703 oder niedriger wird Windows Admin Center von Ihrer Version von Microsoft Edge nicht unterstützt. Aktualisieren Sie auf eine neuere Version von Windows 10 oder verwenden Sie Chrome.

* Wenn Sie eine Insider Preview-Version von Windows 10 oder Server mit einer Buildversion 17134 bis 17637 verwenden, musste Windows einen Fehler der Windows Admin Center, um Fehler verursacht hat. Verwenden Sie eine aktuelle unterstützte Version von Windows.

### <a name="make-sure-the-windows-remote-management-winrm-service-is-running-on-both-the-gateway-machine-and-managed-node"></a>Stellen Sie sicher, dass der Windows-Remoteverwaltung (WinRM)-Dienst auf dem Gatewaycomputer und dem verwalteten Knoten ausgeführt wird

* Öffnen Sie das Dialogfeld "ausführen" mit wiedergegebene + R
* Typ ```services.msc``` und drücken Sie EINGABETASTE
* Stellen Sie im Fenster, das geöffnet wird, suchen Sie nach Windows-Remoteverwaltung (WinRM) sicher, dass es ausgeführt wird, und legen Sie für den automatischen start

### <a name="did-you-upgrade-your-server-from-2016-to-2019"></a>Haben Sie Ihren Server 2016 zu 2019 aktualisiert?

* Dies kann die Einstellungen für die vertrauenswürdigen Hosts gelöscht haben. [Um die Einstellungen für die vertrauenswürdigen Hosts aktualisieren, gehen Sie wie folgt vor.](#configure-trustedhosts) 

## <a name="i-get-the-message-cant-connect-securely-to-this-page-this-might-be-because-the-site-uses-outdated-or-unsafe-tls-security-settings"></a>Ich erhalte die Meldung aus: "Kann eine sichere Verbindung mit dieser Seite. Dies kann sein, da die Website veraltete oder unsafe-TLS-Sicherheit-Einstellungen verwendet.

Ihr Computer ist auf HTTP/2-Verbindungen beschränkt. Windows Admin Center verwendet die integrierte Windows-Authentifizierung, die in HTTP/2 nicht unterstützt wird. Fügen Sie die folgenden beiden Registrierungswerte unter dem ```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Http\Parameters``` auf die Taste **der Computer mit der Browser** So entfernen Sie die HTTP/2-Einschränkung:

```
EnableHttp2Cleartext=dword:00000000
EnableHttp2Tls=dword:00000000
```

## <a name="im-having-trouble-with-the-remote-desktop-events-and-powershell-tools"></a>Ich habe Probleme mit den Tools für Remotedesktop, Ereignisse und PowerShell.

Diese drei Tools erfordern das Websocket-Protokoll, die häufig von Proxy-Server und Firewalls blockiert wird. Wenn Sie Google Chrome verwenden, besteht eine [bekanntes Problem](known-issues.md#google-chrome) mit Websockets oder NTLM-Authentifizierung.

## <a name="i-can-connect-to-some-servers-but-not-others"></a>Ich kann eine Verbindung zu einigen Servern, jedoch nicht zu anderen herstellen.

* Melden Sie sich den Gatewaycomputer lokal und es wurde versucht, ```Enter-PSSession <machine name>``` in PowerShell ersetzen \<Machine-Name > durch den Namen des Computers in Windows Admin Center verwalten möchten. 

* Wenn Ihre Umgebung eine Arbeitsgruppe anstatt eine Domäne verwendet, lesen Sie [Windows Admin Center in einer Arbeitsgruppe verwenden](#using-windows-admin-center-in-a-workgroup).

* **Verwenden lokale Administratorkonten:** Wenn Sie ein lokales Benutzerkonto, das nicht das integrierte Administratorkonto ist verwenden, müssen Sie die Richtlinie auf dem Zielcomputer zu aktivieren, indem Sie mit den folgenden Befehl in PowerShell oder an einer Eingabeaufforderung als Administrator auf dem Zielcomputer:

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

**So ändern Sie die "TrustedHosts" mithilfe von PowerShell-Befehle:**

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
   >     Set-Item WSMan:\localhost\Client\TrustedHosts -Value '*'

4. Wenn Sie fertig mit dem Testen sind, können Sie den folgenden Befehl aus einer PowerShell-Sitzung mit erhöhten Rechten zum Deaktivieren der TrustedHosts-Einstellung ausgeben:

    ```powershell
    Clear-Item WSMan:localhost\Client\TrustedHosts
    ```

5. Wenn Sie Ihre Einstellungen zuvor exportiert haben, öffnen Sie die Datei, kopieren Sie die Werte, und verwenden Sie diesen Befehl:

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '<paste values from text file>'
    ```

## <a name="i-previously-had-windows-admin-center-installed-and-now-nothing-else-can-use-the-same-tcpip-port"></a>Ich hatte zuvor Windows Admin Center installiert kann, und jetzt nichts den gleichen TCP/IP-port

Führen Sie diese beiden Befehle manuell an einer Eingabeaufforderung mit erhöhten Rechten aus:

```cmd
netsh http delete sslcert ipport=0.0.0.0:443
netsh http delete urlacl url=https://+:443/
```

## <a name="azure-features-dont-work-properly-in-edge"></a>Azure-Features funktionieren nicht ordnungsgemäß in Microsoft Edge

Kante hat [bekannte Probleme](https://github.com/AzureAD/azure-activedirectory-library-for-js/wiki/Known-issues-on-Edge) im Zusammenhang mit Sicherheitszonen, die Azure-Anmeldung in Windows Admin Center zu beeinflussen. Wenn Sie schwierigkeiten bei der Verwendung von Azure-Features, wenn Sie Edge verwenden auftreten, versuchen Sie es hinzufügen https://login.microsoftonline.com, https://login.live.com und die URL Ihres Gateways als vertrauenswürdige Sites und Standorte für Edge-Popupblocker-Einstellungen in Ihrem Client-Side-Browser zulässig. 

Gehen Sie dazu wie folgt vor:
1. Suchen Sie nach **Internetoptionen** in der Windows-Startmenü
2. Wechseln Sie zu der **Sicherheit** Registerkarte
3. Unter den **vertrauenswürdige Sites** aus, klicken Sie auf die **Websites** Schaltfläche, und fügen Sie die URLs im Dialogfeld, das geöffnet wird. Sie müssen Ihre Gateway-URL hinzufügen sowie https://login.microsoftonline.com und https://login.live.com.
4. Wechseln Sie zu der **Datenschutz** Registerkarte
5. Unter den **Popup-Blocker** Abschnitt, klicken Sie auf die **Einstellungen** Schaltfläche, und fügen Sie die URLs im Dialogfeld, das geöffnet wird. Sie müssen Ihre Gateway-URL hinzufügen sowie https://login.microsoftonline.com und https://login.live.com.

## <a name="having-an-issue-with-an-azure-related-feature"></a>Problem ist ein mit einer Azure-bezogenen Features?

Senden Sie uns eine e-Mail an wacFeedbackAzure@microsoft.com mit den folgenden Informationen:
* Allgemeines Problem mit der Informationen aus der [Fragen, die unten aufgeführten](#providing-feedback-on-issues).
* Beschreiben Sie Ihr Problem, und die Schritte, die Sie zum Reproduzieren des Problems ausgeführt. 
* Sie zuvor Registrieren des Gateways in Azure mit dem New-AadApp.ps1 herunterladbare Skript und dann ein upgrade auf Version 1807? Oder haben Sie registrieren das Gateway in Azure über die Benutzeroberfläche vom Gateway-Einstellungen > Azure?
* Ist Ihr Azure-Konto verknüpft ist, können mehrere Verzeichnisse/Mandanten?
    * Wenn dies der Fall: Wenn Sie Azure AD-Anwendung auf Windows Admin Center zu registrieren, wurde das Verzeichnis mit dem Sie Ihr Standardverzeichnis in Azure verwendet? 
* Verfügen Ihr Azure-Konto Zugriff auf mehrere Abonnements?
* Verfügt das Abonnement, für die Verwendung von angefügte Abrechnung?
* Wurden Sie mehrere Azure-Konten angemeldet, wenn Sie das Problem auftritt?
* Ist Ihr Azure-Konto für Multi-Factor Authentication erforderlich?
* Ist auf der Computer werden zum Verwalten einer Azure-VM an?
* Werden Windows Admin Center ist auf einer Azure-VM installiert?

## <a name="providing-feedback-on-issues"></a>Senden von Feedback zu Problemen

Navigieren Sie zur Ereignisanzeige > Anwendung und Dienste > Microsoft ServerManagementExperience und suchen Sie nach Fehlern oder Warnungen.

Melden Sie den Fehler und eine Beschreibung auf unserer [UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5BBug%5D).

Geben Sie dabei auch alle Fehler oder Warnungen an, die Sie im Ereignisprotokoll gefunden haben sowie die folgenden Informationen: 

* Die Plattform, auf der Windows Admin Center (Windows 10 oder Windows Server) **installiert** ist:
    * Wenn auf dem Server installiert haben, was ist die Windows [Version](#check-the-windows-version) von **der Computer mit der Browser** auf Windows Admin Center zugreifen: 
    * Verwenden Sie das selbstsignierte Zertifikat, das vom Installationsprogramm erstellt werden?
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

