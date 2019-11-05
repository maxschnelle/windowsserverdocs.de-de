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
ms.openlocfilehash: 0b4e02e6759bdb91ea51b5dcf5e1d0ae307d13b4
ms.sourcegitcommit: 1da993bbb7d578a542e224dde07f93adfcd2f489
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73567102"
---
# <a name="troubleshooting-windows-admin-center"></a>Problembehandlung für Windows Admin Center

> Applies to: Windows Admin Center, Windows Admin Center Preview

> [!Important]
> Dieses Handbuch hilft Ihnen beim Diagnostizieren und Beheben von Problemen, die mit Windows Admin Center auftreten. Wenn Sie ein Problem mit einem bestimmten Tool haben, überprüfen Sie, ob Sie ein [bekanntes Problems haben.](https://aka.ms/wacknownissues)

## <a name="installer-fails-with-message-_the-module-microsoftpowershelllocalaccounts-could-not-be-loaded_"></a>Installer fails with message: **_The Module 'Microsoft.PowerShell.LocalAccounts' could not be loaded._**

This can happen if your default PowerShell module path has been modified or removed. To resolve the issue, make sure that ```%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules``` is the **first** item in your PSModulePath environment variable. You can achieve this with the following line of PowerShell:

```powershell
[Environment]::SetEnvironmentVariable("PSModulePath","%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules;" + ([Environment]::GetEnvironmentVariable("PSModulePath","User")),"User")
```

## <a name="i-get-a-this-sitepage-cant-be-reached-error-in-my-web-browser"></a>Ich erhalte einen Fehler **diese Websiteseite kann nicht erreicht werden** im Webbrowser

### <a name="if-youve-installed-windows-admin-center-as-an-app-on-windows-10"></a>Wenn Sie Windows Admin Center als eine **App für Windows 10** installiert haben

* Überprüfen Sie, dass Windows Admin Center ausgeführt wird. Look for the Windows Admin Center icon ![](../media/trayIcon.PNG) in the System tray or **Windows Admin Center Desktop / SmeDesktop.exe** in Task Manager. Wenn dies nicht der Fall ist, starten Sie **Windows Admin Center** im Startmenü.

> [!NOTE] 
> Nach dem Neustart müssen Sie Windows Admin Center im Startmenü starten.  

* [Check the Windows version](#check-the-windows-version)

* Stellen Sie sicher, dass Sie Microsoft Edge oder Google Chrome als Webbrowser verwenden.

* Haben Sie [beim Startvorgang](../use/get-started.md#selecting-a-client-certificate) das richtige Zertifikat ausgewählt?

  * Versuchen Sie Ihren Browser in einer privaten Sitzung zu öffnen - Wenn das funktioniert, müssen Sie Ihren Cache leeren.

* Did you recently upgrade Windows 10 to a new build or version?

  * This may have cleared your trusted hosts settings. [Follow these instructions to update your trusted hosts settings.](#configure-trustedhosts)

### <a name="if-youve-installed-windows-admin-center-as-a-gateway-on-windows-server"></a>Wenn Sie Windows Admin Center als **Gateway unter Windows Server** installiert haben

* [Überprüfen Sie die Windows-Version](#check-the-windows-version) auf dem Client und Server.

* Stellen Sie sicher, dass Sie Microsoft Edge oder Google Chrome als Webbrowser verwenden.

* On the server, open Task Manager > Services and make sure **ServerManagementGateway / Windows Admin Center** is running.
![](../media/Service-TaskMan.PNG)

* Test the network connection to the Gateway (replace \<values> with the information from your deployment)

    ```powershell
    Test-NetConnection -Port <port> -ComputerName <gateway> -InformationLevel Detailed
    ```

### <a name="if-you-have-installed-windows-admin-center-in-an-azure-windows-server-vm"></a>If you have installed Windows Admin Center in an Azure Windows Server VM

* [Check the Windows version](#check-the-windows-version)
* Haben Sie eine eingehende Portregel für HTTPS hinzugefügt? 
* [Learn more about installing Windows Admin Center in an Azure VM](https://docs.microsoft.com/windows-server/manage/windows-admin-center/configure/azure-integration#use-a-windows-admin-center-gateway-deployed-in-azure)

### <a name="check-the-windows-version"></a>Überprüfen Sie die Windows-Version

* Öffnen Sie das Dialogfeld "Ausführen" (Windows-Taste + R) und starten Sie ```winver```.

* Bei Verwendung der Windows 10 Version 1703 oder niedriger wird Windows Admin Center von Ihrer Version von Microsoft Edge nicht unterstützt. Aktualisieren Sie auf eine neuere Version von Windows 10 oder verwenden Sie Chrome.

* If you are using an insider preview version of Windows 10 or Server with a build version between 17134 and 17637, Windows had a bug which caused Windows Admin Center to fail. Please use a current supported version of Windows.

### <a name="make-sure-the-windows-remote-management-winrm-service-is-running-on-both-the-gateway-machine-and-managed-node"></a>Make sure the Windows Remote Management (WinRM) service is running on both the gateway machine and managed node

* Open the run dialog with WindowsKey + R
* Type ```services.msc``` and press enter
* In the window that opens, look for Windows Remote Management (WinRM), make sure it is running and set to automatically start

### <a name="did-you-upgrade-your-server-from-2016-to-2019"></a>Did you upgrade your server from 2016 to 2019?

* This may have cleared your trusted hosts settings. [Follow these instructions to update your trusted hosts settings.](#configure-trustedhosts) 

## <a name="i-get-the-message-cant-connect-securely-to-this-page-this-might-be-because-the-site-uses-outdated-or-unsafe-tls-security-settings"></a>I get the message: "Cant connect securely to this page. This might be because the site uses outdated or unsafe TLS security settings.

Your machine is restricted to HTTP/2 connections. Windows Admin Center uses integrated Windows authentication, which is not supported in HTTP/2. Add the following two registry values under the ```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Http\Parameters``` key on **the machine running the browser** to remove the HTTP/2 restriction:

```
EnableHttp2Cleartext=dword:00000000
EnableHttp2Tls=dword:00000000
```

## <a name="im-having-trouble-with-the-remote-desktop-events-and-powershell-tools"></a>I'm having trouble with the Remote Desktop, Events, and PowerShell tools.

These three tools require the websocket protocol, which is commonly blocked by proxy servers and firewalls. If you are using Google Chrome, there is a [known issue](known-issues.md#google-chrome) with websockets and NTLM authentication.

## <a name="i-can-connect-to-some-servers-but-not-others"></a>Ich kann eine Verbindung zu einigen Servern, jedoch nicht zu anderen herstellen.

* Log on to the gateway machine locally and try to ```Enter-PSSession <machine name>``` in PowerShell, replacing \<machine name> with the name of the Machine you are trying to manage in Windows Admin Center. 

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

**To modify TrustedHosts using PowerShell commands:**

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

## <a name="i-previously-had-windows-admin-center-installed-and-now-nothing-else-can-use-the-same-tcpip-port"></a>I previously had Windows Admin Center installed, and now nothing else can use the same TCP/IP port

Manually run these two commands in an elevated command prompt:

```cmd
netsh http delete sslcert ipport=0.0.0.0:443
netsh http delete urlacl url=https://+:443/
```

## <a name="azure-features-dont-work-properly-in-edge"></a>Azure features don't work properly in Edge

Edge has [known issues](https://github.com/AzureAD/azure-activedirectory-library-for-js/wiki/Known-issues-on-Edge) related to security zones that affect Azure login in Windows Admin Center. If you are having trouble using Azure features when using Edge, try adding https://login.microsoftonline.com, https://login.live.com and the URL of your gateway as trusted sites and to allowed sites for Edge pop-up blocker settings on your client side browser. 

Gehen Sie dazu wie folgt vor:
1. Search for **Internet Options** in the Windows Start Menu
2. Go to the **Security** tab
3. Under the **Trusted Sites** option, click on the **sites** button and add the URLs in the dialog box that opens. You'll need to add your gateway URL as well as https://login.microsoftonline.com and https://login.live.com.
4. Go to the **Privacy** tab
5. Under the **Pop-up Blocker** section, click on the **Settings** button and add the URLs in the dialog box that opens. You'll need to add your gateway URL as well as https://login.microsoftonline.com and https://login.live.com.

## <a name="having-an-issue-with-an-azure-related-feature"></a>Having an issue with an Azure-related feature?

Please send us an email at wacFeedbackAzure@microsoft.com with the following information:
* General issue information from the [questions listed below](#providing-feedback-on-issues).
* Describe your issue and the steps you took to reproduce the issue. 
* Did you previously register your gateway to Azure using the New-AadApp.ps1 downloadable script and then upgrade to version 1807? Or did you register your gateway to Azure using the UI from gateway Settings > Azure?
* Is your Azure account associated with multiple directories/tenants?
    * If yes: When registering the Azure AD application to Windows Admin Center, was the directory you used your default directory in Azure? 
* Does your Azure account have access to multiple subscriptions?
* Does the subscription you were using have billing attached?
* Were you logged in to multiple Azure accounts when you encountered the issue?
* Does your Azure account require multi-factor authentication?
* Is the machine you are trying to manage an Azure VM?
* Is Windows Admin Center installed on an Azure VM?

## <a name="providing-feedback-on-issues"></a>Providing feedback on issues

Navigieren Sie zur Ereignisanzeige > Anwendung und Dienste > Microsoft ServerManagementExperience und suchen Sie nach Fehlern oder Warnungen.

Melden Sie den Fehler und eine Beschreibung auf unserer [UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5BBug%5D).

Geben Sie dabei auch alle Fehler oder Warnungen an, die Sie im Ereignisprotokoll gefunden haben sowie die folgenden Informationen: 

* Die Plattform, auf der Windows Admin Center (Windows 10 oder Windows Server) **installiert** ist:
    * If installed on Server, what is the Windows [version](#check-the-windows-version) of **the machine running the browser** to access Windows Admin Center: 
    * Are you using the self-signed certificate created by the installer?
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

