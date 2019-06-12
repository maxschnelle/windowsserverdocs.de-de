---
title: Windows Admin Center – bekannte Probleme
description: Windows Admin Center – bekannte Probleme (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 06/07/2019
ms.openlocfilehash: e7cf6fc6a4fae2eee76409bd6af4ef2ff6ed35a3
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811778"
---
# <a name="windows-admin-center-known-issues"></a>Windows Admin Center – bekannte Probleme

> Gilt für: Windows Admin Center, Windows Admin Center Preview

Wenn Sie ein Problem haben, das auf dieser Seite nicht beschrieben ist, bitte [Teilen Sie uns dies mit](http://aka.ms/WACfeedback).

## <a name="lenovo-xclarity-integrator"></a>Lenovo XClarity Integrator

Das zuvor offengelegte Inkompatibilitätsproblem Windows Admin Center Version 1904 und Lenovo XClarity Integrator-Erweiterung ist jetzt mit Windows Admin Center Version 1904.1 behoben. Es wird dringend empfohlen, dass Sie auf die neueste unterstützte Version von Windows Admin Center aktualisieren.

- Lenovo XClarity Integrator-Erweiterung, Version 1.1 ist vollständig kompatibel mit Windows Admin Center 1904.1. Es wird dringend empfohlen, auf die neueste Version von Windows Admin Center und die Lenovo-Erweiterung zu aktualisieren.
- Aus irgendeinem Grund Wenn Sie weiterhin Windows Admin Center 1809.5 für die Zeit wird müssen, können Sie XClarity Integrator 1.0.4 verwenden, die auch verfügbar in den Feed zu Windows Admin Center Erweiterung bis Windows Admin Center 1809.5 nicht mehr basierend unterstützt wird auf unsere [Supportrichtlinie](../support/index.md).

## <a name="installer"></a>Installer

- Beim Installieren von Windows Admin Center mit einem eigenen Zertifikat, wenn Sie den Fingerabdruck aus dem Zertifikat-Manager-MMC-Tool kopieren, [enthält dieser ein ungültiges Zeichen am Anfang.](https://support.microsoft.com/help/2023835/certificate-thumbprint-displayed-in-mmc-certificate-snap-in-has-extra) Um dieses Problem zu umgehen, geben Sie das erste Zeichen des Fingerabdrucks ein und kopieren Sie den Rest.

- Über Port unter 1024 wird nicht unterstützt. Im Modus "Dienst" können Sie optional Port 80 an den angegebenen Port umleiten konfigurieren.

- Wenn der Windows Update-Dienst (Wuauserv) wurde beendet und deaktiviert ist, wird das Installationsprogramm fehl. [19100629]

### <a name="upgrade"></a>Upgrade/Aktualisieren

- Wenn Windows Admin Center im Modus "Dienst" von einer früheren Version zu aktualisieren, wenn Sie Msiexec im stillen Modus verwenden, können Fehler auftreten, in dem die eingehende Firewallregel für den Port für Windows Admin Center gelöscht wird.
  - Erstellen Sie die Regel neu, führen Sie den folgenden Befehl aus einer PowerShell-Konsole mit erhöhten Rechten, und Ersetzen Sie dabei \<Port > mit dem Port konfiguriert werden, für die Windows Admin Center (standardmäßig 443).

    ```powershell
    New-NetFirewallRule -DisplayName "SmeInboundOpenException" -Description "Windows Admin Center inbound port exception" -LocalPort <port> -RemoteAddress Any -Protocol TCP
    ```

## <a name="general"></a>Allgemein

- Wenn Sie Windows Admin Center auf als Gateway installiert haben **Windows Server 2016** stark ausgelastet, der Dienst stürzt möglicherweise ab, mit einem Fehler im Ereignisprotokoll, die enthält ```Faulting application name: sme.exe``` und ```Faulting module name: WsmSvc.dll```. Dies ist aufgrund eines Fehlers, das in Windows Server-2019 behoben wurde. Der Patch für Windows Server 2016 enthalten war das kumulative Update für Februar 2019, [KB4480977](https://www.catalog.update.microsoft.com/Search.aspx?q=4480977).

- Wenn Sie Windows Admin Center als ein Gateway installiert und der Verbindungsliste angezeigt wird, ist möglicherweise beschädigt, führen Sie die folgenden Schritte aus:

   > [!WARNING]
   >Hierdurch werden die Verbindungsliste und die Einstellungen für alle Windows Admin Center-Benutzer auf das Gateway gelöscht.

  1. Deinstallieren Sie Windows Admin Center
  2. Löschen Sie den Ordner **Server Management Experience** unter **C:\Windows\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft**
  3. Installieren Sie Windows Admin Center erneut

- Wenn Sie das Tool geöffnet lassen und einen langen Zeitraum im Leerlauf, Sie möglicherweise mehrere erhalten **Fehler: Der Runspace-Zustand ist nicht für diesen Vorgang ungültig** Fehler. Aktualisieren Sie dann den Browser. Wenn dies auftritt [senden Sie uns Feedback](http://aka.ms/WACfeedback).

- Ein **500 Fehler** kann auftreten, wenn Sie Seiten mit sehr langen URLs aktualisieren. [12443710]

- In einigen Tools kann die Rechtschreibprüfung Ihres Browsers bestimmte Feldwerte als falsch geschriebenen kennzeichnen. [12425477]

- In einigen Tools spiegeln Befehlsschaltflächen möglicherweise die Änderungen nicht unmittelbar nach einem Klick wieder, und die Tool-UI spiegelt möglicherweise nicht automatisch Änderungen an bestimmte Eigenschaften wider. Klicken Sie auf **Aktualisieren**, um den aktuellen Stand vom Zielserver abzurufen. [11445790]

- Filtern von Transpondern auf Verbindungsliste – Wenn Sie Verbindungen, die über die Mehrfachauswahl Kontrollkästchen auswählen und dann Ihre Verbindungsliste Filtern nach tags, die ursprüngliche Auswahl weiterhin besteht, wendet alle von Ihnen ausgewählte Aktion für alle zuvor ausgewählten Computer an. [18099259]

- Es gibt möglicherweise geringfügige Abweichung zwischen den Versionsnummern von OSS, die unter Windows Admin Center-Module und was sich innerhalb der 3rd Party Software aufgeführt ist.

### <a name="extension-manager"></a>Erweiterungs-Manager

- Wenn Sie Windows Admin Center aktualisieren, müssen Sie Ihre Erweiterungen neu installieren.
- Wenn Sie eine Erweiterung feed, die nicht zugegriffen werden kann hinzufügen, gibt es keine Warnung. [14412861]

## <a name="browser-specific-issues"></a>Bestimmte Browserprobleme

### <a name="microsoft-edge"></a>Microsoft Edge

- In einigen Fällen gibt es möglicherweise lange Ladezeiten, wenn Sie Microsoft Edge verwenden, wenn Sie auf ein Windows Admin Center-Gateway über das Internet zugreifen. Dies kann auf virtuellen Azure-Computern auftreten, auf dem das Windows Admin Center Gateway ein selbstsigniertes Zertifikat verwendet wird. [13819912]

- Wenn Sie AAD als Identitätsanbieter verwenden und Windows Admin Center mit einem selbstsignierten oder nicht vertrauenswürdigen Zertifikat konfiguriert ist, kann die Authentifizierung AAD in Microsoft Edge nicht abschließen.  [15968377]

- Wenn Sie Windows Admin Center, die als Dienst bereitgestellt haben, und Sie Microsoft Edge als Browser verwenden, verbinden Ihr Gateway in Azure möglicherweise nach einem neuen Browserfenster zu erzeugen. Versuchen Sie, dieses Problem umgehen, indem Sie hinzufügen https://login.microsoftonline.com, https://login.live.com, und die URL Ihres Gateways als vertrauenswürdige Sites und Standorte für die Popupblocker-Einstellungen in Ihrem Client-Side-Browser zulässig. Weitere Anleitungen zum Beheben von in die [Handbuch zur Problembehandlung](troubleshooting.md#azure-features-dont-work-properly-in-edge). [17990376]

- Wenn Sie Windows Admin Center im Desktopmodus installiert haben, nicht die Registerkarte "Browser" in Microsoft Edge das Favicon angezeigt. [17665801]

### <a name="google-chrome"></a>Google Chrome

- Vor Version 70 (Ende Oktober 2018 veröffentlicht) Chrome hatte eine [Fehler](https://bugs.chromium.org/p/chromium/issues/detail?id=423609) im Hinblick auf die Websockets-Protokoll und NTLM-Authentifizierung. Dies wirkt sich die folgenden Tools: Ereignisse, PowerShell, eine Remotedesktopverbindung.

- Chrome zeigt eventuell mehrere Anmeldeinformationen an, vor allem in Zeiten der Verbindungsprozesse in einer **Arbeitsgruppen**-Umgebung (nicht der Domäne).

- Wenn Sie Windows Admin Center, die als Dienst bereitgestellt haben, müssen Popups von der Gateway-URL für alle Funktionen der Azure-Integration funktioniert aktiviert werden soll. Zu diesen Diensten gehören Azure-Netzwerkadapter, die Verwaltung von Azure und Azure Site Recovery.

### <a name="mozilla-firefox"></a>Mozilla Firefox

Windows Admin Center wurde nicht mit Mozilla Firefox getestet, aber die meisten Funktionen sollten funktionieren.

- Windows 10 Installation: Mozilla Firefox hat seinem eigenen Zertifikatspeicher, damit Sie importieren müssen die ```Windows Admin Center Client``` Zertifikats in Firefox unter Windows 10 Windows Admin Center verwenden.

## <a name="websocket-compatibility-when-using-a-proxy-service"></a>WebSocket-Kompatibilität bei Verwendung von einem Proxy-Dienst

Remotedesktop, PowerShell und Ereignismodule im Windows Admin Center nutzen das WebSocket-Protokoll, das häufig nicht unterstützt wird, wenn ein Proxydienst verwendet wird. WebSocket unterstützt Azure AD-Anwendungsproxy-Kompatibilität in der [Vorschau](https://blogs.technet.microsoft.com/applicationproxyblog/2018/03/28/limited-websocket-support-now-in-public-preview/) und sucht nach Feedback zur Kompatibilität.

## <a name="support-for-windows-server-versions-before-2016-2012-r2-2012-2008-r2"></a>Unterstützung für Windows Server-Versionen vor 2016 (2012 R2, 2012, 2008 R2)

> [!NOTE]
> Windows Admin Center erfordert PowerShell-Funktionen, die nicht in Windows Server 2012 R2, 2012 oder 2008 R2 enthalten sind. Wenn Sie Windows Server mit Windows Admin Center verwalten, müssen Sie WMF-Version 5.1 oder höher auf diesen Servern installieren.

Geben Sie `$PSVersiontable` in PowerShell ein, um zu prüfen, ob WMF 5.1 oder einen neuere Version installiert ist.

Wenn dies nicht der Fall ist, können Sie [herunterladen und WMF 5.1 installieren](https://www.microsoft.com/en-us/download/details.aspx?id=54616).

## <a name="role-based-access-control-rbac"></a>Rollenbasierte Zugriffssteuerung (RBAC)

- RBAC-Bereitstellung ist auf Computern, die für die Windows Defender-Anwendungssteuerung (WDAC, früher als Integrität des Codes bezeichnet) konfiguriert werden, nicht erfolgreich [16568455]

- Um RBAC in einem Cluster verwenden, müssen Sie die Konfiguration für jeden Memberknoten einzeln bereitstellen.

- Wenn RBAC bereitgestellt wird, können Sie unauthorized-Fehler erhalten, die nicht ordnungsgemäß an der RBAC-Konfiguration Ergebnisarray als Attribut zugewiesen werden. [16369238]

## <a name="server-manager-solution"></a>Server-Manager-Lösung

### <a name="server-settings"></a>Server-Einstellungen

- Wenn Sie eine Einstellung ändern und anschließend versuchen, eine verlassen, ohne zu speichern, wird die Seite warnt Sie nicht gespeicherten Änderungen, jedoch weiterhin verlassen. Sie können in einen Zustand enden, in dem die Registerkarte "Einstellungen", die ausgewählt wird den Inhalt der Seite nicht übereinstimmt. [19905798] [19905787]

### <a name="certificates"></a>Zertifikate

- Kann nicht importiert werden. PFX verschlüsselt Zertifikat im Speicher des aktuellen Benutzers. [11818622]

### <a name="devices"></a>Geräte

- Beim Navigieren durch die Tabelle mit der Tastatur, kann die Auswahl an den Anfang der Tabellengruppe springen. [16646059]

### <a name="events"></a>Ereignisse

- Ereignisse erfolgen durch [Websocket-Kompatibilität bei Verwendung eines Proxydiensts.](#websocket-compatibility-when-using-a-proxy-service)

- Möglicherweise erhalten Sie die Fehlermeldung "Packet Size" beim Exportieren von großen Protokolldateien. [16630279]

  - Um dies zu beheben, verwenden Sie den folgenden Befehl in einer Eingabeaufforderung mit erhöhten Rechten auf dem Gatewaycomputer aus: ```winrm set winrm/config @{MaxEnvelopeSizekb="8192"}```

### <a name="files"></a>Dateien

- Hoch- oder heruntergeladen großer Dateien wird noch nicht unterstützt. (\~Limit von 100 mb) [12524234]

### <a name="powershell"></a>PowerShell

- PowerShell erfolgt durch [Websocket-Kompatibilität bei Verwendung eines Proxydiensts](#websocket-compatibility-when-using-a-proxy-service)

- Das Einfügen mit einem einzelnen Klick mit der rechten Maustaste wie in der Desktop PowerShell-Konsole ist nicht funktionsfähig. Stattdessen erhalten Sie Kontextmenüs des Browsers, in dem Sie „einfügen” auswählen können. STRG + V funktioniert auch.

- STRG + C kann nicht zum Kopieren verwendet werden, es sendet immer den Befehl STRG + C an die Konsole. Das Kopieren über das mit der rechten Maustaste aufgerufenen Kontextmenü funktioniert.

- Wenn Sie das Windows Admin Center-Fenster kleiner machen, wird der Terminalinhalt umgeleitet, aber wenn Sie es erneut vergrößern, kann der Inhalt nicht in den vorherigen Zustand zurückkehren. Wenn Dinge durcheinander geraten, können Sie Clear-Host verwenden, oder die Verbindung trennen und erneut eine Verbindung mit der Schaltfläche oberhalb des Terminaldienstes herstellen.

### <a name="registry-editor"></a>Registrierungs-Editor

- Die Suchfunktion ist nicht implementiert. [13820009]

### <a name="remote-desktop"></a>Remotedesktop

- Das Remote Desktop-Tool kann fehlschlagen, eine Verbindung herstellen, wenn Sie Windows Server 2012 verwalten. [20258278]

- Der Remotedesktop mit einem Computer herstellen, für die keine Domäne eingebunden ist, geben Sie Ihr Konto in der ```MACHINENAME\USERNAME``` Format.

- Einige Konfigurationen können Windows Admin Center des Remotedesktop-Client mit der Gruppenrichtlinie blockieren. Wenn dies auftritt, aktivieren Sie ```Allow users to connect remotely by using Remote Desktop Services``` unter ```Computer Configuration/Policies/Administrative Templates/Windows Components/Remote Desktop Services/Remote Desktop Session Host/Connections```

- Remotedesktop wird beeinflusst von [Websocket-Kompatibilität.](#websocket-compatibility-when-using-a-proxy-service)

- Das Tool Remotedesktop unterstützt derzeit weder Text, Bild oder Datei Kopieren/Einfügen zwischen dem lokalen Desktop und der Remotesitzung.

- Zum Kopieren/Einfügen innerhalb der Remotesitzung können Sie normal kopieren (Klicken + Kopieren oder STRG + C), das Einfügen erfordert Klick + Einfügen (STRG + V funktioniert nicht)

- Sie können die folgenden Befehle nicht an die Remotesitzung senden.
  - ALT+TAB
  - Funktionstasten
  - Windows-Taste
  - DRUCK

- Remote-App – kann nach dem Aktivieren der Remote-App-Tool von Einstellungen für Remotedesktop, das Tool nicht in der Liste der Tools angezeigt, wenn einen Server mit Desktopdarstellung verwalten. [18906904]

### <a name="roles-and-features"></a>Rollen und Features

- Bei der Auswahl von Rollen oder Funktionen mit nicht verfügbaren Quellen zur Installation, werden diese übersprungen. [12946914]

- Wenn Sie nach der Installation der Serverrollen nicht automatisch neu starten, wird nicht erneut gefragt. [13098852]

- Wenn Sie automatisch neu starten auswählen, wird der Neustart erfolgen, bevor der Status auf 100 % aktualisiert wird. [13098852]

### <a name="storage"></a>Speicher

- Abrufen von Informationen zum Kontingent kann fehlschlagen, ohne eine Fehlermeldung angezeigt (es werden Fehler in der Konsole des Browsers) [18962274]

- Kompatible: CD/DVD/Diskette Laufwerke werden nicht als Volumes auf Elementebene angezeigt.

- Kompatible: Einige Eigenschaften in der Volumes und Datenträgern sind nicht kompatible verfügbar, sodass sie unbekannte oder ein Leerzeichen im Bereich "Details" angezeigt werden.

- Kompatible: Wenn Sie ein neues Volume zu erstellen, ReFS unterstützt nur eine zuordnungseinheitsgröße von 64 KB auf Windows 2012 und 2012 R2-Computern. Wenn ein Volume ReFS mit einer kleineren Zuordnungseinheit für ältere Ziele erstellt wird, schlägt die File System-Formatierung fehl. Das neue Volume kann nicht verwendet werden. Die Lösung besteht darin, das Volume zu löschen und Zuordnungseinheiten mit 64 KB zu verwenden.

### <a name="updates"></a>Updates

- Nach der Installation von Updates, Installationsstatus können zwischengespeichert werden und erfordern eine Aktualisierung des Browsers.

- Sie können den Fehler auftreten: "Keyset ist nicht vorhanden" beim Versuch, die Verwaltung von Azure einrichten. In diesem Fall versuchen Sie die folgenden wiederherstellungsschritten auf dem verwalteten Knoten:
    1. Dienst "Kryptografischen Dienste" zu beenden.
    2. Ordner ändern Sie Optionen zum Anzeigen versteckter Dateien (falls erforderlich).
    3. Navigieren Sie zu "% allusersprofile%\Microsoft\Crypto\RSA\S-1-5-18" Ordner und seinen gesamten Inhalt zu löschen.
    4. Starten Sie "kryptografischen Dienste" neu.
    5. Wiederholen Sie die Einrichtung der Verwaltung von Updates mit Windows Admin Center

### <a name="virtual-machines"></a>Virtuelle Computer

- Wenn Sie die virtuellen Computer auf einem Windows Server 2012-Host zu verwalten, die VM in einem Browser eine Verbindung herstellen Tool für die Verbindung mit dem virtuellen Computer nicht. Herunterladen der RDP-Datei für die Verbindung mit dem virtuellen Computer sollte weiterhin funktionieren. [20258278]

- Azure Site Recovery – wenn ASR Setup auf dem Host außerhalb WAC, ist Sie nicht schützen, einen virtuellen Computer über WAC [18972276] werden

- Erweiterte Funktionen in Hyper-V-Manager wie Virtual SAN-Manager, Move VM, Export VM und VM-Replikation werden derzeit nicht unterstützt.

### <a name="virtual-switches"></a>Virtuelle Switches

- Switch Embedded Teaming (SET): Wenn Sie Netzwerkkarten zu einem Team hinzufügen, müssen sie sich im gleichen Subnetz sein.

## <a name="computer-management-solution"></a>Computer-Management-Lösung

Die Computer-Management-Lösung enthält eine Teilmenge der Tools der Server-Manager-Lösung, daher sind die gleichen bekannten Probleme vorhanden, sowie die folgenden Computer Management-Lösungen für bestimmte Probleme:

- Bei Verwendung einer Microsoft Account ([MSA](https://account.microsoft.com/account/)) oder wenn Sie Azure Active Directory (AAD) verwenden, um Sie Windows 10-Computer anmelden, müssen Sie angeben "verwalten – als" Anmeldeinformationen zum Verwalten Ihres lokalen Computers [16568455]

- Wenn Sie versuchen, den "localhost" zu verwalten, werden Sie aufgefordert, den Gateway-Prozess zu erhöhen. Wenn Sie **Nein** im folgenden Benutzerkontensteuerungsfenster anklicken, kann Windows Admin Center dies nicht erneut anzeigen. Beenden Sie in diesem Fall den Gateway-Prozess, indem Sie das Windows Admin Center-Symbol in der Taskleiste mit der rechten Maustaste anklicken, und beenden wählen. Starten Sie Windows Admin Center im Startmenü dann erneut.

- Auf Windows 10 ist WinRM/PowerShell-Remoting standardmäßig nicht vorhanden
  
  - Um die Verwaltung des Windows 10-Clients zu ermöglichen, müssen Sie den Befehl ```Enable-PSRemoting``` aus einer PowerShell-Eingabeaufforderung mit erhöhten Rechten eingeben.

  - Sie müssen auch Ihre Firewall für Verbindungen von außerhalb des lokalen Subnetzes mit ```Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any``` aktualisieren. Restriktiver Netzwerke Szenarien finden Sie in [dieser Dokumentation](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enable-psremoting?view=powershell-5.1).

## <a name="failover-cluster-manager-solution"></a>Failovercluster-Manager-Lösung

- Wenn Sie einen Cluster verwalten (entweder hyperkonvergent oder herkömmlich) tritt möglicherweise der Fehler **shell was not found** auf. Laden Sie in diesem Fall entweder Ihren Browser erneut oder navigieren Sie zu einem anderen Tool und zurück. [13882442]

- Ein Problem kann auftreten, wenn Sie einen älteren Cluster verwalten (Windows Server 2012 oder 2012 R2), der nicht vollständig konfiguriert wurde. Die Fehlerbehebung für dieses Problem besteht darin, sicherzustellen, dass das Windows-Feature **RSAT-Clustering-PowerShell** installiert und auf **jedem Mitgliedsknoten** des Clusters aktiviert wurde. Um dies mit PowerShell auszuführen, geben Sie den Befehl `Install-WindowsFeature -Name RSAT-Windows-PowerShell` auf den Clusterknoten an. [12524664]

- Cluster müssen möglicherweise über den gesamten FQDN hinzugefügt werden, um richtig erkannt zu werden.

- Bei der Verbindung mit einem Cluster mit Windows Admin Center als Gateway und beim Bereitstellen des expliziten Benutzernamens und Kennwort,um sich zu authentifizieren, müssen Sie **diese Anmeldeinformationen für alle Verbindungen verwenden** auswählen, damit die Anmeldeinformationen zum Abfragen des Mitgliedknotens verfügbar sind.

## <a name="hyper-converged-cluster-manager-solution"></a>Hyperkonvergente Cluster-Manager-Lösung

- Einige Befehle wie **Drives - Update firmware**, **Servers - Remove** und **Volumes - Open** sind nicht aktiviert und zur Zeit nicht verfügbar.