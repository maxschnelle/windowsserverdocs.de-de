---
title: Einrichten des Remotedesktop-Webclients für Ihre Benutzer
description: In diesem Artikel wird beschrieben, wie ein Administrator den Remotedesktop-Webclient einrichten kann.
ms.author: helohr
ms.date: 09/19/2019
ms.topic: article
author: Heidilohr
ms.localizationpriority: medium
ms.openlocfilehash: 33d3bf9c27f9e504594823c7868140147164593d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971627"
---
# <a name="set-up-the-remote-desktop-web-client-for-your-users"></a>Einrichten des Remotedesktop-Webclients für Ihre Benutzer

Mit dem Remotedesktop-Webclient können Benutzer über einen kompatiblen Webbrowser auf die Remotedesktopinfrastruktur Ihrer Organisation zugreifen. Die Benutzer können unabhängig von ihrem jeweiligen Standort mit Remote-Apps oder Remotedesktops so interagieren wie mit einem lokalen PC. Nachdem Sie Ihren Remotedesktop-Webclient eingerichtet haben, benötigen Ihre Benutzer für den Einstieg nur die URL, über die sie auf den Client zugreifen können, ihre Anmeldeinformationen und einen unterstützten Webbrowser.

>[!IMPORTANT]
>Der Webclient bietet Unterstützung für den Azure AD-Anwendungsproxy aber keine Unterstützung für den Webanwendungsproxy. Weitere Informationen finden Sie unter [Verwenden von Remotedesktopdiensten mit Anwendungsproxydiensten](../rds-supported-config.md#using-remote-desktop-services-with-application-proxy-services).

## <a name="what-youll-need-to-set-up-the-web-client"></a>Voraussetzungen für das Einrichten des Webclients

Beachten Sie vor dem Ausführen der ersten Schritte die folgenden Punkte:

* Stellen Sie sicher, dass Ihre [Remotedesktopbereitstellung](../rds-deploy-infrastructure.md) ein Remotedesktopgateway, einen Remotedesktop-Verbindungsbroker und eine Komponente mit Web Access für Remotedesktop unter Windows Server 2016 oder 2019 umfasst.
* Stellen Sie sicher, dass Ihre Bereitstellung für [Clientzugriffslizenzen](../rds-client-access-license.md) (Client Access Licenses, CALs) vom Typ „Pro Benutzer“ (und nicht vom Typ „Pro Gerät“) konfiguriert ist. Andernfalls werden alle Lizenzen verwendet.
* Installieren Sie das [Windows 10-Update KB4025334](https://support.microsoft.com/help/4025334/windows-10-update-kb4025334) auf dem RD-Gateway. Spätere kumulative Updates enthalten möglicherweise bereits diese KB-Version.
* Stellen Sie sicher, dass öffentliche vertrauenswürdige Zertifikate für die Rollen „RD-Gateway“ und „Web Access für Remotedesktop“ konfiguriert sind.
* Stellen Sie sicher, dass alle Computer, mit denen Ihre Benutzer eine Verbindung herstellen, unter einer der folgenden Betriebssystemversionen ausgeführt werden:
  * Windows 10
  * Windows Server 2008 R2 oder höher

Die Benutzer können eine bessere Leistung verzeichnen, wenn die Verbindung mit Windows Server 2016 (oder höher) und Windows 10 (Version 1611 oder höher) hergestellt wird.

>[!IMPORTANT]
>Wenn Sie den Webclient während des Vorschauzeitraums verwendet und eine Version vor 1.0.0 installiert haben, müssen Sie zuerst den alten Client deinstallieren, bevor Sie auf die neue Version umsteigen. Wenn Sie eine Fehlermeldung erhalten, die besagt, dass der Webclient mit einer älteren Version von RDWebClientManagement installiert wurde und vor der Bereitstellung der neuen Version entfernt werden muss, führen Sie die folgenden Schritte aus:
>
>1. Öffnen Sie eine PowerShell-Eingabeaufforderung mit erhöhten Rechten.
>2. Führen Sie **Uninstall-Module RDWebClientManagement** aus, um das neue Modul zu deinstallieren.
>3. Schließen Sie die PowerShell-Eingabeaufforderung mit erhöhten Rechten, und öffnen Sie sie erneut.
>4. Führen Sie **Install-Module RDWebClientManagement -RequiredVersion \<old version> aus, um das alte Modul zu installieren.**
>5. Führen Sie **Uninstall-RDWebClient** aus, um den alten Webclient zu deinstallieren.
>6. Führen Sie **Uninstall-Module RDWebClientManagement** aus, um das alte Modul zu deinstallieren.
>7. Schließen Sie die PowerShell-Eingabeaufforderung mit erhöhten Rechten, und öffnen Sie sie erneut.
>8. Fahren Sie wie folgt mit den normalen Installationsschritten fort.

## <a name="how-to-publish-the-remote-desktop-web-client"></a>Veröffentlichen des Remotedesktop-Webclients

Um den Webclient zum ersten Mal zu installieren, führen Sie die folgenden Schritte aus:

1. Rufen Sie auf dem Remotedesktop-Verbindungsbrokerserver das für Remotedesktopverbindungen verwendete Zertifikat ab, und exportieren Sie es als CER-Datei. Kopieren Sie die CER-Datei vom Remotedesktop-Verbindungsbroker auf den Server, auf dem die Rolle „Web Access für Remotedesktop“ ausgeführt wird.
2. Öffnen Sie auf dem Server mit Web Access für Remotedesktop eine PowerShell-Eingabeaufforderung mit erhöhten Rechten.
3. Aktualisieren Sie unter Windows Server 2016 das PowerShellGet-Modul, weil die mitgelieferte Version die Installation des Webclient-Verwaltungsmoduls nicht unterstützt. Führen Sie zum Aktualisieren von PowerShellGet das folgende Cmdlet aus:
    ```PowerShell
    Install-Module -Name PowerShellGet -Force
    ```

    >[!IMPORTANT]
    >Sie müssen PowerShell neu starten, damit die Aktualisierung wirksam wird. Andernfalls funktioniert das Modul möglicherweise nicht.

4. Installieren Sie das PowerShell-Modul für die Remotedesktop-Webclientverwaltung (RDWebClientManagement) aus dem PowerShell-Katalog mit dem folgenden Cmdlet:
    ```PowerShell
    Install-Module -Name RDWebClientManagement
    ```

5. Führen Sie danach das folgende Cmdlet aus, um die aktuelle Version des Remotedesktop-Webclients herunterzuladen:
    ```PowerShell
    Install-RDWebClientPackage
    ```

6. Führen Sie als Nächstes das folgende Cmdlet aus, wobei Sie den in Klammern stehenden Wert durch den Pfad der CER-Datei ersetzen, die Sie vom Remotedesktop-Verbindungsbroker kopiert haben:
    ```PowerShell
    Import-RDWebClientBrokerCert <.cer file path>
    ```

7. Führen Sie abschließend das folgende Cmdlet aus, um den Remotedesktop-Webclient zu veröffentlichen:
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```
    Stellen Sie sicher, dass Sie unter der Webclient-URL mit dem Servernamen im Format <https://server_FQDN/RDWeb/webclient/index.html> auf den Webclient zugreifen können. Es ist wichtig, den Servernamen zu verwenden, der dem öffentlichen Zertifikat von Web Access für Remotedesktop in der URL entspricht (das ist in der Regel der FQDN des Servers).

    >[!NOTE]
    >Beim Ausführen des Cmdlets **Publish-RDWebClientPackage** wird möglicherweise eine Warnmeldung angezeigt, die besagt, dass CALs vom Typ „Pro Gerät“ nicht unterstützt werden, obwohl Ihre Bereitstellung für CALs vom Typ „Pro Benutzer“ konfiguriert ist. Wenn Ihre Bereitstellung CALs vom Typ „Pro Benutzer“ verwendet, können Sie diese Warnung ignorieren. Die Warnung wird angezeigt, um sicherzustellen, dass Sie sich der Konfigurationseinschränkung bewusst sind.
8. Wenn Sie so weit sind, dass die Benutzer auf den Webclient zugreifen können, senden Sie Ihnen einfach die von Ihnen erstellte Webclient-URL.

>[!NOTE]
>Wenn Sie eine Liste aller unterstützten Cmdlets für das Modul „RDWebClientManagement“ anzeigen möchten, führen Sie in PowerShell das folgende Cmdlet aus:
>```PowerShell
>Get-Command -Module RDWebClientManagement
>```

## <a name="how-to-update-the-remote-desktop-web-client"></a>Aktualisieren des Remotedesktop-Webclients

Wenn eine neue Version des Remotedesktop-Webclients verfügbar ist, führen Sie die folgenden Schritte aus, um die Bereitstellung mit dem neuen Client zu aktualisieren:

1. Öffnen Sie auf dem Server mit Web Access für Remotedesktop eine PowerShell-Eingabeaufforderung mit erhöhten Rechten, und führen Sie das folgende Cmdlet aus, um die neueste verfügbare Version des Webclients herunterzuladen:
    ```PowerShell
    Install-RDWebClientPackage
    ```

2. Optional können Sie den Client zu Testzwecken vor der offiziellen Freigabe veröffentlichen, indem Sie das folgende Cmdlet ausführen:
    ```PowerShell
    Publish-RDWebClientPackage -Type Test -Latest
    ```

    Der Client sollte in der Test-URL angezeigt werden, die Ihrer Webclient-URL entspricht (Beispiel: <https://server_FQDN/RDWeb/webclient-test/index.html>).
3. Veröffentlichen Sie den Client für Benutzer, indem Sie das folgende Cmdlet ausführen:
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```

    Dadurch wird der Client für alle Benutzer ersetzt, wenn sie die Webseite neu starten.

## <a name="how-to-uninstall-the-remote-desktop-web-client"></a>Deinstallieren des Remotedesktop-Webclients

Führen Sie die folgenden Schritte aus, um alle Spuren des Webclients zu entfernen:

1. Öffnen Sie auf dem Server mit Web Access für Remotedesktop eine PowerShell-Eingabeaufforderung mit erhöhten Rechten.
2. Heben Sie die Veröffentlichung der Test- und Produktionsclients auf, deinstallieren Sie alle lokalen Pakete, und entfernen Sie die Webclienteinstellungen:

   ```PowerShell
   Uninstall-RDWebClient
   ```

3. Deinstallieren Sie das PowerShell-Modul für die Remotedesktop-Webclientverwaltung:

   ```PowerShell
   Uninstall-Module -Name RDWebClientManagement
   ```

## <a name="how-to-install-the-remote-desktop-web-client-without-an-internet-connection"></a>Installieren des Remotedesktop-Webclients ohne Internetverbindung

Führen Sie die folgenden Schritte aus, um den Webclient auf einem Server mit Web Access für Remotedesktop bereitzustellen, der nicht über eine Internetverbindung verfügt.

> [!NOTE]
> Die Option der Installation ohne Internetverbindung ist in Version 1.0.1 (und höher) des PowerShell-Moduls „RDWebClientManagement“ verfügbar.

> [!NOTE]
> Sie benötigen jedoch einen Administrator-PC mit Internetzugang, um die erforderlichen Dateien herunterzuladen, bevor sie an den Offlineserver übertragen werden.

> [!NOTE]
> Der Endbenutzer-PC benötigt vorerst eine Internetverbindung. Dies wird in einer zukünftigen Version des Clients gelöst, um ein vollständiges Offlineszenario zu ermöglichen.

### <a name="from-a-device-with-internet-access"></a>Auf einem Gerät mit Internetzugang

1. Öffnen Sie eine PowerShell-Eingabeaufforderung.

2. Importieren Sie das PowerShell-Modul für die Remotedesktop-Webclientverwaltung aus dem PowerShell-Katalog:
    ```PowerShell
    Import-Module -Name RDWebClientManagement
    ```

3. Laden Sie die aktuelle Version des Remotedesktop-Webclients zur Installation auf einem anderen Gerät herunter:
    ```PowerShell
    Save-RDWebClientPackage "C:\WebClient\"
    ```

4. Laden Sie die aktuelle Version des PowerShell-Moduls „RDWebClientManagement“ herunter:
    ```PowerShell
    Find-Module -Name "RDWebClientManagement" -Repository "PSGallery" | Save-Module -Path "C:\WebClient\"
    ```

5. Kopieren Sie den Inhalt des Verzeichnisses „C:\WebClient\" auf den Server mit Web Access für Remotedesktop.

### <a name="from-the-rd-web-access-server"></a>Auf dem Server mit Web Access für Remotedesktop

Folgen Sie den Anweisungen unter [Veröffentlichen des Remotedesktop-Webclients](remote-desktop-web-client-admin.md#how-to-publish-the-remote-desktop-web-client), und ersetzen Sie dabei die Schritte 4 und 5 durch die folgenden Schritte.

4. Du hast zwei Möglichkeiten, das neueste PowerShell-Modul für die Webclientverwaltung abzurufen:
    - Importiere das PowerShell-Modul für die Remotedesktop-Webclientverwaltung:
      ```PowerShell
      Import-Module -Name RDWebClientManagement
      ```
    - Kopiere den heruntergeladenen Ordner „RDWebClientManagement“ in einen der lokalen PowerShell-Modulordner, die unter **$env:psmodulePath** aufgeführt sind, oder füge den Pfad zu dem Ordner mit den heruntergeladenen Dateien dem **$env:psmodulePath** hinzu.

5. Stellen Sie die aktuelle Version des Remotedesktop-Webclients aus dem lokalen Ordner bereit (ersetzen Sie dabei die Angabe durch die entsprechende ZIP-Datei):
    ```PowerShell
    Install-RDWebClientPackage -Source "C:\WebClient\rdwebclient-1.0.1.zip"
    ```

## <a name="connecting-to-rd-broker-without-rd-gateway-in-windows-server-2019"></a>Herstellen einer Verbindung mit dem RD-Broker ohne RD-Gateway in Windows Server 2019
In diesem Abschnitt wird beschrieben, wie Sie eine Webclientverbindung mit einem Remotedesktop-Verbindungsbroker ohne RD-Gateway in Windows Server 2019 aktivieren.

### <a name="setting-up-the-rd-broker-server"></a>Einrichten des Remotedesktop-Verbindungsbrokerservers

#### <a name="follow-these-steps-if-there-is-no-certificate-bound-to-the-rd-broker-server"></a>Führen Sie die folgenden Schritte aus, wenn kein Zertifikat an den Remotedesktop-Verbindungsbrokerserver gebunden ist:

1. Öffnen Sie **Server-Manager** > **Remotedesktopdienste**.

2. Wählen Sie im Abschnitt **Bereitstellungsübersicht** das Dropdownmenü **Aufgaben** aus.

3. Wählen Sie **Bereitstellungseigenschaften bearbeiten** aus. Daraufhin wird ein neues Fenster mit dem Titel **Bereitstellungseigenschaften** geöffnet.

4. Wählen Sie im Fenster **Bereitstellungseigenschaften** im linken Menü die Option **Zertifikate** aus.

5. Wählen Sie in der Liste der Zertifikatsstufen den Eintrag **Remotedesktop-Verbindungsbroker – einmaliges Anmelden aktivieren** aus. Sie haben zwei Möglichkeiten: (1) Sie können ein neues Zertifikat erstellen oder (2) ein vorhandenes Zertifikat auswählen.

#### <a name="follow-these-steps-if-there-is-a-certificate-previously-bound-to-the-rd-broker-server"></a>Führen Sie die folgenden Schritte aus, wenn ein zuvor an den Remotedesktop-Verbindungsbrokerserver gebundenes Zertifikat vorhanden ist:

1. Öffnen Sie das an den Verbindungsbroker gebundene Zertifikat, und kopieren Sie den **Fingerabdruckwert**.

2. Um dieses Zertifikat an den sicheren Port 3392 zu binden, öffnen Sie ein PowerShell-Fenster mit erhöhten Rechten, und führen Sie den folgenden Befehl aus, wobei Sie **"<Fingerabdruck>"** durch den Wert ersetzen, den Sie im vorherigen Schritt kopiert haben:

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" certstorename="Remote Desktop" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > Wenn Sie überprüfen möchten, ob das Zertifikat ordnungsgemäß gebunden wurde, führen Sie den folgenden Befehl aus:
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > Vergewissern Sie sich, dass in der Liste der SSL-Zertifikatbindungen das richtige Zertifikat an Port 3392 gebunden ist.

3. Öffnen Sie die Windows-Registrierung (regedit), navigieren Sie zu ```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp```, und suchen Sie nach dem Schlüssel **WebSocketURI**. Der Wert muss auf <strong>https://+:3392/rdp/</strong> festgelegt sein.

### <a name="setting-up-the-rd-session-host"></a>Einrichten des Remotedesktop-Sitzungshosts
Führen Sie die folgenden Schritte aus, wenn sich der Remotedesktop-Sitzungshostserver vom Remotedesktop-Verbindungsbrokerserver unterscheidet:

1. Erstellen Sie ein Zertifikat für den Remotedesktop-Sitzungshostcomputer, öffnen Sie es, und kopieren Sie den **Fingerabdruckwert**.

2. Um dieses Zertifikat an den sicheren Port 3392 zu binden, öffnen Sie ein PowerShell-Fenster mit erhöhten Rechten, und führen Sie den folgenden Befehl aus, wobei Sie **"<Fingerabdruck>"** durch den Wert ersetzen, den Sie im vorherigen Schritt kopiert haben:

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > Wenn Sie überprüfen möchten, ob das Zertifikat ordnungsgemäß gebunden wurde, führen Sie den folgenden Befehl aus:
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > Vergewissern Sie sich, dass in der Liste der SSL-Zertifikatbindungen das richtige Zertifikat an Port 3392 gebunden ist.

3. Öffnen Sie die Windows-Registrierung (regedit), navigieren Sie zu ```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp```, und suchen Sie nach dem Schlüssel **WebSocketURI**. Der Wert muss auf <https://+:3392/rdp/> festgelegt sein.

### <a name="general-observations"></a>Allgemeine Hinweise

* Stellen Sie sicher, dass der Remotedesktop-Sitzungshostserver und der Remotedesktop-Verbindungsbrokerserver unter Windows Server 2019 ausgeführt werden.

* Stellen Sie sicher, dass öffentliche vertrauenswürdige Zertifikate sowohl für den RD-Sitzungshostserver als auch für den RD-Verbindungsbrokerserver konfiguriert sind.
    > [!NOTE]
    > Wenn der RD-Sitzungshostserver und der RD-Verbindungsbrokerserver denselben Computer verwenden, legen Sie nur das Zertifikat des RD-Verbindungsbrokerservers fest. Wenn der RD-Sitzungshostserver und der RD-Verbindungsbrokerserver unterschiedliche Computer verwenden, müssen für beide Server eindeutige Zertifikate konfiguriert werden.

* Der **alternative Antragstellername** (Subject Alternative Name, SAN) für jedes Zertifikat muss auf den **vollqualifizierten Domänennamen** (Fully Qualified Domain Name, FQDN) des Computers festgelegt werden. Der **allgemeine Name** (Common Name, CN) muss dem alternativen Antragstellernamen entsprechen.

## <a name="how-to-pre-configure-settings-for-remote-desktop-web-client-users"></a>Vorkonfigurieren von Einstellungen für Benutzer des Remotedesktop-Webclients
In diesem Abschnitt wird beschrieben, wie Sie die Einstellungen für Ihre Remotedesktop-Webclientbereitstellung mithilfe von PowerShell konfigurieren. Mit diesen PowerShell-Cmdlets wird die Fähigkeit eines Benutzers zum Ändern von Einstellungen basierend auf den Sicherheitsaspekten Ihrer Organisation oder dem vorgesehenen Workflow gesteuert. Die folgenden Einstellungen befinden sich auf der Seitenleiste **Einstellungen** des Webclients.

### <a name="suppress-telemetry"></a>Unterdrücken von Telemetriedaten
Standardmäßig können Benutzer auswählen, ob die Erfassung der an Microsoft gesendeten Telemetriedaten aktiviert oder deaktiviert werden soll. Informationen zu den von Microsoft erfassten Telemetriedaten finden Sie in unserer Datenschutzerklärung, auf die Sie über den Link auf der Seitenleiste **Info** zugreifen können.

Als Administrator können Sie die Telemetriedatenerfassung für Ihre Bereitstellung mit dem folgenden PowerShell-Cmdlet unterdrücken:

   ```PowerShell
    Set-RDWebClientDeploymentSetting -Name "SuppressTelemetry" $true
   ```

Standardmäßig kann der Benutzer auswählen, ob die Option für Telemetriedaten aktiviert oder deaktiviert werden soll. Der boolesche Wert **$false** entspricht dem Standardverhalten des Clients. Der boolesche Wert **$true** deaktiviert die Option für Telemetriedaten und verhindert, dass der Benutzer diese aktivieren kann.

### <a name="remote-resource-launch-method"></a>Methode zum Starten von Remoteressourcen

>[!NOTE]
>Diese Einstellung funktioniert zurzeit nur mit dem RDS-Webclient, nicht mit dem Windows Virtual Desktop-Webclient.

Standardmäßig können Benutzer auswählen, ob Remoteressourcen (1) im Browser oder (2) durch Herunterladen einer RDP-Datei zur Bearbeitung mit einem anderen auf dem Computer installierten Client gestartet werden sollen. Als Administrator können Sie die Methode zum Starten von Remoteressourcen für Ihre Bereitstellung mit dem folgenden PowerShell-Befehl einschränken:

   ```PowerShell
    Set-RDWebClientDeploymentSetting -Name "LaunchResourceInBrowser" ($true|$false)
   ```
 Standardmäßig kann der Benutzer eine der Startmethoden auswählen. Der boolesche Wert **$true** zwingt den Benutzer, die Ressourcen im Browser zu starten. Der boolesche Wert **$false** zwingt den Benutzer, die Ressourcen durch Herunterladen einer RDP-Datei zur Bearbeitung mit einem lokal installierten RDP-Client zu starten.

### <a name="reset-rdwebclientdeploymentsetting-configurations-to-default"></a>Zurücksetzen der RDWebClientDeploymentSetting-Konfigurationen auf die Standardwerte

Um eine Webclienteinstellung auf Bereitstellungsebene auf die Standardkonfiguration zurückzusetzen, führe das folgende PowerShell-Cmdlet aus, und gib mit dem Parameter „-name“ die Einstellung an, die du zurücksetzen möchtest:

   ```PowerShell
    Reset-RDWebClientDeploymentSetting -Name "LaunchResourceInBrowser"
    Reset-RDWebClientDeploymentSetting -Name "SuppressTelemetry"
   ```

## <a name="troubleshooting"></a>Problembehandlung

Wenn ein Benutzer meldet, dass beim ersten Öffnen des Webclients eines der folgenden Probleme auftritt, lesen Sie die folgenden Abschnitte, um zu erfahren, was zu tun ist, um diese Probleme zu beheben.

### <a name="what-to-do-if-the-users-browser-shows-a-security-warning-when-they-try-to-access-the-web-client"></a>Was zu tun ist, wenn im Browser des Benutzers beim Versuch, auf den Webclient zuzugreifen, eine Sicherheitswarnung angezeigt wird

Die Rolle „Web Access für Remotedesktop“ verwendet möglicherweise kein vertrauenswürdiges Zertifikat. Stellen Sie sicher, dass die Rolle „Web Access für Remotedesktop“ mit einem öffentlich vertrauenswürdigen Zertifikat konfiguriert ist.

Wenn das nicht funktioniert, stimmt der Servername in der Webclient-URL möglicherweise nicht mit dem Namen überein, der vom Zertifikat für Web Access für Remotedesktop angegeben wurde. Stellen Sie sicher, dass in Ihrer URL der FQDN des Servers verwendet wird, auf dem die Rolle „Web Access für Remotedesktop“ gehostet wird.

### <a name="what-to-do-if-the-user-cant-connect-to-a-resource-with-the-web-client-even-though-they-can-see-the-items-under-all-resources"></a>Was zu tun ist, wenn der Benutzer mit dem Webclient keine Verbindung mit einer Ressource herstellen kann, obwohl die Elemente unter „Alle Ressourcen“ angezeigt werden

Wenn der Benutzer meldet, dass er keine Verbindung mit dem Webclient herstellen kann, obwohl er die aufgeführten Ressourcen sehen kann, überprüfen Sie die folgenden Punkte:

* Ist die Rolle „RD-Gateway“ ordnungsgemäß für die Verwendung eines öffentlichen vertrauenswürdigen Zertifikats konfiguriert?
* Sind auf dem RD-Gatewayserver die erforderlichen Updates installiert? Stellen Sie sicher, dass das [Update KB4025334](https://support.microsoft.com/help/4025334/windows-10-update-kb4025334) auf dem Server installiert ist.

Wenn der Benutzer beim Versuch, eine Verbindung herzustellen, eine Fehlermeldung erhält, die besagt, dass ein unerwartetes Serverauthentifizierungszertifikat empfangen wurde, wird in der Meldung der Fingerabdruck des Zertifikats angezeigt. Durchsuchen Sie den Zertifikat-Manager des Remotedesktop-Verbindungsbrokerservers anhand dieses Fingerabdrucks, um das richtige Zertifikat zu finden. Vergewissern Sie sich auf der Seite mit den Remotedesktop-Bereitstellungseigenschaften, dass das Zertifikat für die Rolle „Remotedesktop-Verbindungsbroker“ konfiguriert ist. Nachdem Sie sichergestellt haben, dass das Zertifikat nicht abgelaufen ist, können Sie das Zertifikat im CER-Dateiformat auf den Server mit Web Access für Remotedesktop kopieren und auf dem Server mit Web Access für Remotedesktop den folgenden Befehl ausführen, wobei Sie den in Klammern stehenden Wert durch den Pfad der Zertifikatdatei ersetzen:

```PowerShell
Import-RDWebClientBrokerCert <certificate file path>
```

### <a name="diagnose-issues-with-the-console-log"></a>Diagnostizieren von Problemen mit dem Konsolenprotokoll

Wenn Sie das Problem nicht anhand der in diesem Artikel aufgeführten Anweisungen zur Problembehandlung lösen können, versuchen Sie, die Ursache des Problems selbst zu ermitteln, indem Sie sich das Konsolenprotokoll im Browser ansehen. Der Webclient bietet eine Methode zum Aufzeichnen der Browser-Konsolenprotokollaktivität, während der Webclient zum Diagnostizieren von Problemen verwendet wird.

* Wählen Sie in der oberen rechten Ecke die Auslassungspunkte aus, und navigieren Sie im Dropdownmenü zur Seite **Info**.
* Wählen Sie unter **Supportinformationen erfassen** die Schaltfläche **Aufzeichnung starten** aus.
* Führen Sie im Webclient die Vorgänge aus, die das Problem verursacht haben, das Sie diagnostizieren möchten.
* Navigieren Sie zur Seite **Info**, und wählen Sie **Aufzeichnung beenden** aus.
* Ihr Browser lädt automatisch eine TXT-Datei mit dem Namen **RD Console Logs.txt** herunter. Diese Datei enthält die vollständige Konsolenprotokollaktivität, die beim Reproduzieren des Zielproblems generiert wurde.

Sie können auch über Ihren Browser direkt auf die Konsole zugreifen. Die Konsole befindet sich im Allgemeinen unter den Entwicklertools. Beispielsweise können Sie in Microsoft Edge auf das Protokoll zugreifen, indem Sie entweder die **F12**-Taste drücken oder die Auslassungspunkte auswählen und dann zu **Weitere Tools** > **Entwicklertools** navigieren.

## <a name="get-help-with-the-web-client"></a>Anfordern von Hilfe zum Webclient

Wenn ein Problem aufgetreten ist, das nicht anhand der in diesem Artikel enthaltenen Informationen gelöst werden kann, können Sie es der [Tech-Community](https://aka.ms/wvdtc) melden. Sie können auch auf unserer [Suggestion Box](https://remotedesktop.uservoice.com/forums/911494-remote-desktop-web-client)-Seite neue Features vorschlagen oder über neue Features abstimmen.
