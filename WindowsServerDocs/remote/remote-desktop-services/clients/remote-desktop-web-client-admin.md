---
title: Einrichten des Remotedesktop-Webclients für Ihre Benutzer
description: Beschreibt, wie ein Administrator der Remotedesktop-Webclient einrichten kann.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 11/2/2018
ms.topic: article
author: Heidilohr
ms.localizationpriority: medium
ms.openlocfilehash: 2cb819a7f91646c61b84c3ee70550af6033ba340
ms.sourcegitcommit: 491c94b25501732c4a4abda533cc62b8bd278ed2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/22/2019
ms.locfileid: "9099183"
---
# Einrichten des Remotedesktop-Webclients für Ihre Benutzer

Der Remotedesktop-Webclient ermöglicht Benutzern das Remotedesktop-Infrastruktur Ihres Unternehmens über eine kompatible Webbrowser zugreifen. Er kann dann für die Interaktion mit remote-apps oder Desktops, wie sie mit einem lokalen PC unabhängig davon, wo sie sind. Nachdem Sie Ihre Remotedesktop-Webclient einrichten, alles, was Ihre Benutzer benötigen für den Einstieg ist die URL, sodass sie den Client, seine Anmeldeinformationen und einem unterstützten Webbrowser zugreifen.

>[!IMPORTANT]
>Der Webclient unterstützt derzeit nicht mithilfe von Azure und Web Application Proxy nicht überhaupt unterstützt. Details finden Sie unter [Verwendung von RDS mit Application Proxy-Dienste](../rds-supported-config.md#using-remote-desktop-services-with-application-proxy-services) .

## Was Sie benötigen, zum Einrichten des Webclients

Beachten Sie bevor Sie beginnen Folgendes beachten:

* Stellen Sie sicher, dass Ihre [Remotedesktop-Bereitstellung](../rds-deploy-infrastructure.md) RD-Gateway, ein RD Connection Broker und Web Access für Remotedesktop auf Windows Server 2016 oder 2019 ausgeführt hat.
* Stellen Sie sicher, dass die Bereitstellung für [pro-Benutzer-Clientzugriffslizenzen](../rds-client-access-license.md) (CALs) anstelle von pro-Gerät, andernfalls konfiguriert ist, die alle Lizenzen verwendet werden.
* Installieren Sie das [Windows 10 KB4025334 aktualisieren](https://support.microsoft.com/en-us/help/4025334/windows-10-update-kb4025334) , auf dem RD-Gateway. Später kumulativen Updates möglicherweise bereits dieser KB enthält.
* Stellen Sie sicher, dass öffentlich vertrauenswürdige Zertifikate für die RD-Gateway und Web Access für Remotedesktop-Rollen konfiguriert sind.
* Stellen Sie sicher, dass alle Computer, auf denen die Benutzer eine Verbindung herstellt, die eine der folgenden Betriebssystemversionen ausgeführt werden:
  * Windows 10
  * Windows Server 2008 R2 oder höher

Ihre Benutzer sehen eine bessere Leistung Herstellen einer Verbindung zu Windows Server 2016 (oder höher) und Windows 10 (Version 1611 oder höher).

>[!IMPORTANT]
>Wenn Sie den WebClient während der Testphase Vorschau und eine Version vor 1.0.0 installiert, müssen Sie zunächst den alten Client deinstallieren, vor der Umstellung auf die neue Version. Wenn Sie eine Fehlermeldung mit der Bezeichnung "Webclient mit einer älteren Version von RDWebClientManagement installiert wurde, und muss vor der Bereitstellung der neuen Version zuerst entfernt werden", gehen Sie folgendermaßen vor:
>
>1. Öffnen Sie eine PowerShell-Eingabeaufforderung mit erhöhten Rechten.
>2. Führen Sie die **Deinstallations-Modul RDWebClientManagement** , um das neue Modul zu deinstallieren.
>3. Schließen Sie und öffnen Sie die PowerShell-Eingabeaufforderung.
>4. Führen Sie **Installation-Modul RDWebClientManagement - Parametern \<old Version> das alte Modul installiert.**
>5. Führen Sie die **Deinstallations-RDWebClient** zum Deinstallieren Sie den alten WebClient.
>6. Führen Sie die **Deinstallations-Modul RDWebClientManagement** , um das alte Modul zu deinstallieren.
>7. Schließen Sie und öffnen Sie die PowerShell-Eingabeaufforderung.
>8. Gehen Sie wie folgt mit den normalen Installationsschritten.

## So veröffentlichen Sie den Remotedesktop-Webclient

Um die WebClient zum ersten Mal installieren, gehen Sie folgendermaßen vor:

1. Beziehen Sie auf dem RD Connection Broker-Server das Zertifikat für den Remotedesktop-Verbindungen verwendete und als eine CER-Datei exportieren. Kopieren Sie die CER-Datei aus der Remotedesktop-Verbindungsbroker an den Server, der Rolle des virtuellen RD Web-ausführen.
2. Öffnen Sie auf dem Server Web Access für Remotedesktop eine PowerShell-Eingabeaufforderung mit erhöhten Rechten aus.
3. Aktualisieren Sie unter Windows Server 2016 das Modul PowerShellGet, da die Inbox-Version nicht unterstützt, Web Client Management-Modul installieren. Um PowerShellGet zu aktualisieren, führen Sie das folgende Cmdlet:
    ```PowerShell
    Install-Module -Name PowerShellGet -Force
    ```

    >[!IMPORTANT]
    >Sie müssen PowerShell neu starten, bevor das Update, andernfalls wirksam werden, die das Modul möglicherweise nicht funktionieren.

4. Installieren Sie das Remotedesktop-Web-Client-Management-PowerShell-Modul von der PowerShell-Galerie mit dem folgenden Cmdlet:
    ```PowerShell
    Install-Module -Name RDWebClientManagement
    ```

5. Führen Sie anschließend das folgende Cmdlet um die neueste Version des Remotedesktop-Webclients herunterzuladen:
    ```PowerShell
    Install-RDWebClientPackage
    ```

6. Führen Sie als Nächstes dieses Cmdlet mit dem Klammern gesetzten Wert mit dem Pfad der CER-Datei, die Sie aus der RD-Broker kopiert ersetzt:
    ```PowerShell
    Import-RDWebClientBrokerCert <.cer file path>
    ```

7. Führen Sie abschließend dieses Cmdlet, um den Remotedesktop-Webclient veröffentlichen:
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```
    Stellen Sie sicher, dass Sie Zugriff auf den Webclient im Web Client-URL zu, mit der Servernamen, die als formatiert <https://server_FQDN/RDWeb/webclient/index.html>. Es ist wichtig, den Namen des Servers verwenden, der das öffentliche Web Access für Remotedesktop-Zertifikat in der URL (in der Regel den FQDN des Servers) entspricht.

    >[!NOTE]
    >Wenn Sie das **Veröffentlichen-RDWebClientPackage** -Cmdlet ausführen, sehen Sie eine Warnung mit der Bezeichnung pro Gerät-CALs werden nicht unterstützt, auch wenn Ihre Bereitstellung für pro-Benutzer-CALs konfiguriert ist. Wenn Ihre Bereitstellung pro Benutzer-CALs verwendet, können Sie diese Warnung ignorieren. Angezeigt, um sicherzustellen, dass Sie im Hinblick auf die Konfiguration Einschränkung sind.
8. Wenn Sie bereit sind für Benutzer auf den WebClient zugreifen, senden sie einfach die-Client-URL, die Sie erstellt haben.

>[!NOTE]
>Um eine Liste aller unterstützten Cmdlets für das Modul RDWebClientManagement anzuzeigen, führen Sie das folgende Cmdlet in PowerShell aus:
>```PowerShell
>Get-Command -Module RDWebClientManagement
>```

## So aktualisieren Sie den Remotedesktop-Webclient

Gehen folgendermaßen Sie vor, um die Bereitstellung mit den neuen Client zu aktualisieren, wenn eine neue Version des Remotedesktop-Webclients verfügbar ist, haben:

1. Öffnen Sie eine PowerShell-Eingabeaufforderung auf dem Server Web Access für Remotedesktop und führen Sie das folgende Cmdlet, um die neueste Version des Webclients, der herunterzuladen:
    ```PowerShell
    Install-RDWebClientPackage
    ```

2. Optional können Sie den Client veröffentlichen, für den Test vor dem offiziellen Version durch Ausführen dieses Cmdlet:
    ```PowerShell
    Publish-RDWebClientPackage -Type Test -Latest
    ```

    Der Client sollte angezeigt werden, für die Test-URL, die Ihre Web-Client-URL entspricht (z. B. <https://server_FQDN/RDWeb/webclient-test/index.html>).
3. Veröffentlichen Sie den Client für den Benutzer durch Ausführen des folgenden Cmdlets:
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```

    Dadurch wird den Client für alle Benutzer ersetzt, wenn sie auf der Seite "Web" starten.

## So deinstallieren Sie den Remotedesktop-Webclient

Gehen Sie folgendermaßen vor, um alle Spuren des Webclients zu entfernen:

1. Öffnen Sie auf dem Server Web Access für Remotedesktop eine PowerShell-Eingabeaufforderung mit erhöhten Rechten aus.
2. Aufheben der Veröffentlichung der Test und Produktion Clients, deinstallieren Sie alle lokalen Pakete, und entfernen Sie die Web-Client-Einstellungen:

   ```PowerShell
   Uninstall-RDWebClient
   ```

3. Deinstallieren Sie das Remotedesktop-Web-Client-Management-PowerShell-Modul:

   ```PowerShell
   Uninstall-Module -Name RDWebClientManagement
   ```

## So installieren Sie den Remotedesktop-Webclient ohne Internetzugang

Führen Sie diese Schritte, um WebClient auf einem Web Access für Remotedesktop-Server bereitstellen, die Verbindung mit dem Internet besitzt.

> [!NOTE]
> Installieren, ohne Internetzugang verfügbar in Version 1.0.1 und höher des RDWebClientManagement PowerShell-Moduls.

> [!NOTE]
> Sie benötigen noch ein Administrator PC mit Internetzugriff die erforderlichen Dateien herunterladen, bevor sie an den Server offline zu übertragen.

> [!NOTE]
> Der Endbenutzer-PC benötigt eine Internetverbindung für den Moment. Dieses Problem wird in einer zukünftigen Version des Clients, um eine vollständige offline Szenario bereitzustellen behoben werden.

### Von einem Gerät mit Zugriff auf das internet

1. Öffnen Sie eine PowerShell-Eingabeaufforderung.

2. Importieren Sie das Remotedesktop-Web-Client-Management-PowerShell-Modul aus der PowerShell-Galerie:
    ```PowerShell
    Import-Module -Name RDWebClientManagement
    ```

3. Herunterladen der neuesten Version des Remotedesktop-Webclients für die Installation auf einem anderen Gerät:
    ```PowerShell
    Save-RDWebClientPackage "C:\WebClient\"
    ```

4. Laden Sie die neueste Version des RDWebClientManagement-PowerShell-Moduls herunter:
    ```PowerShell
    Find-Module -Name "RDWebClientManagement" -Repository "PSGallery" | Save-Module -Path "C:\WebClient\"
    ```

5. Kopieren Sie den Inhalt von "C:\WebClient\" mit dem Web Access für Remotedesktop-Server.

### Vom Server Web Access für Remotedesktop

Folgen Sie den Anweisungen unter [So veröffentlichen Sie den Remotedesktop-Webclient](remote-desktop-web-client-admin.md#how-to-publish-the-remote-desktop-web-client), ersetzen durch die folgenden Schritte 4 und 5.

4. Importieren Sie das Remotedesktop-Web-Client-Management-PowerShell-Modul aus dem lokalen Ordner:
    ```PowerShell
    Import-Module -Name "C:\WebClient\"
    ```

5. Die neueste Version des Remotedesktop-Webclients aus dem lokalen Ordner (ersetzen durch die entsprechenden Zip-Datei) bereitzustellen:
    ```PowerShell
    Install-RDWebClientPackage -Source "C:\WebClient\rdwebclient-1.0.1.zip"
    ```

## Herstellen einer Verbindung mit Remotedesktop-Broker ohne RD-Gateway unter WindowsServer 2019
Dieser Abschnitt beschreibt, wie Sie eine Web-Client-Verbindung mit einer RD-Broker ohne RD-Gateway in Windows Server 2019 aktivieren.

### Einrichten des Remotedesktop-Broker-Servers

#### Gehen Sie folgendermaßen vor, wenn kein Zertifikat an den Remotedesktop-Broker-Server gebunden

1. Öffnen Sie den **Server-Manager** > **Remote Desktop Services**.

2. Wählen Sie im Abschnitt **Übersicht über die Bereitstellung** im Dropdownmenü **Aufgaben** .

3. Wählen Sie **Bereitstellungseigenschaften bearbeiten**, ein neues Fenster mit dem Titel **Bereitstellungseigenschaften** wird geöffnet.

4. Wählen Sie im Fenster **Eigenschaften für die Bereitstellung** **Zertifikate** im linken Menü.

5. Wählen Sie in der Liste der Zertifikat-Ebenen **RD Connection Broker - einmaliges Anmelden aktivieren**. Sie haben zwei Optionen: (1) erstellen Sie ein neues Zertifikat oder (2) ein vorhandenes Zertifikat.

#### Gehen Sie folgendermaßen vor, wenn ein Zertifikat an den Remotedesktop-Broker-Server zuvor gebunden ist

1. Öffnen Sie das Zertifikat, das an die Broker und Kopie der **Fingerabdruck** Wert gebunden ist.

2. Um dieses Zertifikat mit dem sicheren Port 3392 binden, öffnen Sie ein PowerShell-Fenster mit erhöhten Rechten, und führen Sie folgenden Befehl ein, ersetzen **"< Fingerabdruck >"** mit dem Wert aus dem vorherigen Schritt kopiert:

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" certstorename="Remote Desktop" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > Um zu überprüfen, ob das Zertifikat ordnungsgemäß gebunden wurde, führen Sie den folgenden Befehl ein:
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > In der Liste der SSL-Zertifikat Bindungen stellen Sie sicher, dass das richtige Zertifikat an Port 3392 gebunden ist.

3. Öffnen Sie die Windows-Registrierung (Regedit) und Nagivate, ```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp``` und suchen Sie den Schlüssel **WebSocketURI**. Der Wert muss festgelegt werden, um **https://+:3392/rdp/**.

### Einrichten der RD-Sitzungshostserver
Gehen Sie folgendermaßen vor, wenn der Remotedesktop-Sitzungshostserver unterscheidet die RD-Broker-Servers:

1. Erstellen Sie ein Zertifikat für den Computer RD-Sitzungshostserver, öffnen Sie es, und kopieren Sie den **Fingerabdruck** -Wert.

2. Um dieses Zertifikat mit dem sicheren Port 3392 binden, öffnen Sie ein PowerShell-Fenster mit erhöhten Rechten, und führen Sie folgenden Befehl ein, ersetzen **"< Fingerabdruck >"** mit dem Wert aus dem vorherigen Schritt kopiert:

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > Um zu überprüfen, ob das Zertifikat ordnungsgemäß gebunden wurde, führen Sie den folgenden Befehl ein:
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > In der Liste der SSL-Zertifikat Bindungen stellen Sie sicher, dass das richtige Zertifikat an Port 3392 gebunden ist.

3. Öffnen Sie die Windows-Registrierung (Regedit) und Nagivate, ```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp``` und suchen Sie den Schlüssel **WebSocketURI**. Der Wert muss festgelegt werden, um **https://+:3392/rdp/**.

### Allgemeine Messwerte

* Stellen Sie sicher, dass die RD-Sitzungshostserver und die RD-Broker-Server Windows Server 2019 ausgeführt werden.

* Stellen Sie sicher, dass öffentliche vertrauenswürdige Zertifikate für die RD-Sitzungshostserver und die RD-Broker-Server konfiguriert sind.
    > [!NOTE]
    > Wenn sowohl die RD-Sitzungshostserver und des Remotedesktop-Broker-Servers demselben Computer gemeinsam verwenden, legen Sie das Remotedesktop-Broker-Serverzertifikat nur fest. Wenn der RD-Sitzungshostserver und RD-Broker-Server auf verschiedene Computern verwenden, müssen beide mit eindeutigen Zertifikaten konfiguriert werden.

* **Subject Alternative Name (SAN)** für jedes Zertifikat muss auf dem Computer **Vollständig qualifizierten Domänennamen (FQDN)** festgelegt werden. Die **Allgemeinen Namen (CN)** muss die SAN für jedes Zertifikat übereinstimmen.

## Problembehandlung

Wenn ein Benutzer eines der folgenden Probleme meldet, wenn den WebClient zum ersten Mal öffnen, werden in den folgenden Abschnitten was Sie tun müssen, um diese zu beheben Sie informieren.

### Was Sie tun müssen, wenn der Browser des Benutzers eine Warnung der Sicherheit zeigt, wenn sie versuchen, den-Webclient zuzugreifen

Die Rolle "Web Access für Remotedesktop" möglicherweise kein vertrauenswürdiges Zertifikat verwenden. Stellen Sie sicher, dass die Rolle "Web Access für Remotedesktop" mit einem öffentlich vertrauenswürdigen Zertifikat konfiguriert ist.

Wenn dies nicht funktioniert, möglicherweise den Servernamen im Web Client-URL nicht der vom das Zertifikat RD Web-angegebene Name übereinstimmen. Stellen Sie sicher, dass die URL den FQDN des Servers, der die Rolle "RD Web-" verwendet.

### Was Sie tun müssen, wenn der Benutzer auf eine Ressource mit dem Webclient keine Verbindung herstellen kann, obwohl sie Elemente unter alle Ressourcen sehen kann

Wenn der Benutzer meldet, dass sie keine Verbindung mit dem Webclient herstellen können, obwohl sie die aufgeführten Ressourcen sehen können, überprüfen Sie Folgendes:

* Wird die Rolle "RD-Gateway" ordnungsgemäß konfiguriert vertrauenswürdige Zertifikate mit öffentlichem?
* Verfügt der RD-Gateway-Server die erforderlichen Updates installiert? Stellen Sie sicher, dass Ihre Server installiert [die KB4025334 zu aktualisieren](https://support.microsoft.com/en-us/help/4025334/windows-10-update-kb4025334) .

Wenn der Benutzer einen Fehler "Unerwarteter Serverauthentifizierungszertifikat empfangen wurde" wird angezeigt, wenn sie versuchen, eine Verbindung herzustellen, und klicken Sie dann die Nachricht der Fingerabdruck des Zertifikats angezeigt wird. Suchen Sie den Remotedesktop-Broker-Server Zertifikat-Manager, Fingerabdruck verwenden, um das richtige Zertifikat zu suchen. Stellen Sie sicher, dass das Zertifikat konfiguriert ist, um für den Remotedesktop-Broker-Rolle auf der Eigenschaftenseite des Remotedesktop-Bereitstellung verwendet werden. Nachdem sichergestellt wird das Zertifikat abgelaufen ist, kopieren Sie das Zertifikat im CER-Format mit dem Web Access für Remotedesktop-Server, und führen Sie den folgenden Befehl auf dem Web Access für Remotedesktop-Server mit dem Klammern gesetzten Wert, der durch das Zertifikat Dateipfad ersetzt:

```PowerShell
Import-RDWebClientBrokerCert <certificate file path>
```

### Diagnostizieren von Probleme mit der Konsole-Protokoll

Wenn Sie das Problem basierend auf der Anleitung zur Problembehandlung in diesem Artikel lösen können, können Sie versuchen, auf die Quelle des Problems selbst diagnostizieren, indem Sie die Überwachung auf der Konsole melden Sie sich im Browser. Der Webclient bietet eine Methode für die Aufzeichnung der Browser-Konsole Aktivität bei der Verwendung des Webclients Probleme zu diagnostizieren.

* Wählen Sie die Auslassungspunkte in der oberen rechten Ecke, und navigieren Sie zur Seite **zu** im Dropdownmenü aus.
* Wählen Sie unter **Aufnahme Supportinformationen** die Schaltfläche **Aufzeichnung starten** .
* Führen Sie die Vorgänge im Webclient, der das Problem verursacht, die, das Sie versuchen hat, zu diagnostizieren.
* Navigieren Sie zu der Seite " **zu** ", und wählen Sie die **Aufzeichnung beenden**.
* Der Browser wird automatisch eine TXT-Datei mit dem Titel **RD-Konsole Logs.txt**herunter. Diese Datei enthält die vollständige Konsole Aktivität während der Wiedergabe des Ziel-Problems generiert.

Die Konsole kann auch direkt über den Browser zugegriffen werden. Die Konsole befindet sich in der Regel unter die Developer Tools. Sie können z. B. das Protokoll in Microsoft Edge zugreifen, durch Drücken der Taste **F12** oder durch auswählen das Schaltfläche mit den Auslassungszeichen, und navigieren zu **Weitere Tools** > **Developer Tools**.

## Erhalten Sie Hilfe mit dem Webclient

Wenn Sie ein Problem festgestellt haben, die von den Informationen in diesem Artikel gelöst werden kann, können Sie [uns eine e-Mail](mailto:rdwbclnt@microsoft.com) , um es zu melden. Sie können auch anfordern oder stimmen Sie für neue Features auf unsere [Vorschläge](https://aka.ms/rdwebfbk).