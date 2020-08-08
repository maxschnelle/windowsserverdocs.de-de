---
title: Bekannte Probleme im Windows Admin Center
description: Bekannte Probleme im Windows Admin Center (Projekt Honolulu)
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.date: 06/07/2019
ms.openlocfilehash: 91e14b5ac023f6726ffc508f945567b83311d7a4
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997019"
---
# <a name="windows-admin-center-known-issues"></a>Bekannte Probleme im Windows Admin Center

> Gilt für: Windows Admin Center, Windows Admin Center (Vorschauversion)

Wenn Sie ein Problem feststellen, das nicht auf dieser Seite beschrieben wird, [informieren Sie uns](https://aka.ms/WACfeedback)bitte.

## <a name="installer"></a>Installationsprogramm

- Beachten Sie beim Installieren des Windows Admin Centers mithilfe Ihres eigenen Zertifikats, dass Sie beim Kopieren des Fingerabdrucks aus dem Zertifikat-Manager-MMC-Tool [ein ungültiges Zeichen am Anfang enthalten.](https://support.microsoft.com/help/2023835/certificate-thumbprint-displayed-in-mmc-certificate-snap-in-has-extra) Um dieses Problem zu umgehen, geben Sie das erste Zeichen des Fingerabdrucks ein, kopieren Sie den Rest, und fügen Sie ihn ein.

- Die Verwendung von Port unter 1024 wird nicht unterstützt. Im Dienst Modus können Sie optional Port 80 für die Umleitung an den angegebenen Port konfigurieren.

## <a name="general"></a>Allgemein

- In der 1910,2-Version des Windows Admin Centers können Sie möglicherweise keine Verbindung zu Hyper-V-Servern auf bestimmter Hardware herstellen. Wenn dieses Problem blockiert ist, laden Sie [den vorherigen Build herunter](https://aka.ms/wacprevious).

- Wenn Sie Windows Admin Center als Gateway unter **Windows Server 2016** unter starker Verwendung installiert haben, stürzt der Dienst möglicherweise mit einem Fehler im Ereignisprotokoll ab, der ```Faulting application name: sme.exe``` und enthält ```Faulting module name: WsmSvc.dll``` . Der Grund hierfür ist ein Fehler, der in Windows Server 2019 behoben wurde. Der Patch für Windows Server 2016 enthielt das kumulative Update vom Februar 2019, [KB4480977](https://www.catalog.update.microsoft.com/Search.aspx?q=4480977).

- Wenn Sie Windows Admin Center als Gateway installiert haben und die Verbindungsliste beschädigt erscheint, führen Sie die folgenden Schritte aus:

   > [!WARNING]
   >Hierdurch werden die Verbindungsliste und Einstellungen für alle Benutzer des Windows Admin Centers auf dem Gateway gelöscht.

  1. Deinstallieren des Windows Admin Centers
  2. Löschen Sie den Ordner " **Server Verwaltungs** Umgebung" unter " **c:\windows\serviceprofiles\networkservice\appdata\roaming\microsoft** ".
  3. Neuinstallieren des Windows Admin Centers

- Wenn Sie das Tool für einen längeren Zeitraum geöffnet lassen und im Leerlauf sind, erhalten Sie möglicherweise mehrere **Fehler: der Runspace-Status ist für diese Vorgangs Fehler ungültig** . Wenn dies der Fall ist, aktualisieren Sie den Browser. Wenn dies der Meinung ist, [Senden Sie uns Feedback](https://aka.ms/WACfeedback).

- Möglicherweise gibt es eine geringfügige Abweichung zwischen den Versionsnummern von Betriebssystemen, die in den Modulen des Windows Admin Centers ausgeführt werden, und den im Software Hinweis eines Drittanbieters aufgeführten Betriebssystemen.

### <a name="extension-manager"></a>Erweiterungs-Manager

- Wenn Sie das Windows Admin Center aktualisieren, müssen Sie die Erweiterungen neu installieren.
- Wenn Sie einen Erweiterungs Feed hinzufügen, auf den nicht zugegriffen werden kann, wird keine Warnung angezeigt. [14412861]

## <a name="browser-specific-issues"></a>Browser spezifische Probleme

### <a name="microsoft-edge"></a>Microsoft Edge

- Wenn Sie das Windows Admin Center als Dienst bereitgestellt haben und Microsoft Edge als Browser verwenden, kann das Verbinden Ihres Gateways mit Azure nach dem Auslösen eines neuen Browserfensters fehlschlagen. Versuchen Sie, dieses Problem zu umgehen, indem Sie https://login.microsoftonline.com , https://login.live.com und die URL Ihres Gateways als vertrauenswürdige Sites und zulässige Websites für die Popup Blocker Einstellungen in Ihrem Client seitigen Browser hinzufügen. Weitere Anleitungen zur Behebung dieses Problem finden Sie im [Handbuch zur Problem](troubleshooting.md#azure-features-dont-work-properly-in-edge)Behandlung. [17990376]

### <a name="google-chrome"></a>Google Chrome

- Vor Version 70 (veröffentlicht am Ende Oktober, 2018) gab es einen [Fehler](https://bugs.chromium.org/p/chromium/issues/detail?id=423609) im Zusammenhang mit dem websockets-Protokoll und der NTLM-Authentifizierung. Dies wirkt sich auf die folgenden Tools aus: Events, PowerShell, Remotedesktop.

- Chrome zeigt möglicherweise mehrere Eingabe Aufforderungen für Anmelde Informationen an, insbesondere während der Add connection-Umgebung in einer **Arbeitsgruppen** Umgebung (nicht-Domäne).

- Wenn Sie das Windows Admin Center als Dienst bereitgestellt haben, müssen Popups von der Gateway-URL aktiviert werden, damit alle Azure-Integrationsfunktionen funktionieren.

### <a name="mozilla-firefox"></a>Mozilla Firefox

Windows Admin Center wird nicht mit Mozilla Firefox getestet, aber die meisten Funktionen sollten funktionieren.

- Windows 10-Installation: Mozilla Firefox verfügt über einen eigenen Zertifikat Speicher, sodass Sie das Zertifikat in Firefox importieren müssen, damit ```Windows Admin Center Client``` Windows Admin Center unter Windows 10 verwendet werden kann.

## <a name="websocket-compatibility-when-using-a-proxy-service"></a>WebSocket-Kompatibilität bei Verwendung eines Proxy Dienstanbieter

Remotedesktop-, PowerShell-und Events-Module in Windows Admin Center verwenden das WebSocket-Protokoll, das häufig bei Verwendung eines Proxy Dienstanbieter nicht unterstützt wird.

## <a name="support-for-windows-server-versions-before-2016-2012-r2-2012-2008-r2"></a>Unterstützung für Windows Server-Versionen vor 2016 (2012 R2, 2012, 2008 R2)

> [!NOTE]
> Windows Admin Center erfordert PowerShell-Features, die nicht in Windows Server 2012 R2, 2012 oder 2008 R2 enthalten sind. Wenn Sie Windows Server mit dem Windows Admin Center verwalten, müssen Sie WMF Version 5,1 oder höher auf diesen Servern installieren.

Gebe `$PSVersiontable` in PowerShell ein, um zu prüfen, ob WMF 5.1 oder höher installiert ist.

Wenn dies nicht der Fall ist, kannst du [herunterladen und WMF 5.1 installieren](https://www.microsoft.com/download/details.aspx?id=54616).

## <a name="role-based-access-control-rbac"></a>Rollenbasierte Zugriffssteuerung

- Die RBAC-Bereitstellung auf Computern, die für die Verwendung von Windows Defender Application Control (WDac, früher als Code Integrität bezeichnet) konfiguriert sind, ist nicht erfolgreich. [16568455]

- Wenn Sie die rollenbasierte Zugriffs Steuerung in einem Cluster verwenden möchten, müssen Sie die Konfiguration für jeden Mitglieds Knoten einzeln bereitstellen.

- Wenn RBAC bereitgestellt ist, erhalten Sie möglicherweise nicht autorisierte Fehler, die fälschlicherweise der RBAC-Konfiguration zugeordnet sind. [16369238]

## <a name="server-manager-solution"></a>Server-Manager Lösung

### <a name="certificates"></a>Zertifikate

- Importieren nicht möglich. PFX-verschlüsseltes Zertifikat in den Speicher des aktuellen Benutzers. [11818622]

### <a name="events"></a>Ereignisse

- Ereignisse werden von der [WebSocket-Kompatibilität bei der Verwendung eines Proxy Dienstanbieter beeinflusst.](#websocket-compatibility-when-using-a-proxy-service)

- Wenn Sie große Protokolldateien exportieren, erhalten Sie möglicherweise eine Fehlermeldung, die auf "Paketgröße" verweist.

  - Um dieses Problem zu beheben, verwenden Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten auf dem Gatewaycomputer:```winrm set winrm/config @{MaxEnvelopeSizekb="8192"}```

### <a name="files"></a>Dateien

- Das Hochladen oder Herunterladen großer Dateien wurde noch nicht unterstützt. ( \~ Limit von 100 MB) [12524234]

### <a name="powershell"></a>PowerShell

- PowerShell wird [bei Verwendung eines Proxy Dienstanbieter von der WebSocket-Kompatibilität](#websocket-compatibility-when-using-a-proxy-service) beeinflusst

- Das Einfügen mit einem einzelnen Rechtsklick wie in der Desktop-PowerShell-Konsole funktioniert nicht. Stattdessen wird das Kontextmenü des Browsers angezeigt, in dem Sie Einfügen auswählen können. STRG + V funktioniert ebenfalls.

- Strg + c zum Kopieren funktioniert nicht. es wird immer der Befehl Strg + c-Unterbrechung an die Konsole gesendet. Kopieren Sie das Kontextmenü, das mit der rechten Maustaste angezeigt wird.

- Wenn Sie das Fenster des Windows Admin Centers verkleinern, wird der Terminal Inhalt wieder verwendet. Wenn Sie ihn jedoch wieder vergrößern, wird der Inhalt möglicherweise nicht in den vorherigen Zustand zurückversetzt. Wenn es zu einem Durcheinander kommt, können Sie mit der Schaltfläche über dem Terminal löschen oder die Verbindung trennen und wiederherstellen.

### <a name="registry-editor"></a>Registrierungs-Editor

- Die Such Funktionalität ist nicht implementiert. [13820009]

### <a name="remote-desktop"></a>Remotedesktop

- Wenn das Windows Admin Center als Dienst bereitgestellt wird, kann das Remotedesktop Tool nach dem Aktualisieren des Windows Admin Center-Dienstanbieter auf eine neue Version möglicherweise nicht geladen werden. Um dieses Problem zu umgehen, löschen Sie den Browser Cache.   [23824194]

- Das Remotedesktop Tool kann bei der Verwaltung von Windows Server 2012 möglicherweise keine Verbindung herstellen. [20258278]

- Wenn Sie die Remotedesktop zum Herstellen einer Verbindung mit einem Computer verwenden, der keiner Domäne beigetreten ist, müssen Sie Ihr Konto im ```MACHINENAME\USERNAME``` Format eingeben.

- Einige Konfigurationen können den Remote Desktop Client des Windows Admin Centers mit der Gruppenrichtlinie blockieren. Wenn dies der gibt, aktivieren Sie ```Allow users to connect remotely by using Remote Desktop Services``` unter```Computer Configuration/Policies/Administrative Templates/Windows Components/Remote Desktop Services/Remote Desktop Session Host/Connections```

- Remotedesktop wird von der [WebSocket-Kompatibilität beeinflusst.](#websocket-compatibility-when-using-a-proxy-service)

- Das Remotedesktop Tool unterstützt derzeit weder Text, Bilder noch Dateien zum Kopieren und Einfügen zwischen dem lokalen Desktop und der Remote Sitzung.

- Wenn Sie Kopieren/Einfügen innerhalb der Remote Sitzung ausführen möchten, können Sie Sie in normaler Form kopieren (Klicken Sie mit der rechten Maustaste auf + Kopieren oder STRG + C), aber einfügen erfordert den Rechtsklick + Einfügen (STRG + V funktioniert nicht).

- Die folgenden Schlüsselbefehle können nicht an die Remote Sitzung gesendet werden.
  - ALT+TAB
  - Funktionstasten
  - Windows-Taste
  - Druck

### <a name="roles-and-features"></a>Rollen und Features

- Wenn Sie Rollen oder Features mit nicht verfügbaren Quellen für die Installation auswählen, werden diese übersprungen. [12946914]

- Wenn Sie sich für einen automatischen Neustart nach der Rollen Installation entscheiden, werden wir nicht erneut nachfragen. [13098852]

- Wenn Sie einen automatischen Neustart durchführen, erfolgt der Neustart, bevor der Status auf 100% aktualisiert wird. [13098852]

### <a name="storage"></a>Storage

- Unterebene: DVD/CD/Diskettenlaufwerke werden nicht als Volumes auf der Ebene der untergeordneten Ebene angezeigt.

- Herabstufen: einige Eigenschaften in Volumes und Datenträgern sind nicht im Detailbereich als "unbekannt" oder "leer" verfügbar.

- Herabstufen: Wenn Sie ein neues Volume erstellen, unterstützt Refs nur die Größe der Zuordnungs Einheiten von 64 KB auf Computern mit Windows 2012 und 2012 R2. Wenn ein Refs-Volume mit einer geringeren Zuordnungs Einheitsgröße für Ziele auf niedrigerer Ebene erstellt wird, schlägt die Formatierung des Dateisystems fehl. Das neue Volume kann nicht verwendet werden. Die Lösung besteht darin, das Volume zu löschen und die Größe der Zuordnungs Einheiten von 64K zu verwenden.

### <a name="updates"></a>Aktualisierungen

- Nach der Installation von Updates kann der Installationsstatus zwischengespeichert werden und eine Browser Aktualisierung erfordern.

- Bei dem Versuch, die Azure-Update Verwaltung einzurichten, wird möglicherweise der folgende Fehler angezeigt: "Keyset ist nicht vorhanden". Versuchen Sie in diesem Fall die folgenden Schritte zur Behebung auf dem verwalteten Knoten:
    1. Beendet den Dienst "Kryptografiedienste".
    2. Ändern Sie die Ordneroptionen, um ausgeblendete Dateien anzuzeigen (falls erforderlich).
    3. Sie haben den Ordner "%ALLUSERSPROFILE%\microsoft\crypto\rsa\s-1-5-18" erhalten, und löschen Sie den gesamten Inhalt.
    4. Starten Sie den Dienst "Kryptografiedienste" neu.
    5. Wiederholen der Einrichtung von Updateverwaltung mit dem Windows Admin Center

### <a name="virtual-machines"></a>Virtual Machines

- Beim Verwalten der virtuellen Computer auf einem Windows Server 2012-Host kann das in-Browser-VM-Verbindungs Tool keine Verbindung mit dem virtuellen Computer herstellen. Das Herunterladen der RDP-Datei, um eine Verbindung mit dem virtuellen Computer herzustellen, sollte weiterhin funktionieren. [20258278]

- Azure Site Recovery – Wenn ASR auf dem Host außerhalb von WAC eingerichtet ist, können Sie einen virtuellen Computer nicht innerhalb von WAC schützen [18972276]

- Erweiterte Features, die im Hyper-V-Manager wie Virtual SAN Manager, Move VM, Export VM und VM Replication verfügbar sind, werden zurzeit nicht unterstützt.

### <a name="virtual-switches"></a>Virtuelle Switches

- Eingebetteten Teaming (Set) wechseln: beim Hinzufügen von NICs zu einem Team müssen Sie sich im gleichen Subnetz befinden.

## <a name="computer-management-solution"></a>Computer Verwaltungs Lösung

Die Lösung für die Computer Verwaltung enthält eine Teilmenge der Tools aus der Server-Manager-Lösung, sodass dieselben bekannten Probleme zutreffen, sowie die folgenden spezifischen Probleme der Computer Verwaltungs Lösung:

- Wenn Sie ein Microsoft-Konto ([MSA](https://account.microsoft.com/account/)) verwenden oder Azure Active Directory (AAD) verwenden, um sich bei Ihrem Windows 10-Computer anzumelden, müssen Sie "Manage-as" verwenden, um Anmelde Informationen für ein lokales Administrator Konto anzugeben [16568455]

- Wenn Sie versuchen, den localhost zu verwalten, werden Sie aufgefordert, den Gatewayprozess zu erhöhen. Wenn Sie im folgenden Popup Fenster "Benutzerkontensteuerung" auf **Nein** klicken, müssen Sie den Verbindungsversuch abbrechen und beginnen.

- Für Windows 10 ist standardmäßig kein WinRM-/PowerShell-Remoting aktiviert.

  - Um die Verwaltung des Windows 10-Clients zu aktivieren, müssen Sie den Befehl an ```Enable-PSRemoting``` einer PowerShell-Eingabeaufforderung mit erhöhten Rechten ausgeben.

  - Möglicherweise müssen Sie die Firewall auch aktualisieren, um Verbindungen von außerhalb des lokalen Subnetzes mit zuzulassen ```Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any``` . Weitere einschränkende Netzwerk Szenarios finden Sie in [dieser Dokumentation](/powershell/module/microsoft.powershell.core/enable-psremoting?view=powershell-5.1).

## <a name="cluster-deployment"></a>Cluster Bereitstellung

### <a name="step-12"></a>Schritt 1,2
Gemischte Arbeitsgruppen Computer werden beim Hinzufügen von Servern derzeit nicht unterstützt. Alle Computer, die für das Clustering verwendet werden, müssen derselben Arbeitsgruppe angehören. Wenn dies nicht der Fall ist, wird die Schaltfläche Weiter deaktiviert, und der folgende Fehler wird angezeigt: "ein Cluster mit Servern in anderen Active Directory Domänen kann nicht erstellt werden. Vergewissern Sie sich, dass die Servernamen richtig sind. Verschieben Sie alle Server in dieselbe Domäne, und wiederholen Sie den Vorgang. "

### <a name="step-14"></a>Schritt 1,4
Hyper-V muss auf virtuellen Computern installiert werden, auf denen das Azure Stack HCI-Betriebssystem ausgeführt wird. Der Versuch, das Hyper-V-Feature für diese virtuellen Computer zu aktivieren, schlägt mit dem folgenden Fehler fehl:

![Screenshot des Hyper-V-Aktivierungs Fehlers](../media/cluster-create-install-hyperv.png)

Führen Sie den folgenden Befehl aus, um Hyper-V auf virtuellen Computern zu installieren, auf denen die Azure Stack HCI OS ausgeführt wird:

```PowerShell
Enable-windowsoptionalfeature -online -featurename Microsoft-hyper-v
```

### <a name="step-17"></a>Schritt 1,7
Manchmal dauert es länger, bis Server nach der Installation von Updates neu gestartet werden. Der Assistent für die Cluster Bereitstellung in Windows Admin Center prüft regelmäßig den Neustart Status des Servers, um zu ermitteln, ob der Server erfolgreich neu gestartet wurde. Wenn der Benutzer den Server jedoch manuell außerhalb des Assistenten neu startet, bietet der Assistent keine Möglichkeit, den Server Zustand in angemessener Weise zu erfassen.

Wenn Sie den Server manuell neu starten möchten, beenden Sie die aktuelle Assistenten Sitzung. Nachdem Sie den Server neu gestartet haben, können Sie den Assistenten neu starten.

### <a name="stretch-cluster-creation"></a>Stretch-Cluster Erstellung
Es wird empfohlen, bei der Erstellung eines Stretch-Clusters Server zu verwenden, die einer Domäne beigetreten sind. Bei der Verwendung von Arbeitsgruppen Computern für die Stretch-Cluster Bereitstellung aufgrund von WinRM-Einschränkungen gibt es ein Problem mit der Netzwerksegmentierung.

### <a name="undo-and-start-over"></a>Rückgängig machen und beginnen
Wenn Sie dieselben Computer für die Cluster Bereitstellung wiederholt verwenden, ist die Bereinigung vorheriger Cluster Entitäten wichtig, um eine erfolgreiche Cluster Bereitstellung auf derselben Gruppe von Computern zu erhalten. Anweisungen zum Bereinigen des Clusters finden Sie auf der Seite zum Bereitstellen der [hyperkonvergierten Infrastruktur](../use/deploy-hyperconverged-infrastructure.md#undo-and-start-over) .

### <a name="credssp"></a>CredSSP
Der Assistent für die Cluster Bereitstellung in Windows Admin Center verwendet an verschiedenen Stellen "kredssp". Diese Fehlermeldung wird während des Assistenten angezeigt (Dies tritt am häufigsten im Schritt "Cluster überprüfen" auf):

![Screenshot: Fehler beim Erstellen eines Clusters mit Cluster Erstellung](../media/cluster-create-credssp-error.jpg)

Mit den folgenden Schritten können Sie Probleme beheben:

1. Deaktivieren Sie die Einstellungen für die Einstellungen auf allen Knoten und dem Windows Admin Center-Gatewaycomputer. Führen Sie den ersten Befehl auf Ihrem Gatewaycomputer und den zweiten Befehl auf allen Knoten im Cluster aus:

```PowerShell
Disable-WsmanCredSSP -Role Client
```
```PowerShell
Disable-WsmanCredSSP -Role Server
```
2. Reparieren Sie die Vertrauensstellung auf allen Knoten. Führen Sie den folgenden Befehl auf allen Knoten aus:
```PowerShell
Test-ComputerSecureChannel -Verbose -Repair -Credential <account name>
```

3. Zurücksetzen von Gruppenrichtlinien-datasregierten Daten mit dem Befehl
```Command Line
gpupdate /force
```

4. Starten Sie die Knoten neu. Testen Sie nach dem Neustart die Konnektivität zwischen dem Gatewaycomputer und den Zielknoten sowie der Konnektivität zwischen den Knoten mit dem folgenden Befehl:
```PowerShell
Enter-PSSession -computername <node fqdn>
```

### <a name="nested-virtualization"></a>Geschachtelte Virtualisierung
Wenn Sie Azure Stack HCI-Betriebssystem Cluster-Bereitstellung auf virtuellen Computern validieren, muss die schsted Virtualisierung aktiviert werden, bevor Rollen/Features mithilfe des folgenden PowerShell-Befehls aktiviert werden:

```PowerShell
Set-VMProcessor -VMName <VMName> -ExposeVirtualizationExtensions $true
```

  > [!Note]
  > Damit der Team Vorgang für virtuelle Switches erfolgreich in einer Umgebung für virtuelle Computer ausgeführt werden kann, muss der folgende Befehl in PowerShell auf dem Host ausgeführt werden, kurz nachdem die virtuellen Maschinen erstellt wurden: Get-VM | % {Set-vmnetworkadapter-VMName $ _. Name-macaddressspoofing on-allowteaming für}

Wenn Sie einen Cluster mit dem Azure Stack HCI-Betriebssystem bereitstellen, müssen Sie zusätzliche Voraussetzungen erfüllen. Die virtuelle Festplatte des VM-Starts muss mit den Hyper-V-Features vorinstalliert werden. Führen Sie hierzu den folgenden Befehl aus, bevor Sie die virtuellen Computer erstellen:

```PowerShell
Install-WindowsFeature –VHD <Path to the VHD> -Name Hyper-V, RSAT-Hyper-V-Tools, Hyper-V-PowerShell
```

### <a name="support-for-rdma"></a>Unterstützung für RDMA
Der Assistent für die Cluster Bereitstellung in Windows Admin Center, Version 2007, bietet keine Unterstützung für die RDMA-Konfiguration.

## <a name="failover-cluster-manager-solution"></a>Failovercluster-Manager Lösung

- Beim Verwalten eines Clusters (hyperkonvergiert oder traditionell) wird möglicherweise die Fehlermeldung " **Shell wurde nicht gefunden** " angezeigt. Wenn dies der Fall ist, laden Sie Ihren Browser neu, oder navigieren Sie zu einem anderen Tool und wieder zurück. [13882442]

- Ein Problem kann auftreten, wenn ein Windows Server 2012-oder 2012 R2-Cluster verwaltet wird, der noch nicht vollständig konfiguriert wurde. Um dieses Problem zu beheben, müssen Sie sicherstellen, dass die Windows-Funktion **rsat-Clustering-PowerShell** auf **jedem Mitglieds Knoten** des Clusters installiert und aktiviert ist. Um dies mit PowerShell zu erreichen, geben Sie den Befehl `Install-WindowsFeature -Name RSAT-Clustering-PowerShell` auf allen Cluster Knoten ein. [12524664]

- Der Cluster muss ggf. mit dem gesamten FQDN hinzugefügt werden, damit er ordnungsgemäß ermittelt werden kann.

- Wenn Sie mithilfe des Windows Admin Centers, das als Gateway installiert ist, eine Verbindung mit einem Cluster herstellen und einen expliziten Benutzernamen/ein Kennwort für die Authentifizierung bereitstellen, müssen Sie **diese Anmelde Informationen für alle Verbindungen verwenden** auswählen, damit die Anmelde Informationen zum Abfragen der Mitglieds Knoten verfügbar sind

## <a name="hyper-converged-cluster-manager-solution"></a>Hyperkonvergierte Cluster-Manager-Lösung

- Einige Befehle, wie z. b. **Laufwerke-Firmware aktualisieren**, **Server-Remove** und **Volumes-Open** sind deaktiviert und werden zurzeit nicht unterstützt.

## <a name="azure-services"></a>Azure-Dienste

### <a name="azure-file-sync-permissions"></a>Azure-Dateisynchronisierung Berechtigungen

Azure-Dateisynchronisierung erfordert Berechtigungen in Azure, die von Windows Admin Center vor Version 1910 nicht bereitgestellt wurden. Wenn Sie Ihr Windows Admin Center-Gateway in Azure mit einer älteren Version als Windows Admin Center, Version 1910, registriert haben, müssen Sie Ihre Azure Active Directory Anwendung aktualisieren, um die richtigen Berechtigungen für die Verwendung Azure-Dateisynchronisierung in der neuesten Version von Windows Admin Center zu erhalten. Mit der zusätzlichen Berechtigung können Azure-Dateisynchronisierung die automatische Konfiguration des Speicherkonto Zugriffs ausführen, wie in diesem Artikel beschrieben: [sicherstellen, dass Azure-Dateisynchronisierung Zugriff auf das Speicherkonto hat](/azure/storage/files/storage-sync-files-troubleshoot?tabs=portal1%2cazure-portal#tabpanel_CeZOj-G++Q-5_azure-portal).

Zum Aktualisieren Ihrer Azure Active Directory-App können Sie eine der beiden folgenden Aktionen ausführen:
1. Wechseln Sie zu **Einstellungen**  >  **Azure**  >  **Unregister**, und registrieren Sie dann das Windows Admin Center erneut bei Azure. Stellen Sie sicher, dass Sie eine neue Azure Active Directory Anwendung erstellen.
2. Wechseln Sie zu ihrer Azure Active Directory Anwendung, und fügen Sie die erforderliche Berechtigung manuell zu Ihrer vorhandenen Azure Active Directory-APP hinzu, die im Windows Admin Center registriert ist. Wechseln Sie zu diesem Zweck zu **Einstellungen**  >  **Azure**-  >  **Ansicht in Azure**. Navigieren Sie auf dem Blatt für die **App-Registrierung** in Azure zu **API-Berechtigungen**, und wählen Sie **Berechtigung hinzufügen**aus. Scrollen Sie nach unten, und wählen Sie **Azure Active Directory Graph**aus, wählen Sie **Delegierte Berechtigungen**und dann **Verzeichnis**, und wählen Sie **Directory. accessasuser. all**aus. Klicken Sie auf **Berechtigungen hinzufügen** , um die Updates für die APP zu speichern.

### <a name="options-for-setting-up-azure-management-services"></a>Optionen zum Einrichten von Azure-Verwaltungsdiensten

Azure-Verwaltungsdienste, einschließlich Azure Monitor, Azure Updateverwaltung und Azure Security Center, verwenden denselben Agent für einen lokalen Server: die Microsoft Monitoring Agent. Azure Updateverwaltung verfügt über eine begrenzte Anzahl von unterstützten Regionen und erfordert, dass der Arbeitsbereich Log Analytics mit einem Azure Automation Konto verknüpft ist. Wenn Sie im Windows Admin Center mehrere Dienste einrichten möchten, müssen Sie die Azure-Updateverwaltung zuerst einrichten und dann entweder Azure Security Center oder Azure Monitor. Wenn Sie Azure-Verwaltungsdienste konfiguriert haben, die die Microsoft Monitoring Agent verwenden, und dann versuchen, Azure Updateverwaltung mithilfe des Windows Admin Centers einzurichten, gestattet Ihnen Windows Admin Center nur das Konfigurieren von Azure Updateverwaltung, wenn die vorhandenen Ressourcen, die mit dem Microsoft Monitoring Agent verknüpft sind, Azure Updateverwaltung unterstützen. Wenn dies nicht der Fall ist, haben Sie zwei Möglichkeiten:

1. Wechseln Sie zur Systemsteuerung > Microsoft Monitoring Agent, um [den Server von den vorhandenen Azure-Verwaltungslösungen](/azure/azure-monitor/platform/log-faq#q-how-do-i-stop-an-agent-from-communicating-with-log-analytics) (wie Azure Monitor oder Azure Security Center) zu trennen. Richten Sie dann das Azure-Updateverwaltung im Windows Admin Center ein. Danach können Sie Ihre anderen Azure-Verwaltungslösungen ohne Probleme über das Windows Admin Center einrichten.
2. Sie können [die erforderlichen Azure-Ressourcen für Azure Updateverwaltung manuell einrichten](/azure/automation/automation-update-management) und dann [die Microsoft Monitoring Agent](/azure/azure-monitor/platform/agent-manage#adding-or-removing-a-workspace) (außerhalb des Windows Admin Centers) manuell aktualisieren, um den neuen Arbeitsbereich hinzuzufügen, der der Updateverwaltung Lösung entspricht, die Sie verwenden möchten.