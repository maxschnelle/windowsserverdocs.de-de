---
title: Windows Admin Center allgemeine Schritte zur Problembehandlung
description: Windows Admin Center allgemeine Problembehandlungsschritte (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 02/12/2019
ms.openlocfilehash: a91a8dcf6f05ef0ef66dee603851150b2145d559
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297081"
---
# Problembehandlung für Windows Admin Center

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

> [!Important]
> Dieses Handbuch hilft Ihnen beim Diagnostizieren und Beheben von Problemen, die mit Windows Admin Center auftreten. Wenn Sie ein Problem mit einem bestimmten Tool haben, überprüfen Sie, ob Sie ein [bekanntes Problems haben.](http://aka.ms/wacknownissues)

<a id="toc"></a>

## Direktlink

* [Das Installationsprogramm schlägt fehl, wenn die Nachricht: ** _das Modul "Microsoft.PowerShell.LocalAccounts" konnte nicht geladen werden._**](#psmodulepath)

* Ich erhalte einen Fehler **diese Websiteseite kann nicht erreicht werden** im Webbrowser (Wählen Sie Ihren Bereitstellungstyp aus)
    * [Ich habe Windows Admin Center als eine App auf Windows 10 installiert](#whitescreenw10)
    * [Ich habe Windows Admin Center als Gateway unter Windows Server installiert](#whitescreenws)
    * [Ich habe Windows Admin Center als Gateway auf Azure-VM installiert](#whitescreenazvm)

* [Windows Administrationscenter Startseite geladen, aber ich kann auf den Bereich Verbindung hinzufügen nicht verlassen oder keine Verbindung mehr auf dem Computer.](#winvercompat)

* [Ich erhalte die Meldung: "Fehler beim Laden des Moduls. RPC: abgelaufener Wiederholungsversuch 'Ping'."](#winvercompat)

* [Ich erhalte die Meldung: "kann nicht sichere Verbindung zu dieser Seite. Dies kann, da die Website veraltete oder unsichere TLS-Sicherheitseinstellungen verwendet."](#tls)

* [Ich habe Probleme mit der Remotedesktop-Ereignisse und PowerShell-Tools.](#websockets)

* [Beim treten Probleme mit der Azure-Features in Edge](#azlogin)

* [Ich kann eine Verbindung zu einigen Servern, jedoch nicht zu anderen herstellen.](#connectionissues)

* [Ich verwende Windows Admin Center in einer **Arbeitsgruppe**](#workgroup)

* [Ich habe zuvor Windows Admin Center installiert und sonst nichts können jetzt den gleichen TCP/IP-port](#urlacl)

* [Mein Problem ist hier nicht aufgeführt, oder die Schritte auf dieser Seite konnten mein Problem nicht lösen.](#filebug)

<a id="psmodulepath"></a>

## Installer schlägt fehl, mit der Meldung: ** _das Modul "Microsoft.PowerShell.LocalAccounts" konnte nicht geladen werden._**

Dies kann passieren, wenn Ihre PowerShell-Modul Standardpfad geändert oder entfernt wurde. Um das Problem zu beheben, stellen Sie sicher, dass ```%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules``` ist das **erste** Element in Ihrer PSModulePath Umgebungsvariablen. Sie können dies erreichen, mit dem folgenden PowerShell:

```powershell
[Environment]::SetEnvironmentVariable("PSModulePath","%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules;" + ([Environment]::GetEnvironmentVariable("PSModulePath","User")),"User")
```

## Ich erhalte einen Fehler **diese Websiteseite kann nicht erreicht werden** im Webbrowser

<a id="whitescreenw10"></a>

### Wenn Sie Windows Admin Center als eine **App für Windows 10** installiert haben

* Überprüfen Sie, dass Windows Admin Center ausgeführt wird. Suchen Sie nach der Windows Admin Center-Symbol ![](../media/trayIcon.PNG) in der Taskleiste oder **Windows Admin Center Desktop / SmeDesktop.exe** im Task-Manager. Wenn dies nicht der Fall ist, starten Sie **Windows Admin Center** im Startmenü.

> [!NOTE] 
> Nach dem Neustart müssen Sie Windows Admin Center im Startmenü starten.  

* [Überprüfen Sie die Windows-Version](#winvercompat)

* Stellen Sie sicher, dass Sie Microsoft Edge oder Google Chrome als Webbrowser verwenden.

* Haben Sie [beim Startvorgang](../use/get-started.md#selecting-a-client-certificate) das richtige Zertifikat ausgewählt?

  * Versuchen Sie Ihren Browser in einer privaten Sitzung zu öffnen - Wenn das funktioniert, müssen Sie Ihren Cache leeren.

* Haben Sie vor kurzem Windows 10 auf einem neuen Build oder Version aktualisiert?

  * Dies möglicherweise Ihre vertrauenswürdigen Hosts-Einstellungen deaktiviert haben. [Befolgen Sie diese Anweisungen, um die Einstellungen für die vertrauenswürdigen Hosts zu aktualisieren.](#configure-trustedhosts) 

[[Zurück zum Anfang]](#toc)

<a id="whitescreenws"></a>

### Wenn Sie Windows Admin Center als **Gateway unter Windows Server** installiert haben

* Haben Sie von einer früheren Version von Windows Admin Center aktualisiert? Überprüfen Sie, um sicherzustellen, dass die Firewall-Regel aufgrund [Dieses bekannte Problem](known-issues.md#upgrade)nicht gelöscht wurde. Verwenden Sie den folgende PowerShell-Befehl, um festzustellen, ob die Regel vorhanden ist. Wenn dies nicht der Fall ist, befolgen Sie [diese Anweisungen,](known-issues.md#upgrade) um sie neu zu erstellen.
    ```powershell
    Get-NetFirewallRule -DisplayName "SmeInboundOpenException"
    ```

* [Überprüfen Sie die Windows-Version](#winvercompat) auf dem Client und Server.

* Stellen Sie sicher, dass Sie Microsoft Edge oder Google Chrome als Webbrowser verwenden.

* Klicken Sie auf dem Server öffnen Sie Task-Manager > Dienste, und stellen Sie sicher, dass **ServerManagementGateway / Windows Admin Center** ausgeführt wird.
![](../media/Service-TaskMan.PNG)

* Das Testen der Netzwerkverbindung an das Gateway (ersetzt \ <Werte> mit den Informationen in Ihrer Bereitstellung)
    ```powershell
    Test-NetConnection -Port <port> -ComputerName <gateway> -InformationLevel Detailed
    ```

[[Zurück zum Anfang]](#toc)

<a id="whitescreenazvm"></a>  

### Wenn Sie Windows Admin Center in einer Azure Windows Server-VM installiert haben

* [Überprüfen Sie die Windows-Version](#winvercompat)
* Haben Sie eine eingehende Portregel für HTTPS hinzugefügt? 
* [Weitere Informationen zum Installieren von Windows Admin Center in einer Azure-VM](https://docs.microsoft.com/windows-server/manage/windows-admin-center/configure/azure-integration#use-a-windows-admin-center-gateway-deployed-in-azure)

[[Zurück zum Anfang]](#toc)

<a id="winvercompat"></a>

### Überprüfen Sie die Windows-Version

* Öffnen Sie das Dialogfeld "Ausführen" (Windows-Taste + R) und starten Sie ```winver```.

* Bei Verwendung der Windows 10 Version 1703 oder niedriger wird Windows Admin Center von Ihrer Version von Microsoft Edge nicht unterstützt. Aktualisieren Sie auf eine neuere Version von Windows 10 oder verwenden Sie Chrome.

* Wenn Sie eine Insider Preview-Version von Windows 10 oder Server mit einer Buildversion zwischen 17134 und 17637 verwenden, wurden in Windows einen Fehler der Windows Admin Center fehlschlagen ließ. Verwenden Sie eine aktuelle unterstützte Version von Windows.

### Stellen Sie sicher, dass der Windows-Remoteverwaltung (WinRM)-Dienst auf dem Gateway-Computer und dem verwalteten Knoten ausgeführt wird

* Öffnen Sie das Dialogfeld "ausführen" mit wiedergegebene + R
* Typ ```services.msc``` und drücken Sie die EINGABETASTE
* Stellen Sie in dem Fenster, das geöffnet wird, suchen Sie nach Windows-Remoteverwaltung (WinRM) sicher ausgeführt wird, und legen für den automatischen start

### Haben Sie den Server aus 2016 2019 aktualisiert?

* Dies möglicherweise Ihre vertrauenswürdigen Hosts-Einstellungen deaktiviert haben. [Befolgen Sie diese Anweisungen, um die Einstellungen für die vertrauenswürdigen Hosts zu aktualisieren.](#configure-trustedhosts) 

[[Zurück zum Anfang]](#toc)

<a id="tls"></a>

## Ich erhalte die Meldung: "kann nicht sichere Verbindung zu dieser Seite. Dies kann, da die Website veraltete oder unsichere TLS-Sicherheitseinstellungen verwendet.

<!--REF: https://docs.microsoft.com/iis/get-started/whats-new-in-iis-10/http2-on-iis#when-is-http2-not-supported -->
Ihr Computer ist eingeschränkt HTTP/2-Verbindungen. Windows Admin Center verwendet die integrierte Windows-Authentifizierung, die nicht im HTTP/2 unterstützt wird. Fügen Sie die folgenden zwei Registrierungswerte unter der ```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Http\Parameters``` Schlüssel auf **dem Computer mit den Browser** die HTTP/2-Einschränkung entfernen:

```
EnableHttp2Cleartext=dword:00000000
EnableHttp2Tls=dword:00000000
```

[[Zurück zum Anfang]](#toc)

<a id="websockets"></a> 

## Ich habe Probleme mit der Remotedesktop-Ereignisse und PowerShell-Tools.

Diese drei Tools erfordern das Websocket-Protokoll, die häufig von Proxyserver und Firewalls blockiert wird. Wenn Sie Google Chrome verwenden, ist es ein [bekanntes Problem](known-issues.md#google-chrome) mit Websockets und NTLM-Authentifizierung.

[[Zurück zum Anfang]](#toc)


<a id="connectionissues"></a> 

## Ich kann eine Verbindung zu einigen Servern, jedoch nicht zu anderen herstellen.
* Melden Sie sich lokal an den Gateway-Computer an und versuchen Sie, ```Enter-PSSession <machine name>``` in PowerShell einzugeben und ersetzen Sie \ <Computername> mit dem Namen des Computers, den Sie in Windows Admin Center verwalten möchten. 

* Wenn Ihre Umgebung eine Arbeitsgruppe anstatt eine Domäne verwendet, lesen Sie [Windows Admin Center in einer Arbeitsgruppe verwenden](#workgroup).

* **Mit lokalen Administratorkonten:** Wenn Sie ein lokales Benutzerkonto verwenden, das nicht das integrierte Administratorkonto ist, müssen Sie die Richtlinie auf dem Zielcomputer mithilfe des folgenden Befehls in PowerShell oder an einer Eingabeaufforderung als Administrator auf dem Zielcomputer aktivieren:

        REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1


[[Zurück zum Anfang]](#toc)

<a id="workgroup"></a>

## Verwenden von Windows Admin Center in einer Arbeitsgruppe 

### Welches Konto verwenden Sie?
Stellen Sie sicher, dass die Anmeldeinformationen, die Sie verwenden, Mitglied der lokalen Administratorgruppe des Zielservers sind. In einigen Fällen erfordert WinRM auch die Mitgliedschaft in der Gruppe Remoteverwaltungsbenutzer. Wenn Sie ein lokales Benutzerkonto verwenden, das **nicht das integrierte Administratorkonto** ist, müssen Sie die Richtlinie auf dem Zielcomputer mithilfe des folgenden Befehls in PowerShell oder an einer Eingabeaufforderung als Administrator auf dem Zielcomputer aktivieren:

```cmd
REG ADD HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1
```
### Verbinden Sie einen Arbeitsgruppencomputer in einem anderen Subnetz?

Um zu einem Arbeitsgruppencomputer eine Verbindung zu erstellen, die nicht im selben Subnetz wie das Gateway ist, stellen Sie sicher, dass die der Firewall-Port (TCP 5985) WinRM den eingehenden Datenverkehr auf dem Zielcomputer ermöglicht. Sie können den folgenden Befehl in PowerShell oder an einer Eingabeaufforderung als Administrator auf dem Zielcomputer zum Erstellen dieser Firewallregel ausführen:

- **Windows Server**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any
    ```

- **Windows 10**

    ```powershell
    Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any
    ```

### Konfigurieren von TrustedHosts

Beim Installieren von Windows Admin Center können Sie Windows Admin Center optional die Gateway TrustedHosts-Einstellung verwalten lassen. Dies ist in einer Arbeitsgruppe erforderlich oder wenn Sie Anmeldeinformationen für lokale Administratoren in einer Domäne verwenden. Wenn Sie auf diese Einstellung verzichten, müssen Sie TrustedHosts manuell konfigurieren.

**So ändern Sie TrustedHosts mithilfe von PowerShell-Befehlen:**

1. Öffnen Sie eine Administrator PowerShell-Sitzung.
2. Zeigen Sie die aktuelle Einstellung von TrustedHosts an:

    ```powershell
    Get-Item WSMan:\localhost\Client\TrustedHosts
    ```

    > [!WARNING]
    > Wenn die aktuelle Einstellung von TrustedHosts nicht leer ist, werden die folgenden Befehle die Einstellung überschreiben. Es wird empfohlen, dass Sie die aktuelle Einstellung in eine Textdatei mit dem folgenden Befehl speichern, damit Sie diese wiederherstellen können, falls erforderlich:

    > `Get-Item WSMan:localhost\Client\TrustedHosts | Out-File C:\OldTrustedHosts.txt`

3. Legen Sie TrustedHosts auf NetBIOS-IP oder FQDN der Computer fest, den Sie verwalten möchten:

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '192.168.1.1,server01.contoso.com,server02'
    ```

    > [!TIP] 
    >Eine einfache Möglichkeit, alle TrustedHosts gleichzeitig festlegen zu können, ist das Verwenden von Platzhaltern.

    >     Set-Item WSMan:\localhost\Client\TrustedHosts -Value '*'

4. Wenn Sie fertig mit dem Testen sind, können Sie den folgenden Befehl aus einer PowerShell-Sitzung mit erhöhten Rechten zum Deaktivieren der TrustedHosts-Einstellung ausgeben:

    ```powershell
    Clear-Item WSMan:localhost\Client\TrustedHosts
    ```

5. Wenn Sie Ihre Einstellungen zuvor exportiert haben, öffnen Sie die Datei, kopieren Sie die Werte, und verwenden Sie diesen Befehl:

    ```powershell
    Set-Item WSMan:localhost\Client\TrustedHosts -Value '<paste values from text file>'
    ```

[[Zurück zum Anfang]](#toc)

<a id="urlacl"></a>

## Ich habe zuvor Windows Admin Center installiert und sonst nichts können jetzt den gleichen TCP/IP-port

Führen Sie diese zwei Befehle manuell in einem Eingabeaufforderungsfenster mit erhöhten Rechten:

```cmd
netsh http delete sslcert ipport=0.0.0.0:443
netsh http delete urlacl url=https://+:443/
```

[[Zurück zum Anfang]](#toc)

<a id="azlogin"></a>

## Beim treten Probleme mit der Azure-Features in Edge

Edge verfügt über [bekannte Probleme](https://github.com/AzureAD/azure-activedirectory-library-for-js/wiki/Known-issues-on-Edge) im Zusammenhang mit Sicherheitszonen, die Azure-Anmeldung in Windows Admin Center zu beeinflussen. Wenn Sie Probleme bei der Verwendung von Azure-Features bei Verwendung von Edge auftreten, versuchen Sie https://login.microsoftonline.com, https://login.live.com und die URL der das Gateway als vertrauenswürdige Sites Websites für Edge Popupblocker-Einstellungen auf Ihrer Seite Clientbrowser gewährt. 

Gehen Sie dazu folgendermaßen vor:
1. Suchen Sie nach **Internetoptionen** in der Windows-Menü "Start"
2. Wechseln Sie zu der Registerkarte " **Sicherheit** "
3. Klicken Sie auf die Schaltfläche " **Sites** ", und fügen Sie die URLs im Dialogfeld, das geöffnet wird, unter der Option " **Vertrauenswürdige Sites** ". Sie müssen die Gateway-URL hinzufügen sowie https://login.microsoftonline.com und https://login.live.com.
4. Wechseln Sie zu der Registerkarte " **Datenschutz** "
5. Klicken Sie im Abschnitt mit **Popupblocker** auf die Schaltfläche " **Einstellungen** ", und fügen Sie die URLs im Dialogfeld, das geöffnet wird. Sie müssen die Gateway-URL hinzufügen sowie https://login.microsoftonline.com und https://login.live.com.


[[Zurück zum Anfang]](#toc)

<a id="azissue"></a>

## Haben Sie ein Problem mit einer Azure-bezogene Features?

Senden Sie uns eine e-Mail an wacFeedbackAzure@microsoft.com mit den folgenden Informationen:
* Allgemeines Probleminformationen aus den [unten aufgeführten Fragen](#filebug). 
* Das Problem beschreiben und die Schritte, die Sie zum Reproduzieren des Problems haben. 
* Sie zuvor registrieren das Gateway mit Azure mithilfe des New-AadApp.ps1 herunterladbare Skripts und dann auf Version 1807 aktualisieren? Oder Sie das Gateway mit Azure, die über die Benutzeroberfläche von Gateway Einstellungen > Azure registriert hat?
* Ist Ihre Azure-Konto mehrere Verzeichnisse-Mandanten zugeordnet?
    * Falls Ja: Wenn Sie die Azure AD-Anwendung für Windows Admin Center zu erfassen, wurde das Verzeichnis, das Sie Ihre Standardverzeichnis in Azure verwendet? 
* Verfügt Ihr Azure-Konto Zugriff auf mehrere Abonnements?
* Verfügt das Abonnement aus, die, das Sie verwendeten, angefügte Abrechnung?
* Wurden Sie an mehreren Azure-Konten angemeldet, wenn Sie das Problem aufgetreten?
* Erfordert Ihre Azure-Konto eine mehrstufige Authentifizierung?
* Ist der Computer, die auf einer Azure VM verwalten möchten?
* Ist Windows Admin Center wird auf einer Azure-VM installiert?

[[Zurück zum Anfang]](#toc)

<a id="filebug"></a>

## Immer noch nicht funktioniert, oder ist Ihr Problem hier nicht aufgeführt? [häufig gestellte Fragen zur Problembehandlung]

Navigieren Sie zur Ereignisanzeige > Anwendung und Dienste > Microsoft ServerManagementExperience und suchen Sie nach Fehlern oder Warnungen.

Melden Sie den Fehler und eine Beschreibung auf unserer [UserVoice](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5BBug%5D).

Geben Sie dabei auch alle Fehler oder Warnungen an, die Sie im Ereignisprotokoll gefunden haben sowie die folgenden Informationen: 

* Die Plattform, auf der Windows Admin Center (Windows 10 oder Windows Server) **installiert** ist:
    * Wenn auf dem Server installiert, ist was die Windows- [Version](#winvercompat) **der Computer, die mit den Browser** auf Windows Admin Center zugreifen: 
    * Verwenden Sie das selbstsignierte Zertifikat, das vom Installationsprogramm erstellt werden?
    * Wenn Sie Ihr eigenes Zertifikat verwenden, stimmt der Antragstellername des Computers überein?
    * Wenn Sie Ihr eigenes Zertifikat verwenden, gibt es einen alternativen Antragstellernamen an?
* Haben Sie den Standard-Port installiert?
    * Falls dies nicht der Fall ist, welchen Port haben Sie angegeben?
* Ist der Computer, auf dem Windows Admin Center **installiert** ist, Mitglied einer Domäne?
* Die -[Version](#winvercompat), auf der Windows Admin Center **installiert** ist:
* Ist der Computer, den Sie **verwalten möchten**, Mitglied einer Domäne?
* Die Windows-[Version](#winvercompat) des Computers, den Sie **versuchen zu verwalten**:
* Welche Browser verwenden Sie?
    * Wenn Sie Google Chrome verwenden, was ist die Version? (Hilfe > Info zu Google Chrome)

[[Zurück zum Anfang]](#toc)