---
title: Einrichten des Remotedesktop-Webclients für Ihre Benutzer
description: Beschreibt, wie der Remotedesktop-Webclient ein Administrator einrichten kann.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 11/2/2018
ms.topic: article
author: Heidilohr
ms.localizationpriority: medium
ms.openlocfilehash: 2cb819a7f91646c61b84c3ee70550af6033ba340
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865971"
---
# <a name="set-up-the-remote-desktop-web-client-for-your-users"></a>Einrichten des Remotedesktop-Webclients für Ihre Benutzer

Der Remote Desktop WebClient ermöglicht Benutzern das Remote Desktop-Infrastruktur Ihres Unternehmens über einen kompatiblen Webbrowser zugreifen. Sie können mit remote-apps oder Desktops, wie sie mit einem lokalen PC unabhängig von deren Position interagieren. Nachdem Sie Ihre Remote Desktop WebClient eingerichtet haben, alles, was Ihre Benutzer müssen für den Einstieg ist die URL, in dem sie den Client, ihre Anmeldeinformationen und einen unterstützten Webbrowser zugreifen.

>[!IMPORTANT]
>Der Webclient unterstützt derzeit nicht mit dem Azure-Anwendungsproxy und Web Application Proxy nicht überhaupt unterstützt. Finden Sie unter [mithilfe von RDS mit anwendungsproxydienste](../rds-supported-config.md#using-remote-desktop-services-with-application-proxy-services) Details.

## <a name="what-youll-need-to-set-up-the-web-client"></a>Sie benötigen Folgendes, um die WebClient einzurichten

Beachten Sie bevor Sie beginnen die folgenden Punkte berücksichtigen:

* Stellen Sie sicher, dass Ihre [remotedesktopbereitstellung](../rds-deploy-infrastructure.md) hat ein RD-Gateway, ein Remotedesktop-Verbindungsbroker und Web Access für Remotedesktop unter Windows Server 2016 oder 2019.
* Stellen Sie sicher, dass Ihre Bereitstellung konfiguriert wurde für [pro Benutzer-Clientzugriffslizenzen](../rds-client-access-license.md) (CALs) anstelle von pro-Gerät, andernfalls alle Lizenzen verwendet werden.
* Installieren Sie die [KB4025334 für Windows 10-Update](https://support.microsoft.com/en-us/help/4025334/windows-10-update-kb4025334) auf dem RD-Gateway. Später kumulativen Updates enthält möglicherweise bereits dieser KB-Artikel.
* Stellen Sie sicher, dass öffentlich vertrauenswürdige Zertifikate für die RD-Gateway und Web Access für Remotedesktop-Rollen konfiguriert sind.
* Stellen Sie sicher, dass alle Computer, die, denen Ihre Benutzer eine Verbindung herstellen, eines der folgenden Betriebssystemversionen ausgeführt werden:
  * Windows 10
  * Windows Server 2008 R2 oder höher

Den Benutzern werden eine bessere Leistung zu verbinden, auf Windows Server 2016 (oder höher) und Windows 10 (Version 1611 oder höher) angezeigt.

>[!IMPORTANT]
>Wenn Sie den WebClient während des Vorschauzeitraums verwendet und eine Version vor 1.0.0 installiert, müssen Sie zunächst die alten Clients vor dem Wechsel zu der neuen Version deinstallieren. Wenn Sie eine Fehlermeldung erhalten, die besagt, dass "der Webclient mit einer älteren Version von RDWebClientManagement installiert wurde, und muss vor der Bereitstellung der neuen Version zuerst entfernt werden", gehen Sie wie folgt vor:
>
>1. Öffnen Sie eine PowerShell-Eingabeaufforderung mit erhöhten Rechten.
>2. Führen Sie **Uninstall-Module RDWebClientManagement** beim Deinstallieren des neuen Moduls.
>3. Schließen und Öffnen der PowerShell-Eingabeaufforderung mit erhöhten Rechten aus.
>4. Führen Sie **"Install-Module RDWebClientManagement - requiredversion" \<alte Version >, das alte Modul installieren.**
>5. Führen Sie **deinstallieren-RDWebClient** zum Deinstallieren des alten Web-Clients.
>6. Führen Sie **Uninstall-Module RDWebClientManagement** beim Deinstallieren des alten Moduls.
>7. Schließen und Öffnen der PowerShell-Eingabeaufforderung mit erhöhten Rechten aus.
>8. Gehen Sie wie folgt mit den normalen Installationsschritten.

## <a name="how-to-publish-the-remote-desktop-web-client"></a>Gewusst wie: Veröffentlichen Sie den Remotedesktop-Web-client

Um den WebClient zum ersten Mal installieren, gehen Sie folgendermaßen vor:

1. Rufen Sie das Zertifikat, das zum Herstellen von Remotedesktopverbindungen und exportieren Sie es als CER-Datei, auf dem Remotedesktop-Verbindungsbroker-Server. Kopieren Sie die CER-Datei aus dem Remotedesktop-Verbindungsbroker an den Server, auf die RD-Web-Rolle ausgeführt wird.
2. Öffnen Sie auf dem Server mit Web Access für Remotedesktop eine PowerShell-Eingabeaufforderung mit erhöhten Rechten aus.
3. Unter Windows Server 2016 aktualisiert das PowerShellGet-Modul werden, weil die Posteingang-Version nicht unterstützt, das Web Client Management-Modul installieren. Führen Sie zum Aktualisieren von PowerShellGet das folgende Cmdlet aus:
    ```PowerShell
    Install-Module -Name PowerShellGet -Force
    ```

    >[!IMPORTANT]
    >Sie müssen PowerShell neu starten, bevor das Update, andernfalls wirksam werden, die das Modul möglicherweise nicht funktioniert.

4. Installieren Sie das Remote Desktop Web Client Management-PowerShell-Modul aus dem PowerShell-Katalog mit diesem Cmdlet:
    ```PowerShell
    Install-Module -Name RDWebClientManagement
    ```

5. Führen Sie anschließend das folgende Cmdlet aus, um die neueste Version des Clients Remote Desktop Web herunterzuladen:
    ```PowerShell
    Install-RDWebClientPackage
    ```

6. Als Nächstes führen Sie dieses Cmdlet mit dem in Klammern stehenden Werte ersetzt werden, mit dem Pfad der CER-Datei, die Sie vom RD-Broker kopiert:
    ```PowerShell
    Import-RDWebClientBrokerCert <.cer file path>
    ```

7. Abschließend führen Sie dieses Cmdlet aus, um den Remotedesktopclient für Web zu veröffentlichen:
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```
    Stellen Sie sicher, Sie können den Webclient an der URL der Web-Client zugreifen, durch den Servernamen als formatierte <https://server_FQDN/RDWeb/webclient/index.html>. Es ist wichtig, den Namen des Servers verwenden, der das öffentliche Zertifikat der Web Access für Remotedesktop in der URL (in der Regel der Server FQDN) entspricht.

    >[!NOTE]
    >Bei der Ausführung der **veröffentlichen-RDWebClientPackage** -Cmdlet, möglicherweise angezeigt, eine Warnung, die pro-Geräte-Clientzugriffslizenzen besagt, werden nicht unterstützt, auch wenn für pro-Benutzer-Clientzugriffslizenzen in der Bereitstellung konfiguriert ist. Wenn die Bereitstellung pro-Benutzer-CALs verwendet, können Sie diese Warnung ignorieren. Wir zeigen, um sicherzustellen, dass Sie über die Configuration-Einschränkung sind.
8. Wenn Sie Benutzer auf die Web-Client zugreifen möchten, senden sie die Web Client-URL, die Sie erstellt haben.

>[!NOTE]
>Um eine Liste aller unterstützten Cmdlets für das Modul RDWebClientManagement anzuzeigen, führen Sie das folgende Cmdlet in PowerShell aus:
>```PowerShell
>Get-Command -Module RDWebClientManagement
>```

## <a name="how-to-update-the-remote-desktop-web-client"></a>Vorgehensweise beim Aktualisieren der Remotedesktop-Webclient

Gehen folgendermaßen Sie vor, um die Bereitstellung mit den neuen Client zu aktualisieren, wenn eine neue Version des Remote Desktop Web-Clients verfügbar ist, haben:

1. Öffnen einer PowerShell-Eingabeaufforderung mit erhöhten auf dem Web Access für Remotedesktop-Server, und führen Sie das folgende Cmdlet aus, um die neueste verfügbare Version des Webclients herunterzuladen:
    ```PowerShell
    Install-RDWebClientPackage
    ```

2. Optional können Sie den Client veröffentlichen, für Tests vor der offiziellen Freigabe durch Ausführen dieses Cmdlets:
    ```PowerShell
    Publish-RDWebClientPackage -Type Test -Latest
    ```

    Der Client sollte angezeigt werden, auf die Test-URL, die Ihre Web-Client-URL entspricht (z. B. <https://server_FQDN/RDWeb/webclient-test/index.html>).
3. Veröffentlichen Sie des Clients für Benutzer, indem Sie das folgende Cmdlet ausführen:
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```

    Dadurch wird den Client für alle Benutzer ersetzt, wenn sie die Webseite neu starten.

## <a name="how-to-uninstall-the-remote-desktop-web-client"></a>Vorgehensweise beim Deinstallieren der Remotedesktop-Webclient

Um alle Spuren des Webclients zu entfernen, gehen Sie folgendermaßen vor:

1. Öffnen Sie auf dem Server mit Web Access für Remotedesktop eine PowerShell-Eingabeaufforderung mit erhöhten Rechten aus.
2. Aufheben Sie die Test- und Produktionsumgebungen Clients, deinstallieren Sie alle lokalen Pakete und entfernen Sie die Web-Client-Einstellungen:

   ```PowerShell
   Uninstall-RDWebClient
   ```

3. Deinstallieren Sie das Remote Desktop Web Client Management-PowerShell-Modul:

   ```PowerShell
   Uninstall-Module -Name RDWebClientManagement
   ```

## <a name="how-to-install-the-remote-desktop-web-client-without-an-internet-connection"></a>Gewusst wie: Installieren des Remote Desktop Web-Clients ohne Internetverbindung

Um die Web-Client auf einem Web Access für Remotedesktop-Server bereitstellen, die über eine Internetverbindung verfügt, gehen Sie wie folgt vor.

> [!NOTE]
> Installieren, ohne eine Internetverbindung in Version 1.0.1 und höher verfügbar ist des RDWebClientManagement-PowerShell-Moduls.

> [!NOTE]
> Sie benötigen ein Admin-PC mit Internetzugriff die erforderlichen Dateien herunterzuladen, bevor sie in der offline-Server übertragen wird.

> [!NOTE]
> Der Endbenutzer-PC benötigt eine Internetverbindung jetzt. Dies wird in einer zukünftigen Version des Clients zu einem vollständigen Offlineszenario behoben werden.

### <a name="from-a-device-with-internet-access"></a>Von einem Gerät mit Zugriff auf das internet

1. Öffnen Sie eine PowerShell-Eingabeaufforderung.

2. Importieren Sie das Remote Desktop Web Client Management-PowerShell-Modul aus dem PowerShell-Katalog:
    ```PowerShell
    Import-Module -Name RDWebClientManagement
    ```

3. Laden Sie die neueste Version von Remotedesktop-Web-Client für die Installation auf einem anderen Gerät herunter:
    ```PowerShell
    Save-RDWebClientPackage "C:\WebClient\"
    ```

4. Laden Sie die neueste Version des RDWebClientManagement-PowerShell-Moduls:
    ```PowerShell
    Find-Module -Name "RDWebClientManagement" -Repository "PSGallery" | Save-Module -Path "C:\WebClient\"
    ```

5. Kopieren Sie den Inhalt von "C:\WebClient\" an den Web Access für Remotedesktop-Server.

### <a name="from-the-rd-web-access-server"></a>Aus dem Web Access für Remotedesktop-server

Befolgen Sie die Anweisungen unter [Gewusst wie: Veröffentlichen Sie den Remote Desktop WebClient](remote-desktop-web-client-admin.md#how-to-publish-the-remote-desktop-web-client), und Ersetzen Sie dabei mit den folgenden Schritten 4 und 5.

4. Importieren Sie das Remote Desktop Web Client Management-PowerShell-Modul aus dem lokalen Ordner aus:
    ```PowerShell
    Import-Module -Name "C:\WebClient\"
    ```

5. Stellen Sie die neueste Version von Remotedesktop-Web-Client aus dem lokalen Ordner (ersetzen Sie dies durch die entsprechende Zip-Datei) bereit:
    ```PowerShell
    Install-RDWebClientPackage -Source "C:\WebClient\rdwebclient-1.0.1.zip"
    ```

## <a name="connecting-to-rd-broker-without-rd-gateway-in-windows-server-2019"></a>Herstellen einer Verbindung mit RD-Broker ohne RD-Gateway unter WindowsServer 2019
Dieser Abschnitt beschreibt, wie Sie eine Verbindung zu einem Remotedesktop-Broker ohne RD-Gateway in Windows Server-2019 Client zu aktivieren.

### <a name="setting-up-the-rd-broker-server"></a>Einrichten der Remotedesktop-Verbindungsbrokerserver

#### <a name="follow-these-steps-if-there-is-no-certificate-bound-to-the-rd-broker-server"></a>Gehen Sie folgendermaßen vor, wenn kein Zertifikat auf dem Remotedesktop-Verbindungsbrokerserver gebunden ist

1. Open **Server-Manager** > **Remotedesktopdienste**.

2. In **Bereitstellungsübersicht** wählen Sie im Abschnitt der **Aufgaben** Dropdown-Menü.

3. Wählen Sie **Bereitstellungseigenschaften bearbeiten**, einem neuen Fenster mit dem Titel **Bereitstellungseigenschaften** wird geöffnet.

4. In der **Bereitstellungseigenschaften** wählen Sie im Fenster **Zertifikate** im linken Menü.

5. Wählen Sie in der Liste der Zertifikat-Ebenen, **RD-Verbindungsbroker - einmaliges Anmelden aktivieren**. Sie haben zwei Möglichkeiten: (1) erstellen Sie ein neues Zertifikat oder (2) ein vorhandenes Zertifikat.

#### <a name="follow-these-steps-if-there-is-a-certificate-previously-bound-to-the-rd-broker-server"></a>Gehen Sie folgendermaßen vor, wenn ein zuvor auf dem Remotedesktop-Verbindungsbrokerserver gebunden Zertifikat

1. Öffnen Sie das Zertifikat gebunden an den Broker und die Kopie der **Fingerabdruck** Wert.

2. Um dieses Zertifikat mit dem sicheren Port 3392 binden möchten, öffnen Sie ein PowerShell-Fenster mit erhöhten Rechten, und führen den folgenden Befehl, und Ersetzen Sie dabei **"< Fingerabdruck >"** mit dem Wert aus dem vorherigen Schritt kopiert haben:

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" certstorename="Remote Desktop" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > Um festzustellen, ob das Zertifikat ordnungsgemäß gebunden wurde, führen Sie den folgenden Befehl aus:
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > In der Liste der SSL-zertifikatbindungen stellen Sie sicher, dass das richtige Zertifikat an Port 3392 gebunden ist.

3. Öffnen Sie die Windows-Registrierung (Regedit) und Nagivate zu ```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp``` und suchen Sie den Registrierungsschlüssel **WebSocketURI**. Der Wert muss festgelegt werden, um **https://+:3392/rdp/**.

### <a name="setting-up-the-rd-session-host"></a>Einrichten der Remotedesktop-Sitzungshost
Wenn der Remotedesktop-Sitzungshostserver den Remotedesktop-Verbindungsbrokerserver unterscheidet, gehen Sie folgendermaßen vor:

1. Erstellen Sie ein Zertifikat für den RD-Sitzungshost-Computer, öffnen Sie sie aus, und kopieren Sie die **Fingerabdruck** Wert.

2. Um dieses Zertifikat mit dem sicheren Port 3392 binden möchten, öffnen Sie ein PowerShell-Fenster mit erhöhten Rechten, und führen den folgenden Befehl, und Ersetzen Sie dabei **"< Fingerabdruck >"** mit dem Wert aus dem vorherigen Schritt kopiert haben:

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > Um festzustellen, ob das Zertifikat ordnungsgemäß gebunden wurde, führen Sie den folgenden Befehl aus:
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > In der Liste der SSL-zertifikatbindungen stellen Sie sicher, dass das richtige Zertifikat an Port 3392 gebunden ist.

3. Öffnen Sie die Windows-Registrierung (Regedit) und Nagivate zu ```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp``` und suchen Sie den Registrierungsschlüssel **WebSocketURI**. Der Wert muss festgelegt werden, um **https://+:3392/rdp/**.

### <a name="general-observations"></a>Allgemeine Beobachtungen

* Stellen Sie sicher, dass dem RD-Sitzungshost und RD-Broker-Server Windows Server-2019 ausgeführt werden.

* Stellen Sie sicher, dass öffentliche vertrauenswürdiger Zertifikate für die dem Remotedesktop-Sitzungshost und RD-Broker-Server konfiguriert sind.
    > [!NOTE]
    > Wenn sowohl auf dem Remotedesktop-Sitzungshost als auch auf dem Remotedesktop-Verbindungsbrokerserver denselben Computer verwenden, legen Sie nur das RD-Broker-Serverzertifikat. Wenn der RD-Sitzungshost und RD-Broker-Server auf unterschiedliche Computern verwenden, müssen sowohl mit eindeutigen Zertifikaten konfiguriert werden.

* Die **alternativen Antragstellernamen (SAN)** für jedes Zertifikat mit des Computers festgelegt werden muss **vollständig qualifizierten Domänennamen (FQDN)**. Die **allgemeiner Name (CN)** muss mit die SAN für jedes Zertifikat übereinstimmen.

## <a name="troubleshooting"></a>Problembehandlung

Wenn ein Benutzer eines der folgenden Probleme meldet, wenn den WebClient zum ersten Mal öffnen, werden in den folgenden Abschnitten Vorgehensweise zur Behebung informieren.

### <a name="what-to-do-if-the-users-browser-shows-a-security-warning-when-they-try-to-access-the-web-client"></a>Was Sie tun, wenn der Browser des Benutzers eine sicherheitswarnung wird, wenn versucht wird, auf die Web-client

Ein vertrauenswürdiges Zertifikat möglicherweise nicht die Rolle Web Access für Remotedesktop verwenden. Stellen Sie sicher, dass die Rolle Web Access für Remotedesktop mit einem öffentlich vertrauenswürdiges Zertifikat konfiguriert ist.

Wenn dies nicht funktioniert, den Servernamen in der Web Client-URL entsprechen möglicherweise nicht den Namen, die über das RD-Web-Zertifikat bereitgestellt. Stellen Sie sicher, dass Ihre URL den vollqualifizierten Domänennamen des Servers mit der RD-Web-Rolle verwendet.

### <a name="what-to-do-if-the-user-cant-connect-to-a-resource-with-the-web-client-even-though-they-can-see-the-items-under-all-resources"></a>Was Sie tun, wenn der Benutzer auf eine Ressource mit dem Webclient keine Verbindung herstellen kann, obwohl sie die Elemente unter alle Ressourcen anzeigen können

Wenn der Benutzer meldet, dass sie keine Verbindung mit dem Webclient herstellen können, auch, wenn sie die aufgeführten Ressourcen sehen können, überprüfen Sie die folgenden Schritte aus:

* Ist die Rolle von RD-Gateway ordnungsgemäß konfiguriert ein öffentliches vertrauenswürdiges Zertifikat?
* Weist der RD-Gateway-Server die erforderlichen Updates installiert? Stellen Sie sicher, dass der Server besitzt [das Update KB4025334](https://support.microsoft.com/en-us/help/4025334/windows-10-update-kb4025334) installiert.

Wenn der Benutzer einen Fehler "unerwartetes CMG-Serverauthentifizierungszertifikat wurde empfangen." angezeigt wird, wenn sie versuchen, eine Verbindung herstellen, und klicken Sie dann die Nachricht den Fingerabdruck des Zertifikats angezeigt wird. Suchen Sie die Remotedesktop-Verbindungsbrokerserver Zertifikat-Manager, die mithilfe dieses Fingerabdrucks an das richtige Zertifikat gefunden. Stellen Sie sicher, dass das Zertifikat konfiguriert ist, für die RD-Broker-Rolle auf der Eigenschaftenseite des Remotedesktop-Bereitstellung verwendet werden soll. Nach dem nicht sichergestellt wird das Zertifikat abgelaufen ist, kopieren Sie das Zertifikat im CER-Dateiformat mit dem Web Access für Remotedesktop-Server, und führen Sie den folgenden Befehl auf dem Web Access für Remotedesktop-Server, mit der in Klammern stehenden Werte durch die zertifikatdateipfad ersetzt:

```PowerShell
Import-RDWebClientBrokerCert <certificate file path>
```

### <a name="diagnose-issues-with-the-console-log"></a>Diagnose von Problemen mit das Konsolenprotokoll

Wenn Sie das Problem anhand der Anweisungen in diesem Artikel zur Problembehandlung lösen können, Sie können versuchen, die Ursache des Problems kennen die Konsole, indem Sie selbst zu diagnostizieren im Browser anmelden. Der Webclient bietet es sich um eine Methode für die Aufzeichnung der Protokollaktivität für Browser-Konsole bei der Verwendung des Webclients an, um Probleme zu diagnostizieren.

* Wählen Sie in der oberen rechten Ecke die Auslassungspunkte, und navigieren Sie zu der **zu** Seite in der Dropdown-Menü.
* Klicken Sie unter **Capture Supportinformationen** wählen Sie die **Aufzeichnung starten** Schaltfläche.
* Führen Sie die Vorgänge in der Webclient, der das Problem, die, das Sie versuchen erzeugt, zu diagnostizieren.
* Navigieren Sie zu der **zu** Seite und wählen Sie **Aufzeichnung beenden**.
* Ihr Browser wird automatisch herunterladen, eine TXT-Datei mit dem Titel **RD-Konsole "Logs.txt"**. Diese Datei enthält die vollständige Console Log-Aktivität, die beim Reproduzieren des Problems Ziel generiert.

Die Konsole kann auch direkt über Ihren Browser zugegriffen werden. Die Konsole befindet sich im Allgemeinen unter der Entwicklertools. Sie können z. B. das Protokoll in Microsoft Edge zugreifen, durch Drücken der **F12** Taste, oder indem Sie auf die Auslassungspunkte, und dann weiter navigieren **mehr Tools** > **Entwicklertools**.

## <a name="get-help-with-the-web-client"></a>Hilfe bei der WebClient

Wenn Sie ein Problem aufgetreten ist, die von den Informationen in diesem Artikel nicht gelöst werden kann, können Sie [e-Mail](mailto:rdwbclnt@microsoft.com) zu melden. Sie können auch anfordern, oder stimmen Sie für die neuen Funktionen finden unsere [Vorschläge](https://aka.ms/rdwebfbk).